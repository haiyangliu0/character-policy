# AGENTS.md — character-policy Execution Guide for Coding Agents

This file defines the deterministic environment setup, I/O tensor schemas, and execution commands for coding agents operating on `haiyangliu0/character-policy`.

---

## 1. Environment Setup (`uv`)

Run from the repository root (`character-policy/`):

```bash
uv venv .venv --python 3.10
source .venv/bin/activate

uv pip install "setuptools<70" pip wheel "numpy<1.24"
uv pip install torch torchvision torchaudio librosa==0.9.2 soundfile scipy scikit-learn tqdm pyyaml wandb
uv pip install transformers==4.46.3 huggingface_hub accelerateeinops timm
uv pip install smplx==0.1.28 trimesh pyrender pyopengl imageio moviepy==1.0.3 opencv-python wget
uv pip install --no-build-isolation chumpy

# Clone the official evaluation & SMPL-X asset repository if not present
if [ ! -d "./emage_evaltools" ]; then
    git clone https://huggingface.co/haiyangliu0/emage_evaltools
fi
```

*Note for headless Linux rendering*: export `PYOPENGL_PLATFORM=egl` (or `osmesa`) before running `--visualization` or `fast_render`. On macOS, standard pyglet/OpenGL works without `PYOPENGL_PLATFORM`.

---

## 2. Input / Output Data Schema

### Input Audio
* Format: `.wav` mono audio, resampled automatically to `16,000 Hz`.
* Default example directory: `./examples/audio/` (contains `2_scott_0_1_1.wav` and `2_scott_0_2_2.wav`).

### Output Motion (`<name>_output.npz`)
Saved by `emage_utils.motion_io.beat_format_save`. Keys and shapes for a sequence of `T` frames at `30 FPS` (`T ≈ int(audio_seconds * 30)`):

| Key | Shape & Dtype | Description |
|-----|---------------|-------------|
| `poses` | `(T, 165)` `float32` | SMPL-X 55-joint axis-angle rotations (`0:3` global orient, `3:66` 21 body joints, `66:69` jaw, `69:75` left/right eyes, `75:165` 30 hand joints) |
| `expressions` | `(T, 100)` `float32` | FLAME 100-D facial expression parameters |
| `trans` | `(T, 3)` `float32` | Root 3D translation in meters |
| `betas` | `(300,)` `float32` | SMPL-X shape parameters |
| `mocap_frame_rate` | scalar `int` (`30`) | Frame rate (`30` FPS) |
| `gender` | scalar `str` (`"neutral"`) | SMPL-X gender |
| `model` | scalar `str` (`"smplx2020"`) | Mesh topology identifier |

---

## 3. Atomic Tasks & Commands

### Task A: Inference + 3D Mesh Video Rendering + Evaluation

```bash
# 1. EMAGE (Full-body + Hands + Face, CVPR 2024)
python test_emage_audio.py --audio_folder ./examples/audio --save_folder ./examples/motion --visualization

# 2. CaMN (Upper-body + Hands, ECCV 2022)
python test_camn_audio.py --audio_folder ./examples/audio --save_folder ./examples/motion --visualization --nopytorch3d

# 3. DisCo (Upper-body + Hands, ACM MM 2022)
python test_disco_audio.py --audio_folder ./examples/audio --save_folder ./examples/motion --visualization --nopytorch3d
```

**Expected Smoke-Test Verification (`test_emage_audio.py` on `./examples/audio`)**:
* Output files created in `./examples/motion/`: `2_scott_0_1_1_output.npz`, `2_scott_0_1_1_output.mp4`, `2_scott_0_2_2_output.npz`, `2_scott_0_2_2_output.mp4`.
* Console metrics on the 2 example sequences: `fgd ≈ 0.619`, `bc ≈ 0.790`, `l1 ≈ 12.64`.

### Task B: Minimal Python API Inference (Custom Single `.wav`)

```python
import torch
import librosa
from models.emage_audio import EmageAudioModel, EmageVQVAEConv, EmageVAEConv
from emage_utils.motion_io import beat_format_save

device = torch.device("cuda" if torch.cuda.is_available() else "cpu")

face_vq = EmageVQVAEConv.from_pretrained("haiyangliu0/emage_audio", subfolder="emage_vq/face").to(device).eval()
upper_vq = EmageVQVAEConv.from_pretrained("haiyangliu0/emage_audio", subfolder="emage_vq/upper").to(device).eval()
lower_vq = EmageVQVAEConv.from_pretrained("haiyangliu0/emage_audio", subfolder="emage_vq/lower").to(device).eval()
hands_vq = EmageVQVAEConv.from_pretrained("haiyangliu0/emage_audio", subfolder="emage_vq/hands").to(device).eval()
global_ae = EmageVAEConv.from_pretrained("haiyangliu0/emage_audio", subfolder="emage_vq/global").to(device).eval()
model = EmageAudioModel.from_pretrained("haiyangliu0/emage_audio").to(device).eval()

audio_np, _ = librosa.load("./examples/audio/2_scott_0_1_1.wav", sr=16000)
audio = torch.from_numpy(audio_np).float().to(device).unsqueeze(0)
speaker_id = torch.zeros((1, 1), dtype=torch.long, device=device)

with torch.no_grad():
    out = model.inference(audio, speaker_id, face_vq, upper_vq, lower_vq, hands_vq, global_ae)
    poses = out["rec_pose"].squeeze(0).cpu().numpy()
    exps = out["rec_exp"].squeeze(0).cpu().numpy()
    trans = out["rec_trans"].squeeze(0).cpu().numpy()

beat_format_save("./examples/motion/custom_out.npz", poses, upsample=30, expressions=exps, trans=trans)
```

### Task C: Standalone Video Rendering from `.npz` + `.wav`

```python
from emage_utils import fast_render

fast_render.render_one_sequence_no_gt(
    res_npz_path="./examples/motion/custom_out.npz",
    audio_path="./examples/audio/2_scott_0_1_1.wav",
    save_dir="./examples/motion/",
    remove_global=False,
)
```

### Task D: Standalone Evaluation (`emage_evaltools`)

```python
import numpy as np
import torch
from emage_evaltools.mertic import FGD, BC, L1div, LVDFace, MSEFace
from emage_utils.motion_rep_transfer import get_motion_rep_numpy
import emage_utils.rotation_conversions as rc

device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
fgd_eval = FGD(download_path="./emage_evaltools/")
bc_eval = BC(download_path="./emage_evaltools/", sigma=0.3, order=7)
l1_eval = L1div()
```

### Task E: Training on BEAT2 or Custom Speaker Data

1. **Download BEAT2 Dataset**:
   ```bash
   hf download haiyangliu0/BEAT2 --repo-type dataset --local-dir ./BEAT2
   python ./datasets/foot_contact.py
   ```
2. **Train EMAGE**:
   ```bash
   # Train VQ-VAEs (optional; pretrained VQ-VAEs are automatically downloaded from haiyangliu0/emage_audio if skipped)
   torchrun --nproc_per_node=1 train_emage_audio.py --config ./configs/emage_audio.yaml --train_vq

   # Train Audio-to-Gesture Policy
   torchrun --nproc_per_node=1 train_emage_audio.py --config ./configs/emage_audio.yaml --evaluation
   ```
3. **Train CaMN or DisCo**:
   ```bash
   torchrun --nproc_per_node=1 train_camn_audio.py --config ./configs/camn_audio.yaml --evaluation
   torchrun --nproc_per_node=1 train_disco_audio.py --config ./configs/disco_audio.yaml --evaluation
   ```
