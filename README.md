# 🎭 Identificación de Caras Conocidas con DLIB y OpenCV

**Especialidad:** Inteligencia Artificial y Big Data  
**Asignatura:** Programación en Inteligencia Artificial (PIA)  

## 📝 Descripción del Proyecto
Este repositorio contiene la resolución de un ejercicio práctico enfocado en el **reconocimiento facial**. El objetivo principal es desarrollar una aplicación capaz de extraer características biométricas de distintos rostros a partir de imágenes individuales, almacenar estos datos en una base de datos persistente (CSV) y, posteriormente, utilizar esa base de datos para identificar a las personas presentes en una imagen grupal.

El caso de prueba se ha realizado utilizando a los personajes de la serie *How I Met Your Mother* (Cómo conocí a vuestra madre).

## ⚙️ Tecnologías Utilizadas
* **Python:** Lenguaje principal.
* **DLIB:** Detección de rostros y extracción de descriptores faciales (vectores de 128 dimensiones).
* **OpenCV (`cv2`):** Procesamiento de imágenes (conversiones de color BGR a RGB) y dibujo de marcas de identificación (Bounding boxes y etiquetas).
* **Pandas & NumPy:** Manipulación de datos, lectura/escritura del dataset en formato `.csv`, y cálculos matemáticos (distancia euclidiana).
* **Matplotlib:** Visualización de la imagen resultante.

## 🗂️ Estructura del Cuaderno (Jupyter Notebook)
El proyecto está estructurado de forma secuencial y modular:

1.  **Importar librerías y modelos:** Carga de los modelos pre-entrenados de DLIB (`shape_predictor` y `face_recognition_model`).
2.  **Obtener vector de la cara:** Función que procesa una imagen, detecta el rostro y extrae su huella digital matemática (`fingerprint`).
3.  **Guardar en csv:** Función que almacena el nombre y el vector formateado en `carasConocidas.csv`, comprobando duplicados mediante Pandas.
4.  **Caras a guardar en csv:** Procesamiento por lotes de las imágenes individuales de los personajes para poblar la base de datos inicial.
5.  **Leer dataset por el csv:** Carga y formateo de los datos persistentes para su uso en memoria.
6.  **Detección y clasificación:** Lógica principal que analiza una imagen grupal, extrae el vector de cada rostro detectado y lo compara matemáticamente (usando `np.linalg.norm` y un umbral de tolerancia) contra los rostros conocidos.

## 🚀 Cómo funciona la identificación
El algoritmo sigue estos pasos sobre la imagen final de prueba:
1.  Escanea la imagen buscando rostros (configurado para evitar falsos positivos en el entorno).
2.  Por cada rostro detectado, calcula su vector de 128 características.
3.  Compara este vector desconocido con todos los vectores de la columna `f2` del dataset cargado utilizando la **distancia euclidiana**.
4.  Si la distancia es menor o igual al umbral de tolerancia, asocia el nombre. Si no encuentra coincidencias, clasifica el rostro como `"NonSei"` (Desconocido).
5.  Dibuja un recuadro delimitador y una etiqueta optimizada (fondo opaco, texto en alto contraste) indicando la identidad del sujeto.

## 📊 Resultados
El programa procesa con éxito la imagen de prueba, identificando a los sujetos registrados en la base de datos (ej. Barney Stinson, Ted Mosby, Robin, Marshall, Alyson) marcándolos en **verde**, y clasificando correctamente en **rojo/azul** como `"NonSei"` a las personas que no constaban en el archivo de registro.

## Ver Notebook
[Face Detection DLIB](/src/facedatectiondlib/faceDetectionDLIB.ipynb)
