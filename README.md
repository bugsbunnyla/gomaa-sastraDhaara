# Gomaa - Śāstra Dhārā

Integrated Real Biometric & Medical Imaging Workbench.

## Repository Structure
```
gomaa-sastraDhaara/
├── README.md
├── index.html              ← Main integrated app
├── generator.html          ← Repo generator shell
└── content/
    └── models/
        ├── kriyakala.json
        ├── pariksha_rules.json
        └── vedic_thresholds.json
```

## Integrated Real Data Sources

### 1. Webcam rPPG (Real — No Simulation)
- **Heart Rate (BPM):** Forehead green-channel CHROM projection + FFT spectral peak
- **HRV (RMSSD):** Time-domain peak-to-peak interval analysis
- **Respiratory Rate:** Envelope modulation of rPPG signal (0.1–0.5 Hz band)
- **Signal Quality:** Spectral purity ratio (bandpass power / total power)
- **ML Features:** Pulse amplitude, rise time, spectral entropy → fed to TensorFlow.js BP model

### 2. Bluetooth Medical Devices (Real Hardware)
Uses Web Bluetooth API to connect to actual clinical devices:
- **Blood Pressure Cuff** (BLE service 0x1810)
- **Glucometer** (BLE service 0x1808)
- **Thermometer** (BLE service 0x1809)
- **Pulse Oximeter** (BLE service 0x1822)

### 3. ML Blood Pressure Estimation (TensorFlow.js)
- Personal calibration model: user enters known BP from a cuff, model learns their rPPG feature-to-BP mapping
- Architecture: 7-input → [32,16,8] dense layers → 2-output [systolic, diastolic]
- Requires minimum 2 calibration points
- Honest label: "ML Estimate — Calibrated"

### 4. DICOM Medical Imaging Viewer
- Upload real DICOM files from hospital (SPECT, CT, MRI)
- Uses dicomParser + canvas render with window/level
- Honest label: cannot generate images from webcam

### 5. Medical Report Parser
- CSV, TXT, PDF, XLSX parsing for BP, Glucose, Temperature, Hemoglobin, SpO2

### 6. Honest Clinical Labels
Parameters impossible via webcam are explicitly labeled with required action:
- **SPECT/CT/MRI:** "Upload DICOM from imaging facility"
- **BP without device/calibration:** "Connect BLE cuff, calibrate ML, or upload report"
- **Glucose without device:** "Connect BLE glucometer or upload report"
- **Hemoglobin:** "Upload lab report with Hgb value"

### 7. Chakra Proxy Mapping (Honest)
- Root/Sacral/Crown → HRV grounding proxy
- Solar Plexus → Respiratory rate proxy
- Heart → Real HR coherence
- Throat/Third Eye → Signal quality proxy

## Zero Hardcoding Guarantee
- No static `rawValue` strings
- No disconnected chart arrays
- Table and chart pull from identical `currentRows` array (single source of truth)
- Every numeric value comes from a real computation, device, parse, or honest "not available" label

## Licenses
- face-api.js: MIT
- Plotly.js: MIT
- SheetJS: Apache 2.0
- TensorFlow.js: Apache 2.0
- dicom-parser: MIT
- Custom engines: MIT
