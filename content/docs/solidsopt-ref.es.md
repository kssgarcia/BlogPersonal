---
title: Referencias SolidsOpt
weight: 3
next: /docs
prev: /docs/getting-started
---


## solidsopt.optimize

### `BESO(length, height, nx, ny, dirs, positions, niter, t, ER, volfrac, plot=False)`

Realiza la Optimización Estructural Evolutiva (ESO) basada en la rigidez para una estructura de viga.

**Parámetros:**

- `length`: Longitud de la viga.
- `height`: Altura de la viga.
- `nx`: Número de elementos en la dirección x.
- `ny`: Número de elementos en la dirección y.
- `dirs`: Lista de direcciones.
- `positions`: Lista de posiciones.
- `niter`: Número de iteraciones para el proceso de ESO.
- `t`: Umbral de error.
- `ER`: Incremento de RR para cada iteración.
- `volfrac`: Fracción de volumen para la estructura óptima.
- `plot`: Si es True, muestra el mallado inicial y optimizado. Por defecto, es False.

**Retorna:**

- `ELS`: ndarray: Elementos optimizados de la estructura.
- `nodes`: ndarray: Nodos optimizados de la estructura.

### `ESO_stiff(length, height, nx, ny, dirs, positions, niter, RR, ER, volfrac, plot=False)`

Realiza la Optimización Estructural Evolutiva (ESO) basada en la rigidez para una estructura de viga.

**Parámetros:**

- `length`: Longitud de la viga.
- `height`: Altura de la viga.
- `nx`: Número de elementos en la dirección x.
- `ny`: Número de elementos en la dirección y.
- `dirs`: Lista de direcciones.
- `positions`: Lista de posiciones.
- `niter`: Número de iteraciones para el proceso de ESO.
- `RR`: Umbral de esfuerzo relativo para eliminar elementos.
- `ER`: Incremento de RR para cada iteración.
- `volfrac`: Fracción de volumen para la estructura óptima.
- `plot`: Si es True, muestra el mallado inicial y optimizado. Por defecto, es False.

**Retorna:**

- `ELS`: ndarray: Elementos optimizados de la estructura.
- `nodes`: ndarray: Nodos optimizados de la estructura.

### `ESO_stress(length, height, nx, ny, dirs, positions, niter, RR, ER, volfrac, plot=False)`

Realiza la Optimización Estructural Evolutiva (ESO) basada en el esfuerzo para una estructura de viga.

**Parámetros:**

- `length`: Longitud de la viga.
- `height`: Altura de la viga.
- `nx`: Número de elementos en la dirección x.
- `ny`: Número de elementos en la dirección y.
- `dirs`: Lista de direcciones.
- `positions`: Lista de posiciones.
- `niter`: Número de iteraciones para el proceso de ESO.
- `RR`: Umbral de esfuerzo relativo para eliminar elementos.
- `ER`: Incremento de RR para cada iteración.
- `volfrac`: Fracción de volumen para la estructura óptima.
- `plot`: Si es True, muestra el mallado inicial y optimizado. Por defecto, es False.

**Retorna:**

- `ELS`: ndarray: Elementos optimizados de la estructura.
- `nodes`: ndarray: Nodos optimizados de la estructura.

### `SIMP(length, height, nx, ny, dirs, positions, niter, penal, plot=False)`

Realiza la Optimización Topológica de Material Isotrópico Sólido con Penalización (SIMP).

**Parámetros:**

- `length`: Longitud de la viga.
- `height`: Altura de la viga.
- `nx`: Número de elementos en la dirección x.
- `ny`: Número de elementos en la dirección y.
- `dirs`: Lista de direcciones.
- `positions`: Lista de posiciones.
- `niter`: Número de iteraciones para el proceso de SIMP.
- `penal`: Factor de penalización utilizado en el método SIMP.
- `plot`: Si es True, muestra el mallado inicial y optimizado. Por defecto, es False.

**Retorna:**

- `rho`: ndarray: Distribución de densidad optimizada de la estructura.

## solidsopt.models

### `CNN_model(input_shape)`

Carga la arquitectura del modelo de red neuronal convolucional (CNN).

**Parámetros:**

- `input_shape`: Forma de la imagen de entrada.

**Retorna:**

- `model`: tensorflow.keras.models.Model
  - Arquitectura del modelo

### `UNN_model(input_shape)`

Carga la arquitectura del modelo de red neuronal U-NET (UNN).

**Parámetros:**

- `input_shape`: Forma de la imagen de entrada.

**Retorna:**

- `model`: tensorflow.keras.models.Model
  - Arquitectura del modelo

### `ViT_model(input_shape)`

Carga la arquitectura del modelo de red neuronal ViT con decodificador CNN.

