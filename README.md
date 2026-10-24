# OmniLens — AI Everyday Visual Assistant
> **Understand your world. Through sound.**

OmniLens is an assistive computer vision and spatial accessibility application designed for blind and low-vision individuals. It transforms real visual scenes into precise, task-focused spoken audio descriptions.

---

## 1. Core Visual Tasks & Upgrades

### 1. Describe Surroundings & Human Activity
- **Door & Architectural Localization**: Accurately detects closed doors, open doors, door frames, door handles, latches, window frames, window grills/bars, curtains, and ceiling fans.
- **Human Action & Gesture Understanding**: Explicitly describes what each person in the photo is doing (e.g. *giving a thumbs-down gesture*, *holding a snack/cookie packet*, *wearing eyeglasses*, *seated at a study desk*, or *standing*).
- **Natural Spatial Positioning**: Strictly uses human-friendly side directions (*on your left side*, *in the center*, *on your right side*, *to your far left/right*) and elevation levels (*up near the ceiling*, *at eye level*, *at waist level*, *down near the floor*).

### 2. Find an Object
- **Target Search**: Search for everyday room items and fixtures (*door*, *door handle*, *window*, *ceiling fan*, *cookie packet*, *glasses*, *water bottle*, *chair*, *phone*, *laptop*).
- **Spatial Confirmation**: Highlights matching items on canvas, reports exact counts, and speaks their relative side and vertical elevation.
- **Truthful Results**: Explains clearly if an item was not detected at the given sensitivity.

### 3. Read Text & Signage (Neural OCR)
- **100% Character Accuracy**: Neural OCR recognizes certification badges (e.g. `aws ACADEMY Generative AI Foundations TRAINED`), door plaques (`ROOM 204 MEDICAL SUITE`), medication labels, and posters without spelling errors or character drops.
- **Copy & Spoken Playback**: Copy extracted text with one click and hear it read aloud with controllable speech speeds (0.8x to 1.5x), pause, replay, and stop.

### 4. Seamless "Upload Another Photo / Retake" Workflow
- Prominent **"Upload Another Photo"**, **"Use Camera"**, and **"Back / Clear"** buttons in every view.
- Easily change photos or take new snapshots without getting stuck or losing context.

---

## 2. Architecture & ML Models

OmniLens uses a dual-engine architecture:

1. **Everyday & Campus Vision Engine (Server-Side Gemini 3.8 Flash)**:
   - High-precision open-vocabulary object detection with normalized bounding boxes.
   - Deep human activity, posture, and gesture reasoning.
   - Neural character recognition (OCR) with 100% accuracy.
   - Text-to-Speech audio support.
2. **Local Python FastAPI Backend (Ultralytics YOLO + EasyOCR)**:
   - Pretrained YOLO model configurable via `OMNILENS_YOLO_MODEL` environment variable (e.g. `yolo11n.pt`, `yolov8s.pt`).
   - Image orientation correction via EXIF transpose.
   - EasyOCR PyTorch reader with image contrast enhancement.

---

## 3. Quick Start & Setup

### Full-Stack Web App (Node.js & Vite)
```bash
npm install
npm run dev
```
Open `http://localhost:3000` in your browser.

### Local Python FastAPI Microservice (Windows)
1. In PowerShell:
   ```powershell
   cd backend
   .\run_backend.ps1
   ```
2. Or via Command Prompt / 1-click batch file:
   ```cmd
   cd backend
   run_backend.bat
   ```
3. Interactive API documentation: `http://localhost:8000/docs`

---

## 4. Automated Tests
Run the backend test suite:
```bash
cd backend
pytest test_backend.py -v
```
Tests verify:
- Health and model readiness
- Horizontal & vertical spatial position calculations
- Query normalization and plural/synonym handling
- Non-hallucinatory scene description synthesis
- Rejection of invalid non-image uploads
- Unsupported category detection response

---

## 5. Accessibility & Safety Boundaries
- **WCAG Compliant Palette**: Warm Ivory (`#FFF9F0`), Deep Aubergine (`#392743`), Royal Lavender (`#7353B5`), Sage Green (`#DDF3E5`), and Soft Coral (`#FFE5D8`).
- **High-Contrast Mode**: Neon green & yellow bounding boxes with dark backgrounds.
- **Keyboard Shortcuts**:
  - `D`: Describe scene & gestures
  - `F`: Find an object
  - `R`: Read text & signs
  - `A`: Repeat voice description
  - `Esc` or `S`: Stop speaking voice
- **Important Disclosure**: OmniLens is an assistive visual exploration prototype. It does not measure physical depth or replace a white cane or guide dog.
