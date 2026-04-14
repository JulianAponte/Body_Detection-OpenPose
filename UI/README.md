# UI - Interfaz de Usuario (Frontend)

Interfaz de usuario del proyecto OpenPose construida con **React**, **TypeScript** y **Tailwind CSS**.

## 📁 Estructura

```
UI/
├── EvaluationPage.tsx      # Página contenedora de la Sala de Evaluación
├── EvaluationRoom.tsx      # Componente principal de grabación
├── EvaluationRoom.css      # Estilos de la Sala de Evaluación
└── README.md               # Este archivo
```

## 🎯 Componentes Principales

### EvaluationRoom.tsx
Componente React que proporciona la interfaz de grabación de presentaciones.

**Características:**
- ✅ Acceso a cámara y micrófono mediante `navigator.mediaDevices.getUserMedia`
- ✅ Streaming de video en tiempo real con vista previa
- ✅ Controles de grabación: Iniciar, Pausar, Reanudar, Finalizar
- ✅ Temporizador de duración (HH:MM:SS)
- ✅ Indicador visual de estado de grabación
- ✅ Descarga automática de video en formato WebM
- ✅ Manejo de errores y estados de carga

**Props:**
- No requiere props (standalone)

**Estados internos:**
- `recordingState`: 'idle' | 'recording' | 'paused'
- `duration`: número de segundos transcurridos
- `isLoading`: boolean para estado de inicialización
- `error`: mensaje de error si ocurre alguno

### EvaluationPage.tsx
Página wrapper que encapsula `EvaluationRoom` como punto de entrada.

Uso:
```tsx
import EvaluationPage from './UI/EvaluationPage';

// En tu router:
<Route path="/evaluation" component={EvaluationPage} />
```

## 🎨 Estilos (EvaluationRoom.css)

Estilos CSS personalizados que incluyen:
- Gradientes de fondo (tema oscuro profesional)
- Animaciones fluidas
- Indicadores visuales de grabación
- Diseño responsivo (desktop, tablet, móvil)
- Temas de colores: Cyan (#00c8db, #00e8ff) y tonos oscuros

### Paleta de Colores
```css
Primary: #00c8db, #00e8ff (Cyan)
Background: #040e1a, #0a1520 (Dark Blue)
Text: #ffffff, #a0b0c0 (White/Gray)
Error: #ff4343 (Red)
Warning: #ffc107 (Amber)
```

## 🚀 Uso

### Importar en tu aplicación React

```tsx
import EvaluationPage from './UI/EvaluationPage';

function App() {
  return (
    <Routes>
      <Route path="/evaluation" element={<EvaluationPage />} />
    </Routes>
  );
}

export default App;
```

### Usar directamente el componente

```tsx
import EvaluationRoom from './UI/EvaluationRoom';

export default function MyPage() {
  return <EvaluationRoom />;
}
```

## 📋 Requisitos

- React 17+
- TypeScript 4.5+
- Navegador moderno con soporte para:
  - `getUserMedia` API
  - `MediaRecorder` API
  - WebM codec (vp9 + opus)

## 🔧 Configuración

### Variables de MediaRecorder

En `EvaluationRoom.tsx`, puedes ajustar la configuración del codec:

```typescript
const mediaRecorder = new MediaRecorder(stream, {
  mimeType: 'video/webm;codecs=vp9,opus',
});
```

**Alternativas:**
```
'video/webm;codecs=vp8,opus'
'video/webm;codecs=vp9,vorbis'
'video/mp4'
```

### Resolución de cámara

Ajusta `getUserMedia` en el hook `useEffect`:

```typescript
const stream = await navigator.mediaDevices.getUserMedia({
  video: {
    width: { ideal: 1920 },    // Cambiar resolución
    height: { ideal: 1080 },
    facingMode: 'user',
  },
  audio: {
    echoCancellation: true,
    noiseSuppression: true,
    autoGainControl: true,
  },
});
```

## 📱 Permisos del Navegador

El componente solicita permisos para:
- 📷 **Cámara**: Para la grabación de video
- 🎤 **Micrófono**: Para captura de audio

Usuario verá un diálogo del navegador pidiendo permiso.

## 🎬 Flujo de Grabación

1. **Inicio (Listo)**: Sistema inicializa y solicita permisos
2. **Grabando**: Usuario presiona "Iniciar Grabación" → comienza captura
3. **En Pausa**: Usuario presiona "Pausar" → pausa la grabación
4. **Reanudar**: Usuario presiona "Reanudar" → continúa grabación
5. **Finalizar**: Usuario presiona "Finalizar" → genera y descarga archivo

## 🐛 Manejo de Errores

El componente muestra errores en casos como:
- Cámara/micrófono no disponibles
- Permisos denegados
- Navegador sin soporte
- Errores de hardware

## 📥 Descarga de grabaciones

Las grabaciones se descargan automáticamente en formato:
```
recording-{TIMESTAMP}.webm
Ejemplo: recording-1702345678901.webm
```

## 🔗 Integración con Backend

Para enviar la grabación al backend:

```typescript
// Modificar handleRecordingComplete
const handleRecordingComplete = (blob: Blob) => {
  const formData = new FormData();
  formData.append('video', blob, `recording-${Date.now()}.webm`);
  
  fetch('/api/upload', {
    method: 'POST',
    body: formData
  })
  .then(res => res.json())
  .then(data => console.log('Subido:', data))
  .catch(err => console.error('Error:', err));
};
```

## 🎯 Casos de Uso

- 📹 Grabación de presentaciones de "Riwers"
- 📊 Análisis de postura + performance (integración con body-cam backend)
- 🎓 Pruebas de desempeño
- 🎬 Contenido multimedia

## ⚙️ Variables de Configuración Sugeridas

Para hacer el componente más flexible, podrías:

```typescript
interface EvaluationRoomProps {
  videoCodec?: string;
  maxDuration?: number;
  onRecordingComplete?: (blob: Blob) => void;
  showIndicator?: boolean;
}
```

## 📝 Notas

- El componente limpia automáticamente recursos al desmontarse
- Las grabaciones se guardan en WebM para compatibilidad
- El temporizador se detiene automáticamente cuando se pausa
- Estilos completamente personalizables vía CSS

## 🤝 Contribución

Para mejoras futuras:
- Agregar selector de dispositivos (múltiples cámaras)
- Filtros de video en tiempo real
- Compresión de audio
- Guardado local antes de subir

---

**Versión:** 1.0.0  
**Última actualización:** April 13, 2026
