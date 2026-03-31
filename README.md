# Jupiter Pose Module

Este es un MVP en Python para detectar postura corporal usando `OpenPose` si está disponible y `MediaPipe` como respaldo automático.

## ¿Qué hace este proyecto?

Este proyecto sirve para detectar y seguir la postura corporal en tiempo real usando una cámara o un video.

Lo que hace, en pocas palabras, es:

- detectar los puntos clave de los hombros,
- decidir si la postura de una persona está "abierta" o "cerrada",
- calcular cuánto movimiento hubo entre un frame y otro.

## ¿Por qué usamos OpenPose como opción principal?

`OpenPose` se usa como backend principal porque funciona muy bien cuando hay varias personas en cámara.

Su ventaja es que analiza primero todas las partes del cuerpo que aparecen en la imagen y después las agrupa por persona. Eso hace que el costo de procesamiento se mantenga bastante estable aunque haya más de un cuerpo en escena.

En cambio, herramientas como `MediaPipe` normalmente detectan a cada persona por separado, así que el esfuerzo de procesamiento crece con cada cuerpo adicional. Por eso, para escenarios con varias personas, `OpenPose` suele ser una mejor opción.

## Archivos principales

- `main.py`: punto de entrada del programa.
- `pose_detector.py`: carga el backend y extrae los puntos de los hombros.
- `utils.py`: dibuja información de depuración y exporta el JSON.
- `config.py`: contiene las constantes por defecto.
- `output.json`: archivo de salida generado al ejecutar el proyecto.

## Requisitos

Se recomienda usar Python 3.12.

## Instalación

```powershell
uv venv --python 3.12 .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

## Ejecutar con webcam

```powershell
python main.py --source 0
```

## Ejecutar con video

```powershell
python main.py --source .\video.mp4
```

## Parámetros útiles

- `--backend auto|openpose|mediapipe`
- `--max-frames 300`
- `--shoulder-threshold 0.16`
- `--no-display`

## Formato de salida JSON

Cada frame se guarda con una estructura como esta:

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

Si tienes `pyopenpose` instalado, el módulo va a intentar usarlo cuando el backend esté en `auto` o en `openpose`.

Si no lo tienes instalado, se usará `MediaPipe` automáticamente. Así puedes probar y validar el MVP sin tener que compilar OpenPose desde el principio.

## Nota sobre multipersona

Con `OpenPose`, el diseño ya está pensado para soportar varias personas de forma más eficiente.

Con `MediaPipe Pose`, este MVP procesa una sola persona por frame. Eso alcanza para validar detección corporal, hombros, postura y movimiento de forma básica, pero no sería la mejor opción para un caso real con varias personas al mismo tiempo.
