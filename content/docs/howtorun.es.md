---
title: Como correr una optimización
weight: 2
next: /docs/license
prev: /docs/getting-started
---

A continuación se muestra un ejemplo de cómo optimizar una viga en voladizo:

```python
import numpy as np
import solidsopt

longitud = 60
altura = 60
nx = 60
ny = 60
dirs = np.array([[0, -1]])
posiciones = np.array([[15, 1]])
penalizacion = 3
niter = 200

solidsopt.SIMP(longitud, altura, nx, ny, dirs, posiciones, niter, penalizacion, plot=True)

```

![Picture 1](/example1.png)
|:--:|
| <b>Figura 1. Resultado.</b>|

{{< callout emoji="ℹ️">}}
Es importante darse cuenta de que el parámetro posiciones está relacionado con los valores de nx y ny. dirs es una lista de listas en la dirección [x, y], y posiciones es una lista de listas en la posición [fila, columna].
{{< /callout >}}

```python
import numpy as np
import solidsopt

longitud = 60
altura = 60
nx = 60
ny = 60
dirs = np.array([[0, -1], [0, 1], [1, 0]])
posiciones = np.array([[61, 30], [1, 30], [30, 1]])
penalizacion = 3
niter = 200

solidsopt.SIMP(longitud, altura, nx, ny, dirs, posiciones, niter, penalizacion, plot=True)
```

![Picture 1](/example2.png)
|:--:|
| <b>Figura 2. Resultado.</b>|