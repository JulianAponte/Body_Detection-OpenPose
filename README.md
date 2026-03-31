# Jupiter Pose Module

MVP en Python para detectar postura corporal usando `OpenPose` si esta disponible y `MediaPipe` como fallback automatico.

## Archivos

- `main.py`: punto de entrada.
- `pose_detector.py`: carga del backend y extraccion de hombros.
- `utils.py`: dibujo debug y exportacion JSON.
- `config.py`: constantes por defecto.
- `output.json`: salida generada por la ejecucion.

## Requisitos

Se recomienda Python 3.12.

## Instalacion

```powershell
uv venv --python 3.12 .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

## Ejecucion con webcam

```powershell
python main.py --source 0
```

## Ejecucion con video

```powershell
python main.py --source .\video.mp4
```

## Parametros utiles

- `--backend auto|openpose|mediapipe`
- `--max-frames 300`
- `--shoulder-threshold 0.16`
- `--no-display`

## Salida JSON

Cada frame se guarda con este formato:

```json
{
  "frame": 1,
  "people": [
    {
      "id": 0,
      "shoulder_left": [100, 200],
      "shoulder_right": [180, 200],
      "posture": "open",
      "movement_px": 12.4
    }
  ]
}
```

## Nota sobre OpenPose

Si tienes `pyopenpose` disponible, el modulo intentara usarlo cuando el backend sea `auto` u `openpose`. Si no esta instalado, se utilizara `MediaPipe` para que puedas validar el MVP sin compilar OpenPose de inmediato.

## Nota sobre multipersona

Con `OpenPose`, el diseno ya soporta multiples personas. Con `MediaPipe Pose`, el MVP procesa una persona por frame, suficiente para validar deteccion corporal, hombros, postura y movimiento.
