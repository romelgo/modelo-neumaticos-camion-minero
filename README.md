# 📊 Análisis de Machine Learning e IoT para la Gestión Predictiva de Neumáticos en Flotas CAT 797F

Este directorio (`/modelos`) contiene los notebooks experimentales y de entrenamiento para los cuatro modelos principales del proyecto, así como sus artefactos asociados (pesos entrenados, gráficas de evaluación, métricas).

## 📁 Estructura del Directorio

- **`artifacts/`**: Carpeta que contiene los resultados del entrenamiento, divididos por modelo (`modelo_A`, `modelo_B`, `modelo_C`, `modelo_D`). Aquí se guardan:
  - Pesos entrenados (`.keras`, `.pkl`).
  - Gráficas de rendimiento (curvas de entrenamiento, matrices de confusión).
  - Scalers y transformadores utilizados para el preprocesamiento.
- **`modelo_A_thermal_lstm.ipynb`**: Entrenamiento del Modelo A.
- **`modelo_B_rul_xgboost.ipynb`**: Entrenamiento del Modelo B.
- **`modelo_C_route_classifier.ipynb`**: Entrenamiento del Modelo C.
- **`modelo_D_swap_engine.ipynb`**: Implementación del Modelo D.

---

## 🧠 Detalle de los Modelos

### 🔥 Modelo A — Predicción de Falla Térmica Inminente
- **Archivo:** `modelo_A_thermal_lstm.ipynb`
- **Arquitectura:** Red Neuronal Recurrente LSTM (SSA-LSTM).
- **Objetivo:** Clasificación binaria para predecir si un neumático superará la temperatura crítica de 85°C en los próximos 30 a 60 minutos.
- **Contexto:** Entrenado con datos de una flota de 60 camiones CAT 797F (Minera Las Bambas).

### 📉 Modelo B — Vida Útil Remanente (RUL)
- **Archivo:** `modelo_B_rul_xgboost.ipynb`
- **Arquitectura:** XGBoost combinado con Análisis de Supervivencia (Kaplan-Meier).
- **Objetivo:** Predecir el día exacto en que la llanta llegará a su "cocada" o profundidad de desgaste mínima permitida (5 mm).
- **Características Clave:** Considera profundidad actual, tasa de desgaste, asignación de tajo, posición y payload acumulado.

### 🗺️ Modelo C — Clasificación de Agresividad de Ruta
- **Archivo:** `modelo_C_route_classifier.ipynb`
- **Arquitectura:** Clustering Geoespacial (K-Means) + Clasificador (Random Forest).
- **Objetivo:** Segmentar y clasificar las vías y rutas mineras según su nivel de agresividad y severidad (Verde / Amarilla / Roja).
- **Características Clave:** Usa datos de latitud, longitud, vibración, presión y velocidad.

### 🔄 Modelo D — Motor de Recomendación de Swap
- **Archivo:** `modelo_D_swap_engine.ipynb`
- **Arquitectura:** Lógica Difusa (Fuzzy Logic con `scikit-fuzzy`) usando Reglas Mamdani.
- **Objetivo:** Emitir recomendaciones de intercambio (swap) de camiones entre zonas (ej. Norte ↔ Sur) para balancear el estrés térmico y operativo en la flota.
- **Variables Lingüísticas:** Estrés térmico, nivel TKPH y RUL restante, que definen la urgencia del swap.

---

## 🚀 Uso General
Cada notebook está diseñado para ser ejecutado secuencialmente. Los modelos entrenados y los gráficos generados se guardan automáticamente en la subcarpeta `artifacts/` bajo el directorio correspondiente a su nombre para ser luego consumidos por la aplicación principal u otros microservicios.
