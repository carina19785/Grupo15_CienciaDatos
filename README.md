# 🫀 Proyecto Integrador: Predicción de Enfermedades Cardiovasculares

<div align="center">

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-orange?logo=scikit-learn)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-yellow?logo=jupyter)
![Estado](https://img.shields.io/badge/Estado-2da%20Entrega-green)

</div>

---

## 📋 Descripción General

Este proyecto aplica técnicas de **Ciencia de Datos y Machine Learning** sobre un dataset clínico de enfermedades cardiovasculares. El objetivo es construir y evaluar modelos predictivos capaces de identificar, a partir de variables clínicas y de estilo de vida, si un paciente presenta o no una patología cardíaca.

**Institución:** UPATecO — Tecnicatura Universitaria en Ciencia de Datos e IA  
**Materia:** Ciencia de Datos y Optimización de Sistemas  
**Docente:** Prof. Amalia Guaymas Canavire  

**Integrantes del Grupo 15:**
- Quispe Alejandra Carina
- Arzola Franco Javier
- Peloc Natalia Zulema
- Lemos Federico

---

## 🎯 Objetivo del Proyecto

Desarrollar un **modelo de clasificación binaria supervisada** que prediga la presencia (`1`) o ausencia (`0`) de enfermedad cardiovascular, usando variables clínicas como edad, presión arterial, colesterol, IMC y hábitos de vida.

El modelo actúa como **herramienta de asistencia y alerta temprana**, no como diagnóstico médico. La decisión final siempre recae en el profesional de salud.

---

## 📁 Estructura del Proyecto

```
grupo15/
├── grupo15_2daEntrega.ipynb   # Notebook principal (2da entrega)
├── README.md                  # Este archivo
└── Data/
    └── health_data.csv        # Dataset de Kaggle (no incluido en el repo)
```

> **Nota:** El dataset `health_data.csv` debe descargarse de Kaggle y colocarse en la carpeta `Data/` antes de ejecutar el notebook.

---

## 📊 Dataset

| Característica | Detalle |
|---|---|
| **Fuente** | Kaggle — Cardiovascular Disease Dataset |
| **Registros** | 70.000 pacientes |
| **Variables** | 12 (tras limpieza de columnas no informativas) |
| **Variable objetivo** | `cardio` (0 = sano, 1 = cardíaco) |
| **Balance de clases** | ~50% / 50% (balanceado) |

### Variables del Dataset

| Variable | Tipo | Descripción |
|---|---|---|
| `edad` | Continua | Edad en años (convertida desde días) |
| `genero` | Binaria | 0 = Masculino, 1 = Femenino |
| `altura` | Continua | Estatura en cm |
| `peso` | Continua | Peso en kg |
| `presion_sistolica` | Continua | Presión arterial sistólica (mmHg) |
| `presion_diastolica` | Continua | Presión arterial diastólica (mmHg) |
| `colesterol` | Categórica | 1=Normal, 2=Elevado, 3=Muy alto |
| `glucosa` | Categórica | 1=Normal, 2=Elevada, 3=Muy alta |
| `fuma` | Binaria | 0=No, 1=Sí |
| `alcohol` | Binaria | 0=No, 1=Sí |
| `activo` | Binaria | 0=Sedentario, 1=Activo |
| `cardio` | Binaria (**objetivo**) | 0=Sano, 1=Cardíaco |

---

## 🔬 Metodología

### 1. Análisis Exploratorio de Datos (EDA)
- Análisis univariado de variables continuas y categóricas
- Análisis bivariado contra la variable objetivo `cardio`
- Detección y tratamiento de outliers (presión arterial, altura, peso)
- Ingeniería de features: cálculo de **IMC** (Índice de Masa Corporal)

### 2. Limpieza de Datos
Filtros aplicados para eliminar valores fisiológicamente imposibles:
- Presión sistólica: 100–250 mmHg
- Presión diastólica: 60–150 mmHg
- Altura: 130–220 cm
- Peso: 30–200 kg

Registros eliminados: ~2.556 (≈3.7% del total)

### 3. Modelado Supervisado — Clasificación Binaria
- **Modelo base:** Regresión Logística
- **División:** 80% entrenamiento / 20% prueba (estratificada)
- **Optimización:** GridSearchCV y RandomizedSearchCV
- **Validación cruzada:** k-fold (k=3 y k=5)

### 4. Aprendizaje No Supervisado
- **Reducción de dimensionalidad:** PCA (2 componentes, ~79% varianza explicada)
- **Clustering:** K-Means con 3 clusters (perfiles de riesgo)

---

## 📈 Resultados

### Comparativa de Modelos

| Métrica | Regresión Logística | GridSearchCV | RandomizedSearchCV |
|---|---|---|---|
| **Accuracy** | 0.7231 | 0.7233 | 0.7234 |
| **Precision** | 0.7436 | 0.7439 | 0.7442 |
| **Recall** | 0.6721 | 0.6721 | 0.6718 |
| **F1-Score** | 0.7060 | 0.7062 | 0.7062 |

### Hallazgos Principales
- La **presión arterial sistólica** y el **colesterol** son los predictores con mayor diferencia descriptiva entre clases
- La **edad** muestra una tendencia creciente de riesgo cardiovascular por décadas
- La optimización de hiperparámetros no produjo mejoras significativas, lo que sugiere que el modelo lineal tiene limitaciones para capturar relaciones no lineales en los datos
- El **PCA** retuvo el 79% de la varianza en 2 componentes, y **K-Means** identificó 3 perfiles de paciente con fronteras suaves (típico en datos clínicos)

---

## ⚙️ Cómo Ejecutar el Notebook

Este proyecto fue desarrollado en **Google Colab**. Para ejecutarlo:

1. Subir el notebook `grupo15_2daEntrega.ipynb` a Google Colab
2. Montar Google Drive:
   ```python
   from google.colab import drive
   drive.mount('/content/drive')
   ```
3. Colocar el archivo `health_data.csv` en la ruta:
   ```
   /content/drive/MyDrive/Tp1_QuispeAlejandra/Data/health_data.csv
   ```
4. Ejecutar las celdas en orden

### Dependencias
```
pandas
numpy
matplotlib
seaborn
scikit-learn
scipy
ydata-profiling
```

---

## 📚 Fuentes

- Dataset: [Cardiovascular Disease Dataset — Kaggle](https://www.kaggle.com/datasets/sulianova/cardiovascular-disease-dataset)
- Organización Mundial de la Salud (OMS) — Enfermedades cardiovasculares
- scikit-learn Documentation: https://scikit-learn.org

---

## 📝 Entregas

| Entrega | Contenido | Estado |
|---|---|---|
| Entrega 1 | EDA inicial, análisis descriptivo, detección de outliers | ✅ Completada |
| **Entrega 2** | **Modelado supervisado, optimización, PCA, K-Means** | ✅ Completada |
