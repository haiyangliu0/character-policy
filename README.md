<div align="center">
<h1>character-policy<br>multimodal interactive 3D character policy</h1>
<code>character-policy</code> is an open-source research project for multimodal interactive 3D character policies:
<br>
(1) generating face and body animation from speech &nbsp;·&nbsp; (2) generating body animation from text
<br>
It works as an API that takes speech, text, trajectory, or scene inputs and outputs standard 3D motion parameters
<br>
such as SMPL, transferable to iPhone ARKit Blendshape weights, Vicon Skeleton BVH files, or game engines.
</div>

<br>

<div align="center">
    <a href="https://huggingface.co/spaces/haiyangliu0/EMAGE"><img src="https://img.shields.io/badge/Try_Our_Demo-HuggingFace_Space-blue?logo=huggingface"></a>
    <a href="https://huggingface.co/haiyangliu0/emage_audio"><img src="https://img.shields.io/badge/Weights-HuggingFace_Models-yellow?logo=huggingface"></a>
    <a href="https://huggingface.co/datasets/haiyangliu0/BEAT2"><img src="https://img.shields.io/badge/Dataset-HuggingFace_Datasets-green?logo=huggingface"></a>
</div>

<br>

## News

- [2026.09] Released **[World2Motion](https://fyantu.github.io/World2Motion/)** for scene-aware 3D motion generation.
- [2026.09] Released **[Triangular Resampling](https://arxiv.org/abs/2609.34697)** for long-horizon streaming motion generation.
- [2026.09] Released **[FloodDiffusion 2](https://alayalab.github.io/FloodDiffusion2/)** for path-controllable streaming motion generation.
- [2026.09] Released **[GestureFAR](https://arxiv.org/abs/2609.21576)** for streaming co-speech gesture generation.
- [2026.09] **[Intentional-Gesture](https://andypinxinliu.github.io/Intentional-Gesture/)** accepted to NeurIPS 2026.
- [2026.05] Released **[PersonaGesture](https://arxiv.org/pdf/2605.06064v1)** for single-reference speaker style personalization.
- [2026.02] **[FloodDiffusion](https://shandaai.github.io/FloodDiffusion/)** accepted to CVPR 2026 (Highlight).
- [2025.07] **[GestureLSM](https://andypinxinliu.github.io/GestureLSM/)** accepted to ICCV 2025.

---

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

## 2. Models, Weights & Benchmarks

### 2.1 Generating Face and Body Animation from Speech (BEAT2)

All outputs are in SMPL-X (body + hands) and FLAME (face) parameters evaluated on BEAT2 (Speaker 2 `Scott`).

#### Models from `character-policy` Team

| Model | Venue | Similarity<br>(FGD ↓) | Audio Alignment<br>(BC ↑) | Diversity<br>(Div →) | Inputs | Outputs | Links |
|-------|-------|--------------------|------------------------|---------------------|--------|---------|-------|
| **Real Data** | — | — | 0.703 | 11.97 | — | Full Body + Face | [BEAT2 Dataset](https://huggingface.co/datasets/haiyangliu0/BEAT2) |
| **DisCo** (Haiyang Liu et al.) | ACM MM 2022 | 0.942 | 0.643 | 9.91 | Audio | Upper + Hands | [Weights](https://huggingface.co/haiyangliu0/disco_audio/tree/main) · [Paper](https://dl.acm.org/doi/abs/10.1145/3503161.3548400) |
| **CaMN** (Haiyang Liu et al.) | ECCV 2022 | 0.664 | 0.676 | 10.86 | Audio | Upper + Hands | [Weights](https://huggingface.co/haiyangliu0/camn_audio/tree/main) · [Paper](https://www.ecva.net/papers/eccv_2022/papers_ECCV/papers/136670605.pdf) |
| **EMAGE** (Haiyang Liu et al.) | CVPR 2024 | 0.551 | 0.772 | 13.06 | Audio + Text | Full Body + Face | [Weights](https://huggingface.co/haiyangliu0/emage_audio/tree/main) · [Paper](https://arxiv.org/abs/2401.00374) |
| **GestureLSM** (Pinxin Liu et al.) | ICCV 2025 | 0.409 | 0.714 | 13.24 | Audio + Text | Full Body + Face | [Code](https://github.com/andypinxinliu/GestureLSM) · [Paper](https://arxiv.org/abs/2501.18898) |
| **Intentional-Gesture** (Pinxin Liu et al.) | NeurIPS 2026 | 0.379 | 0.690 | 11.00 | Audio + Text | Full Body + Face | [Code](https://github.com/andypinxinliu/Intentional-Gesture) · [Paper](https://arxiv.org/abs/2505.15197) |
| **PersonaGesture** (Xiangyue Zhang et al.) | ArXiv 2026 | 0.393 | 0.710 | 13.25 | Audio + Ref Clip | Full Body + Face | [Paper](https://arxiv.org/pdf/2605.06064v1) |
| **GestureFAR** (Pinxin Liu et al.) | ArXiv 2026 | 0.308 | 0.741 | 13.24 | Streaming Audio | Full Body + Face | [Code](https://github.com/andypinxinliu/GestureFAR) · [Paper](https://arxiv.org/abs/2609.21576) |

#### Models from Community*
*\*Agent-summarized models reported on BEAT2 (Speaker 2); may contain inaccuracies, issues or PRs for corrections and new entries are welcome.*

| Model | Venue | Similarity<br>(FGD ↓) | Audio Alignment<br>(BC ↑) | Diversity<br>(Div →) | Links |
|-------|-------|--------------------|------------------------|---------------------|-------|
| **LivelySpeaker** (Yihao Zhi et al.) | ICCV 2023 | 1.180 | 0.666 | 11.28 | [Code](https://github.com/zyhbili/LivelySpeaker) · [Paper](https://arxiv.org/abs/2309.09294) |
| **DiffSHEG** (Junming Chen et al.) | CVPR 2024 | 0.714 | 0.743 | 8.21 | [Code](https://github.com/JeremyCJM/DiffSHEG) · [Paper](https://arxiv.org/abs/2401.04747) |
| **Audio2Photoreal** (Evonne Ng et al.) | CVPR 2024 | 1.020 | 0.550 | 12.47 | [Code](https://github.com/facebookresearch/audio2photoreal) · [Paper](https://arxiv.org/abs/2401.01885) |
| **ProbTalk** (Yifei Liu et al.) | CVPR 2024 | 0.504 | 0.771 | 13.27 | [Code](https://github.com/uuembodiedsocialai/ProbTalk3D) · [Paper](https://arxiv.org/abs/2409.07966) |
| **SynTalker** (Bohong Chen et al.) | ACM MM 2024 | 0.469 | 0.736 | 12.43 | [Code](https://github.com/RobinWitch/SynTalker) · [Paper](https://arxiv.org/abs/2410.00464) |
| **MambaTalk** (Zunnan Xu et al.) | NeurIPS 2024 | 0.537 | 0.781 | 13.05 | [Code](https://github.com/kkakkkka/MambaTalk) · [Paper](https://arxiv.org/abs/2403.09471) |
| **RAG-Gesture** (Mahmoud H. Mughal et al.) | CVPR 2025 | 0.879 | 0.730 | 12.62 | [Code](https://github.com/m-hamza-mughal/RAG-Gesture) · [Paper](https://arxiv.org/abs/2412.06786) |
| **SemTalk** (Xiangyue Zhang et al.) | ICCV 2025 | 0.428 | 0.777 | 12.91 | [Code](https://github.com/Xiangyue-Zhang/SemTalk) · [Paper](https://arxiv.org/abs/2412.16563) |
| **MIBURI** (Mahmoud H. Mughal et al.) | CVPR 2026 | 0.806 | 0.790 | 17.50 | [Code](https://github.com/m-hamza-mughal/miburi) · [Paper](https://arxiv.org/abs/2603.03282) |
| **LiveGesture** (Muhammad H. Saleem et al.) | CVPR 2026 | 0.457 | 0.794 | 13.91 | [Paper](https://arxiv.org/abs/2604.10927) |

### 2.2 Generating Body Animation from Text (HumanML3D)

All outputs are 3D body motion parameters evaluated on HumanML3D.

#### Models from `character-policy` Team

| Model | Venue | Similarity<br>(FID ↓) | Text Alignment<br>(R@3 ↑) | Diversity<br>(Div →) | Inputs | Outputs | Links |
|-------|-------|--------------------|------------------------|-------------------|--------|---------|-------|
| **Real Motion** | — | — | 0.797 | 9.50 | — | Full Body | [HumanML3D](https://github.com/EricGuo5513/HumanML3D) |
| **FloodDiffusion** (Yiyi Cai et al.) | CVPR 2026 | 0.057 | 0.810 | 9.58 | Streaming Text | Full Body | [Code](https://github.com/ShandaAI/FloodDiffusion) · [Paper](https://arxiv.org/abs/2512.03520) |
| **FloodDiffusion 2** (Yiyi Cai et al.) | ArXiv 2026 | 0.050 | 0.816 | 9.31 | Streaming Text + Path | Full Body + Trajectory | [Code](https://github.com/caiyy17/FloodDiffusion2) · [Paper](https://arxiv.org/abs/2609.33167) |
| **Triangular Resampling** (Kunhang Li et al.) | ArXiv 2026 | — | — | — | Streaming Text | Full Body | [Paper](https://arxiv.org/abs/2609.34697) |
| **World2Motion** (Fangyuan Tu et al.) | ArXiv 2026 | — | — | — | Image + Text | Full Body + Video | [Project](https://fyantu.github.io/World2Motion/) · [Paper](https://arxiv.org/abs/2609.37004) |

#### Models from Community*
*\*Agent-summarized models reported on HumanML3D; may contain inaccuracies, issues or PRs for corrections and new entries are welcome.*

| Model | Venue | Similarity<br>(FID ↓) | Text Alignment<br>(R@3 ↑) | Diversity<br>(Div →) | Links |
|-------|-------|--------------------|------------------------|-------------------|-------|
| **MDM** (Guy Tevet et al.) | ICLR 2023 | 0.544 | 0.611 | 9.56 | [Code](https://github.com/GuyTevet/motion-diffusion-model) · [Paper](https://arxiv.org/abs/2209.14916) |
| **MLD** (Xin Chen et al.) | CVPR 2023 | 0.473 | 0.772 | 9.72 | [Code](https://github.com/ChenFengYe/motion-latent-diffusion) · [Paper](https://arxiv.org/abs/2212.04048) |
| **T2M-GPT** (Jianrong Zhang et al.) | CVPR 2023 | 0.141 | 0.775 | 9.72 | [Code](https://github.com/Mael-zys/T2M-GPT) · [Paper](https://arxiv.org/abs/2301.06052) |
| **ReMoDiffuse** (Mingyuan Zhang et al.) | ICCV 2023 | 0.103 | 0.795 | 9.02 | [Code](https://github.com/mingyuan-zhang/ReMoDiffuse) · [Paper](https://arxiv.org/abs/2304.01116) |
| **FineMoGen** (Mingyuan Zhang et al.) | NeurIPS 2023 | 0.151 | 0.784 | 9.26 | [Code](https://github.com/mingyuan-zhang/FineMoGen) · [Paper](https://arxiv.org/abs/2312.15004) |
| **OmniControl** (Yiming Xie et al.) | ICLR 2024 | 0.100 | 0.804 | 9.69 | [Code](https://github.com/neu-vi/OmniControl) · [Paper](https://arxiv.org/abs/2310.08580) |
| **MMM** (Ekkasit Pinyoanuntapong et al.) | CVPR 2024 | 0.089 | 0.804 | 9.41 | [Code](https://github.com/exitudio/MMM) · [Paper](https://arxiv.org/abs/2312.03596) |
| **MoMask** (Chuan Guo et al.) | CVPR 2024 | 0.045 | 0.807 | 9.68 | [Code](https://github.com/EricGuo5513/momask-codes) · [Paper](https://arxiv.org/abs/2312.00063) |
| **Motion Mamba** (Zeyu Zhang et al.) | ECCV 2024 | 0.281 | 0.792 | 9.87 | [Code](https://github.com/steve-zeyu-zhang/MotionMamba) · [Paper](https://arxiv.org/abs/2403.07487) |
| **ParCo** (Qiran Zou et al.) | ECCV 2024 | 0.109 | 0.795 | 9.57 | [Code](https://github.com/qrzou/ParCo) · [Paper](https://arxiv.org/abs/2403.18512) |
| **MotionLCM** (Wenxun Dai et al.) | ECCV 2024 | 0.304 | 0.798 | 9.61 | [Code](https://github.com/Dai-Wenxun/MotionLCM) · [Paper](https://arxiv.org/abs/2404.19759) |
| **BAMM** (Ekkasit Pinyoanuntapong et al.) | ECCV 2024 | 0.055 | 0.814 | 9.72 | [Code](https://github.com/exitudio/BAMM) · [Paper](https://arxiv.org/abs/2403.19435) |
| **MoGenTS** (Weihao Yuan et al.) | NeurIPS 2024 | 0.033 | 0.812 | 9.57 | [Code](https://github.com/weihaoyuan/MoGenTS) · [Paper](https://arxiv.org/abs/2409.17686) |
| **DART** (Kaifeng Zhao et al.) | ICLR 2025 | 0.854 | 0.722 | 9.50 | [Code](https://github.com/zkf1997/DART) · [Paper](https://arxiv.org/abs/2410.05260) |
| **MARDM** (Zichong Meng et al.) | CVPR 2025 | 0.114 | 0.795 | 9.66 | [Code](https://github.com/neu-vi/MARDM) · [Paper](https://arxiv.org/abs/2411.16543) |
| **SALAD** (Seokhyeon Hong et al.) | CVPR 2025 | 0.076 | 0.857 | 9.70 | [Code](https://github.com/seokhyeonhong/salad) · [Paper](https://arxiv.org/abs/2503.13836) |
| **PRIMAL** (Yan Zhang et al.) | ICCV 2025 | 0.511 | 0.780 | 9.52 | [Code](https://github.com/zycliao/PRIMAL) · [Paper](https://arxiv.org/abs/2503.21899) |
| **MotionStreamer** (Lixing Xiao et al.) | ICCV 2025 | 0.092 | 0.802 | 9.72 | [Code](https://github.com/zju3dv/MotionStreamer) · [Paper](https://arxiv.org/abs/2503.15451) |
| **MoMask++** (Chuan Guo et al.) | NeurIPS 2025 | 0.072 | 0.811 | 9.56 | [Code](https://github.com/Snap-Research/SnapMoGen) · [Paper](https://arxiv.org/abs/2507.09122) |
| **Event-T2M** (Seong-Eun Hong et al.) | ICLR 2026 | 0.056 | 0.842 | 9.61 | [Project](https://tjswodud.github.io/EventT2M/) · [Paper](https://arxiv.org/abs/2602.04292) |
| **CMDM** (Qing Yu et al.) | CVPR 2026 | 0.068 | 0.860 | 9.44 | [Code](https://github.com/YU1ut/CMDM) · [Paper](https://arxiv.org/abs/2602.22594) |
| **MotionHiFlow** (Heng Li et al.) | CVPR 2026 | 0.032 | 0.843 | 9.50 | [Paper](https://arxiv.org/abs/2604.23264) |
| **ScaleMoGen** (Inwoo Hwang et al.) | ECCV 2026 | 0.030 | 0.856 | 9.54 | [Project](https://inwoohwang.me/ScaleMoGen) · [Paper](https://arxiv.org/abs/2605.11704) |
| **BiMoGen** (Wanjiang Weng et al.) | NeurIPS 2026 | 0.047 | 0.818 | 9.42 | [Paper](https://arxiv.org/abs/2609.35407) |

---

## 3. Data & Tools

#### Data & Tools from `character-policy` Team

| Resource | Description | Links |
|----------|-------------|-------|
| **BEAT2** | 76h co‑speech 3D body, hand & face dataset (30 speakers, SMPL‑X + FLAME) | [HuggingFace](https://huggingface.co/datasets/haiyangliu0/BEAT2) |
| **BEAT** | 76h co‑speech 3D body, hand & face dataset (30 speakers, BVH + ARKit) | [HuggingFace](https://huggingface.co/datasets/haiyangliu0/BEAT) |
| **EMAGE Eval Tools** | BEAT2 evaluation (FGD / BC / Div) & neutral SMPL‑X model | [HuggingFace](https://huggingface.co/haiyangliu0/emage_evaltools) |
| **ARKit2FLAME** | Convert between FLAME (100‑D) and iPhone ARKit (52‑D) blendshapes | [Download](https://huggingface.co/datasets/haiyangliu0/BEAT2_Tools/blob/main/ARkit_FLAME.zip) |
| **Blender SMPL‑X Add‑on** | Import and animate SMPL‑X + FLAME `.npz` files in Blender | [Download](https://huggingface.co/datasets/haiyangliu0/BEAT2_Tools/blob/main/smplx_blender_addon_20230921.zip) |
| **BEAT Avatars & Renderer** | Rigged 3D character avatars and batch video rendering scripts | [Avatars](https://huggingface.co/datasets/haiyangliu0/BEAT2_Tools/blob/main/BEAT_Avatars.zip) · [Scripts](https://huggingface.co/datasets/haiyangliu0/BEAT2_Tools/blob/main/rendervideo.zip) |

---

## 4. For Agents Using This Repo

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

# Inference & rendering (.npz + .mp4 to ./examples/motion)
python test_emage_audio.py --audio_folder ./examples/audio --save_folder ./examples/motion --visualization
python test_camn_audio.py --audio_folder ./examples/audio --save_folder ./examples/motion --visualization --nopytorch3d
python test_disco_audio.py --audio_folder ./examples/audio --save_folder ./examples/motion --visualization --nopytorch3d

# Training on BEAT2
hf download haiyangliu0/BEAT2 --repo-type dataset --local-dir ./BEAT2
python ./datasets/foot_contact.py
torchrun --nproc_per_node=1 train_emage_audio.py --config ./configs/emage_audio.yaml --evaluation
```

---

<div align="center">
For custom speaker/character style capture or commercial collaboration: <a href="mailto:haiyangliu1997@gmail.com">✉️</a>
</div>
