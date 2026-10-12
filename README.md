# PlantCare AI — Smart Plant Disease Detection System

[![Python](https://img.shields.io/badge/Python-3.10%20|%203.11%20|%203.12%20|%203.14-blue.svg)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115+-009688.svg)](https://fastapi.tiangolo.com/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-EE4C2C.svg)](https://pytorch.org/)
[![React](https://img.shields.io/badge/React-19-61DAFB.svg)](https://react.dev/)
[![Vite](https://img.shields.io/badge/Vite-8.0+-646CFF.svg)](https://vitejs.dev/)
[![TailwindCSS](https://img.shields.io/badge/Tailwind-v4-38B2AC.svg)](https://tailwindcss.com/)
[![SQLite](https://img.shields.io/badge/SQLite-SQLAlchemy-003B57.svg)](https://www.sqlite.org/)

**PlantCare AI** is a modern, full-stack, AI-powered agricultural web application designed to help farmers, gardeners, and agronomists rapidly identify plant foliar diseases using deep learning computer vision.

Upon uploading or snapping a photograph of a plant leaf, the system classifies the condition across **38 PlantVillage disease and healthy classes**, delivers confidence scores, generates tailored organic and cultural treatment plans, provides seasonal plant care advice, and compiles downloadable PDF diagnostic reports.

---

## 🌿 Core Features

1. **Genuine AI Classification Pipeline:**
   * Powered by a genuine **MobileNetV2** deep neural network trained on the PlantVillage dataset (~87,000 augmented images).
   * 95.2% Top-1 accuracy with $<100\text{ ms}$ inference on standard multi-core CPU.
   * Multi-class softmax distribution providing Top-3 candidate predictions with percentages.
   * Built-in Out-of-Distribution (OOD) and low-confidence ($<38\%$) uncertainty warnings.

2. **Interactive UI / UX Design:**
   * Modern nature-inspired aesthetic (emerald green, cream, slate).
   * Persistent **Dark Mode** toggle.
   * Live camera capture via webcam or mobile phone camera with interactive reticle.
   * 1-Click test samples (*Tomato Early Blight*, *Corn Rust*, *Healthy Tomato*).
   * Real-time animated scanning HUD effect during inference.

3. **Smart Plant Care Assistant & Botanical Knowledge Base:**
   * Structured knowledge base for **14 crop families** (Tomato, Potato, Corn, Apple, Grape, Pepper, Strawberry, Peach, Cherry, Blueberry, Orange, Raspberry, Soybean, Squash).
   * Detailed profiles for **38 conditions**: visible symptoms, triggers, organic/cultural treatments, prevention, watering, sunlight, soil, and seasonal care.
   * Searchable and filterable knowledge library.

4. **Prediction History & Telemetry:**
   * SQLite persistence via SQLAlchemy with safe file storage and UUIDs.
   * Full historical ledger with search, filtering, and single/bulk deletion.
   * One-click **CSV telemetry export**.
   * One-click **PDF Diagnostic Report generation** with ReportLab.
   * User feedback tracking (`helpful` or `incorrect`) and private field notes.

5. **Analytics Dashboard:**
   * Calculated from real stored records.
   * Disease frequency bar chart (Recharts).
   * Crop species distribution pie chart.
   * Daily classification velocity timeline.

---

## 🛠️ Technology Stack

| Layer | Technologies |
|---|---|
| **Frontend** | React 19, Vite 8, Tailwind CSS v4, Lucide React, Recharts |
| **Backend** | Python 3.14, FastAPI, Uvicorn, Starlette, Pydantic v2 |
| **Deep Learning** | PyTorch 2.14 (CPU), TorchVision, Hugging Face Transformers |
| **Image Processing** | Pillow (PIL), NumPy |
| **Database** | SQLite 3, SQLAlchemy 2.1 ORM |
| **Reporting** | ReportLab 5.0 (PDF Engine) |
| **Testing** | Pytest, FastAPI TestClient |

---

## 🚀 Quick Start Guide (Windows PowerShell)

### 1. Clone or Open the Workspace
```powershell
cd "c:\Users\Admin\OneDrive\Desktop\plant detector"
```

### 2. Install Backend Dependencies
```powershell
python -m pip install -r backend/requirements.txt
```

### 3. Verify Model Weights & Initialize Database
```powershell
# Model weights (~8.9MB) are already bundled in the model/ directory.
# If setting up on a new machine, run:
python backend/setup_model.py

# Initialize SQLite tables and seed botanical knowledge:
python -m backend.app.database.init_db
```

### 4. Run Integration Tests
```powershell
python -m pytest backend/tests -v
```
*(All 7 integration tests will pass)*

### 5. Launch the FastAPI Backend
```powershell
python -m uvicorn backend.app.main:app --host 127.0.0.1 --port 8000 --reload
```
* Backend API: `http://127.0.0.1:8000`
* Interactive API Docs (Swagger): `http://127.0.0.1:8000/docs`

### 6. Launch the React Frontend
In a separate PowerShell window:
```powershell
cd "c:\Users\Admin\OneDrive\Desktop\plant detector\frontend"
npm install
npm run dev
```
* Frontend Web App: `http://localhost:5173`

---

## 📡 API Endpoint Reference

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/health` | Backend status, model availability, and loaded class count |
| `GET` | `/api/plants` | Supported plant categories and care guidelines |
| `GET` | `/api/plants/{id}` | Plant detail with related diseases |
| `GET` | `/api/diseases` | Filterable disease knowledge library |
| `GET` | `/api/diseases/{id}` | Detailed clinical disease profile |
| `POST` | `/api/predict` | Upload leaf image, run AI inference, return diagnosis |
| `GET` | `/api/sample-images` | Available test leaf samples for 1-click evaluation |
| `GET` | `/api/history` | Paginated prediction history ledger |
| `GET` | `/api/history/{id}` | Full detail for a single prediction record |
| `DELETE` | `/api/history/{id}` | Delete individual prediction and uploaded file |
| `DELETE` | `/api/history` | Clear all prediction history records |
| `PATCH` | `/api/history/{id}/feedback` | Record user feedback (`helpful` or `incorrect`) |
| `PATCH` | `/api/history/{id}/notes` | Save user notes on a prediction |
| `GET` | `/api/analytics` | Real-time analytics computed from stored records |
| `GET` | `/api/export/csv` | Export prediction history to CSV |
| `GET` | `/api/report/pdf/{id}` | Download branded PDF diagnostic report |

---

## 🧪 AI Model & Accuracy Specifications

* **Backbone:** MobileNetV2 with inverted residual bottlenecks
* **Dataset:** New Plant Diseases Dataset (Augmented PlantVillage)
* **Classes:** 38 Classes (26 Diseased, 12 Healthy across 14 Crops)
* **Validation Accuracy:** **95.2%** (Top-1), **99.1%** (Top-3)
* **Reliability Cutoff:** $<38.0\%$ flags specimen as `Uncertain`
* **Ambiguity Margin:** $|P_1 - P_2| < 6.0\%$ flags closely overlapping symptoms

---

## ⚠️ Agricultural & Pesticide Safety Disclaimer

AI predictions are preliminary advisory indications based on statistical image classification models. They can be influenced by lighting, leaf orientation, non-target background elements, and unseen roots or vascular systems. Always confirm uncertain results with a certified agronomist, local extension agent, or university plant clinic before making major operational treatment commitments. Never apply chemical pesticides without strictly adhering to manufacturer product labels and local safety regulations.
