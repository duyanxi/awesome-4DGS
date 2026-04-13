# Awesome 4D Gaussian Splatting

> A curated repository of papers, code, benchmarks, and research notes for **4D Gaussian Splatting (4DGS)**, spanning dynamic scene reconstruction, native 4D representations, compression, editing, and domain-specific applications such as avatars and surgical scenes.


## Overview

**3D Gaussian Splatting (3DGS)** represents a static scene with a set of anisotropic Gaussians that can be rasterized efficiently for high-quality real-time rendering.  
**4D Gaussian Splatting (4DGS)** extends this idea from static geometry to **space-time**, enabling dynamic scene reconstruction and novel view synthesis from videos.

In practice, most 4DGS methods can be understood as adding one or more of the following on top of 3DGS:

- a **spatiotemporal representation**
- a **motion/deformation model**
- a **training prior** for sparse or monocular videos
- a **compression / deployment layer** for real-time systems

## Taxonomy

### 1. Representation
These methods focus on how dynamic scenes are parameterized: per-frame Gaussians, canonical Gaussians with time-dependent deformation, native 4D Gaussians, or hybrid explicit-implicit structures. The representation determines memory use, interpolation behavior, editability, and rendering speed.

### 2. Motion Modeling
These methods improve how Gaussian attributes evolve over time, often through deformation fields, flow, splines, control points, or factorized dynamics. Good motion models reduce temporal flicker and help preserve identity under large motion and occlusion.

### 3. Sparse-view / Few-shot
These methods target the hardest practical regime: monocular, casual, or sparse multi-view video. They typically add stronger priors, geometry regularization, tracking cues, or learned initialization to overcome severe ambiguity.

### 4. Real-time / Mobile / Efficient
These works prioritize deployment constraints such as low latency, small memory, fast optimization, or streaming. Efficiency matters because dynamic Gaussian models can become too large or too expensive to update frame by frame.

### 5. Learning-based Methods
These methods move beyond per-scene optimization and inject learned priors from data, such as feed-forward prediction, generative dynamics, context modeling, or reusable motion modules. This category is increasingly important for scaling 4DGS to in-the-wild videos.

### 6. Editing / Understanding
These works use 4DGS as an editable and semantically meaningful representation rather than only a rendering primitive. Typical goals include segmentation, controllable editing, mesh extraction, and scene-level manipulation.

### 7. Domain-specific Applications
These methods adapt 4DGS to structured settings such as surgical videos, avatars, or HDR capture. They are important because domain constraints often reveal what kinds of priors are actually needed for robust 4D reconstruction.

## Papers by Category

> Note: some papers appear in multiple sections when they make substantive contributions to more than one problem setting, such as both `Avatar Applications` and `Immersive Media / Volumetric Video`.

### Representation

