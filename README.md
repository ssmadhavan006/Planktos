# 🌊 Planktos: Intelligent Embedded Microscopy and Marine Taxonomic Enumeration Platform

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue.svg)](https://www.python.org/)
[![YOLOv8](https://img.shields.io/badge/YOLOv8-Ultralytics-00FFFF.svg)](https://github.com/ultralytics/ultralytics)
[![Gradio](https://img.shields.io/badge/Gradio-4.0%2B-orange.svg)](https://gradio.app/)
[![Hardware](https://img.shields.io/badge/Target-Raspberry%20Pi%205-red.svg)](https://www.raspberrypi.com/products/raspberry-pi-5/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

**An indigenous, edge-ready artificial intelligence platform engineered for automated identification, taxonomic classification, and biodiversity enumeration of marine microorganisms.**

---

## 📋 Table of Contents

- [Overview & National Impact](#-overview--national-impact)
- [Key Features](#-key-features)
- [System Architecture](#-system-architecture)
- [Hardware & Field Specifications](#-hardware--field-specifications)
- [Installation Guide](#-installation-guide)
- [Usage & Workflow](#-usage--workflow)
- [Demonstration](#-demonstration)
- [Taxonomic Classification & Model Details](#-taxonomic-classification--model-details)
- [Project Repository Structure](#-project-repository-structure)
- [Raspberry Pi 5 Deployment & Field Optimization](#-raspberry-pi-5-deployment--field-optimization)
- [Troubleshooting & Diagnostics](#-troubleshooting--diagnostics)
- [Authors & Research Team](#-authors--research-team)
- [Acknowledgments](#-acknowledgments)

---

## 🌐 Overview & National Impact

Marine zooplankton and micro-organisms constitute the biological cornerstone of oceanic trophic webs and serve as vital biological indicators for aquatic ecosystem health, fisheries abundance, water quality, and marine climate shifts. Across national coastal zones, maritime economic zones, and offshore waters, systematic biomonitoring is crucial for sustainable fisheries management, early detection of harmful ecological changes, and marine environmental protection.

### The National Maritime Challenge
Conventional marine biodiversity assessments rely on manual microscopic examination by trained marine biologists and taxonomists. This traditional approach presents major operational hurdles:
- **Time Intensive**: Requires 10 to 20 minutes per specimen slide.
- **High Resource Demand**: Demands specialized taxonomic laboratory infrastructure and manual operators.
- **Subjectivity & Fatigue**: Manual visual counting is vulnerable to observer fatigue and human classification variances.
- **Field Scalability Bottleneck**: Conventional methods cannot be scaled for real-time onboard monitoring on research vessels, remote coastal stations, or automated ocean buoys.

### The Planktos Solution
Planktos provides a fully autonomous, offline-capable, cost-effective embedded AI system. Built on optimized deep learning (YOLOv8) deployed on edge-computing hardware (Raspberry Pi 5), the system enables:
- **Automated Real-Time Detection**: Simultaneously identifies multiple overlapping and microscopic organisms across diverse spatial scales.
- **High-Precision Multi-Class Identification**: Categorizes 13 distinct marine zooplankton taxa.
- **Quantitative Census & Analytics**: Computes species richness, diversity indices, relative abundance percentages, and detection confidence metrics.
- **100% Air-Gapped / Offline Reliability**: Completely operational with no internet or cloud dependence, built specifically for vessels and remote marine laboratories.
- **National Self-Reliance**: An indigenous technology advancing coastal biosurveillance, marine biodiversity conservation, and United Nations Sustainable Development Goals (SDG 6: Clean Water, SDG 14: Life Below Water).

---

## ✨ Key Features

### Core Scientific Capabilities
- **Multi-Organism Detection**: YOLOv8 architecture tuned to detect overlapping, translucent, and morphology-variable organisms.
- **Taxonomic Enumeration**: Automated per-class population tallying and real-time ecological census generation.
- **Statistical Biodiversity Analytics**: Dynamic calculation of sample diversity, species richness, dominant taxa identification, and confidence distribution.
- **High-Throughput Verification**: Accelerates microscopic sample analysis from 20 minutes down to seconds.

### Technical & Engineering Highlights
- **Embedded Edge Acceleration**: Tailored for quad-core ARM Cortex-A76 (Raspberry Pi 5 8GB) with support for NCNN, ONNX, and INT8 TFLite acceleration backends.
- **Thread-Safe Optical Ingestion**: Dedicated non-blocking background thread (`camera.py`) with a one-deep double buffer for continuous digital microscope feed.
- **Field-Ready Web Interface**: Gradient-themed Gradio dashboard supporting static slide uploads, video sample batch analysis, and live microscope view.
- **Air-Gapped Deployment Pipeline**: Includes scripts for building offline wheelhouses, headless systemd service management, and OS-level performance tuning.

---

## 🏗️ System Architecture

```
┌────────────────────────────────────────────────────────┐
│               USB Digital Microscope                   │
│             (1080p / 4K Digital Optical Feed)          │
└───────────────────────┬────────────────────────────────┘
                        │
                        ▼
┌────────────────────────────────────────────────────────┐
│             Raspberry Pi 5 (8GB RAM)                   │
│  ┌──────────────────────────────────────────────────┐  │
│  │   Optical Ingestion Pipeline (camera.py)         │  │
│  │   • Double-buffered capture • Auto-scaling       │  │
│  └───────────────────┬──────────────────────────────┘  │
│                      │                                 │
│  ┌───────────────────▼──────────────────────────────┐  │
│  │   YOLOv8 Inference Engine (models/best.pt)       │  │
│  │   • PyTorch / NCNN / ONNX / TFLite Backends      │  │
│  │   • Multi-scale Detection & Classification       │  │
│  └───────────────────┬──────────────────────────────┘  │
│                      │                                 │
│  ┌───────────────────▼──────────────────────────────┐  │
│  │   Taxonomic Analysis & Enumeration Engine        │  │
│  │   • Class Tallying • Biodiversity Statistics     │  │
│  └───────────────────┬──────────────────────────────┘  │
└────────────────────┬─┴─────────────────────────────────┘
                     │
        ┌────────────┴────────────┐
        ▼                         ▼
┌──────────────┐         ┌──────────────┐
│  Gradio Web  │         │  Analytical  │
│  Dashboard   │         │  Reports &   │
│  (127.0.0.1) │         │  Annotations │
└──────────────┘         └──────────────┘
```

---

## 🔧 Hardware & Field Specifications

### Laboratory Development Environment
- **Operating System**: Linux (Ubuntu 22.04+), Windows 10/11, or macOS
- **Python**: Version 3.9, 3.10, 3.11, or 3.12
- **RAM**: 8 GB minimum (16 GB recommended for model compilation)
- **Acceleration**: Optional CUDA-capable GPU for training/fast verification

### Field Production Deployment (Embedded Station)
| Hardware Component | Recommended Specification | Primary Function |
|---|---|---|
| **SBC Compute** | Raspberry Pi 5 (8GB LPDDR4X RAM) | Embedded edge inference host |
| **Optics** | USB Digital Microscope (1080p / 4K) | Specimen slide visual capture |
| **Power Supply** | Official 27W USB-C Power Adapter (5V / 5A) | Stable rail power without throttling |
| **Primary Storage** | 64GB High-Endurance microSD or NVMe SSD | Operating system, models, and local data |
| **Thermal Solution**| Raspberry Pi Active Cooler (Heatsink + Fan) | Sustained peak CPU clock under continuous load |
| **Enclosure** | Ruggedized sealed protective casing | Protection against marine humidity and salinity |

---

## 📦 Installation Guide

### Prerequisites
Ensure Python 3.9 or higher is installed:
```bash
python --version
pip --version
```

### 1. Clone the Repository
```bash
git clone https://github.com/ssmadhavan006/Planktos.git
cd Planktos
```

### 2. Configure Virtual Environment
```bash
# Create virtual environment
python -m venv venv

# Activate environment
# On Linux / macOS:
source venv/bin/activate

# On Windows (Command Prompt):
venv\Scripts\activate

# On Windows (PowerShell):
venv\Scripts\Activate.ps1
```

### 3. Install Dependencies
```bash
pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Verify Model Placement
Confirm that the trained model weights file is present at:
```
models/best.pt
```
*(You may override this location at runtime using the `MODEL_PATH` environment variable).*

---

## 🚀 Usage & Workflow

### Starting the Application

#### Option 1: Standard Launcher
```bash
python app.py
```

#### Option 2: Production Launcher (Raspberry Pi / Linux)
```bash
chmod +x scripts/run_optimized.sh
./scripts/run_optimized.sh
```

Once started, the application will bind to a local interface (typically `http://127.0.0.1:7860`). Open your browser to access the Planktos control dashboard.

### Operational Modes

1. **Static Specimen Analysis (Slide Upload)**:
   - Navigate to the **Microorganism Analysis** tab.
   - Select an image from the curated test directories:
     - `test_img/`: Standard microscopic reference sample images.
     - `test_new/`: Field verification and macroscopic test sample imagery.
   - Click **Analyze Microorganism Sample**.
   - Review the annotated output highlighting detected organisms alongside the taxonomic breakdown table and diversity metrics.

2. **Live Microscope Video Stream**:
   - Navigate to the **Live Microscope** tab.
   - Connect a compatible USB digital microscope.
   - Click **Start Stream** to initiate low-latency live preview.
   - Click **Capture & Analyze Frame** to freeze a slide frame and run instant enumeration.

3. **Video Batch Processing**:
   - Navigate to the **Video Sample Analysis** tab.
   - Upload a microscope recording or select a sample clip.
   - The pipeline processes frames with dynamic striding, tracking species abundance throughout the sample duration.

---

## 🎥 Demonstration

A demonstration overview of the Planktos embedded analysis system is available below:

[![Planktos Demonstration](https://img.youtube.com/vi/WEvNaXpfy-I/maxresdefault.jpg)](https://youtu.be/WEvNaXpfy-I)

---

## 🧠 Taxonomic Classification & Model Details

Planktos is trained to accurately segment, identify, and count 13 classes of marine organisms:

| Species / Class | Bounding Box Color | Ecological & Taxonomic Description |
|---|---|---|
| **Chaetognath** | 🔴 Red | Predatory arrow worms, key planktonic carnivores |
| **Larval Fish** | 🟢 Green | Early post-embryonic developmental stage fish |
| **Hydromedusa** | 🔵 Blue | Small predatory hydrozoan medusae |
| **Lobate Ctenophore** | 🟡 Yellow | Distinctive lobed comb jellies |
| **Pleurobrachia** | 🟣 Magenta | Sea gooseberries, tentacled comb jellies |
| **Shrimp** | 🔷 Cyan | Decapod crustacean larvae and juveniles |
| **Siphonophore** | 🟣 Purple | Complex colonial pelagic hydrozoans |
| **Stomatopod Larva** | 🌊 Teal | Mantis shrimp planktonic larvae |
| **Thaliac** | 🟠 Orange | Pelagic tunicates, salps, and doliolids |
| **Polychaete Worm** | 💜 Indigo | Bristle worms and segmented marine annelids |
| **Cumacean** | 🌸 Violet | Hooded shrimp, diminutive benthic/pelagic crustaceans |
| **Ctenophore** | 🌳 Dark Green | General pelagic comb jellies |
| **Unknown** | ⚪ Gray | Unclassified or uncharacterized micro-fauna |

> 📄 **Taxonomic Reference Document**: For detailed morphological profiles and taxonomic keys, refer to [`docs/Classification_table_YOLOv8.pdf`](docs/Classification_table_YOLOv8.pdf).

### Model Architecture Specifications
- **Base Architecture**: Ultralytics YOLOv8
- **Input Resolution**: Auto-scaled to 640x640 by default (configurable down to 416x416 via `YOLO_IMGSZ`)
- **Default Confidence Cutoff**: 0.30 (configurable via `CONFIDENCE_THRESHOLD`)
- **Weights File**: `models/best.pt` (tracked via Git LFS)
- **Manifest**: `models/exports.json` (records compilation parameters and verified class indices)

---

## 📁 Project Repository Structure

```
Planktos/
├── app.py                          # Primary Gradio application and pipeline entry point
├── camera.py                       # Thread-safe non-blocking microscope capture engine
├── optimize_model.py               # Model optimization, quantization, and drift verification
│
├── requirements.txt                # Desktop and laboratory development dependencies
├── requirements-pi.txt             # Lightweight dependencies for Raspberry Pi 5 runtime
├── requirements-export.txt         # Toolchain for compiling ONNX, NCNN, and TFLite models
│
├── scripts/
│   ├── run_optimized.sh            # Production launcher with thread and memory tuning
│   ├── create_offline_bundle.sh    # Builder script for air-gapped aarch64 wheelhouse
│   ├── install_offline.sh          # Offline installer script for disconnected stations
│   ├── setup_pi_os.sh              # Linux OS performance optimizer (ZRAM, governor, USB)
│   ├── pi_healthcheck.py           # Field diagnostic and inference benchmarking suite
│   └── planktos.service           # systemd service unit for headless auto-start on boot
│
├── docs/
│   ├── PI5_DEPLOYMENT.md           # In-depth guide for Raspberry Pi field deployment
│   └── Classification_table_YOLOv8.pdf # Comprehensive taxonomic classification reference sheet
│
├── models/
│   ├── best.pt                     # Production YOLOv8 trained weights (Git LFS)
│   └── exports.json                # Model export parameters and class metadata manifest
│
├── test_img/                       # Reference microscopy test images & calibration corpus
├── test_new/                       # Field validation and sample photography dataset
└── tests/
    ├── test_app.py                 # Unit tests for application logic, camera, and backends
    └── test_optimize_model.py      # Unit tests for accuracy-drift verification algorithms
```

---

## 🥧 Raspberry Pi 5 Deployment & Field Optimization

Planktos includes an end-to-end toolchain for deploying directly to embedded Raspberry Pi 5 hardware operating fully air-gapped in the field.

For comprehensive instructions, consult the complete guide in [`docs/PI5_DEPLOYMENT.md`](docs/PI5_DEPLOYMENT.md).

### Quick Deployment Workflow

```bash
# 1. On your development machine: Export and verify optimized model backends
pip install -r requirements.txt -r requirements-export.txt
python optimize_model.py export --formats ncnn onnx tflite --imgsz 416
python optimize_model.py verify --iou-tol 0.85 --conf-tol 0.1

# 2. Build the offline package bundle for air-gapped deployment
./scripts/create_offline_bundle.sh --archive

# 3. On the Raspberry Pi: Run offline installation and OS optimization
./scripts/install_offline.sh
sudo ./scripts/setup_pi_os.sh
sudo reboot

# 4. Launch with optimized runtime parameters
./scripts/run_optimized.sh

# 5. (Optional) Enable continuous boot service
sudo cp scripts/planktos.service /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl enable --now planktos
```

### Runtime Environment Tunables

| Environment Variable | Default | Purpose & Recommendations |
|---|---|---|
| `CPU_THREADS` | `min(4, cpu_count)` | Constrains worker thread pools (PyTorch, OpenCV, OpenMP) to prevent thread oversubscription. |
| `MODEL_BACKEND` | `auto` | Automatically selects the fastest compiled artifact (`ncnn` -> `tflite` -> `onnx` -> `pytorch`). |
| `MODEL_PATH` | None | Direct path to a specific model file, overriding backend auto-selection. |
| `YOLO_IMGSZ` | `640` | Inference resolution. Setting this to `416` provides approximately 2.3x faster execution on embedded CPUs. |
| `MAX_DIMENSION` | `2048` | Caps pre-inference image resizing bounds (set to `1280` on embedded hardware). |
| `CONFIDENCE_THRESHOLD` | `0.3` | Minimum confidence score for retaining detections. |
| `GRADIO_SERVER_NAME` | `127.0.0.1` | Local binding interface. Use `0.0.0.0` when serving over an isolated local vessel network. |
| `GRADIO_SHARE` | `false` | Retained as `false` for field use to maintain strict offline isolation and prevent external timeouts. |

---

## 🔧 Troubleshooting & Diagnostics

Run the integrated diagnostic suite to evaluate system readiness, thermal state, and inference speed:
```bash
python scripts/pi_healthcheck.py --bench
```

### Common Resolutions
- **Model Missing Error**: Ensure `models/best.pt` exists and was pulled with Git LFS:
  ```bash
  git lfs pull
  ```
- **Port In Use Error**: If port 7860 is occupied, Gradio will automatically try the next available port. Alternatively, terminate stale instances:
  ```bash
  fuser -k 7860/tcp
  ```
- **Camera Not Detected**: Check video device permissions on Linux:
  ```bash
  sudo usermod -aG video $USER
  ls -l /dev/video*
  ```

---

## 👥 Authors & Research Team

* **S.S. MADHAVAN**  
  📧 ssmadhavan006@gmail.com  
  🔗 [GitHub Profile](https://github.com/ssmadhavan006)

* **DIVYESH HARI G**  
  📧 divyesh02208@gmail.com  
  🔗 [GitHub Profile](https://github.com/DIVYESH-HARI)

* **VIJAYA KARTHICK RAJA U M**  
  📧 vkr3056@gmail.com  
  🔗 [GitHub Profile](https://github.com/KARTHICK-3056)

* **K. RAKSHITHASRI**  
  📧 rakshiekt@gmail.com  
  🔗 [GitHub Profile](https://github.com/rakshithasri06)

* **M.N. RAKSHA**  
  📧 rakshanathan006@gmail.com  
  🔗 [GitHub Profile](https://github.com/raksha006)

---

## 🙏 Acknowledgments

- **Ultralytics**: For the robust YOLOv8 deep learning vision framework.
- **Gradio Team**: For the flexible edge-compatible user interface architecture.
- **Marine Research Community**: For datasets, taxonomic identification keys, and ecological validation.
- **Open-Source Scientific Python Ecosystem**: For PyTorch, OpenCV, NumPy, and related tools.

---

<div align="center">

### 🌊 Safeguarding Marine Biodiversity Through Indigenous AI Innovation 🌊

**National Marine Conservation & Bio-Intelligence | Open Science**

---

**[⭐ Star this repository](https://github.com/ssmadhavan006/Planktos)** | **[📖 Deployment Guide](docs/PI5_DEPLOYMENT.md)** | **[🐛 Issue Tracker](https://github.com/ssmadhavan006/Planktos/issues)**

</div>
