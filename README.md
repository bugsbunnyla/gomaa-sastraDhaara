# Gomaa - Śāstra Dhārā

Real rPPG Facial Biometrics, Medical Report Parser & Vedic Threshold Engine.

## Repository Structure
```
gomaa-sastraDhaara/
├── README.md
├── index.html                  ← Main biometric app (face-api.js + CHROM rPPG)
├── generator.html              ← Lightweight repo generator
├── workbench_full_source.html  ← Self-contained workbench with embedded filesystem
└── content/
    └── models/
        ├── kriyakala.json
        ├── pariksha_rules.json
        └── vedic_thresholds.json
```

## Real Measurement Architecture

### Webcam rPPG (Real — No Simulation)
- **Heart Rate (BPM):** Forehead green-channel CHROM projection + FFT spectral peak
- **HRV (RMSSD):** Time-domain peak-to-peak interval analysis
- **Respiratory Rate:** Envelope modulation of rPPG signal (0.1–0.5 Hz band)
- **Signal Quality:** Spectral purity ratio (bandpass power / total power)

### Medical Report Parser
Parses **Blood Pressure, Glucose, Temperature, Hemoglobin** from:
- CSV (comma-delimited key-value)
- TXT (regex pattern matching: "BP 120/80", "Glucose 95", etc.)
- PDF (pdf.js text extraction + regex)
- XLSX (SheetJS row parsing)

### Honest Clinical Labels
Parameters impossible via webcam are explicitly labelled:
- **SPECT:** Requires gamma camera + radiotracer
- **BP/Glucose/Temp/Hgb without report:** "Upload report or use clinical device"

### Chakra Mapping
Chakra "resonance" is proxied to real measurable metrics with clear source labels:
- Root/Sacral → HRV grounding proxy
- Solar Plexus → Respiratory rate proxy
- Heart → Real HR coherence
- Throat/Third Eye → Signal quality proxy
- Crown → Integrated HRV proxy

## Licenses
- face-api.js: MIT
- Plotly.js: MIT
- SheetJS: Apache 2.0
- pdf.js: Apache 2.0
- Custom rPPG engine: MIT