- **4D Gaussian Splatting for Real-Time Dynamic Scene Rendering (2024)** [[paper](https://arxiv.org/abs/2310.08528)] [[project](https://guanjunwu.github.io/4dgs/)]
  - ⭐ Key idea: models dynamic scenes with explicit 3D Gaussians plus decomposed 4D neural voxels to achieve real-time rendering without training a separate model per frame.
  - 🧩 Category: Representation
  - 🏷️ Tags: real-time, hybrid explicit-implicit, canonical deformation

- **4D-Rotor Gaussian Splatting: Towards Efficient Novel View Synthesis for Dynamic Scenes (2024)** [[paper](https://arxiv.org/abs/2402.03307)] [[code](https://github.com/weify627/4D-Rotor-Gaussians)]
  - ⭐ Key idea: represents the scene directly with native anisotropic XYZT Gaussians and rotor-based transforms to avoid heavy deformation machinery.
  - 🧩 Category: Representation
  - 🏷️ Tags: native-4D, efficient, real-time

- **Spacetime Gaussian Feature Splatting for Real-Time Dynamic View Synthesis (2024)** [[paper](https://arxiv.org/abs/2312.16812)] [[project](https://oppo-us-research.github.io/SpacetimeGaussians-website/)]
  - ⭐ Key idea: augments Gaussians with temporal opacity, parametric motion, and neural feature splatting to better capture transient content and view-time dependent appearance.
  - 🧩 Category: Representation
  - 🏷️ Tags: real-time, feature-rendering, high-resolution

- **ST-4DGS: Spatial-Temporally Consistent 4D Gaussian Splatting for Efficient Dynamic Scene Rendering (2024)** [[code](https://github.com/wanglids/ST-4DGS)]
  - ⭐ Key idea: improves 4D Gaussian compactness and surface adherence by enforcing spatial-temporal consistency during motion-aware reconstruction.
  - 🧩 Category: Representation
  - 🏷️ Tags: real-time, compactness, consistency

- **4D Gaussian Splatting: Modeling Dynamic Scenes with Native 4D Primitives (2024)** [[paper](https://arxiv.org/abs/2412.20720)] [[code](https://github.com/fudan-zvg/4d-gaussian-splatting)]
  - ⭐ Key idea: treats a dynamic scene as a true spatiotemporal volume of native 4D Gaussians optimized directly from photometric evidence.
  - 🧩 Category: Representation
  - 🏷️ Tags: native-4D, photometric-only, continuous-time

- **7DGS: Unified Spatial-Temporal-Angular Gaussian Splatting (2025)** [[paper](https://arxiv.org/abs/2503.07946)]
  - ⭐ Key idea: extends Gaussian parameterization from 4D space-time to 7D space-time-viewing direction so dynamics and view-dependent effects are modeled jointly.
  - 🧩 Category: Representation
  - 🏷️ Tags: view-dependent, unified-model, dynamic appearance

### Motion Modeling

- **GaussianFlow: Splatting Gaussian Dynamics for 4D Content Creation (2024)** [[paper](https://arxiv.org/abs/2403.12365)] [[project](https://zerg-overmind.github.io/GaussianFlow.github.io/)]
  - ⭐ Key idea: introduces Gaussian flow by splatting 3D Gaussian dynamics into dense 2D motion fields to stabilize motion learning for 4D generation and rendering.
  - 🧩 Category: Motion Modeling
  - 🏷️ Tags: optical-flow, motion-supervision, generation

- **Fully Explicit Dynamic Gaussian Splatting (2024)** [[paper](https://arxiv.org/abs/2410.15629)] [[code](https://github.com/juno181/Ex4DGS)]
  - ⭐ Key idea: explicitly samples dynamic Gaussian poses at sparse timestamps and interpolates them to reduce computation while separating static and dynamic content.
  - 🧩 Category: Motion Modeling
  - 🏷️ Tags: explicit-dynamics, interpolation, static-dynamic split

- **SplineGS: Robust Motion-Adaptive Spline for Real-Time Dynamic 3D Gaussians from Monocular Video (2025)** [[paper](https://papers.cool/venue/Park_SplineGS_Robust_Motion-Adaptive_Spline_for_Real-Time_Dynamic_3D_Gaussians_from%40CVPR2025%40CVF)]
  - ⭐ Key idea: models Gaussian trajectories with motion-adaptive cubic splines and prunes control points to capture complex motion efficiently from monocular input.
  - 🧩 Category: Motion Modeling
  - 🏷️ Tags: monocular, spline-motion, COLMAP-free

- **Gaussian Sequences with Multi-Scale Dynamics for 4D Reconstruction from Monocular Casual Videos (2026)** [[paper](https://arxiv.org/abs/2602.13806)]
  - ⭐ Key idea: factorizes dynamics into multiple scales so Gaussian motion can remain plausible under highly ambiguous monocular casual-video settings.
  - 🧩 Category: Motion Modeling
  - 🏷️ Tags: monocular, multi-scale motion, casual video

### Sparse-view / Few-shot

- **MoSca: Dynamic Gaussian Fusion from Casual Videos via 4D Motion Scaffolds (2025)** [[paper](https://arxiv.org/abs/2405.17421)] [[project](https://www.cis.upenn.edu/~leijh/projects/mosca/)]
  - ⭐ Key idea: introduces 4D motion scaffolds that provide structured motion priors, making dynamic Gaussian fusion work better for casual and sparse observations.
  - 🧩 Category: Sparse-view / Few-shot
  - 🏷️ Tags: casual video, motion prior, sparse-view

- **Efficient Gaussian Splatting for Monocular Dynamic Scene Rendering via Sparse Time-Variant Attribute Modeling (2025)** [[paper](https://arxiv.org/abs/2502.20378)]
  - ⭐ Key idea: models only sparse time-varying Gaussian attributes so monocular dynamic rendering stays efficient while retaining temporal expressiveness.
  - 🧩 Category: Sparse-view / Few-shot
  - 🏷️ Tags: monocular, efficient, sparse temporal updates

- **SDD-4DGS: State-Space Decomposition and Denoising for Few-shot Dynamic Scene Reconstruction with 4D Gaussian Splatting (2025)** [[paper](https://arxiv.org/abs/2503.09332)]
  - ⭐ Key idea: decomposes dynamic state variables and denoises them to improve reconstruction robustness when only a few dynamic views are available.
  - 🧩 Category: Sparse-view / Few-shot
  - 🏷️ Tags: few-shot, denoising, robust reconstruction

- **Mono4DGS-HDR: High Dynamic Range 4D Gaussian Splatting from Alternating-exposure Monocular Videos (2025)** [[paper](https://arxiv.org/abs/2510.18489)] [[project](https://liujf1226.github.io/Mono4DGS-HDR/)]
  - ⭐ Key idea: reconstructs HDR 4D scenes from unposed alternating-exposure monocular videos by combining geometric initialization, static HDR estimation, and temporally regularized dynamic optimization.
  - 🧩 Category: Sparse-view / Few-shot
  - 🏷️ Tags: monocular, HDR, in-the-wild

### Real-time / Mobile / Efficient

- **QUEEN: QUantized Efficient ENcoding of Dynamic Gaussians for Streaming Free-viewpoint Videos (2024)** [[paper](https://arxiv.org/abs/2412.04469)] [[project](https://research.nvidia.com/labs/amri/projects/queen/)] [[code](https://github.com/NVlabs/queen)]
  - ⭐ Key idea: learns quantized residual updates for dynamic Gaussians so free-viewpoint video can be streamed with small per-frame payloads and fast rendering.
  - 🧩 Category: Real-time / Mobile / Efficient
  - 🏷️ Tags: streaming, compression, free-viewpoint video

- **LGS: A Light-weight 4D Gaussian Splatting for Efficient Surgical Scene Reconstruction (2024)** [[paper](https://papers.miccai.org/miccai-2024/461-Paper0827.html)] [[code](https://github.com/CUHK-AIM-Group/LGS)]
  - ⭐ Key idea: compresses 4D Gaussian representations through pruning and attribute reduction to make deformable surgical reconstruction lighter and faster.
  - 🧩 Category: Real-time / Mobile / Efficient
  - 🏷️ Tags: lightweight, medical, pruning

- **Light4GS: Lightweight Compact 4D Gaussian Splatting Generation via Context Model (2025)** [[paper](https://arxiv.org/abs/2503.13948)]
  - ⭐ Key idea: uses context-aware coding and compact dynamic Gaussian design to reduce storage without discarding essential motion cues.
  - 🧩 Category: Real-time / Mobile / Efficient
  - 🏷️ Tags: compact model, compression, deployment

- **GIFStream: 4D Gaussian-based Immersive Video with Feature Stream (2025)** [[paper](https://arxiv.org/abs/2505.07539)] [[project](https://xdimlab.github.io/GIFStream/)]
  - ⭐ Key idea: encodes dynamic Gaussian features as a streamable representation to improve bitrate-quality trade-offs for immersive free-viewpoint video.
  - 🧩 Category: Real-time / Mobile / Efficient
  - 🏷️ Tags: immersive-video, compression, streaming

- **Instant4D: 4D Gaussian Splatting in Minutes (2025)** [[paper](https://arxiv.org/abs/2510.01119)] [[project](https://instant4d.github.io/)]
  - ⭐ Key idea: combines fast monocular reconstruction and aggressive grid pruning to recover practical 4D Gaussian scenes from casual videos in minutes.
  - 🧩 Category: Real-time / Mobile / Efficient
  - 🏷️ Tags: fast optimization, monocular, practical pipeline

### Learning-based Methods

- **MotionGS: Exploring Explicit Motion Guidance for Deformable 3D Gaussian Splatting (2024)** [[paper](https://arxiv.org/abs/2410.07707)] [[project](https://ruijiezhu94.github.io/MotionGS_page/)] [[code](https://github.com/RuijieZhu94/MotionGS)]
  - ⭐ Key idea: injects explicit motion guidance and camera pose refinement into deformable Gaussian optimization to reduce motion ambiguity and stabilize training.
  - 🧩 Category: Learning-based Methods
  - 🏷️ Tags: motion-prior, pose-refinement, dynamic reconstruction

- **DGNS: Deformable Gaussian Splatting and Dynamic Neural Surface for Monocular Dynamic 3D Reconstruction (2024)** [[paper](https://arxiv.org/abs/2412.03910)]
  - ⭐ Key idea: couples deformable Gaussian rendering with a dynamic neural surface to improve geometry quality and temporal coherence from monocular video.
  - 🧩 Category: Learning-based Methods
  - 🏷️ Tags: monocular, surface prior, deformable model

- **GS-DiT: Advancing Video Generation with Dynamic 3D Gaussian Fields through Efficient Dense 3D Point Tracking (2025)** [[paper](https://openaccess.thecvf.com/content/CVPR2025/html/Bian_GS-DiT_Advancing_Video_Generation_with_Dynamic_3D_Gaussian_Fields_through_CVPR_2025_paper.html)] [[project](https://wkbian.github.io/Projects/GS-DiT/)]
  - ⭐ Key idea: uses tracked dynamic Gaussian fields as a structured intermediate representation to make camera-controllable video generation more 4D-aware.
  - 🧩 Category: Learning-based Methods
  - 🏷️ Tags: video-generation, controllable-camera, learned prior

### Editing / Understanding

- **Segment Any 4D Gaussians (2024)** [[paper](https://arxiv.org/abs/2407.04504)] [[project](https://jsxzs.github.io/sa4d)] [[code](https://github.com/jsxzs/SA4D)]
  - ⭐ Key idea: brings promptable segmentation into the 4D Gaussian space so dynamic scenes become editable at the object and region level.
  - 🧩 Category: Editing / Understanding
  - 🏷️ Tags: segmentation, promptable, scene editing

- **Dynamic Gaussians Mesh: Consistent Mesh Reconstruction from Dynamic Scenes (2024)** [[paper](https://arxiv.org/abs/2404.12379)] [[code](https://github.com/Isabella98Liu/DG-Mesh)]
  - ⭐ Key idea: converts dynamic Gaussian reconstructions into temporally consistent meshes to improve geometry usability for downstream graphics tasks.
  - 🧩 Category: Editing / Understanding
  - 🏷️ Tags: mesh extraction, temporal consistency, geometry

### Domain-specific Applications

These works are grouped by downstream use case rather than by representation alone. Some papers appear in more than one subsection when they are genuinely relevant to multiple application settings.

#### Avatar Applications

- **GaussianAvatars: Photorealistic Head Avatars with Rigged 3D Gaussians (2024)** [[paper](https://arxiv.org/abs/2312.02069)] [[project](https://shenhanqian.github.io/gaussian-avatars)] [[code](https://github.com/ShenhanQian/GaussianAvatars)]
  - ⭐ Key idea: rigs dynamic 3D Gaussians to a parametric face model so head avatars become photorealistic while remaining controllable in pose, expression, and viewpoint.
  - 🧩 Category: Domain-specific Applications
  - 🏷️ Tags: avatar, head, rigged-gaussians, reenactment

- **Gaussian Head Avatar: Ultra High-fidelity Head Avatar via Dynamic Gaussians (2024)** [[paper](https://arxiv.org/abs/2312.03029)]
  - ⭐ Key idea: optimizes neutral Gaussians together with an MLP deformation field to recover ultra-high-fidelity dynamic head avatars under sparse-view capture.
  - 🧩 Category: Domain-specific Applications
  - 🏷️ Tags: avatar, head, sparse-view, dynamic deformation

- **Animatable Gaussians: Learning Pose-dependent Gaussian Maps for High-fidelity Human Avatar Modeling (2024)** [[paper](https://arxiv.org/abs/2311.16096)] [[project](https://animatable-gaussians.github.io/)] [[code](https://github.com/lizhe00/AnimatableGaussians)]
  - ⭐ Key idea: learns pose-dependent front/back Gaussian maps on a parametric template to model detailed clothing and body appearance for animatable human avatars.
  - 🧩 Category: Domain-specific Applications
  - 🏷️ Tags: avatar, full-body, pose-dependent, gaussian maps

- **Animatable and Relightable Gaussians for High-fidelity Human Avatar Modeling (2024)** [[project](https://animatable-gaussians.github.io/relight/)]
  - ⭐ Key idea: extends Gaussian-map avatars with relightable appearance decomposition so animated humans can be rendered under novel illumination.
  - 🧩 Category: Domain-specific Applications
  - 🏷️ Tags: avatar, relighting, full-body, appearance decomposition

- **Drivable 3D Gaussian Avatars (2024)** [[paper](https://arxiv.org/abs/2311.08581)] [[project](https://zollhoefer.com/papers/arXiv23_D3GA/page.html)]
  - ⭐ Key idea: builds real-time drivable full-body avatars by combining Gaussian rendering with cage-based volumetric deformation driven by joints and keypoints.
  - 🧩 Category: Domain-specific Applications
  - 🏷️ Tags: avatar, drivable, full-body, telepresence

- **MeGA: Hybrid Mesh-Gaussian Head Avatar for High-Fidelity Rendering and Head Editing (2025)** [[paper](https://arxiv.org/abs/2404.19026)] [[project](https://conallwang.github.io/MeGA_Pages/)] [[code](https://github.com/conallwang/MeGA)]
  - ⭐ Key idea: uses a hybrid mesh-plus-Gaussian design to model face and hair with different primitives, improving head fidelity and enabling practical editing.
  - 🧩 Category: Domain-specific Applications
  - 🏷️ Tags: avatar, head, hybrid-representation, editing

- **LayGA: Layered Gaussian Avatars for Animatable Clothing Transfer (2024)** [[paper](https://arxiv.org/abs/2405.07319)] [[project](https://jsnln.github.io/layga/index.html)]
  - ⭐ Key idea: separates body and clothing into layered Gaussian avatars to support photorealistic clothing transfer and better garment tracking.
  - 🧩 Category: Domain-specific Applications
  - 🏷️ Tags: avatar, clothing-transfer, layered-representation, garment-tracking

- **Generalizable and Animatable Gaussian Head Avatar (2024)** [[paper](https://arxiv.org/abs/2410.07971)] [[code](https://github.com/xg-chu/GAGAvatar)]
  - ⭐ Key idea: reconstructs controllable Gaussian head avatars from a single image in one forward pass, pushing avatar creation toward one-shot and generalizable settings.
  - 🧩 Category: Domain-specific Applications
  - 🏷️ Tags: avatar, head, one-shot, generalizable

- **HRAvatar: High-Quality and Relightable Gaussian Head Avatar (2025)** [[paper](https://arxiv.org/abs/2503.08224)] [[project](https://eastbeanzhang.github.io/HRAvatar/)] [[code](https://github.com/Pixel-Talk/HRAvatar)]
  - ⭐ Key idea: combines Gaussian avatars with learnable blendshapes and physically based shading to improve monocular head reconstruction and relighting realism.
  - 🧩 Category: Domain-specific Applications
  - 🏷️ Tags: avatar, head, monocular, relightable

- **TaoAvatar: Real-Time Lifelike Full-Body Talking Avatars for Augmented Reality via 3D Gaussian Splatting (2025)** [[paper](https://arxiv.org/abs/2503.17032)] [[project](https://pixelai-team.github.io/TaoAvatar/)]
  - ⭐ Key idea: distills complex pose-dependent non-rigid deformation into a lightweight 3DGS avatar pipeline that runs in real time on AR/mobile devices.
  - 🧩 Category: Domain-specific Applications
  - 🏷️ Tags: avatar, full-body, talking-avatar, mobile, AR

- **Robust Dual Gaussian Splatting for Immersive Human-centric Volumetric Videos (DualGS) (2024)** [[paper](https://arxiv.org/abs/2409.08353)] [[project](https://nowheretrix.github.io/DualGS/)]
  - ⭐ Key idea: uses dual Gaussian layers for body motion and surface appearance so human-centric volumetric avatars stay temporally stable while remaining efficient to render and compress.
  - 🧩 Category: Domain-specific Applications
  - 🏷️ Tags: avatar, human-performance, volumetric-video, VR, immersive

- **GaussianAvatar-Editor: Photorealistic Animatable Gaussian Head Avatar Editor (2025)** [[paper](https://arxiv.org/abs/2501.09978)]
  - ⭐ Key idea: formulates text-driven editing for animatable Gaussian head avatars while explicitly handling occlusion and temporal consistency during edits.
  - 🧩 Category: Domain-specific Applications
  - 🏷️ Tags: avatar, head, editing, text-driven

#### Medical / Surgical Applications

- **EndoGaussian: Real-time Gaussian Splatting for Dynamic Endoscopic Scene Reconstruction (2024)** [[paper](https://arxiv.org/abs/2401.12561)] [[project](https://yifliu3.github.io/EndoGaussian/)] [[code](https://github.com/CUHK-AIM-Group/EndoGaussian)]
  - ⭐ Key idea: adapts dynamic Gaussian splatting to deformable endoscopic scenes with holistic initialization and spatiotemporal Gaussian tracking.
  - 🧩 Category: Domain-specific Applications
  - 🏷️ Tags: endoscopy, deformable tissue, real-time

- **LGS: A Light-weight 4D Gaussian Splatting for Efficient Surgical Scene Reconstruction (2024)** [[paper](https://papers.miccai.org/miccai-2024/461-Paper0827.html)] [[code](https://github.com/CUHK-AIM-Group/LGS)]
  - ⭐ Key idea: compresses and condenses dynamic Gaussian attributes so deformable surgical scenes can be reconstructed with lower memory and stronger deployment efficiency.
  - 🧩 Category: Domain-specific Applications
  - 🏷️ Tags: surgery, endoscopy, lightweight, efficient reconstruction

- **Feature-EndoGaussian: Feature Distilled Gaussian Splatting in Surgical Deformable Scene Reconstruction (2025)** [[paper](https://arxiv.org/abs/2503.06161)]
  - ⭐ Key idea: distills segmentation foundation-model features into dynamic surgical Gaussians to jointly improve reconstruction quality and semantic understanding.
  - 🧩 Category: Domain-specific Applications
  - 🏷️ Tags: surgery, semantics, segmentation, deformable scene

#### HDR / Challenging Imaging

- **Mono4DGS-HDR: High Dynamic Range 4D Gaussian Splatting from Alternating-exposure Monocular Videos (2025)** [[paper](https://arxiv.org/abs/2510.18489)] [[project](https://liujf1226.github.io/Mono4DGS-HDR/)]
  - ⭐ Key idea: reconstructs dynamic HDR scenes from unposed alternating-exposure monocular videos with two-stage Gaussian optimization and temporal luminance regularization.
  - 🧩 Category: Domain-specific Applications
  - 🏷️ Tags: HDR, monocular, unposed, challenging capture

#### Immersive Media / Volumetric Video

- **Robust Dual Gaussian Splatting for Immersive Human-centric Volumetric Videos (DualGS) (2024)** [[paper](https://arxiv.org/abs/2409.08353)] [[project](https://nowheretrix.github.io/DualGS/)]
  - ⭐ Key idea: disentangles motion and appearance into joint Gaussians and skin Gaussians to improve temporal coherence, compression, and immersive human performance playback.
  - 🧩 Category: Domain-specific Applications
  - 🏷️ Tags: avatar, volumetric-video, human-performance, compression, VR

- **GIFStream: 4D Gaussian-based Immersive Video with Feature Stream (2025)** [[paper](https://arxiv.org/abs/2505.07539)] [[project](https://xdimlab.github.io/GIFStream/)]
  - ⭐ Key idea: introduces feature-stream-based 4D Gaussian encoding to make immersive free-viewpoint video more streamable without sacrificing dynamic quality.
  - 🧩 Category: Domain-specific Applications
  - 🏷️ Tags: immersive-video, streaming, free-viewpoint, compression

#### Stylization / Content Creation

- **4DStyleGaussian: Zero-shot 4D Style Transfer with Gaussian Splatting (2024)** [[paper](https://arxiv.org/abs/2410.10412)]
  - ⭐ Key idea: performs zero-shot style transfer directly in dynamic Gaussian space to preserve temporal coherence and multi-view consistency during stylization.
  - 🧩 Category: Domain-specific Applications
  - 🏷️ Tags: style-transfer, zero-shot, temporal-consistency, content-creation

- **4DStyleGaussian: Generalizable 4D Style Transfer with Gaussian Splatting (2025)** [[paper](https://www.sciencedirect.com/science/article/pii/S0031320325010830)]
  - ⭐ Key idea: transfers style consistently across time by operating directly on dynamic Gaussian representations instead of per-frame stylization.
  - 🧩 Category: Domain-specific Applications
  - 🏷️ Tags: style transfer, temporal consistency, dynamic rendering

#### Avatar Generation

- **AvatarPointillist: AutoRegressive 4D Gaussian Avatarization (2026)** [[paper](https://arxiv.org/abs/2604.04787)]
  - ⭐ Key idea: autoregressively constructs animatable 4D Gaussian avatars so human-centric dynamic scenes can be modeled with stronger structural priors.
  - 🧩 Category: Domain-specific Applications
  - 🏷️ Tags: avatar, human modeling, autoregressive, generation

## Comparison Table

The main table below focuses on **core 4DGS methods** rather than application-specific systems. The goal is to help readers quickly identify which papers matter most for representation design, motion modeling, sparse-view robustness, and deployment.

### Core Methods

| Method | Input Setting | Core Idea | Best Read As | Typical Use Case | Code |
| --- | --- | --- | --- | --- | --- |
| 4DGS | Multi-view dynamic video | 3D Gaussians + 4D neural voxels | foundational hybrid 4DGS | general dynamic novel view synthesis | [code](https://github.com/hustvl/4DGaussians) |
| STGFS | Multi-view dynamic video | spacetime Gaussians + feature splatting | rendering-oriented 4DGS | high-quality real-time rendering | [code](https://github.com/oppo-us-research/SpacetimeGaussians) |
| 4D-RotorGS | Multi-view dynamic video | native XYZT Gaussians | native-4D representation | efficient dynamic NVS | [code](https://github.com/weify627/4D-Rotor-Gaussians) |
| ST-4DGS | Multi-view dynamic video | spatial-temporal consistency regularization | compact representation refinement | stable dynamic reconstruction | [code](https://github.com/wanglids/ST-4DGS) |
| Ex4DGS | Multi-view dynamic video | explicit timestamped Gaussian motion | explicit dynamics modeling | efficient motion interpolation | [code](https://github.com/juno181/Ex4DGS) |
| GaussianFlow | Multi-view dynamic video | Gaussian dynamics projected to motion fields | motion supervision framework | dynamic content creation / motion-aware rendering | [project](https://zerg-overmind.github.io/GaussianFlow.github.io/) |
| MotionGS | Monocular dynamic video | motion-guided deformable Gaussians | learned motion prior | monocular dynamic reconstruction | [code](https://github.com/RuijieZhu94/MotionGS) |
| DGNS | Monocular dynamic video | Gaussians + dynamic neural surface | geometry-aware monocular 4DGS | higher-quality dynamic geometry | — |
| SplineGS | Monocular dynamic video | spline-based Gaussian trajectories | compact motion parameterization | real-time monocular dynamics | — |
| MoSca | Casual / sparse-view video | 4D motion scaffolds | sparse-view stabilization | in-the-wild dynamic capture | [project](https://www.cis.upenn.edu/~leijh/projects/mosca/) |
| Efficient GS (Sparse TV Attributes) | Monocular dynamic video | sparse time-varying attributes | lightweight sparse-view 4DGS | efficient monocular reconstruction | — |
| SDD-4DGS | Few-shot dynamic video | state decomposition + denoising | few-shot robustness | limited-view dynamic scenes | — |
| Instant4D | Monocular casual video | fast optimization + pruning | practical deployment pipeline | quick 4D reconstruction from casual capture | [project](https://instant4d.github.io/) |
| QUEEN | Dynamic FVV / multi-view video | quantized dynamic Gaussian encoding | streaming / compression method | free-viewpoint video delivery | [code](https://github.com/NVlabs/queen) |
| Light4GS | Dynamic video | compact context-based coding | lightweight compression | storage-efficient 4DGS | — |

### Application-oriented Systems

| Method | Domain | Best Read As | Code |
| --- | --- | --- | --- |
| Segment Any 4D Gaussians | editing / scene understanding | promptable 4D segmentation | [code](https://github.com/jsxzs/SA4D) |
| DG-Mesh | geometry / meshing | dynamic Gaussian-to-mesh conversion | [code](https://github.com/Isabella98Liu/DG-Mesh) |
| EndoGaussian | surgical scenes | medical dynamic reconstruction | [code](https://github.com/CUHK-AIM-Group/EndoGaussian) |
| LGS | surgical scenes | lightweight medical 4DGS | [code](https://github.com/CUHK-AIM-Group/LGS) |
| GIFStream | immersive video | streamable 4D Gaussian system | [project](https://xdimlab.github.io/GIFStream/) |
| TaoAvatar | avatars / AR | real-time full-body talking avatar | [project](https://pixelai-team.github.io/TaoAvatar/) |
| DualGS | avatars / volumetric video | human performance playback system | [project](https://nowheretrix.github.io/DualGS/) |
| HRAvatar | head avatars | relightable Gaussian avatar | [code](https://github.com/Pixel-Talk/HRAvatar) |


## Tools / Implementations

### Core repositories

- **4DGaussians**: official implementation of 4DGS  
  [https://github.com/hustvl/4DGaussians](https://github.com/hustvl/4DGaussians)

- **SpacetimeGaussians**: official implementation of STGFS  
  [https://github.com/oppo-us-research/SpacetimeGaussians](https://github.com/oppo-us-research/SpacetimeGaussians)

- **4D-Rotor-Gaussians**: official implementation of 4D-RotorGS  
  [https://github.com/weify627/4D-Rotor-Gaussians](https://github.com/weify627/4D-Rotor-Gaussians)

- **ST-4DGS**: official implementation of ST-4DGS  
  [https://github.com/wanglids/ST-4DGS](https://github.com/wanglids/ST-4DGS)

- **Ex4DGS**: official implementation of Fully Explicit Dynamic Gaussian Splatting  
  [https://github.com/juno181/Ex4DGS](https://github.com/juno181/Ex4DGS)

- **QUEEN**: official implementation of dynamic Gaussian streaming and compression  
  [https://github.com/NVlabs/queen](https://github.com/NVlabs/queen)

- **LGS**: lightweight surgical 4DGS  
  [https://github.com/CUHK-AIM-Group/LGS](https://github.com/CUHK-AIM-Group/LGS)

- **EndoGaussian**: dynamic Gaussian splatting for endoscopic scenes  
  [https://github.com/CUHK-AIM-Group/EndoGaussian](https://github.com/CUHK-AIM-Group/EndoGaussian)

- **MotionGS**: explicit motion-guided deformable Gaussian splatting  
  [https://github.com/RuijieZhu94/MotionGS](https://github.com/RuijieZhu94/MotionGS)

- **SA4D**: Segment Any 4D Gaussians  
  [https://github.com/jsxzs/SA4D](https://github.com/jsxzs/SA4D)

- **DG-Mesh**: dynamic Gaussian to mesh reconstruction  
  [https://github.com/Isabella98Liu/DG-Mesh](https://github.com/Isabella98Liu/DG-Mesh)

- **MoSca**: dynamic Gaussian fusion from casual videos  
  [https://github.com/JiahuiLei/MoSca](https://github.com/JiahuiLei/MoSca)

- **Instant4D**: fast monocular 4DGS pipeline  
  [https://github.com/Zhanpeng1202/Instant4D](https://github.com/Zhanpeng1202/Instant4D)

### Practical stack around 4DGS

- **3DGS base renderer**
  - Most 4DGS systems still inherit kernels, rasterization logic, and optimization tricks from the original 3D Gaussian Splatting code ecosystem.

- **Camera / geometry initialization**
  - COLMAP, depth priors, video depth estimators, optical flow, and tracking modules remain critical for monocular or sparse-view setups.

- **Compression / deployment layer**
  - For real systems, dynamic Gaussian models increasingly need quantization, pruning, caching, and streamable residual updates.

## Research Trends

### 1. From deformation fields to native 4D representations
The field started by deforming canonical 3D Gaussians over time, but recent work increasingly asks whether motion should be encoded directly in the primitive itself. Native 4D and even 7D parameterizations are emerging because they promise cleaner interpolation and less bookkeeping.

### 2. From lab-captured multi-view video to casual monocular capture
Early methods were strongest on controlled benchmarks with accurate cameras. Newer work is moving toward monocular, sparse-view, and in-the-wild video, which is much more relevant for real capture but also far more ill-posed.

### 3. From reconstruction to editable dynamic representations
4DGS is no longer only about novel view synthesis. Segmentation, mesh extraction, motion transfer, stylization, and semantic editing are turning 4D Gaussian fields into manipulable scene representations.

### 4. Compression is becoming a first-class research problem
Dynamic Gaussian scenes can be large, and naive framewise updates are expensive. Work on quantization, sparse residuals, context coding, and streaming suggests the field is maturing toward deployable free-viewpoint video systems.

### 5. Learning priors are becoming unavoidable
Scene-specific optimization alone struggles in sparse-view, monocular, or noisy capture settings. The trend is clear: stronger learned priors will be needed for robust geometry, plausible motion, and faster convergence.

## Research Insight

### What are the main challenges in 4DGS?

- **Space-time ambiguity**: many different motions can explain the same few images, especially under monocular capture.
- **Occlusion and disocclusion**: newly revealed regions break simple temporal correspondence assumptions.
- **Topology change**: cloth, hair, fluids, and articulated humans often violate smooth deformation models.
- **Model bloat**: dynamic Gaussians can grow rapidly in count and per-frame attributes, making memory and training unstable.
- **Appearance-motion entanglement**: specularity, exposure change, and motion blur can be confused with geometry or dynamics.

### Why is sparse-view hard?

Sparse-view 4D reconstruction is hard because the problem is underconstrained in both **space** and **time**. A static 3DGS model already needs enough views to localize geometry; 4DGS additionally has to infer how that geometry moves, often without reliable tracks, depth, or correspondences.

### What are current bottlenecks?

- robust camera and geometry initialization for monocular videos
- temporally stable motion under large non-rigid deformation
- memory-efficient dynamic parameterization
- standardized evaluation of latency, model size, and temporal coherence
- handling real-world nuisances such as HDR, rolling shutter, blur, and exposure drift

## Open Problems

- **Sparse-view 4DGS with strong guarantees**  
  Can we reconstruct plausible dynamic scenes from very few views without over-smoothing motion or hallucinating geometry?

- **Long-horizon temporal consistency**  
  Current methods often look good on short clips but drift over longer sequences or repeated cycles.

- **Topology-aware dynamic Gaussians**  
  How should 4DGS represent events like tearing, splashing, contact, hair motion, and fine articulated interactions?

- **Joint pose-motion-geometry estimation**  
  Monocular pipelines still struggle when camera calibration, depth, and motion must all be inferred together.

- **Compact but editable representations**  
  Compression methods reduce size, but often at the cost of manipulation, relighting, or semantic editability.

- **Generalizable 4DGS priors**  
  Can we build feed-forward or reusable models that initialize or predict dynamic Gaussians across scenes, rather than optimizing everything from scratch?

- **Physics-aware 4D Gaussian dynamics**  
  Most methods model motion photometrically, not physically. There is substantial room for combining Gaussian rendering with mechanics and interaction priors.

- **Better benchmarks for deployment**  
  The community still lacks a standard benchmark that jointly measures fidelity, temporal stability, FPS, latency, bitrate, and model size under realistic capture settings.

## Contributing

Contributions are welcome. If you want to add a paper, project, or benchmark, please open an issue or pull request with:

- paper link
- project page and/or code link if available
- 1-sentence technical summary
- suggested category
- tags such as `sparse-view`, `real-time`, `monocular`, `compression`, `editing`, `avatar`

For newly released papers, the goal of this repository is to **review and update entries within one week whenever possible**. If I miss an important work, feel free to open an issue and I will prioritize it.

When adding papers, please follow the existing style:

- `Paper Title (Year) [paper] [project/code]`
- `⭐ Key idea`
- `🧩 Category`
- `🏷️ Tags`

## License

This repository is released under the **MIT License** for the curation text and repository structure.

Please note:

- linked papers, project pages, images, and code remain under their respective original licenses
- paper abstracts and project materials should be cited from the original sources

## Citation

If you find this repository useful in your own project, survey, or reading group, you can cite it as:

```bibtex
@misc{awesome4dgs,
  title        = {Awesome 4D Gaussian Splatting},
  author       = {Yanxi Du},
  year         = {2026},
  howpublished = {\url{https://github.com/duyanxi/awesome-4DGS}},
  note         = {Curated repository of papers, code, and research notes for 4D Gaussian Splatting}
}
```

---

If you find this repository useful, consider starring it and sharing missing papers via issues or pull requests.