**Parámetros:**

- `input_shape`: Forma de la imagen de entrada.

**Retorna:**

- `model`: tensorflow.keras.models.Model
  - Arquitectura del modelo

## solidsopt.Utils.beams

### `beam(L=10, H=10, E=206800000000.0, v=0.28, nx=20, ny=20, dirs=array([], dtype=float64), positions=array([], dtype=float64), n=1)`

Esta función selecciona la función de viga apropiada para llamar según el valor de n.

**Parámetros:**

- `L`: Longitud de la viga, por defecto 10
- `H`: Altura de la viga, por defecto 10
- `F`: Fuerza vertical, por defecto -1000000
- `E`: Módulo de Young, por defecto 206.8e9
- `v`: Coeficiente de Poisson, por defecto 0.28
- `nx`: Número de elementos en la dirección x, por defecto 20
- `ny`: Número de elementos en la dirección y, por defecto 20
- `n`: Selector para la función de viga a llamar, por defecto 1

**Retorna:**

- `ndarray`: Array de nodos devuelto por la función de viga seleccionada

### `beam_1(L=10, H=10, E=206800000000.0, v=0.28, nx=20, ny=20, dirs=array([], dtype=float64), positions=array([], dtype=float64))`

Crea la malla para un modelo cuadrilátero con restricciones de viga empotrada.

**Parámetros:**

- `L`: Longitud de la viga, por defecto 10
- `H`: Altura de la viga, por defecto 10
- `E`: Módulo de Young, por defecto 206.8e9
- `v`: Coeficiente de Poisson, por defecto 0.28
- `nx`: Número de elementos en la dirección x, por defecto 20
- `ny`: Número de elementos en la dirección y, por defecto 20
- `dirs`: Un array con las direcciones de las cargas, por defecto array vacío. `[[0,1],[1,0],[0,-1]]`
- `positions`: Un array con las posiciones de las cargas, por defecto array vacío. `[[61,30], [1,30], [30, 1]]`

**Retorna:**

- `nodes`: Array de nodos
- `mats`: Array de propiedades del material
- `els`: Array de elementos
- `loads`: Array de cargas

### `beam_2(L=10, H=10, E=206800000000.0, v=0.28, nx=20, ny=20, dirs=array([], dtype=float64), positions=array([], dtype=float64))`

Crea la malla para un modelo cuadrilátero con restricciones de viga simplemente apoyada.

**Parámetros:**

- `L`: Longitud de la viga, por defecto 10
- `H`: Altura de la viga, por defecto 10
- `E`: Módulo de Young, por defecto 206.8e9
- `v`: Coeficiente de Poisson, por defecto 0.28
- `nx`: Número de elementos en la dirección x, por defecto 20
- `ny`: Número de elementos en la dirección y, por defecto 20
- `dirs`: Un array con las direcciones de las cargas, por defecto array vacío. `[[0,1],[1,0],[0,-1]]`
- `positions`: Un array con las posiciones de las cargas, por defecto array vacío. `[[61,30], [1,30], [30, 1]]`

**Retorna:**

- `nodes`: Array de nodos
- `mats`: Array de propiedades del material
- `els`: Array de elementos
- `loads`: Array de cargas

## solidsopt.Utils.solver

### `adjacency_nodes(nodes, els)`

Crea una matriz de adyacencia para los elementos conectados a cada nodo.

**Parámetros:**

- `nodes`: Array con los nodos del modelo.
- `els`: Array con los elementos del modelo.

**Retorna:**

- `adj_nodes`: Elementos adyacentes para cada nodo.

### `center_els(nodes, els)`

Calcula el centro de cada elemento.

**Parámetros:**

- `nodes`: Array con los nodos del modelo.
- `els`: Array con los elementos del modelo.

**Retorna:**

- `centers`: Centros de cada elemento.

### `del_node(nodes, els, loads, BC)`

Restringe los grados de libertad de los nodos que no se utilizan y libera los nodos que están en uso.

**Parámetros:**

- `nodes`: Array con los nodos del modelo.
- `els`: Array con los elementos del modelo.
- `loads`: Array con las cargas del modelo.
- `BC`: Nodos con condiciones de contorno.

**Retorna:**

### `del_nodeESO(nodes, els)`

Restringe los grados de libertad de los nodos que no se utilizan.

**Parámetros:**

- `nodes`: Array con los nodos del modelo.
- `els`: Array con los elementos del modelo.

**Retorna:**

### `density_filter(centers, r_min, rho, d_rho)`

Realiza el filtro de sensibilidad.

**Parámetros:**

- `centers`: Array con los centros de cada elemento.
- `r_min`: Radio mínimo del filtro.
- `rho`: Array con la densidad de cada elemento.
- `d_rho`: Array con la derivada de la densidad de cada elemento.

