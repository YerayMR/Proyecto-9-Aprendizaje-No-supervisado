# Proyecto 9 · Aprendizaje No Supervisado

Análisis no supervisado sobre el dataset **Handwriting and Personality Traits** para detectar estructura latente en los datos de escritura y relacionarla con rasgos de personalidad (Big Five).

---

## 1) Objetivo académico

Construir un flujo reproducible de aprendizaje no supervisado que permita:
- preparar datos para modelado,
- entrenar y comparar algoritmos de clustering,
- evaluar calidad de clusters con métricas internas,
- interpretar clusters en términos de perfil psicológico.

> Alcance: exploración y análisis; no incluye despliegue ni optimización avanzada.

---

## 2) Dataset

- **Fuente:** Kaggle · Handwriting and Personality Traits Dataset.
- **Registros usados:** 2.000 observaciones.
- **Variables para clustering:** 20 features procesadas (numéricas escaladas + género codificado).
- **Variables de interpretación:** 5 rasgos Big Five (`Openness`, `Conscientiousness`, `Extraversion`, `Agreeableness`, `Neuroticism`).

Archivos clave:
- `data/raw/handwriting_personality_large_dataset.csv`
- `data/processed/handwriting_personality_clustering_input.csv`
- `data/processed/handwriting_personality_profile_targets.csv`

---

## 3) Proceso seguido en el proyecto

### Fase 1 · EDA (`notebooks/01_eda.ipynb`)
- Revisión de estructura, tipos, calidad de datos y distribución general.
- Identificación de variables útiles para el flujo no supervisado.

### Fase 2 · Preprocesado (`notebooks/02_preprocessing.ipynb`)
- Limpieza y transformación reproducible.
- Escalado de variables numéricas.
- Codificación de variables categóricas.
- Export de datasets finales en `data/processed/`.

### Fase 3 · Modelado no supervisado (`notebooks/03_unsupervised_modeling.ipynb`)
- Baseline con **K-Means**.
- Evaluación de `k = 2..8`.
- Comparativa con **Agglomerative Clustering** y **DBSCAN**.
- Métricas internas: **Silhouette**, **Davies-Bouldin**, **Calinski-Harabasz**.
- Análisis de composición de clusters y perfil Big Five.
- Evaluación básica de estabilidad (ARI entre semillas).
- Síntesis en `reports/unsupervised_modeling_report.md`.

---

## 4) Resultados principales

### 4.1 Selección de modelo
- Mejor configuración en el rango evaluado: **K-Means con k=2**.
- Silhouette (mejor caso): **0.0441**.

### 4.2 Comparativa de algoritmos
- **K-Means (k=2):** mejor desempeño relativo dentro de lo probado.
- **Agglomerative (k=2):** peor separación interna que K-Means.
- **DBSCAN:** no detectó clusters válidos en los `eps` evaluados.

### 4.3 Composición de clusters (K-Means, k=2)
- Cluster 0: **989** observaciones.
- Cluster 1: **1011** observaciones.
- Diferencias en promedios Big Five **moderadas**, sin separación fuerte.

### 4.4 Estabilidad
- ARI medio entre ejecuciones con distintas semillas: **0.3770**.
- ARI mínimo: **-0.0005**.
- ARI máximo: **0.9761**.

Interpretación: la estructura detectada es **débil** y sensible a inicialización; los clusters son útiles para segmentación exploratoria, no para tipologías rígidas.

---

## 5) Conclusión final del proyecto

El objetivo del proyecto no supervisado se cumple: se construyó un pipeline reproducible, se compararon algoritmos y se obtuvo una lectura clara de la estructura de los datos.

Sin embargo, los resultados indican que la separabilidad natural de clusters es baja. Por ello, una extensión metodológicamente sólida para una siguiente fase sería incorporar un enfoque **supervisado de regresión multisalida** para predecir los rasgos Big Five continuos.

### ¿Por qué regresión (y no clasificación) en la continuación?
- Los rasgos Big Five están representados como **variables continuas**.
- Clasificar exigiría discretizar artificialmente esos valores, con pérdida de información.
- La evidencia del clustering (silhouette bajo y estabilidad variable) sugiere que una formulación predictiva continua puede ser más informativa para evaluación de desempeño.

---

## 6) Estructura del repositorio

```text
Proyecto-9-Aprendizaje-No-supervisado/
├── config/
│   └── params.yaml
├── data/
│   ├── raw/
│   └── processed/
├── notebooks/
│   ├── 01_eda.ipynb
│   ├── 02_preprocessing.ipynb
│   └── 03_unsupervised_modeling.ipynb
├── reports/
│   └── unsupervised_modeling_report.md
├── src/
└── requirements.txt
```

---

## 7) Cómo reproducir

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter lab
```

Ejecutar notebooks en orden: `01_eda` → `02_preprocessing` → `03_unsupervised_modeling`.
