# Proyecto de Percepción Multimodelo

## Resumen del Proyecto
* **Tema elegido y caso de uso**

## Referencias
* Pega tus 4–6 enlaces clave de Colab/Docs

## Pipeline
* Diagrama + explicación breve de cada etapa

## Parámetros Clave

### YOLO
* Modelo
* Umbral conf/NMS
* Resolución

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

### Entorno virtual de python
```bash
python -m venv venv
source venv/bin/activate  # En Windows usa `venv\Scripts\activate`
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
