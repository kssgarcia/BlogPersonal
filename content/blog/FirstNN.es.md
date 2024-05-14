---
title: "Mi primera red neuronal"
date: 2023-08-03T11:48:52-05:00
draft: false
---

En las últimas décadas, las redes neuronales han emergido como una poderosa herramienta en el campo del aprendizaje automático y la inteligencia artificial. Estas redes artificiales han demostrado su eficacia en una amplia gama de aplicaciones, desde el reconocimiento de voz y la visión por computadora hasta la traducción automática y la predicción del comportamiento del usuario.

Una red neuronal es un modelo computacional compuesto por unidades interconectadas llamadas neuronas, que trabajan en conjunto para procesar y aprender patrones complejos de datos. Estas redes se organizan en capas, donde cada capa se compone de múltiples neuronas que procesan información y transmiten señales a través de conexiones ponderadas.

La flexibilidad y adaptabilidad de las redes neuronales las han convertido en una herramienta prometedora para una variedad de aplicaciones, ya que pueden aprender automáticamente a partir de ejemplos y generar predicciones precisas. En el campo de la optimización topológica, donde se busca encontrar la configuración óptima de un sistema o estructura dada, las redes neuronales también han demostrado ser de gran utilidad. La optimización topológica implica determinar la distribución óptima de material dentro de una región dada, maximizando la eficiencia estructural o minimizando alguna métrica de costo.

La integración de redes neuronales en la optimización topológica ha permitido superar las limitaciones de los enfoques tradicionales, que a menudo se basan en métodos heurísticos o algoritmos específicos para resolver problemas de optimización. Al utilizar redes neuronales, es posible obtener soluciones más rápidas y eficientes, ya que estas redes pueden aprender a reconocer patrones y características clave en los datos de entrada.

En particular, las redes neuronales pueden ayudar en la generación automática de diseños óptimos en la optimización topológica. Al entrenar una red neuronal con datos de entrada que representan las condiciones y restricciones del problema de optimización, junto con la salida correspondiente que representa el diseño óptimo, la red puede aprender a generar diseños estructurales optimizados de manera eficiente y precisa.

En este informe se describe el proceso de construcción de una red neuronal convolucional, que sin ningún esquema iterativo, toma como datos de entrada las condiciones de frontera y las restricciones del problema y devuelve la distribución de densidades del diseño óptimo. Para esto los datos se generaron utilizando el método SIMP. En sección 2 se presenta el paso a paso de la construcción de la red neuronal, en 2.1 se explica el proceso de generación de datos, en 2.2 se expone la arquitectura de la red neuronal, en la subsección 2.3 todo la parte de entrenamiento y por ultimo la sección 3 se muestran los resultados.

## 2. Red neuronal

Para resolver el problema de optimización estructural se decidió utilizar una red neuronal convolución, ya que la estructura de los datos se acomoda a este problema. Esta red neuronal se baso en lo propuesto en el articulo Yu et al., 2018 en donde también se utiliza una red convolucional y una red generativa adversaria para este proceso. 

Para construir esta red primero se generaron los datos de muestra utilizando el método tradicional SIMP, el cual utiliza el esquema de elementos solidos, en el cual cada elementos tiene una densidad relativa. Esta distribución de densidades es la que se tomará como salida para la red neuronal. 
La red neuronal cuenta con dos canales de entrada de 61x61, en donde están representadas las condiciones de frontera, las restricciones y la fracción de volumen. La salida es un canal de 60x60.


## 2.1. Generación de muestras

En la figura 1 se muestra el esquema de generación de datos, para esto se tomo una malla de 60x60 elementos. Para poder llevar los datos de entrada y salida de forma que la red neuronal los pueda procesar se organizaron en dos matrices 2d, en una se incluyeron las condiciones de frontera 3 y en la otra las restricciones y la fracción de volumen 2. Para la generación de datos se trabajó con un [código](https://github.com/kssgarcia/DeepLearningOpt/blob/main/simp/SIMP_multi.py) propio en donde se utilizó el paquete de  [SolidsPy](https://github.com/AppliedMechanics-EAFIT/SolidsPy)

![Picture 1](/generacion.png)
|:--:|
| <b>Figure 1. Esquema para generación de datos.</b>|

![Picture 1](/canal1.jpg)
|:--:|
| <b>Figure 2. Matriz canal restricciones y fracción de volumen.</b>|

![Picture 1](/canal2.jpg)
|:--:|
| <b>Figure 3. Matriz canal condiciones de frontera.</b>|


## 2.2. Arquitectura

La arquitectura de la red neuronal se presenta en la imagen 4, esta red cuenta con 11 capaz que se
pueden dividir en capaz de muestreo descendente y capaz de muestreo ascendente.

![Picture 1](/arquitec.png)
|:--:|
| <b>Figure 4. Arquitectura de red neuronal.</b>|


## Entrenamiento

Para el entrenamiento se tomaron 3660 muestras que corresponden a la variación de la carga en la
zona verde mostrada en la figura 5 esto tomo alrededor de 4.83 horas, con estos datos se realizó el
entrenamiento 6 con un epoch de 10 y con el optimizador Adam tomando un tiempo de 11.31 horas. [Código](https://github.com/kssgarcia/DeepLearningOpt/blob/main/simp/SIMP_multi.py)

![Picture 1](/cargas.jpg)
|:--:|
| <b>Figure 5. Esquema para generación de datos.</b>|


![Picture 1](/entrenamiento.png)
|:--:|
| <b>Figure 6. Esquema para entrenamiento de datos.</b>|

## Resultados 

Como se muestra en la figura 7 en algunos de los resultados se evidencia gran similitud con el resultado
esperado, la diferencia se presenta cuando se da en las zonas grises, para la viga esperada esta zona
esta más suavizada.


![Picture 1](/FNNresultados.png)
|:--:|
| <b>Figure 7. Resultados de entrenamiento.</b>|


## Conclusiones

La optimización topológica se refiere a la búsqueda de la mejor distribución de material en una estructura para cumplir con ciertos criterios de rendimiento, como la minimización del peso o la maximización de la rigidez. Tradicionalmente, esta tarea ha sido desafiante debido a la complejidad de los problemas y la necesidad de realizar múltiples iteraciones. Sin embargo, con el surgimiento de las redes neuronales, se ha abierto una nueva forma de abordar la optimización topológica. Hay diferentes esquemas para el tipo de implementación de estos métodos en la optimización estructural el presentado en este escrito es de los mas interesantes por no tener ningún esquema iterativo, ya que intenta utilizar todo el potencial de estas herramientas de aprendizaje automático, por esto demanda mayor esfuerzo. Para construir estos modelos es importante la cantidad de muestras y variedad de las mismas. Entre más cantidad se tenga mayor cantidad de patrones se podrán reconocer.


## Referencias

Yu, Y., Hur, T., Jung, J., & Jang, I. G. (2018). Deep learning for determining a near-optimal topological
design without any iteration. Structural and Multidisciplinary Optimization, 59 (3), 787-799.
https://doi.org/10.1007/s00158-018-2101-5
6

