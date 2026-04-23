# Predicción de Inversión en Tienda de Videojuegos 🎮

Este proyecto contiene el script de despliegue para un modelo predictivo entrenado para estimar la inversión de los usuarios en una tienda de videojuegos basándose en su perfil demográfico y hábitos de consumo.

## 📋 Descripción
El archivo `7_despliegue_videojuegos.py` integra un modelo de Machine Learning previamente entrenado (guardado en formato `.pkl`) con una interfaz web interactiva creada en **Streamlit**.

### Características principales:
* **Interfaz de Usuario:** Permite capturar datos en tiempo real (Edad, Género, Plataforma, etc.).
* **Procesamiento de Datos:** Realiza ingeniería de características (One-Hot Encoding) y reindexación de columnas para asegurar la compatibilidad con el modelo.
* **Predicción:** Genera una estimación de inversión instantánea al procesar los datos de entrada.

## 🛠️ Tecnologías Utilizadas
* **Python 3.x**
* **Streamlit:** Para la creación de la interfaz web.
* **Pandas & Numpy:** Para la manipulación y limpieza de datos.
* **Scikit-Learn:** (Dependencia del modelo cargado).
* **Pickle:** Para la serialización y carga del modelo y escaladores.

## 🚀 Instalación y Uso

1.  **Clonar el repositorio o descargar el archivo.**
2.  **Instalar las dependencias necesarias:**
    ```bash
    pip install streamlit pandas numpy matplotlib scikit-learn
    ```
3.  **Asegurarse de tener el archivo del modelo:**
    El script busca el archivo `modelo-reg.pkl` en la misma carpeta. Este archivo debe contener una tupla con: `(modelo, min_max_scaler, variables)`.
4.  **Ejecutar la aplicación:**
    ```bash
    streamlit run 7_despliegue_videojuegos.py
    ```

## ⚙️ Funcionamiento del Código

### 1. Carga de Activos
El script carga mediante `pickle` no solo el modelo predictivo, sino también el escalador y la lista de variables originales para garantizar que los datos de entrada coincidan exactamente con la estructura del entrenamiento.

### 2. Captura de Datos
Se utilizan componentes de Streamlit como:
* `st.slider`: Para la edad.
* `st.selectbox`: Para categorías como Videojuego, Plataforma y Sexo.

### 3. Preprocesamiento en Despliegue
* **Dummies:** Se generan variables categóricas. Se utiliza `drop_first=False` para asegurar que todas las opciones posibles sean consideradas.
* **Reindexación:** Se utiliza `.reindex` con la lista `variables` para añadir columnas faltantes con valor `0` y eliminar aquellas que el modelo no espera.

### 4. Salida
El modelo realiza la predicción y muestra el resultado en pantalla, incluyendo una advertencia sobre el margen de error del modelo (2%).

## ⚠️ Notas Importantes
* **Normalización:** El código incluye una línea comentada para escalar la 'Edad'. Si utilizas modelos basados en distancia (KNN, SVM) o Redes Neuronales, debes descomentar la sección de `min_max_scaler`. Para modelos de Árboles de Decisión o Random Forest, esto no es necesario.
* **Consistencia:** El nombre de las columnas en el DataFrame `datos` debe ser idéntico al utilizado durante el entrenamiento.

---
