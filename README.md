Descripción del Script de Entrenamiento y Evaluación del Modelo

Este script entrena y evalúa un modelo de clasificación binaria mediante Regresión Logística utilizando un dataset preprocesado relacionado con enfermedad cardiovascular. El objetivo es medir el rendimiento del modelo aplicando un umbral ajustado para mejorar la detección de casos positivos, lo cual es relevante en aplicaciones médicas.

Proceso del Script
1. Carga del dataset

Se monta Google Drive y se carga el archivo CSV preprocesado. El script asegura que los nombres de las columnas estén limpios y correctamente interpretados.

2. Preparación de los datos

Se separan las características predictoras (X) de la variable objetivo (y), correspondiente a la columna que indica presencia o ausencia de enfermedad cardiovascular.
Posteriormente, los datos se dividen en conjunto de entrenamiento y prueba, conservando la proporción original de clases mediante estratificación.

3. Construcción del modelo

El script construye un pipeline que contiene un único estimador:
Regresión Logística, configurada con las siguientes características:

solver='liblinear', adecuado para problemas binarios.

class_weight='balanced', para compensar desbalanceos entre clases.

random_state=42, para asegurar reproducibilidad.

El modelo se entrena usando los datos del conjunto de entrenamiento.

4. Predicciones con threshold ajustado

Una vez obtenido el modelo, se calculan probabilidades de pertenencia a la clase positiva.
En lugar de usar el umbral estándar de 0.5, se aplica un umbral de decisión de 0.4.
Este ajuste ayuda a aumentar el recall, lo que permite detectar más casos positivos, lo cual es especialmente importante en escenarios médicos.

5. Evaluación del modelo

Se calculan diversas métricas de clasificación utilizando el umbral ajustado:

Exactitud (Accuracy)

Sensibilidad (Recall)

F1-Score

Área bajo la curva ROC (ROC AUC)

También se genera e imprime la matriz de confusión para observar los aciertos y errores del modelo en ambas clases.

6. Visualización

Se traza la curva ROC utilizando RocCurveDisplay.
Esta curva permite evaluar el rendimiento general del modelo en distintos umbrales de decisión y observar la relación entre sensibilidad y especificidad.
