---
title: "Redes neuronales"
date: 2023-07-13T11:48:52-05:00
draft: false
---

## Introducción

En los últimos años, los avances en Deep Learning, y en particular en las redes neuronales, han revolucionado el campo de la inteligencia artificial. Gracias a su capacidad para aprender de forma autónoma a partir de grandes cantidades de datos, las redes neuronales han logrado superar los límites de rendimiento en una variedad de tareas.

Una de las áreas en las que las redes neuronales han tenido un impacto significativo es el reconocimiento de imágenes y la visión por computadora. Mediante la utilización de arquitecturas como las redes neuronales convolucionales (CNN), se han alcanzado resultados sorprendentes en la clasificación de objetos, detección de objetos y segmentación semántica.

La optimización estructural es un desafío fundamental en el campo de la ingeniería, donde el objetivo es encontrar diseños eficientes y económicos para estructuras que cumplan con los requisitos de carga y restricciones específicas. En esta búsqueda de soluciones óptimas, las redes neuronales han surgido como una poderosa herramienta en la optimización estructural. Gracias a su capacidad de aprendizaje automático y modelado de relaciones complejas, las redes neuronales ofrecen una forma innovadora de mejorar la eficiencia y el rendimiento de las estructuras. En esta introducción, exploraremos cómo las redes neuronales se aplican en la optimización estructural, destacando su potencial para generar diseños óptimos y revolucionar la ingeniería estructural.

En este articulo se presentarán los resultados de la revisión de antecedentes sobre Deep Learning y los diferentes algoritmos presentados actualmente, dando a conocer las arquitecturas mas convenientes para resolver estos problemas y las diferentes formas de implementación de estas redes a los algoritmos de optimización tradicionales.

## Tipos de redes neuronales

El aprendizaje profundo, conocido como Deep Learning en inglés, es una rama de la inteligencia artificial que se basa en la construcción y entrenamiento de redes neuronales artificiales para que puedan aprender y realizar tareas de forma autónoma. A diferencia de los algoritmos tradicionales de aprendizaje automático, que requieren una cuidadosa selección de características y conocimiento experto para extraer patrones de los datos, el Deep Learning se enfoca en permitir que las redes neuronales aprendan automáticamente a partir de grandes volúmenes de datos sin una guía o preprocesamiento explícitos.

Las redes neuronales profundas están compuestas por múltiples capas de unidades de procesamiento interconectadas llamadas neuronas. Cada capa extrae características progresivamente más abstractas y complejas a medida que se avanza en la red, lo que permite una representación jerárquica de los datos. Esta arquitectura profunda permite al modelo aprender características de alto nivel y construir una comprensión más sofisticada de los datos de entrada.

El entrenamiento de una red neuronal profunda implica presentarle ejemplos etiquetados y ajustar los pesos y las conexiones entre las neuronas para que el modelo pueda hacer predicciones precisas. Este proceso se realiza mediante el uso de algoritmos de optimización y retro propagación del error, que permiten calcular la contribución de cada neurona y ajustar los parámetros de manera que se minimice el error entre las predicciones del modelo y las etiquetas reales.

Dentro de las redes neuronales se presentan diferentes arquitecturas que tienen como objetivo abstraer diferentes funciones que se acomodan mejor a la tarea que se quiere realizar, como clasificación de imágenes, procesamiento de lenguaje natural, entre otras. En este articulo se presentarán tres tipos de arquitecturas las cuales son comúnmente utilizadas en los métodos de optimización estructural:


### Red neuronal multicapa

Una red neuronal multicapa es una arquitectura de redes neuronales artificiales que consta de múltiples capas de unidades de procesamiento interconectadas llamadas neuronas, esta arquitectura es la mas simple por lo que su capacidad de aprendizaje esta mas limitada que otras redes neuronales, sin embargo se presenta en este articulo debido a que se puede contiene la idea general que abarca todas las arquitecturas presentes en las redes neuronales. Esta estructura en capas permite un aprendizaje y una representación más complejos de los datos, lo que la convierte en una herramienta poderosa en el campo del aprendizaje automático y el procesamiento de información.

