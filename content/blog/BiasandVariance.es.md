---
title: "Variación y sesgo en redes neuronales"
date: 2024-04-25T11:48:52-05:00
draft: false
math: true
---

En este post, hablaré sobre un tema crucial en redes neuronales que se presenta en todas ellas: la regularización. Es importante entender las métricas utilizadas en el entrenamiento, siendo la más común la pérdida (loss).

### High Variance

El término "high variance", también conocido como overfitting, se refiere a cuando el modelo tiene un buen rendimiento en el conjunto de entrenamiento pero no en el conjunto de validación. Esto indica que el modelo ha aprendido muy bien la información del dataset, incluyendo el ruido, pero no ha logrado generalizar bien a datos no vistos. Aunque el overfitting es una señal de que el modelo tiene la capacidad de aprender, es necesario aplicar técnicas de regularización para mejorar su capacidad de generalización. Algunas técnicas comunes incluyen L1, L2, dropout, early stopping, entre otras. En mi opinión, el early stopping no debería usarse, aunque algunos lo prefieren.

### High Bias

El "high bias" o underfitting ocurre cuando la red neuronal no es capaz de aprender adecuadamente del conjunto de entrenamiento, lo cual se refleja en una pérdida alta tanto en el conjunto de entrenamiento como en el de validación. Las métricas de ambos conjuntos serán similares y bajas.

### High Bias y High Variance

Este caso ocurre cuando el modelo tiene un mal rendimiento tanto en el entrenamiento como en la validación, mostrando métricas deficientes en ambos conjuntos.

### ¿Qué hacer?

#### High Bias

El underfitting indica que el modelo no es lo suficientemente complejo para la tarea o que el dataset no está bien estructurado.

#### Pasos:
1. Revisar el dataset y comprobar si está bien construido.
2. Si el dataset está bien, cambiar a un modelo más grande y observar las métricas.

#### High Variance

El overfitting puede contrarrestarse usando técnicas de regularización, que ajustan la capacidad de las redes neuronales para que se adapten mejor a la tarea y generalicen adecuadamente.

### Técnicas de Regularización

#### 1. **Regularización L1 y L2 (Weight Decay)**

##### Regularización L1 (Lasso):

- **Descripción**: Añade una penalización basada en la suma de los valores absolutos de los coeficientes de los parámetros, lo que puede conducir a modelos más esparsos.
- **Fórmula**: $Loss = \text{Loss original} + \lambda \sum |w_i|$

##### Regularización L2 (Ridge):

- **Descripción**: Añade una penalización basada en la suma de los cuadrados de los coeficientes de los parámetros, distribuyendo el peso entre todos los coeficientes.
- **Fórmula**: $Loss = \text{Loss original} + \lambda \sum |w_i|^2$

#### 2. **Dropout**

- **Descripción**: Durante el entrenamiento, se desactivan aleatoriamente una fracción de neuronas en cada capa para evitar que las neuronas dependan demasiado unas de otras, reduciendo el sobreajuste y mejorando la generalización.

#### 3. **Early Stopping**

- **Descripción**: Detiene el entrenamiento cuando el rendimiento en el conjunto de validación deja de mejorar, previniendo el sobreajuste.

#### 4. **Batch Normalization**

- **Descripción**: Normaliza las salidas de una capa para tener una media cero y una varianza unitaria, aplicando luego una transformación lineal. Acelera el entrenamiento y mejora la estabilidad del modelo, también actúa como una forma de regularización al introducir ruido en el entrenamiento.

### Consideraciones

Al pensar en el proceso de machine learning, es útil verlo como varios pasos independientes:

1. **Optimizar una función de costo $J(W,b)$**: Revisar el dataset y buscar un modelo que minimice esta función.
2. **Evitar el sobreajuste**: Utilizar técnicas de regularización como L1, L2, batch normalization y dropout. No recomiendo el early stopping ya que combina ambas tareas y puede impedir que el modelo llegue a su mejor punto de convergencia en el entrenamiento.
