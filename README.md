<div align="center">
<h1>character-policy<br>Generating Face and Body Animation from Speech</h1>
<code>character-policy</code> is an Open-Source and research project to generate 3D body and face animation from speech.
It works as an API inputs speech audio and outputs body and face motion parameters.
You may transfer these motion parameters to other formats such as Iphone ARKit Blendshape Weights or Vicon Skeleton bvh files.
<br><br>
For custom speaker style capture or commercial collaboration: <a href="mailto:haiyangliu1997@gmail.com">haiyangliu1997@gmail.com</a>
</div>

<br>

<div align="center">
    <a href="https://huggingface.co/spaces/haiyangliu0/EMAGE"><img src="https://img.shields.io/badge/Try_Our_Demo-HuggingFace_Space-blue?logo=huggingface"></a>
    <a href="https://huggingface.co/haiyangliu0/emage_audio"><img src="https://img.shields.io/badge/Weights-HuggingFace_Models-yellow?logo=huggingface"></a>
    <a href="https://huggingface.co/datasets/haiyangliu0/BEAT2"><img src="https://img.shields.io/badge/Dataset-HuggingFace_Datasets-green?logo=huggingface"></a>
</div>

<br>

## 1. Demo

<div align="center">
  <img src="assets/intro.gif" alt="Animation Example" style="width:95%; clip-path: inset(0px 0px 3px 0px);">
</div>

<table align="center">
  <tr>
    <td align="center"><b>DisCo (3D Mesh)</b></td>
    <td align="center"><b>CaMN (3D Mesh)</b></td>
    <td align="center"><b>EMAGE (3D Mesh)</b></td>
  </tr>
  <tr>
    <td align="center"><a target="_blank" href="./assets/videos/2_scott_0_103_103_output_disco_mesh.mp4"><img src="./assets/videos/2_scott_0_103_103_output_disco_mesh_v1.gif" width="240"></a></td>
    <td align="center"><a target="_blank" href="./assets/videos/2_scott_0_103_103_output_camn_mesh.mp4"><img src="./assets/videos/2_scott_0_103_103_output_camn_mesh_V2.gif" width="240"></a></td>
    <td align="center"><a target="_blank" href="./assets/videos/2_scott_0_103_103_output_emage_mesh.mp4"><img src="./assets/videos/2_scott_0_103_103_output_emage_mesh_v1.gif" width="480"></a></td>
  </tr>
</table>

<table align="center">
  <tr>
    <td align="center"><b>DisCo (2D Pose)</b></td>
    <td align="center"><b>CaMN (2D Pose)</b></td>
    <td align="center"><b>EMAGE (2D Pose)</b></td>
    <td align="center"><b>EMAGE-Face (2D Pose)</b></td>
  </tr>
  <tr>
    <td align="center"><a target="_blank" href="./assets/videos/2_scott_0_103_103_disco.mp4"><img src="./assets/videos/2_scott_0_103_103_disco_V1.gif" width="240"></a></td>
    <td align="center"><a target="_blank" href="./assets/videos/2_scott_0_103_103_output_camn.mp4"><img src="./assets/videos/2_scott_0_103_103_output_camn_V1.gif" width="240"></a></td>
    <td align="center"><a target="_blank" href="./assets/videos/2_scott_0_103_103_output_emage.mp4"><img src="./assets/videos/2_scott_0_103_103_output_emage_V1.gif" width="240"></a></td>
    <td align="center"><a target="_blank" href="./assets/videos/2_scott_0_103_103_output_emage_face.mp4"><img src="./assets/videos/2_scott_0_103_103_output_emage_face_V1.gif" width="240"></a></td>
  </tr>
</table>

---

## 2. Models & BEAT2 Benchmark

All outputs are in SMPL-X (body + hands) and FLAME (face) parameters evaluated on BEAT2 (Speaker 2 `Scott`).

### Models from `character-policy` Team

