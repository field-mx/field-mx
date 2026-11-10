# Welcome to my Profile !

**AI for Sensing Systems · Digital Twins · World Models · Biomedical Signal Intelligence**

I am a graduate student at **Tsinghua University**, working at the intersection of **instrument science, artificial intelligence, signal processing, and intelligent sensing systems**.

My interests lie in developing AI models that can understand, reconstruct, and predict complex physical and biological signals, with applications in industrial digital twins, world models, EEG/BCI systems, wearable sensing, and scientific instrumentation.

---

## Research Interests

* **Physical AI & IWorld Models**

  Committed to integrating the real physical world into AI, promoting the creation of a learnable, reusable, and evolvable digital world, and helping AGI arrive sooner!

* **Digital Twins & Multi-sensor Modeling**

  Sparse sensing, spatiotemporal reconstruction, anomaly detection, health-state estimation, and industrial system modeling.

* **EEG / BCI & Human-state Decoding**

  Motor imagery classification, real-time EEG processing, cognitive-state modeling, and neural feedback systems.


* **Biomedical & Wearable Sensing**

  Optical blood-flow monitoring, pulse-wave extraction, physiological signal processing, and portable sensing instruments.



* **Computer Vision for Measurement Systems**

  Image stitching, visual inspection, remote-sensing image classification, and vision-based sensing platforms.


---

## Selected Projects


### 🦾 [LeWorldModel — Long-Horizon Robotic Manipulation](https://github.com/field-mx/LeWm_Saimo)

Extended a short-horizon **Joint-Embedding Predictive World Model (LeWM)** to long-horizon robotic cube grasping and transfer—without retraining the world model.

- Identified that final-goal latent distance is non-monotonic during long-horizon manipulation, causing the original CEM planner to become trapped in local optima.
<p align="center">
  <img src="./assets/actor分析.gif" alt="latent驱动信号逐帧分析">
</p>

- Developed **Proprio V2**, combining a frozen LeWM with 6D robot proprioception, an `ALIGN → GRASP → TRANSFER` state machine, actor-guided MPC, value estimation, and uncertainty-aware candidate scoring.
- Built a closed-loop planner that evaluates 96 candidate action sequences and replans after every real action using only RGB observations and robot proprioception.
- Trained on 64 successful teacher trajectories (3,007 frames) and achieved **7/10 grasp-to-transfer confirmations** and **4/10 end-to-end task successes**, with **31.7 ms average LeWM inference time**.

<h2 align="center">Before</h2>
<p align="center">
  <img src="./assets/改造前.gif" alt="latent差驱动cem规划">
</p>

<h2 align="center">After</h2>

<table>
  <tr>
    <td align="center">
      <img src="./assets/0.gif" width="150" alt="Experiment 1">
      <br>
      <strong>Experiment 1</strong>
    </td>
    <td align="center">
      <img src="./assets/1.gif" width="150" alt="Experiment 2">
      <br>
      <strong>Experiment 2</strong>
    </td>
    <td align="center">
      <img src="./assets/2.gif" width="150" alt="Experiment 3">
      <br>
      <strong>Experiment 3</strong>
    </td>
    <td align="center">
      <img src="./assets/3.gif" width="150" alt="Experiment 4">
      <br>
      <strong>Experiment 4</strong>
    </td>
    <td align="center">
      <img src="./assets/4.gif" width="150" alt="Experiment 5">
      <br>
      <strong>Experiment 5</strong>
    </td>
  </tr>

  <tr>
    <td align="center">
      <img src="./assets/5.gif" width="150" alt="Experiment 6">
      <br>
      <strong>Experiment 6</strong>
    </td>
    <td align="center">
      <img src="./assets/6.gif" width="150" alt="Experiment 7">
      <br>
      <strong>Experiment 7</strong>
    </td>
    <td align="center">
      <img src="./assets/7.gif" width="150" alt="Experiment 8">
      <br>
      <strong>Experiment 8</strong>
    </td>
    <td align="center">
      <img src="./assets/8.gif" width="150" alt="Experiment 9">
      <br>
      <strong>Experiment 9</strong>
    </td>
    <td align="center">
      <img src="./assets/9.gif" width="150" alt="Experiment 10">
      <br>
      <strong>Experiment 10</strong>
    </td>
  </tr>
</table>


