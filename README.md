# 🚀 Supervisely ML Training Studio for Google Colab

<p align="center">
  <a href="https://colab.research.google.com/github/LorenzFon/supervisely-colab-trainer/blob/main/supervisely_training.ipynb">
    <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab" height="32">
  </a>
  <img src="https://img.shields.io/badge/Python-3.10%2B-blue.svg" alt="Python 3.10+">
  <img src="https://img.shields.io/badge/PyTorch-2.0%2B-orange.svg" alt="PyTorch">
  <img src="https://img.shields.io/badge/Apple_CoreML-Enabled-black.svg" alt="CoreML">
  <img src="https://img.shields.io/badge/Google_LiteRT-Enabled-yellow.svg" alt="Google LiteRT">
  <img src="https://img.shields.io/badge/ONNX-Supported-blue.svg" alt="ONNX">
  <img src="https://img.shields.io/badge/License-MIT-green.svg" alt="License: MIT">
</p>

An end-to-end, zero-restart interactive GUI studio for Google Colab that connects directly to your [Supervisely](https://supervisely.com) workspace. Select projects from an interactive dropdown, automatically convert annotations, and train state-of-the-art vision models (**RT-DETRv2**, **DEIMv2**, **MMDetection**, **YOLOX**, **YOLO11**, **YOLOv10**, **YOLOv9**, **YOLOv8**, **YOLOv5u**, and **YOLO-World v2**). 

Includes **automated multi-format on-device model export** for **Apple CoreML** (`.mlpackage`), **Google LiteRT / TFLite** (`.tflite`), and **ONNX** (`.onnx`) bundled directly into your download!

---

## 🌟 Highlights

- **⚡ Zero-Restart Setup (~60s):** Custom dependency resolution with memory-mapped Pillow freezing prevents breaking Google Colab's native binary drivers. No manual runtime restarts required!
- **📊 Live Visual Dashboard & Accurate ETA:** Monitor training in real-time with live KPI cards (Current Epoch, Train Loss, Val Loss) and dynamic **Time Remaining (ETA)** calculation with iterations-per-second pace. Switch instantaneously between the visual dashboard and raw console logs at any point during active training via asynchronous threading.
- **📈 Collapsible Loss Convergence Drill:** Compact, vector-rendered convergence graph plotting Training & Validation Loss curves live as epochs complete. Built as a sleek collapsible drill-down drawer that folds in and out with one click to maximize vertical screen space.
- **⚡ Smart Auto-Batch Mode:** Automatically calculates and profiles the optimal batch size based on your active GPU VRAM (T4 / L4 / A100), model architecture scale, image resolution, and dataset size.
- **🎯 Smart Validation Dataset Detection:** Automatically detects if your Supervisely project contains a dedicated dataset named `"validation"` (or `"val"`). When detected, it locks the manual split slider, displays an informational badge, and routes the dedicated dataset directly to validation while using remaining datasets for training.
- **⏹️ Graceful Stop / Cancel Button:** Safely stop training at any point with one click. The studio automatically finalizes the current step, preserves checkpoints, and lets you export the best model weights.
- **📱 Automated Edge & On-Device Exports:**
  - **Apple CoreML (`.mlpackage`):** Seamless deployment on iOS 16+, iPadOS, and macOS utilizing the Apple Neural Engine.
  - **Google LiteRT / TFLite (`.tflite`):** Google's on-device AI runtime for Android, Raspberry Pi, Coral Edge TPU, and microcontrollers.
  - **ONNX (`.onnx`):** Universal cross-platform runtime for Windows, Linux, TensorRT, OpenVINO, and Web.
- **📦 On-Demand Package Installation:** Only installs packages required for your selected model family and export targets, keeping your environment clean and fast.
- **⚡ Instant Background Prefetch & Persistent Image Cache:** Selecting a project automatically prefetches all images and annotations in a background daemon thread into `/content/sly_projects/project_<id>`. Before every training run, the studio verifies if the images are already cached on disk and reuses them immediately without re-downloading.
- **🧠 Multi-Model Support (10 Families, 54 Checkpoints):**
  - **RT-DETRv2** (Hugging Face Transformers: ResNet-18, 34, 50, 101 | Apache 2.0)
  - **DEIMv2** (DINOv3 / Real-Time DETR: Atto, Femto, Pico, Nano, Small, Medium, Large, Extra-Large | Apache 2.0)
  - **MMDetection** (OpenMMLab: RTMDet-Tiny/S/M/L/X, Faster R-CNN | Apache 2.0)
  - **YOLOX** (Megvii: Nano, Tiny, Small, Medium, Large, Extra-Large | Apache 2.0)
  - **YOLO11** (Ultralytics: Nano, Small, Medium, Large, Extra-Large)
  - **YOLOv10** (NMS-Free: Nano, Small, Medium, Balanced, Large, Extra-Large)
  - **YOLOv9** (PGI & GELAN: Tiny, Small, Medium, Compact, Extended)
  - **YOLOv8** (Production Standard: Nano, Small, Medium, Large, Extra-Large)
  - **YOLOv5u** (Industrial Workhorse: Nano, Small, Medium, Large, Extra-Large)
  - **YOLO-World v2** (Vision-Language Open-Vocabulary: Small, Medium, Large, Extra-Large)
- **💾 One-Click Bundle Export:** Download all trained weights and converted edge formats packed into a single `.zip` file.

---

## 🚀 Quick Start Guide

### 1. Launch in Google Colab
Click the badge above or open the notebook directly in Colab:
> **Note:** Once you fork or push this repository to your GitHub account, update `YOUR_USERNAME` in the badge link with your actual GitHub username.

### 2. Enable GPU Acceleration
1. In Colab's top menu, navigate to **Runtime** ➔ **Change runtime type**.
2. Select **T4 GPU** (or any higher GPU tier) under *Hardware accelerator*.
3. Click **Save**.

### 3. Run the Studio
Click the **Play button (▶️)** on the form cell. Supervisely installs in the background in approximately ~60 seconds.

### 4. Connect to Supervisely
- **API Token:** Enter your Supervisely API Token in the text box.
  > 💡 **Pro-Tip (Colab Secrets):** Save your token in Google Colab's **Secrets** (the key icon 🔑 in the left sidebar) with the name `SUPERVISELY_TOKEN`. The notebook will automatically read and populate it every time you open the notebook!
- Click **🔄 Fetch My Projects** to load your projects into the dropdown.

### 5. Configure & Train
- Select your target project and choose your desired model architecture.
- Select your desired **Export Formats** (Apple CoreML, Google LiteRT, ONNX, PyTorch).
- Adjust hyperparameters (Epochs, Batch Size, Image Size, Learning Rate, Validation Split).
- Click **🚀 Start Training**.
- Once training and exports complete, click **💾 Download Model Bundle (.zip)** to save your complete multi-platform model package!

---

## 📱 Export Formats & Deployment Targets

| Format | File Type | Target Platforms | Key Advantages |
| :--- | :--- | :--- | :--- |
| **PyTorch** | `.pt` / `.safetensors` | Python, PyTorch Servers | Full training state, checkpointing, and research reproduction. |
| **Apple CoreML** | `.mlpackage` | iOS, iPadOS, macOS, visionOS | Hardware-accelerated inference via Apple Neural Engine (ANE); built-in NMS. |
| **Google LiteRT** | `.tflite` | Android, Raspberry Pi, Coral TPU, Edge | Ultra-low latency and memory footprint; Google's official on-device runtime. |
| **ONNX Runtime** | `.onnx` | Cross-Platform, Web, TensorRT, OpenVINO | High-performance production serving across NVIDIA, Intel, and AMD hardware. |

---

## 📊 Supported Model Families & Open-Source Licenses

| Architecture | Framework | License | Variants / Checkpoints | Strengths & Best Targets |
| :--- | :--- | :--- | :--- | :--- |
| **RT-DETRv2** | Hugging Face Transformers | `Apache 2.0` *(Commercial Friendly)* | `rtdetr_v2_r18vd`<br>`rtdetr_v2_r34vd`<br>`rtdetr_v2_r50vd`<br>`rtdetr_v2_r101vd` | Real-time transformer; no NMS post-processing needed. Ideal for **PyTorch**, **ONNX**, and **CoreML**. |
| **DEIMv2** | Intellindust AI Lab | `Apache 2.0` *(Commercial Friendly)* | `deimv2_atto`, `deimv2_femto`, `deimv2_pico`, `deimv2_n`<br>`deimv2_s`, `deimv2_m`, `deimv2_l`, `deimv2_x` | Real-Time DETR meets DINOv3. Combines DINOv3 foundation features with Dense O2O matching and HGNetv2 edge backbones. Native **ONNX**. |
| **MMDetection** | OpenMMLab | `Apache 2.0` *(Commercial Friendly)* | `rtmdet_tiny`, `rtmdet_s`, `rtmdet_m`<br>`rtmdet_l`, `rtmdet_x`, `faster-rcnn_r50` | OpenMMLab's high-speed real-time detector (RTMDet) and two-stage classic (Faster R-CNN). **ONNX** for RTMDet (raw head outputs, decoding & NMS not included); Faster R-CNN requires [MMDeploy](https://github.com/open-mmlab/mmdeploy). |
| **YOLOX** | Megvii | `Apache 2.0` *(Commercial Friendly)* | `yolox_nano.pth`, `yolox_tiny.pth`, `yolox_s.pth`<br>`yolox_m.pth`, `yolox_l.pth`, `yolox_x.pth` | High-performance anchor-free detector with decoupled head and SimOTA assignment. 100% permissive commercial license; native **ONNX**, **CoreML**, and **LiteRT**. |
| **YOLO11** | Ultralytics | `AGPL-3.0` *(Commercial via Ultralytics)* | `yolo11n.pt`, `yolo11s.pt`, `yolo11m.pt`<br>`yolo11l.pt`, `yolo11x.pt` | Latest YOLO generation; ultra-fast inference and 100% native support for **Google LiteRT (.tflite)** & **CoreML**. |
| **YOLOv10** | Ultralytics / Tsinghua | `AGPL-3.0` *(Ultralytics / Commercial)* | `yolov10n.pt`, `yolov10s.pt`, `yolov10m.pt`<br>`yolov10b.pt`, `yolov10l.pt`, `yolov10x.pt` | End-to-end NMS-free training. Dual label assignments eliminate post-processing overhead for lower edge latency. |
| **YOLOv9** | Ultralytics / PGI | `AGPL-3.0 / GPL-3.0` | `yolov9t.pt`, `yolov9s.pt`, `yolov9m.pt`<br>`yolov9c.pt`, `yolov9e.pt` | Programmable Gradient Information (PGI) & GELAN architecture; preserves rich gradient flow for complex datasets. |
| **YOLOv8** | Ultralytics | `AGPL-3.0` *(Commercial via Ultralytics)* | `yolov8n.pt`, `yolov8s.pt`, `yolov8m.pt`<br>`yolov8l.pt`, `yolov8x.pt` | Industry-standard anchor-free detector with broad production tooling (TensorRT, OpenVINO, CoreML, LiteRT). |
| **YOLOv5u** | Ultralytics | `AGPL-3.0` *(Commercial via Ultralytics)* | `yolov5nu.pt`, `yolov5su.pt`, `yolov5mu.pt`<br>`yolov5lu.pt`, `yolov5xu.pt` | Modernized anchor-free split-head YOLOv5; unrivaled compatibility with industrial cameras and legacy hardware. |
| **YOLO-World v2** | Ultralytics | `GPL-3.0 / AGPL-3.0` | `yolov8s-worldv2.pt`, `yolov8m-worldv2.pt`<br>`yolov8l-worldv2.pt`, `yolov8x-worldv2.pt` | Real-time Vision-Language open-vocabulary detector; excellent transfer learning on custom Supervisely classes. |

### 📜 Licensing Summary
- **Apache 2.0 (RT-DETRv2, DEIMv2, MMDetection, YOLOX):** Permissive open-source licenses. You can freely use, modify, and distribute models in proprietary commercial applications without disclosing your source code or paying licensing royalties.
- **AGPL-3.0 / GPL-3.0 (YOLO11, YOLOv10, YOLOv9, YOLOv8, YOLOv5u, YOLO-World):** GNU Affero General Public License. Free for open-source and research projects. Closed-source enterprise commercial distribution requires a commercial license directly from [Ultralytics](https://ultralytics.com/license).

---

## 🛠️ How It Works Under The Hood

```
   ┌──────────────────────────────────────────────────────────────┐
   │                Supervisely Server (Cloud/Self-Hosted)        │
   └──────────────────────────────┬───────────────────────────────┘
                                  │ sly.Project.download (50-batch)
                                  ▼
   ┌──────────────────────────────────────────────────────────────┐
   │                  Raw Supervisely Dataset                     │
   │           (/content/sly_project: images + annotations)       │
   └──────────────────────────────┬───────────────────────────────┘
                                  │
         ┌────────────────────────┼────────────────────────┐
         │ (Automatic Conversion & Train/Val Split)        │
         ▼                        ▼                        ▼
┌──────────────────┐    ┌──────────────────┐    ┌──────────────────┐
│RT-DETRv2 Pipeline│    │DEIMv2 / MMDetection   │Ultralytics Branch│
│• SLYDataset      │    │  & YOLOX Pipelines    │• YOLO .txt labels│
│• ImageProcessor  │    │• COCO JSON format│    │• dataset.yaml    │
│• HuggingFace Tr. │    │• PyTorch / MMEngine   │• model.train()   │
└────────┬─────────┘    └────────┬─────────┘    └────────┬─────────┘
         │                       │                       │
         └───────────────────────┼───────────────────────┘
                                 ▼
        ┌──────────────────────────────────────────────────┐
        │          Automated Multi-Format Exporter         │
        │  • Apple CoreML (.mlpackage)                     │
        │  • Google LiteRT / TFLite (.tflite)              │
        │  • ONNX Runtime (.onnx)                          │
        │  • Native PyTorch (.pt / .pth / .safetensors)    │
        └────────────────────────┬─────────────────────────┘
                                 ▼
                 ┌─────────────────────────────────┐
                 │   Complete Multi-Platform Bundle│
                 │   One-Click .zip Download to PC │
                 └─────────────────────────────────┘
```

---

## 📤 Uploading to Your GitHub

Follow these steps to upload this project to your GitHub account:

### Step 1: Create a New GitHub Repository
1. Go to [github.com/new](https://github.com/new).
2. Set the repository name (e.g. `supervisely-colab-trainer`).
3. Set the repository to **Public** (required for Google Colab badge to open directly without login issues).
4. Do not initialize with README, .gitignore, or license (we already have them here).

### Step 2: Push from Local Terminal
Open PowerShell or your terminal in this project folder:

```bash
# 1. Navigate to the project folder
cd C:\Users\Lars\.gemini\antigravity\scratch\supervisely-colab

# 2. Add all updated files
git add .

# 3. Commit
git commit -m "Add automated CoreML, Google LiteRT, and ONNX export pipeline"

# 4. Set main branch
git branch -M main

# 5. Connect to your GitHub repository (replace with your repo URL)
git remote add origin https://github.com/<YOUR_USERNAME>/<YOUR_REPOSITORY>.git

# 6. Push to GitHub
git push -u origin main
```

### Step 3: Update Colab Badge Link
In `README.md` and `supervisely_training.ipynb`, replace `LorenzFon/supervisely-colab-trainer` with your actual repository path.

---

## 🔐 Credentials & Security

- **Never commit your Supervisely API Token to git!**
- The notebook is intentionally configured without hardcoded credentials.
- Use **Google Colab Secrets** (accessible via the 🔑 key icon on the left panel in Colab):
  - Key: `SUPERVISELY_TOKEN`
  - Value: `<your_supervisely_api_token>`
  - Toggle *Notebook access* to **ON**.

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
