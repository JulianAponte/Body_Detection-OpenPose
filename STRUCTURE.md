# 📊 Estructura del Proyecto Body Detection OpenPose

Mapa detallado de la organización del proyecto.

---

## 🏗️ Árbol de Directorios

```
Body_Detection-OpenPose/
│
├── 📄 Documentación Principal
│   ├── README.md                    ⭐ Punto de entrada
│   ├── QUICK_START.md              🚀 Inicio en 5 min
│   ├── INDEX.md                    📰 Índice de navegación
│   ├── CONTRIBUTING.md             🤝 Cómo contribuir
│   ├── ARCHITECTURE.md             🏗️ Detalles técnicos
│   └── STRUCTURE.md                📊 Este archivo
│
├── 📁 body-cam/                    ⭐ BACKEND PYTHON
│   ├── main.py                     # Script principal
│   ├── pose_detector.py            # Detector de postura
│   ├── config.py                   # Configuración global
│   ├── utils.py                    # Helper functions
│   ├── requirements.txt            # Dependencias Python
│   ├── README.md                   # Documentación backend
│   │
│   ├── app/
│   │   └── services/
│   │       └── vision_service.py   # VisionService
│   │
│   ├── models/
│   │   ├── face_landmarker.task   # Modelo MediaPipe facial
│   │   └── pose_landmarker_full.task # Modelo MediaPipe pose
│   │
│   ├── tests/
│   │   └── test_vision.py         # Tests
│   │
│   └── .venv/                      # Virtual environment
│
├── 📁 UI/                          ⭐ FRONTEND - UI
│   ├── EvaluationRoom.tsx          # Componente de grabación
│   ├── EvaluationRoom.css          # Estilos
│   ├── EvaluationPage.tsx          # Página wrapper
│   └── README.md                   # Documentación UI
│
├── 📁 src/                         ⭐ FRONTEND - REACT
│   ├── App.tsx                     # Root app
│   ├── main.tsx                    # React DOM
│   ├── index.css                   # Estilos globales
│   ├── README.md                   # Documentación
│   │
│   ├── components/
│   │   ├── common/
│   │   │   ├── Button.tsx          # Botón reutilizable
│   │   │   └── Input.tsx           # Input reutilizable
│   │
│   └── pages/
│       └── Login/                  # Autenticación
│
├── 📄 Configuración
│   ├── package.json                # Dependencias Node.js
│   ├── tsconfig.json               # TypeScript config
│   ├── vite.config.ts              # Vite config
│   └── .gitignore                  # Git ignore
│
└── 📁 .github/                     # GitHub config (futuro)
    └── workflows/                  # CI/CD workflows
```

---

## 🎯 Mapeo: Características → Archivos

| Característica | Ubicación | Archivo |
|---|---|---|
| Grabación de video | UI | EvaluationRoom.tsx |
| Botón reutilizable | src | components/common/Button.tsx |
| Input reutilizable | src | components/common/Input.tsx |
| Detección de postura | body-cam | pose_detector.py |
| Detección facial | body-cam | app/services/vision_service.py |
| Configuración global | body-cam | config.py |
| Utilidades visuales | body-cam | utils.py |

---

## 📦 Dependencias

### Frontend (package.json)
- React 18+
- TypeScript 5+
- Vite 5+

### Backend (requirements.txt)
- Python 3.12
- mediapipe 0.10+
- opencv-python 4.8+
- numpy 1.24+

---

## 📚 Referencias Cruzadas

- Para inicio rápido → [QUICK_START.md](QUICK_START.md)
- Para documentación UI → [UI/README.md](UI/README.md)
- Para documentación src → [src/README.md](src/README.md)
- Para documentación backend → [body-cam/README.md](body-cam/README.md)
- Para contribuir → [CONTRIBUTING.md](CONTRIBUTING.md)
- Para arquitectura → [ARCHITECTURE.md](ARCHITECTURE.md)

---

**Última actualización:** April 14, 2026
