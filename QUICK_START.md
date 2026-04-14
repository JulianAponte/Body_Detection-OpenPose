# 🚀 Quick Start - Body Detection OpenPose

Inicia el proyecto en **5 minutos** con dos terminales.

---

## ⚡ Pasos

### 1️⃣ Abre dos terminales

**Terminal 1: Backend (Python)**
```powershell
cd body-cam
.\.venv\Scripts\Activate.ps1
python main.py --source 0
```

**Terminal 2: Frontend (React)**
```powershell
npm run dev
```

### 2️⃣ Abre en el navegador

```
http://localhost:5173
```

---

## ✅ Verificar que funciona

### Prueba 1: Captura de video
1. Ve a `/evaluation` en el navegador
2. Presiona **"Iniciar Grabación"**
3. Presiona **"Finalizar"** → Se descarga video

### Prueba 2: Backend (Pose Detection)
```powershell
cd body-cam
python tests/test_vision.py
```

---

## 📚 Documentación Completa

| Documento | Propósito |
|-----------|-----------|
| [README.md](README.md) | Visión general y arquitectura |
| [STRUCTURE.md](STRUCTURE.md) | Estructura detallada del proyecto |
| [CONTRIBUTING.md](CONTRIBUTING.md) | Cómo contribuir |
| [ARCHITECTURE.md](ARCHITECTURE.md) | Detalles técnicos |
| [INDEX.md](INDEX.md) | Índice de navegación |

---

## 🔧 ¿Problemas?

| Problema | Solución |
|----------|----------|
| Cámara no funciona | Verificar permisos del navegador |
| Permisos denegados | Settings → Privacy → Camera/Microphone |
| Backend no responde | Verificar que Python está corriendo en Terminal 1 |
| Videos no descargan | Verificar config de descarga del navegador |

---

**¿Necesitas más ayuda?** Lee [README.md](README.md)
