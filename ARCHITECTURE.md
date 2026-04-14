# 🏗️ Arquitectura de Body Detection OpenPose

Documento técnico detallado sobre la arquitectura del proyecto.

---

## 📐 Arquitectura General

```
┌────────────────────────────────────────────────────────────────┐
│                    OPENPOSE SYSTEM                             │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│  ┌──────────────────────────┐    ┌──────────────────────────┐  │
│  │   CLIENT LAYER           │    │   SERVER LAYER           │  │
│  │  (React + TypeScript)    │    │  (Python + MediaPipe)    │  │
│  │                          │    │                          │  │
│  │  ┌────────────────────┐  │    │  ┌──────────────────────┐  │
│  │  │ EvaluationRoom    │  │    │  │ Vision Service       │  │
│  │  │ - Capture         │  │    │  │ - Pose Detection     │  │
│  │  │ - Stream          │  │    │  │ - Face Detection     │  │
│  │  │ - Download        │  │    │  │ - Process JSON       │  │
│  │  └────────────────────┘  │    │  └──────────────────────┘  │
│  │                          │    │         │                  │
│  │  ┌────────────────────┐  │    │  ┌──────▼──────────────┐  │
│  │  │ UI Components     │  │    │  │ MediaPipe Models   │  │
│  │  │ - Button          │  │    │  │ - face_landmarker  │  │
│  │  │ - Input           │  │    │  │ - pose_landmarker  │  │
│  │  │ - Pages           │  │    │  └────────────────────┘  │
│  │  └────────────────────┘  │    │                          │
│  └──────────────────────────┘    └──────────────────────────┘
│         │                                    │                 │
│         │      WebRTC/HTTP                   │                 │
│         └────────────────────────────────────┘                 │
│                                                                │
│  ┌────────────────────────────────────────────────────────┐   │
│  │  STORAGE LAYER                                        │   │
│  │  - Local Downloads (WebM)                             │   │
│  │  - JSON Output Files                                  │   │
│  └────────────────────────────────────────────────────────┘   │
│                                                                │
└────────────────────────────────────────────────────────────────┘
```

---

## 🎯 Componentes Principales

### 1. Frontend (React + TypeScript)

**Estructura de Carpetas:**
```
src/
├── components/
│   ├── common/          # Componentes reutilizables
│   │   ├── Button.tsx
│   │   └── Input.tsx
│   └── ...
├── pages/
│   ├── Login/           # Autenticación
│   └── ...
└── App.tsx              # Root component
```

**Flujo de Datos:**
```
User Interaction → React Event → State Update → Re-render → DOM
```

### 2. Backend (Python + MediaPipe)

**Estructura de Carpetas:**
```
body-cam/
├── main.py                      # Entry point
├── pose_detector.py             # Pose detector
├── config.py                    # Configuration
├── utils.py                     # Helpers
│
├── app/
│   └── services/
│       └── vision_service.py    # Vision service
│
├── models/
│   ├── face_landmarker.task    # Face model
│   └── pose_landmarker_full.task # Pose model
│
└── tests/
    └── test_vision.py          # Unit tests
```

**Vision Pipeline:**
```
Frame (Input)
    ↓
MediaPipe PoseLandmarker
    ├─ Detect 33 body keypoints
    ├─ Filter by confidence
    └─ Return normalized coords
    ↓
MediaPipe FaceLandmarker
    ├─ Detect 478 face landmarks
    ├─ Extract blend shapes
    └─ Return facial features
    ↓
Post-processing
    ├─ Classify pose
    ├─ Calculate movement
    └─ Format JSON
    ↓
Output (JSON)
```

---

## 🔄 Integración Frontend-Backend

### Actual (Local)

```
Frontend (http://localhost:5173)
    ├─ Record video locally
    ├─ Save as WebM
    └─ Download to device

Backend (http://localhost:8000)
    ├─ Process local videos
    └─ Output JSON files
```

### Futuro (REST API)

```
Frontend → POST /api/upload
    ↓
REST Server
    ├─ Receive video
    ├─ Queue processing
    └─ Return results
    ↓
Backend Worker
    ├─ Process video
    ├─ Save results
    └─ Update status
```

---

## 📦 Dependencias Clave

### Frontend

| Paquete | Versión | Propósito |
|---------|---------|-----------|
| React | 18+ | UI framework |
| TypeScript | 5+ | Type safety |
| Vite | 5+ | Build tool |

### Backend

| Paquete | Versión | Propósito |
|---------|---------|-----------|
| Python | 3.12 | Runtime |
| MediaPipe | 0.10+ | ML inference |
| OpenCV | 4.8+ | Video processing |
| NumPy | 1.24+ | Numerical computing |

---

## ⚙️ Configuración

### Frontend (vite.config.ts)
- Base URL: /
- Dev server: localhost:5173
- Build output: dist/

### Backend (config.py)
- POSE_MODEL = "pose_landmarker_full.task"
- CONFIDENCE_THRESHOLD = 0.5

---

## 🚀 Performance

### Frontend
- Target: < 3s First Contentful Paint
- Code splitting (lazy loading)
- Optimization: Images, CSS minification

### Backend
- Target: 30+ FPS on GPU, 15+ FPS on CPU
- GPU acceleration (if available)
- Model caching in memory

---

## 🔮 Arquitectura Futura

### Phase 2: Cloud Integration
- REST API Server (FastAPI)
- Video storage (S3)
- Job queue (Celery)
- Database (PostgreSQL)

### Phase 3: Advanced Features
- Multi-person pose detection
- Real-time streaming analysis
- Mobile app (React Native)
- Analytics dashboard

---

**Última actualización:** April 14, 2026