`World Models` · `Model Predictive Control` · `Robot Manipulation` · `Joint-Embedding Prediction` · `MuJoCo` · `Python`

---

### 🎬 [Masked Visual Actions — Robot Video Generation](https://github.com/field-mx/masked-visual-actions)

Reproduced the **Masked Visual Actions** robot video generation pipeline using **Wan2.2-Fun-A14B-Control**, dual LoRA adapters, and robot trajectories generated from LeWM/OGBench.
<h2 align="center">Input image and masked video</h2>
<table>
  <tr>
    <td align="center">
      <img src="./assets/action.gif" width="400">
    </td>
    <td align="center">
      <img src="./assets/initial_actor_first_frame.png" width="400">
    </td>
  </tr>
</table>

<h2 align="center">Output video</h2>
<table>
  <tr>
    <td align="center">
      <img src="./assets/2round_denoisy.gif" width="500">
    </td>
    <td align="center">
      <img src="./assets/5rounds_denoisy.gif" width="400">
    </td>
  </tr>
</table>

- Built an inference pipeline conditioned on a **dynamic robot mask**, a first-frame reference image, and a text instruction.
- Converted UR5e manipulation trajectories into visual action controls for generating temporally consistent robot videos.
- Reproduced **480 × 480, 81-frame** video generation and evaluated fast-preview and standard 50-step denoising configurations.
- Stress-tested the model on complex and high-speed dexterous manipulation, revealing limitations in physical consistency, motion reasoning, and hallucination control.

`Video World Models` · `Diffusion Models` · `Masked Visual Actions` · `LoRA` · `Robot Manipulation` · `Wan2.2`

---

### [PhysicsRelationCTF — Physics-Guided Forecasting for Electrolyzer Monitoring](https://github.com/field-mx/PhysicsRelationCTF)

**From sensor measurements to future operating trends: forecasting support for fault early warning.**

Industrial electrolyzers generate coupled electrical, thermal, pressure, flow, and gas-composition signals. Forecasting these signals can provide advance information for anomaly assessment and fault early warning, but complete equipment parameters and dynamic equations are often unavailable. This project asks how the physical knowledge that is available can still improve prediction.

Developed **PhysicsRelationCTF (PRCTF)**, which enhances **ChannelTokenFormer (CTF)** through two complementary interfaces while retaining its masked attention and channel-token decoder:

- **Structural guidance:** map sparse, directed physical relationships to channel-attention biases, guiding information exchange while preserving data-driven learning of unknown dependencies.
- **Equation-informed content:** compute reference features from historical measurements, such as electrical power and Faradaic gas-generation references, and inject their encoded messages into attention aggregation. Data-driven attention and a lightweight residual branch learn unmodeled dynamics.

<p align="center">
  <a href="https://github.com/field-mx/PhysicsRelationCTF">
    <img src="https://raw.githubusercontent.com/field-mx/PhysicsRelationCTF/main/figures/architecture/model_architecture.png" width="100%" alt="PRCTF model overview: physical topology guides channel attention, equation-derived messages enrich predictive representations, and channel tokens decode future sensor trajectories">
  </a>
</p>

**Industrial task:** use **96 seconds of history to forecast the next 96 seconds across 56 monitoring channels**. Three fixed-seed comparisons against Original CTF show:

| Evaluation setting | Role | Mean normalized MSE reduction | Best paired-seed reduction |
|---|---|---:|---:|
| Real industrial alkaline electrolyzer | Application evaluation | **0.393%** | **1.275%** |
| LBNL simulated chiller plant | Physical-module numerical validation | **0.778%** | **2.588%** |
| Tennessee Eastman Process | Physical-module numerical validation | **0.712%** | **0.760%** |

Mean reductions use seeds 42, 43, and 44; the best paired-seed result is reported separately. Each system uses its own physical relationships and is trained independently. The experiments evaluate forecasting accuracy; predictions can serve as inputs to downstream warning logic.

**Deployment:** released trained reference weights, fitted normalization/calibration, and CPU/CUDA inference tools for all three systems. The implementation returns forecasts in physical measurement units without requiring retraining.

**Prediction examples — hydrogen outlet flow and instrument-air pressure**

