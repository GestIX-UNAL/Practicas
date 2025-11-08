# Proyecto de Percepción Multimodelo

## Resumen del Proyecto
* **Tema elegido y caso de uso**

## Referencias
* Pega tus 4–6 enlaces clave de Colab/Docs

## Pipeline
* Diagrama + explicación breve de cada etapa

## Parámetros Clave

### YOLO
* Modelo: yolov11n v8.3.0 ´!wget -O /content/yolov11n.pt https://github.com/ultralytics/assets/releases/download/v8.3.0/yolo11n.pt´
* Umbral conf/NMS: 0.25
* Resolución: 640x640
* Entrada: 
  * Imagen 1 [data/yolo/img1.jpeg](data/yolo/img1.jpeg)
  * Imagen 2 [data/yolo/img2.jpeg](data/yolo/img2.jpeg)
  * Imagen 3 [data/yolo/img3.jpeg](data/yolo/img3.jpeg)
  * Imagen 4 [data/yolo/img4.jpeg](data/yolo/img4.jpeg)
  * Imagen 5 [data/yolo/img5.jpeg](data/yolo/img5.jpeg)
* Salida:
  * BBox Imagen 1 [results/yolo/img1.jpg](results/yolo/img1.jpg)
  * BBox Imagen 2 [results/yolo/img2.jpg](results/yolo/img2.jpg)
  * BBox Imagen 3 [results/yolo/img3.jpg](results/yolo/img3.jpg)
  * BBox Imagen 4 [results/yolo/img4.jpg](results/yolo/img4.jpg)
  * BBox Imagen 5 [results/yolo/img5.jpg](results/yolo/img5.jpg)
  * Coordenadas BBox de imágenes [results/yolo/yolo_results.csv](results/yolo/yolo_results.csv)

### MediaPipe
* Task
* FPS
* Landmarks usados

### MiDaS
* Versión del modelo
* Normalización del mapa

### SAM
* Tipo de prompt (punto/caja)
* Versión del checkpoint

## Setup

### Requerimientos
- Python 3.9 - 3.11
- pyenv
- pyenv-virtualenv

### Entorno virtual de python
```bash
pyenv install 3.11
pyenv virtualenv 3.11 venv
pyenv activate venv
pip install -r requirements.txt
```


## Métricas
* Latencia por etapa
* IoU de máscaras
* % de aciertos "cerca/medio/lejos"

## Limitaciones
* Ruido en profundidad
* Oclusiones
* Sensibilidad a luz

## Futuro
* SAM-2 para video
* Cuantización
* Seguimiento multi-objeto