**Retorna:**

- `densi_els`: Sensibilidad de cada elemento con filtro

### `optimality_criteria(nelx, nely, rho, d_c, g)`

Método de criterio de optimalidad.

**Parámetros:**

- `nelx`: Número de elementos en la dirección x.
- `nely`: Número de elementos en la dirección y.
- `rho`: Array con la densidad de cada elemento.
- `d_c`: Array con la derivada de la cumplimiento.
- `g`: Restricción de volumen.

**Retorna:**

- `rho_new`: Array con la nueva densidad de cada elemento.
- `gt`: Restricción de volumen.

### `protect_els(els, nels, loads, BC)`

Calcula una matriz de máscara con los elementos que no deben eliminarse.

**Parámetros:**

- `els`: Array con los elementos del modelo.
- `nels`: Número de elementos.
- `loads`: Array con las cargas del modelo.
- `BC`: Nodos con condiciones de contorno.

**Retorna:**

- `mask_els`: Array con los elementos que no deben eliminarse.

### `protect_elsESO(els, loads, BC)`

Calcula una matriz de máscara con los elementos que no deben eliminarse.

**Parámetros:**

- `els`: Array con los elementos del modelo.
- `loads`: Array con las cargas del modelo.
- `BC`: Nodos con condiciones de contorno.

**Retorna:**

- `mask_els`: Array con los elementos que no deben eliminarse.

### `sensitivity_elsBESO(nodes, mats, els, mask, UC)`

Calcula el número de sensibilidad para cada elemento.

**Parámetros:**

- `nodes`: Array con los nodos del modelo.
- `mats`: Array con los materiales del modelo.
- `els`: Array con los elementos del modelo.
- `mask`: Máscara de estructura óptima.
- `UC`: Desplazamientos en los nodos.

**Retorna:**

- `sensi_number`: Número de sensibilidad para cada elemento.

### `sensitivity_elsESO(nodes, mats, els, UC)`

Calcula el número de sensibilidad para cada elemento.

**Parámetros:**

- `nodes`: Array con los nodos del modelo.
- `mats`: Array con los materiales del modelo.
- `els`: Array con los elementos del modelo.
- `UC`: Desplazamientos en los nodos.

**Retorna:**

- `sensi_number`: Número de sensibilidad para cada elemento.

### `sensitivity_filter(nodes, centers, sensi_nodes, r_min)`

Realiza el filtro de sensibilidad.

**Parámetros:**

- `nodes`: Array con los nodos del modelo.
- `sensi_nodes`: Array con la sensibilidad nodal.
- `centers`: Array con el centro de los elementos.
- `r_min`: Distancia mínima.

**Retorna:**

- `sensi_els`: Sensibilidad de cada elemento con filtro

### `sensitivity_nodes(nodes, adj_nodes, centers, sensi_els)`

Calcula la sensibilidad de cada nodo.

**Parámetros:**

- `nodes`: Array con los nodos del modelo.
- `adj_nodes`: Matriz de adyacencia de nodos.
- `centers`: Array con el centro de los elementos.
- `sensi_els`: Sensibilidad de cada elemento sin filtro.

**Retorna:**

- `sensi_nodes`: Sensibilidad de cada nodo

### `sparse_assem(elements, mats, neq, assem_op, kloc)`

Ensambla la matriz de rigidez global utilizando un esquema de almacenamiento disperso

**Parámetros:**

- `elements`: Array con el número de los nodos en cada elemento.
- `mats`: Array con los perfiles de material.
- `neq`: Número de ecuaciones activas en el sistema.
- `assem_op`: Operador de ensamblaje.
- `uel`: Función de Python que devuelve la matriz de rigidez local.
- `kloc`: Matriz de rigidez de un solo elemento

**Retorna:**

- `stiff`: Array con la matriz de rigidez global en un formato disperso Compressed Sparse Row (CSR).

### `strain_els(els, E_nodes, S_nodes)`

Calcula las deformaciones y tensiones de los elementos.

**Parámetros:**

- `els`: Array con los elementos del modelo.
- `E_nodes`: Deformaciones en los nodos.
- `S_nodes`: Tensiones en los nodos.

**Retorna:**

- `E_els`: Deformaciones en los elementos.
- `S_els`: Tensiones en los elementos.

### `volume(els, length, height, nx, ny)`

Calcula el volumen.

**Parámetros:**

- `els`: Array con los elementos del modelo.
- `length`: Longitud de la viga.
- `height`: Altura de la viga.
- `nx`: Número de elementos en la dirección x.
- `ny`: Número de elementos en la dirección y.

**Retorna:**

- `V`: float: Volumen de la estructura.
