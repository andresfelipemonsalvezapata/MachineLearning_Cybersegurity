# Clasificación y Regresión sobre Amenazas de Ciberseguridad Globales (2015-2024)

Proyecto 1 del curso de Machine Learning: dos modelos de aprendizaje supervisado entrenados sobre el mismo dataset de incidentes de ciberseguridad — un clasificador multiclase para predecir el **tipo de ataque** y un modelo de regresión para predecir la **pérdida financiera** asociada a cada incidente.

## Contenido del repositorio

| Archivo | Descripción |
|---|---|
| `Proyecto_1_Cybersecurity_corregido.ipynb` | Notebook con la descripción del dataset, el análisis exploratorio (EDA), el pipeline de preprocesamiento, el entrenamiento y validación cruzada de ambos modelos, la búsqueda de hiperparámetros y las conclusiones. |
| `Global_Cybersecurity_Threats_2015-2024.csv` | Dataset usado (3000 registros, 10 columnas). |

## Dataset

**Global Cybersecurity Threats (2015-2024)**, de Kaggle: [kaggle.com/datasets/atharvasoundankar/global-cybersecurity-threats-2015-2024](https://www.kaggle.com/datasets/atharvasoundankar/global-cybersecurity-threats-2015-2024).

Cada fila representa un incidente de ciberseguridad ocurrido entre 2015 y 2024, con variables como país, año, tipo de ataque, industria afectada, pérdida financiera, usuarios afectados, origen del atacante, vulnerabilidad explotada, mecanismo de defensa usado y tiempo de resolución. El notebook incluye la descripción detallada de cada variable.

## Metodología

- Preprocesamiento (imputación, escalado de numéricas y one-hot encoding de categóricas) encapsulado en un `Pipeline` de scikit-learn, para evitar fuga de datos entre folds.
- **Clasificación** (`Attack Type`, 6 clases): regresión logística con validación cruzada estratificada de 10 folds y `GridSearchCV` sobre `C`, `penalty` y `class_weight`. Métricas: Precision, Recall y F1 macro.
- **Regresión** (`Financial Loss`): modelo Ridge con validación cruzada de 10 folds y `GridSearchCV` sobre `alpha`. Métrica: Error Cuadrático Medio (ECM).
- Evaluación final sobre un conjunto de prueba independiente (80/20), separado antes de la búsqueda de hiperparámetros.

## Resultados principales

Ambos modelos rinden cerca del nivel de un modelo trivial (F1 macro ≈ 0.17 en clasificación, equivalente al azar sobre 6 clases; ECM de regresión prácticamente igual al de predecir siempre el promedio). El EDA del notebook muestra evidencia de que el dataset fue probablemente generado de forma sintética/aleatoria (distribuciones uniformes en todas las variables categóricas, medias centradas en el punto medio del rango en las numéricas, correlaciones ≈ 0 entre ellas), lo que explica esta falta de señal predictiva. El notebook desarrolla este análisis con más detalle en su sección de conclusiones.

## Cómo ejecutarlo

1. Clona o descarga este repositorio (notebook + CSV en la misma carpeta).
2. Requiere Python 3 con `pandas`, `numpy`, `matplotlib`, `seaborn` y `scikit-learn`.
3. Ábrelo en Jupyter Notebook/Lab, o súbelo a Google Colab junto con el CSV, y ejecuta todas las celdas en orden.