| Model | Venue | Inputs | Outputs | Similarity (FGD ↓) | Audio Alignment (BC ↑) | Diversity (L1Div ↑) | Links |
|-------|-------|--------|---------|--------------------|------------------------|---------------------|-------|
| **Real Data** | — | — | Full Body + Face | 0.000 | 0.703 | 11.97 | [BEAT2 Dataset](https://huggingface.co/datasets/haiyangliu0/BEAT2) |
| **DisCo** (Haiyang Liu et al.) | ACM MM 2022 | Audio | Upper + Hands | 0.942 | 0.643 | 9.91 | [Weights](https://huggingface.co/haiyangliu0/disco_audio/tree/main) · [Paper](https://dl.acm.org/doi/abs/10.1145/3503161.3548400) |
| **CaMN** (Haiyang Liu et al.) | ECCV 2022 | Audio | Upper + Hands | 0.664 | 0.676 | 10.86 | [Weights](https://huggingface.co/haiyangliu0/camn_audio/tree/main) · [Paper](https://www.ecva.net/papers/eccv_2022/papers_ECCV/papers/136670605.pdf) |
| **EMAGE** (Haiyang Liu et al.) | CVPR 2024 | Audio + Text | Full Body + Face | 0.551 | 0.772 | 13.06 | [Weights](https://huggingface.co/haiyangliu0/emage_audio/tree/main) · [Paper](https://arxiv.org/abs/2401.00374) |
| **GestureLSM** (Pinxin Liu et al.) | ICCV 2025 | Audio + Text | Full Body + Face | 0.409 | 0.714 | 13.24 | [Code](https://github.com/andypinxinliu/GestureLSM) · [Paper](https://arxiv.org/abs/2501.18898) |
| **Intentional-Gesture** (Pinxin Liu et al.) | NeurIPS 2026 | Audio + Text | Full Body + Face | 0.379 | 0.690 | 11.00 | [Code](https://github.com/andypinxinliu/Intentional-Gesture) · [Paper](https://arxiv.org/abs/2505.15197) |
| **PersonaGesture** (Xiangyue Zhang et al.) | 2026 | Audio + Ref Clip | Full Body | — | — | — | [Paper](https://arxiv.org/abs/2605.06064) |
| **GestureFAR** (Pinxin Liu et al.) | 2026 | Streaming Audio | Full Body + Face | **0.308** | **0.741** | **13.24** | [Code](https://github.com/andypinxinliu/GestureFAR) · [Paper](https://arxiv.org/abs/2609.21576) |

### Other Community Methods Reported on BEAT2 (Speaker 2)*
*\*Summarized by agents from published papers (normalized to raw `emage_evaltools` FGD scale) and may contain inaccuracies; issues or PRs for corrections and new entries are welcome.*

| Method | Venue | Similarity (FGD ↓) | Audio Alignment (BC ↑) | Diversity (L1Div ↑) |
|--------|-------|--------------------|------------------------|---------------------|
| **Habibie et al.** (Ikhsanul Habibie et al.) | IVA 2021 | 0.904 | 0.772 | 8.21 |
| **HA2G** (Xian Liu et al.) | CVPR 2022 | 1.232 | 0.677 | 8.63 |
| **TalkSHOW** (Hongwei Yi et al.) | CVPR 2023 | 0.621 | 0.695 | 13.47 |
| **DiffuseStyleGesture** (Sicheng Yang et al.) | IJCAI 2023 | 0.881 | 0.724 | 11.49 |
| **LivelySpeaker** (Yihao Zhi et al.) | ICCV 2023 | 1.180 | 0.666 | 11.28 |
| **DiffSHEG** (Junming Chen et al.) | CVPR 2024 | 0.714 | 0.743 | 8.21 |
| **Audio2Photoreal** (Evonne Ng et al.) | CVPR 2024 | 1.020 | 0.550 | 12.47 |
| **ProbTalk** (Yifei Liu et al.) | CVPR 2024 | 0.504 | 0.771 | 13.27 |
| **SynTalker** (Bohong Chen et al.) | ACM MM 2024 | 0.469 | 0.736 | 12.43 |
| **MambaTalk** (Zunnan Xu et al.) | NeurIPS 2024 | 0.537 | 0.781 | 13.05 |
| **RAG-Gesture** (Mahmoud H. Mughal et al.) | CVPR 2025 | 0.879 | 0.730 | 12.62 |
| **SemTalk** (Xiangyue Zhang et al.) | ICCV 2025 | 0.428 | 0.777 | 12.91 |
| **MIBURI** (Mahmoud H. Mughal et al.) | CVPR 2026 | 0.806 | 0.790 | 17.50 |
| **LiveGesture** (Muhammad H. Saleem et al.) | CVPR 2026 | 0.457 | 0.794 | 13.91 |

### Datasets, Blender Add-on & Evaluation Tools

| Category | Resource 1 | Resource 2 | Resource 3 |
|----------|------------|------------|------------|
| **Datasets** | [BEAT2 (SMPL-X + FLAME)](https://huggingface.co/datasets/haiyangliu0/BEAT2) | [BEAT (BVH + ARKit)](https://huggingface.co/datasets/haiyangliu0/BEAT) | [Rendered Skeleton Videos](https://huggingface.co/datasets/haiyangliu0/BEAT_Rendered_Videos) |
| **Blender Tools** | [Blender Addon](https://huggingface.co/datasets/haiyangliu0/BEAT2_Tools/blob/main/smplx_blender_addon_20230921.zip) | [Character on BEAT](https://huggingface.co/datasets/haiyangliu0/BEAT2_Tools/blob/main/BEAT_Avatars.zip) | [Blender Render Scripts](https://huggingface.co/datasets/haiyangliu0/BEAT2_Tools/blob/main/rendervideo.zip) |
| **SMPL-X & Eval** | [SMPLX-FLAME Model](https://huggingface.co/haiyangliu0/emage_evaltools/blob/main/smplx_models/smplx/SMPLX_NEUTRAL_2020.npz) | [FGD on BEAT2](https://huggingface.co/haiyangliu0/emage_evaltools/blob/main/AESKConv_240_100.bin) | [ARKit2FLAME Tools](https://huggingface.co/datasets/haiyangliu0/BEAT2_Tools/blob/main/ARkit_FLAME.zip) |

---

## 3. Input / Output Schema

* **Input**: `.wav` mono speech audio (resampled automatically to `16,000 Hz`).
* **Output**: `.npz` dictionary at `30 FPS` (`T = int(audio_seconds * 30)`), saved via `emage_utils.motion_io.beat_format_save`:

| Key | Shape & Dtype | Specification |
|-----|---------------|---------------|
| `poses` | `(T, 165)` `float32` | SMPL-X 55-joint axis-angle (`0:3` root, `3:66` 21 body, `66:69` jaw, `69:75` eyes, `75:165` 30 hands) |
| `expressions` | `(T, 100)` `float32` | FLAME 100-D facial expression parameters |
| `trans` | `(T, 3)` `float32` | Global root translation in meters |
| `betas` | `(300,)` `float32` | SMPL-X shape parameters |
| `mocap_frame_rate` | `30` | Frame rate (`30` FPS) |
| `gender` / `model` | `"neutral"` / `"smplx2020"` | Mesh topology identifiers |

---

## 4. Environment, Inference, Evaluation & Training (Agent Execution Spec)

### 4.1 Environment Setup (`uv`)

```bash
git clone https://github.com/haiyangliu0/character-policy.git
cd character-policy

uv venv .venv --python 3.10
source .venv/bin/activate
uv pip install "setuptools<70" pip wheel "numpy<1.24"
uv pip install torch torchvision torchaudio librosa==0.9.2 soundfile scipy scikit-learn tqdm pyyaml wandb
uv pip install transformers==4.46.3 huggingface_hub accelerate einops timm
uv pip install smplx==0.1.28 trimesh pyrender pyopengl imageio moviepy==1.0.3 opencv-python wget
uv pip install --no-build-isolation chumpy

git clone https://huggingface.co/haiyangliu0/emage_evaltools
```

### 4.2 Inference & Video Rendering

```bash
# EMAGE (Full Body + Hands + Face): outputs .npz and .mp4 to ./examples/motion
# Expected evaluation output on ./examples/audio: fgd ≈ 0.619, bc ≈ 0.790, l1 ≈ 12.64
python test_emage_audio.py --audio_folder ./examples/audio --save_folder ./examples/motion --visualization

# CaMN / DisCo (Upper Body + Hands)
python test_camn_audio.py --audio_folder ./examples/audio --save_folder ./examples/motion --visualization --nopytorch3d
python test_disco_audio.py --audio_folder ./examples/audio --save_folder ./examples/motion --visualization --nopytorch3d
```

### 4.3 Direct Python API

```python
import torch, librosa
from models.emage_audio import EmageAudioModel, EmageVQVAEConv, EmageVAEConv
from emage_utils.motion_io import beat_format_save
from emage_utils import fast_render

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
    beat_format_save(
        "./examples/motion/out.npz",
        out["rec_pose"].squeeze(0).cpu().numpy(),
        upsample=30,
        expressions=out["rec_exp"].squeeze(0).cpu().numpy(),
        trans=out["rec_trans"].squeeze(0).cpu().numpy(),
    )

fast_render.render_one_sequence_no_gt("./examples/motion/out.npz", "./examples/audio/2_scott_0_1_1.wav", "./examples/motion/")
```

### 4.4 Training on BEAT2 or Custom Speaker Data

```bash
hf download haiyangliu0/BEAT2 --repo-type dataset --local-dir ./BEAT2
python ./datasets/foot_contact.py

# Optional: train VQ-VAEs (pretrained VQ-VAEs from haiyangliu0/emage_audio are used if skipped)
torchrun --nproc_per_node=1 train_emage_audio.py --config ./configs/emage_audio.yaml --train_vq

# Train policy model
torchrun --nproc_per_node=1 train_emage_audio.py --config ./configs/emage_audio.yaml --evaluation
torchrun --nproc_per_node=1 train_camn_audio.py --config ./configs/camn_audio.yaml --evaluation
torchrun --nproc_per_node=1 train_disco_audio.py --config ./configs/disco_audio.yaml --evaluation
```
