# challenge_TelecomX2_palp
Desafío Alura Latam 

---

## 📌 **1. Introducción**

Este proyecto tiene como objetivo analizar los factores que influyen en la **cancelación de clientes (churn)** y construir modelos predictivos capaces de identificar a los clientes con mayor probabilidad de abandonar el servicio.

El análisis incluye:

- Exploración de variables relevantes  
- Visualización de patrones  
- Construcción de modelos predictivos  
- Evaluación de métricas  
- Interpretación de la importancia de variables  

---

## 📌 **2. Preparación de los datos**

### ✔️ División del dataset  
El conjunto de datos se dividió en:

- **70% entrenamiento**
- **30% prueba**

Usando `train_test_split` con `stratify=y` para mantener la proporción de clases.

### ✔️ Imputación de valores faltantes  
Se detectaron valores faltantes en variables numéricas (como `cuenta.cargos_totales`).  
Para evitar errores en modelos como Regresión Logística o SVM, se aplicó:

- **SimpleImputer(strategy='median')**

### ✔️ Normalización  
Se aplicó **StandardScaler** solo en los modelos que lo requieren:

- Regresión Logística  
- KNN  
- SVM  

Modelos basados en árboles (Random Forest) **no requieren normalización**.

---

## 📌 **3. Visualización de relaciones clave**

Se exploraron relaciones entre variables y la cancelación mediante:

### 🔹 Boxplots
- **Antigüedad × Cancelación**  
- **Gasto total × Cancelación**

### 🔹 Scatter plots
- **Antigüedad vs Gasto total (coloreado por cancelación)**  
- **Cargos mensuales vs Gasto total**

### ✔️ Principales hallazgos visuales:
- Los clientes **nuevos** cancelan más.  
- Los clientes con **bajo gasto total** tienen mayor churn.  
- Los **planes más caros** están asociados a mayor cancelación.  
- Los **contratos largos** reducen fuertemente la cancelación.

---

## 📌 **4. Modelos construidos**

Se entrenaron cuatro modelos:

### 🔹 **1. Regresión Logística (con normalización)**  
Modelo lineal, interpretable y sensible a la escala.

### 🔹 **2. KNN (con normalización)**  
Modelo basado en distancia; requiere normalización.

### 🔹 **3. Random Forest (sin normalización)**  
Modelo basado en árboles, robusto y no sensible a la escala.

### 🔹 **4. SVM lineal (con normalización)**  
Modelo lineal que maximiza la separación entre clases.

---

## 📌 **5. Evaluación de modelos**

Se utilizaron las siguientes métricas:

- **Accuracy**
- **Precisión**
- **Recall**
- **F1-score**
- **Matriz de confusión**

### ✔️ Resultados principales

#### **Regresión Logística**
- Accuracy: **0.7949**
- Recall: **0.5321**
- F1-score: **0.5793**

#### **Random Forest**
- Accuracy: **0.7700**
- Recall: **0.4465**
- F1-score: **0.5076**

### ✔️ Conclusión de desempeño
- **La Regresión Logística fue el mejor modelo**, especialmente en recall y F1-score.  
- Random Forest mostró **overfitting leve**.  
- Regresión Logística mostró **underfitting leve**, típico de modelos lineales.  

---

## 📌 **6. Importancia de variables**

Se analizó la relevancia de las variables según cada modelo:

---

### 🔹 **Regresión Logística (coeficientes)**  
Variables que **aumentan** la cancelación:

- `cuenta.cargos_totales`  
- `internet.servicio_internet_Fiber optic`  
- `cuenta.metodo_pago_Electronic check`  
- `internet.tv_streaming_Yes`  

Variables que **reducen** la cancelación:

- `cliente.antiguedad` (la más importante)  
- `cuenta.contrato_Two year`  
- `cuenta.contrato_One year`  
- `internet.soporte_tecnico_Yes`  
- `internet.seguridad_en_linea_Yes`  

---

### 🔹 **KNN (Permutation Importance)**  
Variables más influyentes:

- `cliente.antiguedad`  
- `internet.servicio_internet_Fiber optic`  
- `cuenta.contrato_One year`  
- `cuenta.cargos_totales`  

---

### 🔹 **Random Forest (feature_importances_)**  
Variables más importantes:

- `cuenta.cargos_totales`  
- `cliente.antiguedad`  
- `cuenta_diaria`  
- `cuenta.cargos_mensuales`  
- `cuenta.metodo_pago_Electronic check`  
- `internet.servicio_internet_Fiber optic`  

---

### 🔹 **SVM (coeficientes)**  
Variables que aumentan la cancelación:

- `internet.servicio_internet_Fiber optic`  
- `cuenta.metodo_pago_Electronic check`  
- `internet.tv_streaming_Yes`  

Variables que reducen la cancelación:

- `cliente.antiguedad`  
- `cuenta.contrato_Two year`  
- `cuenta.contrato_One year`  
- `internet.soporte_tecnico_Yes`  

---

## 📌 **7. Conclusiones generales del proyecto**

### 🔥 Factores que AUMENTAN la probabilidad de cancelación:
- Ser cliente nuevo  
- Tener fibra óptica  
- Usar Electronic Check  
- Tener cargos mensuales altos  
- Tener bajo gasto total acumulado  
- Servicios adicionales como TV streaming  

### 🔵 Factores que REDUCEN la probabilidad de cancelación:
- Antigüedad del cliente (variable más importante en todos los modelos)  
- Contratos de 1 y 2 años  
- Mayor uso del servicio (cuenta_diaria)  
- Servicios de soporte técnico y seguridad  
- Tener dependientes o pareja  

### 🧠 Mejor modelo:
- **Regresión Logística**, por su equilibrio entre precisión, recall y F1-score.

---


