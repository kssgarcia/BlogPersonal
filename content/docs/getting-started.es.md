---
title: Empezando
weight: 1
next: /docs/howtorun
prev: /docs/
---

El código está escrito en Python y depende de [Numpy](https://numpy.org), [scipy](https://scipy.org), [TensorFlow](https://www.tensorflow.org) y [SolidsPy](https://solidspy.readthedocs.io/en/latest/).

### Instalación

```sh
pip install solidsopt
```

### Cargar pesos para redes neuronales


```sh
Load model
```

## Repositorios

Se crearon dos repositorios a partir de este proyecto, uno contiene los algoritmos de optimización estructural y el otro tiene todo lo relacionado con el desarrollo de métodos de aprendizaje profundo.

- {{< icon "github" >}}&nbsp;[kssgarcia/DeepLearningOpt](https://github.com/kssgarcia/DeepLearningOpt)
- {{< icon "github" >}}&nbsp;[kssgarcia/OptTopolgy](https://github.com/kssgarcia/OptTopolgy)

## Repositorio de Optimización Topológica

- Método BESO [BESO.py](https://github.com/kssgarcia/OptTopolgy/blob/main/BESO.py)
- Método basado en esfuerzos ESO [ESO_stress_based.py](https://github.com/kssgarcia/OptTopolgy/blob/main/ESO_stress_based.py)
- Método basado en rigidez ESO [ESO_stiff_based.py](https://github.com/kssgarcia/OptTopolgy/blob/main/ESO_stiff_based.py)
- Método SIMP [SIMP.py](https://github.com/kssgarcia/OptTopolgy/blob/main/SIMP.py)

### Instrucciones

{{% steps %}}

### Clonar el repositorio

```sh
git clone https://github.com/kssgarcia/OptTopolgy.git
```

### Descargar los paquetes requeridos ejecutando el siguiente comando

```sh
conda env create -f environment.yml
```

### Instalar solidspy

```sh
pip install solidspy
```
{{% /steps %}}

## Repositorio de Optimización con Aprendizaje Profundo

- [SIMP_multi.py](https://github.com/kssgarcia/DeepLearningOpt/blob/main/simp/SIMP_multi.py) código utilizado para generar el conjunto de datos de entrenamiento.
- [CNN.py](https://github.com/kssgarcia/DeepLearningOpt/blob/main/neural_network/CNN.py) código utilizado para entrenar la red neuronal.
- [load_model.py](https://github.com/kssgarcia/DeepLearningOpt/blob/main/neural_network/CNN2.py) código utilizado para cargar la red neuronal.
- [SIMP_multi_dist.py](https://github.com/kssgarcia/DeepLearningOpt/blob/main/neural_network/SIMP_multi_dist.py) código utilizado para generar un conjunto de datos con una carga distribuida.

### Instrucciones

{{% steps %}}

### Clonar el repositorio

```sh
git clone https://github.com/kssgarcia/DeepLearningOpt.git
```

### Descargar los paquetes requeridos ejecutando el siguiente comando

```sh
conda env create -f environment.yml
```

### Instalar solidspy

```sh
pip install solidspy
```
{{% /steps %}}