En una red neuronal multicapa, se distinguen tres tipos principales de capas: capa de entrada, capas ocultas y capa de salida. La capa de entrada recibe los datos de entrada y los transmite a la siguiente capa, que generalmente es una capa oculta. Las capas ocultas, como su nombre indica, se encuentran entre la capa de entrada y la capa de salida y son responsables de aprender y extraer características más abstractas y complejas a medida que se profundiza en la red. Finalmente, la capa de salida genera las predicciones o resultados deseados en función de la tarea específica que se esté abordando.

Cada neurona en una red neuronal multicapa está conectada a las neuronas de las capas vecinas mediante conexiones ponderadas. Estas conexiones representan la fuerza de influencia que una neurona tiene sobre otra. Cada neurona en una capa recibe entradas de las neuronas de la capa anterior, las multiplica por los pesos correspondientes y el bias de dicha neurona. El bias permite a una red neuronal aprender y representar relaciones más complejas y no lineales entre las variables de entrada y salida, este parámetro se suma ponderadamente a la combinación lineal de las entradas antes de aplicar la función de activación de la neurona, después de hacer la suma ponderada esta se pasa a través de una función de activación no lineal. La función de activación introduce no linealidad en el modelo y permite que la red neuronal capture relaciones complejas y no lineales entre las variables.

El entrenamiento de una red neuronal multicapa implica ajustar los pesos de las conexiones y el bias de cada neurona para que el modelo pueda hacer predicciones precisas. Esto se logra mediante el uso de algoritmos de aprendizaje, como la retro-propagación del error, que calcula la diferencia entre las predicciones del modelo y las etiquetas reales y ajusta los pesos en función de este error. El proceso de entrenamiento se repite iterativamente hasta que el modelo alcance un nivel de precisión deseado. La retro-propagación se hace implementando algoritmos de optimización como del gradiente de descenso. De una forma simple en una red neuronal multicapa lo que esta pasando en cada ciclo del entrenamiento es evaluando la red (forward), inicialmente con pesos y bias aleatorios, y posteriormente se aplica la retro-propagación (backpropagation) para calcular las sensibilidad de los parámetros de la red con la función de error para poder actualizar estos parámetros con el objetivo de minimizar el error. La función de error o de costo varia según el problema que se este realizando.

#IMAGESSSSSS

### Red convolucional

Una red convolucional, también conocida como red neuronal convolucional (CNN), es un tipo de arquitectura de redes neuronales diseñada específicamente para procesar datos con una estructura de cuadrícula, como imágenes. Se caracteriza por la inclusión de capas convolucionales, que aplican filtros de convolución para extraer características visuales, y capas de pooling, que reducen la dimensionalidad de los datos.

Las redes convolucionales son altamente efectivas en tareas relacionadas con la visión por computadora, como el reconocimiento de objetos, la detección de objetos, la segmentación de imágenes y la clasificación de imágenes. Esto se debe a que las capas convolucionales pueden aprender características locales y jerárquicas a partir de las imágenes, como bordes, texturas y formas, y las capas de pooling permiten la invarianza a pequeñas deformaciones y desplazamientos.

En la optimización estructural por medio de redes neuronales es comunmente utilizada una variación de esta red neuronal, red de codificador y decodificador basada en CNN, la diferencia de esta arquitectura con la CNN convencional es que esta consta de un codificador y un decodificador, ambos basados en capas convolucionales. 