<p align="center">
  <a href="https://github.com/field-mx/PhysicsRelationCTF/blob/main/figures/industrial/lowpass_test_predictions.pdf">
    <img src="https://raw.githubusercontent.com/field-mx/PhysicsRelationCTF/main/figures/industrial/lowpass_test_predictions.png?v=flow96-pressure-weighted24-20261110" width="100%" alt="PRCTF versus CTF: hydrogen outlet flow using direct 96-second forecast blocks, and instrument-air pressure using validation-weighted overlapping forecasts with a minimum 24-second lead">
  </a>
</p>

**PRCTF has lower full-test MSE in both channel/policy examples:** **23.78%** lower for hydrogen outlet flow and **0.62%** lower for instrument-air pressure. In the flow transition, PRCTF reduces CTF's sustained overprediction.

- **Top — hydrogen outlet flow (FT010304):** directly concatenate complete 96 s forecasts, updated every 96 s. The image shows the selected first 960 s; [the full-test flow plot is also available](https://github.com/field-mx/PhysicsRelationCTF/blob/main/figures/industrial/flow_block96_detail_and_full.pdf).
- **Bottom — instrument-air header pressure (PT010003):** selected panel C of the matched-minimum-lead comparison. Update every 12 s and combine lead-24–96 s forecasts using each model's inverse validation-MSE weights, rather than equal weights. All 4847 test observations are shown.

*These are separate seed-42 causal-low-pass illustrations, not the original-data three-seed benchmark above. Both full-region scores use the same 4751 targets after the first 96 s; the flow score is not limited to the displayed 960 s. CTF and PRCTF use the same policy within each panel. The two policies have different lead times, no time shifts or extra smoothing are applied, and the gains do not imply improvement on every channel.*


[Code & Results](https://github.com/field-mx/PhysicsRelationCTF) · [Pretrained Weights](https://github.com/field-mx/PhysicsRelationCTF/tree/main/weights) · [Deployment Guide](https://github.com/field-mx/PhysicsRelationCTF/blob/main/weights/README.md)

**Paper / Preprint:** Public link to be added.
<!-- PRCTF_PAPER_LINK: Replace the placeholder above with [Paper](PUBLIC_PAPER_URL) when the manuscript is publicly available. -->

`Physics-Guided AI` · `Multivariate Forecasting` · `Channel Attention` · `Industrial Sensors` · `PyTorch`

---

### [Electrolyzer AI Monitoring — Desktop UI & On-device Model Orchestration](https://github.com/field-mx/Sensor_Dashboard)

**Designing the monitoring front end and the local model workflow, from measurements to forecasts and model updates.**

Built a **PyQt6 desktop application** that connects multi-sensor data, an interactive 3D equipment view, rolling forecasts, and residual alerts. A **FastAPI + PyTorch** backend runs inference and fine-tuning on the user's Windows PC using CPU.

- **Monitoring interface design:** coordinated process overview, trend/forecast plots, 3D structure, and model-update views; measurement selection links the table to its curve, with external plot legends and visible service, version, and task states. The current 3D scene is schematic; sensor coordinates remain uncalibrated.
- **Asynchronous model integration:** call the local model service without blocking the UI; align 96-second histories with the next 96 forecast points across 56 channels, handle timeouts and reconnection, and discard stale responses after a reset or version change.
- **On-device resource scheduling:** serialize model access, run fine-tuning in a separate worker process, and share a lock between manual and daily jobs. Inference pauses during training while the interface remains responsive.
- **Model lifecycle:** validate imported normal Excel, partition windows chronologically, show real training progress/loss, evaluate candidates, then activate or roll back. Daily training is optional, persistent, and deduplicates previously processed data; it does not automatically activate candidates.
- **Deployment and interaction:** provide `Setup.cmd` and `StartDemo.cmd` for the complete offline delivery, plus play/pause/reset/speed controls, residual-based upward/downward fault demonstrations, and event-history export.

<p align="center">
  <img src="https://raw.githubusercontent.com/field-mx/Sensor_Dashboard/main/docs/images/modelshowing.gif" width="800" alt="Electrolyzer 3D structure and synchronized measurement data">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/field-mx/Sensor_Dashboard/main/docs/images/forecast.gif" width="800" alt="Rolling on-device AI forecasts and residual alerts">
</p>

*The presentation replays Excel history to simulate live acquisition; inference and residual alerts execute locally. The forecasting algorithm and released weights are maintained separately in [PhysicsRelationCTF](https://github.com/field-mx/PhysicsRelationCTF).*

[Project & setup](https://github.com/field-mx/Sensor_Dashboard) · [English README](https://github.com/field-mx/Sensor_Dashboard/blob/main/README.en.md) · [Operation guide](https://github.com/field-mx/Sensor_Dashboard/blob/main/docs/操作指南.md)

`Desktop UI Design` · `PyQt6` · `pyqtgraph/OpenGL` · `FastAPI` · `PyTorch` · `On-device AI` · `Model Orchestration` · `Time-series Forecasting`

---

### [Real-time EEG Three-class BCI System](https://github.com/field-mx/SE-EEGNet-Real-time-EEG-Three-Class-Classification-Model)

**Real-time EEG decoding and online control**
<p align="center">
  <img src="pictures/系统流程图.jpg" width="70%">
</p>


* Implemented a real-time EEG classification system based on SE-EEGNet.
* Focused on online preprocessing, motor imagery classification, and real-time inference.
* Integrated EEG decoding with device-side communication and control.

---

### [EEG Training System with Visual Feedback](https://github.com/field-mx/EEG_TrainingSystemwithVisualFeedback)

**Visual-feedback EEG training for motor imagery**
<p align="center">
  <img src="pictures/镜像神经元原理.png" width="70%">
  <img src="pictures/训练流程图.png" width="70%">
</p>

* Designed an EEG training platform with real-time visual feedback.
* Explored mirror-neuron-inspired interaction for motor imagery training.
* Implemented signal acquisition, feedback visualization, and user interaction modules.

---

### [Wearable Blood-flow Monitoring System](https://github.com/field-mx/Blood_flow_testing_instruments)

**Portable diffuse-speckle-based physiological sensing**
<p align="center">
  <img src="pictures/深度模拟.png" width="70%">
  <img src="pictures/滤波.png" width="70%">
  <img src="pictures/硬件2.png" width="70%">
</p>

* Developed a wearable optical sensing system for blood-flow and pulse-wave monitoring.
* Implemented single-exposure pulse-wave extraction and multi-exposure flow-index estimation.
* Combined hardware design, signal processing, and simulation analysis for biomedical instrumentation.

---

### Visual-Tactile 3D Reconstruction

**Vision-based tactile sensing and deformation-field reconstruction**

* Developed a visual-tactile sensing system for reconstructing three-dimensional deformation fields.
* Built a measurement pipeline involving optical imaging, calibration, and deformation estimation.
* Focused on accurate tactile perception for intelligent sensing and robotic interaction.

---

### [Image Stitching System](https://github.com/field-mx/image_stitching)

**Panoramic sensing and image-processing pipeline**

* Implemented image segmentation, feature extraction, registration, and stitching.
* Applied the system to panoramic detection and inspection scenarios.

---

### [Remote Sensing CNN Classification](https://github.com/field-mx/CNN_image_classifications)

**CNN-based remote-sensing image classification**

* Built a CNN-based classification pipeline for remote-sensing image data.
* Implemented dataset preprocessing, model training, evaluation, and visualization.

---

## Technical Skills

**Programming:** Python, C/C++, MATLAB, Shell
**Machine Learning:** PyTorch, TensorFlow/Keras, scikit-learn
**Signal Processing:** time-series analysis, EEG processing, physiological signal processing, anomaly detection
**Computer Vision:** OpenCV, image stitching, CNN-based classification, visual measurement
**Systems & Tools:** Git, Linux, Conda, Raspberry Pi, socket communication, data acquisition systems
**Research Topics:** self-supervised learning, multimodal learning, digital twins, world models, physics-aware AI

---

## Current Focus

I am currently working on:

* lightweight world models for action-conditioned prediction
* physics-aware representation learning for sensing systems
* multi-sensor digital twins for industrial state estimation
* EEG/BCI systems for human intention and cognitive-state decoding
* wearable physiological sensing and biomedical instrumentation

---

## Long-term Direction

My long-term goal is to build **AI systems that connect physical measurement, scientific instrumentation, and intelligent decision-making**.

I am particularly interested in research problems where models are not only accurate, but also **physically grounded, interpretable, robust, and deployable in real-world sensing environments**.

---

## Contact

* GitHub: [@field-mx](https://github.com/field-mx)
* Institution: Tsinghua University
* Research interests: AI for sensors, digital twins, world models, EEG/BCI, biomedical sensing
