# Reporte de modelado no supervisado

## Dataset final de entrada
- Matriz de clustering: **2000 filas x 20 features** (datos escalados y codificados).
- Matriz de perfiles Big Five para interpretación: **2000 filas x 5 variables**.

## Evaluación de K-Means (baseline)

 k  silhouette  davies_bouldin  calinski_harabasz    inertia
 2      0.0441          4.5848            93.9708 33745.6321
 3      0.0382          4.0766            79.7527 32719.3918
 4      0.0397          3.7614            73.1969 31830.8839
 5      0.0387          3.5380            66.1370 31196.0056
 6      0.0389          3.3940            61.3451 30622.3163
 7      0.0390          3.2737            57.3004 30134.4342
 8      0.0400          3.1583            54.4045 29661.9810

Se selecciona **k=2** por presentar el mejor valor de silhouette (0.0441) dentro del rango evaluado.

## Comparación de algoritmos

     algorithm  n_clusters  silhouette  davies_bouldin  calinski_harabasz
        KMeans           2      0.0441          4.5848            93.9708
 Agglomerative           2      0.0190          6.3780            40.3350
DBSCAN eps=1.5           0         NaN             NaN                NaN
DBSCAN eps=2.0           0         NaN             NaN                NaN
DBSCAN eps=2.5           0         NaN             NaN                NaN
DBSCAN eps=3.0           0         NaN             NaN                NaN

DBSCAN no encontró una estructura densa útil con los eps probados (0 clusters válidos en todos los casos).

## Composición del modelo seleccionado
- Tamaño de clusters:
  - Cluster 0: 989 observaciones
  - Cluster 1: 1011 observaciones

- Promedio de rasgos Big Five por cluster:

         Openness  Conscientiousness  Extraversion  Agreeableness  Neuroticism
cluster                                                                       
0           0.510              0.502         0.477          0.493        0.485
1           0.497              0.503         0.509          0.489        0.522

## Estabilidad básica
- ARI medio entre ejecuciones con distintas semillas: **0.3770**
- ARI mínimo: **-0.0005**
- ARI máximo: **0.9761**

Estos resultados indican estabilidad moderada-baja, coherente con la baja separación interna detectada por silhouette.

## Interpretación y limitaciones
- La estructura de clusters parece **débil**: no hay separaciones claras en alta dimensión.
- El modelo es útil para segmentación **exploratoria** y generación de hipótesis, no para tipologías rígidas de personalidad.
- Sería recomendable ampliar el análisis con reducción de dimensionalidad no lineal, validación por submuestras y tuning más fino de densidad/distancia.