El codificador, también conocido como red de extracción de características, se encarga de capturar y comprimir la información relevante de una imagen en una representación de menor dimensionalidad. Utiliza capas convolucionales para extraer características de alto nivel a partir de la entrada de la imagen, como bordes, texturas y formas. Estas capas convolucionales suelen estar seguidas de capas de pooling o submuestreo para reducir la resolución espacial y mantener solo las características más importantes. El decodificador, por otro lado, se encarga de reconstruir una imagen a partir de la representación de baja dimensionalidad generada por el codificador. Utiliza capas convolucionales transpuestas, también conocidas como capas de desconvolución, para aumentar gradualmente la resolución espacial y generar una imagen de salida que se asemeje a la imagen original. El decodificador también puede incluir capas de convolución adicionales para refinar aún más la reconstrucción y mejorar los detalles finos.

La conexión entre el codificador y el decodificador se realiza a través de una conexión de salto, que permite que la información de las capas de alto nivel del codificador se transmita directamente al decodificador. Esta conexión ayuda a fusionar las características extraídas por el codificador con la información espacial del decodificador, lo que permite una mejor reconstrucción de la imagen final.

### Red neuronal generativa adversarial

Una Red Neuronal Generativa Adversarial (GAN, por sus siglas en inglés) es un tipo de arquitectura de redes neuronales compuesta por dos componentes principales: un generador y un discriminador. GAN se utiliza para generar datos sintéticos, como imágenes, música o texto, que se asemejan a los datos reales.

El generador es responsable de crear muestras sintéticas a partir de un espacio de entrada aleatorio, como vectores de ruido. A medida que el generador aprende durante el entrenamiento, intenta generar datos que sean indistinguibles de los datos reales.

El discriminador, por otro lado, actúa como un clasificador que intenta distinguir entre las muestras generadas por el generador y las muestras reales. Su objetivo es aprender a discernir entre los datos generados y los datos reales.

Durante el entrenamiento de la GAN, el generador y el discriminador se entrenan de manera adversarial, compitiendo uno contra el otro. El generador trata de engañar al discriminador generando muestras cada vez más realistas, mientras que el discriminador se entrena para ser más preciso en la detección de las muestras generadas. Esta competencia genera un ciclo de retroalimentación donde ambos componentes se mejoran continuamente.

El objetivo final de una GAN es que el generador pueda dar muestras sintéticas de alta calidad que sean indistinguibles de los datos reales, mientras que el discriminador se vuelve cada vez menos capaz de diferenciar entre las muestras generadas y las muestras reales.

Las GAN han demostrado ser eficaces en la generación de imágenes realistas, el procesamiento del lenguaje natural y otras tareas de generación de datos.


# Referencias


[1] 3Blue1Brown. (2017, 5 de octubre). But what is a neural network? — Chapter 1, Deep Learning.  
YouTube. https://www.youtube.com/watch?v=aircAruvnKk  
[2] arlethv. (2022, 19 de septiembre). Red Neuronal Recursiva en Deep Learning. https://forum.huawei.  
com/enterprise/es/red-neuronal-recursiva-en-deep-learning/thread/1003551-100757  
[3] Chandrasekhar, A., Sridhara, S., & Suresh, K. (2022). GM-TOuNN: Graded Multiscale Topology  
Optimization using Neural Networks.  
[4] Sosnovik, I., & Oseledets, I. V. (2017). Neural networks for topology optimization. CoRR, abs/1709.09578.  
http://arxiv.org/abs/1709.09578  
[5] Xiang, C., Chen, A., & Wang, D. (2022). Real-time stress-based topology optimization via deep lear-  
ning. Thin-Walled Structures, 181, 110055. https://doi.org/https://doi.org/10.1016/j.tws.  
2022.110055  
[6] Yu, Y., Hur, T., Jung, J., & Jang, I. G. (2018). Deep learning for determining a near-optimal topological  
design without any iteration. Structural and Multidisciplinary Optimization, 59 (3), 787-799.  
https://doi.org/10.1007/s00158-018-2101-5  
[7] Zhang, Y., Peng, B., Zhou, X., Xiang, C., & Wang, D. (2020). A deep Convolutional Neural Network  
for topology optimization with strong generalization ability.  
9