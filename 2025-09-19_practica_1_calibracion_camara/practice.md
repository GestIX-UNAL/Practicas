# 📘 Taller de Calibración de Cámaras con Tablero de Ajedrez

## 1. Introducción
La calibración de cámaras es un proceso fundamental en **visión por computador** para estimar los parámetros intrínsecos (focal, centro óptico, distorsión) y extrínsecos (posición y orientación en el espacio) de una cámara.  
Un método clásico y robusto consiste en usar un **patrón de tablero de ajedrez (checkerboard)** impreso y fotografiado desde múltiples ángulos.  

---

## 2. Objetivos del Taller
- Comprender qué es la calibración y por qué es necesaria.  
- Aprender a capturar imágenes de un tablero de ajedrez para calibración.  
- Implementar un pipeline de calibración con **OpenCV**.  
- Analizar y validar los parámetros obtenidos.  

---

## 3. Conceptos Básicos
- **Parámetros intrínsecos**:  
  - Longitud focal ($f_x, f_y$).  
  - Centro óptico ($c_x, c_y$).  
  - Distorsión radial y tangencial.  

- **Parámetros extrínsecos**:  
  - Rotación y traslación de la cámara respecto al tablero.  

- **Proyección pinhole**:  
  $$
  s \begin{bmatrix} u \\ v \\ 1 \end{bmatrix} =
  K [R|t] \begin{bmatrix} X \\ Y \\ Z \\ 1 \end{bmatrix}
  $$

---

## 4. Materiales Necesarios
- Cámara (webcam, celular, cámara industrial).  
- Tablero de ajedrez impreso (ej: 9x6 esquinas internas).  
- Software:  
  - [OpenCV](https://docs.opencv.org/master/dc/dbb/tutorial_py_calibration.html)  
  - [NumPy](https://numpy.org/)  
  - [Matplotlib](https://matplotlib.org/)  

---

## 5. Procedimiento Paso a Paso

### 5.1. Captura de Imágenes
1. Imprime un tablero de ajedrez (ej: 9x6).  
2. Captura al menos **15–20 imágenes** desde distintos ángulos y posiciones.  
3. Evita reflejos y asegúrate de que el patrón esté bien enfocado.  

### 5.2. Detección de Esquinas
- OpenCV ofrece `cv2.findChessboardCorners()` para localizar las esquinas internas del tablero.  

### 5.3. Calibración
- Usar `cv2.calibrateCamera()` con las esquinas detectadas.  

### 5.4. Validación
- Calcular error de reproyección.  
- Aplicar `cv2.undistort()` para comprobar la corrección de distorsión.  

---

## 6. Código Ejemplo (Python + OpenCV)

```python
import cv2
import numpy as np
import glob

# Definir dimensiones del tablero (esquinas internas)
chessboard_size = (9, 6)

# Criterio de terminación de subpixeles
criteria = (cv2.TERM_CRITERIA_EPS + cv2.TERM_CRITERIA_MAX_ITER, 30, 0.001)

# Preparar puntos 3D (0,0,0 ... 8,5,0)
objp = np.zeros((np.prod(chessboard_size), 3), np.float32)
objp[:, :2] = np.mgrid[0:chessboard_size[0], 0:chessboard_size[1]].T.reshape(-1, 2)

objpoints = [] # Puntos 3D
imgpoints = [] # Puntos 2D

# Cargar imágenes del tablero
images = glob.glob('chessboard/*.jpg')

for fname in images:
    img = cv2.imread(fname)
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

    ret, corners = cv2.findChessboardCorners(gray, chessboard_size, None)
    if ret:
        objpoints.append(objp)
        corners2 = cv2.cornerSubPix(gray, corners, (11, 11), (-1, -1), criteria)
        imgpoints.append(corners2)

# Calibración
ret, mtx, dist, rvecs, tvecs = cv2.calibrateCamera(objpoints, imgpoints, gray.shape[::-1], None, None)

print("Matriz de la cámara:\n", mtx)
print("Coeficientes de distorsión:\n", dist)

# Corrección de una imagen de prueba
img = cv2.imread(images[0])
h, w = img.shape[:2]
newcameramtx, roi = cv2.getOptimalNewCameraMatrix(mtx, dist, (w,h), 1, (w,h))

dst = cv2.undistort(img, mtx, dist, None, newcameramtx)
cv2.imwrite('calibrated_result.jpg', dst)
```

---

## 7. Documentación y Recursos
- OpenCV Camera Calibration Tutorial: [https://docs.opencv.org/4.x/dc/dbb/tutorial_py_calibration.html](https://docs.opencv.org/4.x/dc/dbb/tutorial_py_calibration.html)  
- Zhang, Z. (2000). *A flexible new technique for camera calibration*. IEEE Transactions on Pattern Analysis and Machine Intelligence.  
- Wikipedia: [Camera Reprojection Error](https://en.wikipedia.org/wiki/Reprojection_error)  
- Librerías útiles:  
  - `opencv-python`  
  - `numpy`  
  - `matplotlib`  

---

## 8. Actividad Final
1. Calibra tu cámara con las imágenes que tomes.  
2. Calcula el error medio de reproyección.  
3. Aplica la corrección a un video en tiempo real con `cv2.VideoCapture`.  
4. Discute en clase las diferencias entre la imagen original y la corregida.  
