# Predicción temprana de caballos de salto de élite

Proyecto final de analítica predictiva, hecho con la metodología CRISP-DM.

Equipo_4_Caballos

Integrantes:

Luca Amodio Díaz

Carolina Bermejo Rodríguez

Anna Sofia Fernández Mata

Armando González Peña

Emilio Guevara Elizondo


## La pregunta

Con el historial de competencias de un caballo hasta los 8 años, ¿podemos predecir si su carrera va a llegar al nivel élite del salto ecuestre, es decir, un recorrido limpio a 160 cm?

Es un problema de clasificación binaria. El target es `champion` (1 = llegó a 160 cm limpio, 0 = no llegó).

## Datos

- Base: `df_ml_fra_swe_bel_once_fei.csv`, 782,175 recorridos de 4,248 caballos (competencias FEI y nacionales de Francia, Bélgica y Suecia).
- Fuente: Zenodo, https://zenodo.org/records/20526601
- Artículo: Zanchi M, Bordin C, Ablondi M, Asti V, Summer A, Valle E, Ozella L. (2026). *Improving sport horse selection using machine learning: Early prediction of elite-level show jumping performance*. PLoS One, 21(9), e0357799. https://doi.org/10.1371/journal.pone.0357799
- El CSV **no está en este repositorio**. Descárgalo de Zenodo y ponlo en la carpeta `data/`.

## Contenido

| Archivo | Qué es |
|---|---|
| `Proyecto_Caballos_Elite.ipynb` | Notebook completo con código, tablas y gráficas, en orden |
| `requirements.txt` | Librerías necesarias |

## Cómo está organizado el notebook

1. Entendimiento del negocio
2. Entendimiento de los datos
3. Procesamiento (outliers, nulos, codificación, escalamiento, selección de variables)
4. Modelos (regresión logística, KNN, árbol, Random Forest y K-means)
5. Evaluación con validación cruzada de 10 pliegues
6. Conclusiones

## Resultados principales

Modelo final: **Random Forest**, validación cruzada de 10 pliegues.

| Métrica | Meta | Resultado |
|---|---|---|
| AUC-ROC | ≥ 0.80 | 0.804 ± 0.034 |
| Recall de campeones | ≥ 0.65 | 0.659 ± 0.050 |

Supera a la "regla del entrenador" (AUC 0.745). La regresión logística quedó muy cerca (AUC 0.794) y sirve mejor para explicar cuánto pesa cada variable.

## Decisiones importantes

- Solo caballos de Grado II (ningún Grado I llegó a campeón).
- Solo caballos nacidos hasta 2007: de 2008 en adelante la base solo tiene campeones por cómo se armó.
- Solo recorridos hasta los 8 años.
- `isOutdoor` en pruebas nacionales mide el país, no la pista, así que solo se usa dentro de las pruebas FEI.
- `first_age_champion` no se usa porque es la respuesta disfrazada (fuga de datos).
- Todo el preprocesamiento se ajusta solo con los datos de entrenamiento.


