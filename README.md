# Proyecto 9 · Aprendizaje No Supervisado

Proyecto de clase inspirado en la guía de Factoría F5 para **Machine Learning no supervisado**, adaptado para trabajar con un dataset diferente de Kaggle:

- **Dataset:** Handwriting and Personality Traits Dataset.
- **Objetivo académico:** aplicar un flujo end-to-end de *unsupervised learning* (EDA, preparación, clustering/reducción de dimensionalidad y conclusiones).

> Este README está planteado como versión inicial del proyecto: simple, accionable y lista para iterar según avance el análisis.

---

## 1) Objetivo del proyecto

Analizar rasgos de personalidad asociados a características de escritura y descubrir patrones sin etiqueta objetivo mediante técnicas de aprendizaje no supervisado.

Preguntas guía iniciales:
- ¿Existen grupos naturales de perfiles en los datos?
- ¿Qué variables explican mejor las diferencias entre grupos?
- ¿Se puede reducir dimensionalidad manteniendo estructura útil para visualización e interpretación?

---

## 2) Dataset seleccionado

**Fuente:** Kaggle (Handwriting and Personality Traits Dataset).

### Resumen de trabajo con el dataset
1. Revisar la *data card* y diccionario de variables.
2. Descargar y guardar el fichero original en `data/raw/`.
3. Validar estructura:
   - tipos de dato,
   - valores nulos,
   - duplicados,
   - outliers básicos.
4. Definir versión limpia en `data/processed/` con trazabilidad.

---

## 3) Plan de trabajo previo (pre-proyecto)

Antes de modelar, se seguirá este checklist:

### A. Entendimiento del problema
- Definir alcance del entregable final (insights + visualizaciones + conclusiones).
- Formular hipótesis exploratorias (sin variable target).

### B. Preparación del entorno
- Crear entorno virtual.
- Instalar dependencias base.
- Estructurar carpetas de trabajo.

### C. Auditoría inicial de datos
- Perfilado rápido de dataset.
- Registro de calidad de datos.
- Decidir estrategia de imputación/transformación.

### D. Diseño del pipeline no supervisado
- Escalado y codificación.
- Modelos candidatos:
  - K-Means,
  - Agglomerative Clustering,
  - DBSCAN,
  - PCA / t-SNE / UMAP (según viabilidad).
- Métricas de evaluación interna:
  - Silhouette,
  - Davies-Bouldin,
  - Calinski-Harabasz.

### E. Comunicación
- Consolidar notebook final y/o scripts reproducibles.
- Documentar decisiones y limitaciones.

---

## 4) Estructura de carpetas (inicial)

```text
Proyecto-9-Aprendizaje-No-supervisado/
├── data/
│   ├── raw/            # datos originales descargados
│   ├── interim/        # datos temporales en limpieza
│   └── processed/      # datasets listos para modelado
├── notebooks/
│   ├── 01_eda.ipynb
│   ├── 02_preprocessing.ipynb
│   └── 03_unsupervised_modeling.ipynb
├── src/
│   ├── data/           # carga/validación de datos
│   ├── features/       # transformaciones y features
│   ├── models/         # clustering y reducción de dimensión
│   └── visualization/  # gráficos de apoyo
├── reports/
│   └── figures/        # imágenes exportadas
├── config/
│   └── params.yaml     # parámetros de experimentos
├── requirements.txt
└── README.md
```

---

## 5) Primeros pasos para iniciar el proyecto

```bash
# 1) crear entorno virtual
python -m venv .venv
source .venv/bin/activate  # en Windows: .venv\\Scripts\\activate

# 2) instalar dependencias
pip install -r requirements.txt

# 3) arrancar jupyter
jupyter lab
```

---

## 6) Dependencias iniciales

Incluidas en `requirements.txt`:
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn
- jupyterlab
- umap-learn
- yellowbrick

---

## 7) Próximos hitos

1. Cargar dataset y generar informe EDA inicial.
2. Definir pipeline de preprocesado reproducible.
3. Comparar varios algoritmos de clustering.
4. Evaluar calidad de clusters y estabilidad.
5. Elaborar storytelling final con conclusiones.

---

## Estado actual

✅ README inicial actualizado  
✅ Estructura base del proyecto creada  
⏳ Pendiente: ingestión del dataset y EDA inicial
