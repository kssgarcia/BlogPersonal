---
title: How to optimize
weight: 2
next: /docs/license
prev: /docs/getting-started
---


The below example shows how to optimize a cantilever beam

```python
import numpy as np
import solidsopt

length = 60
height = 60
nx = 60
ny= 60
dirs = np.array([[0,-1]])
positions = np.array([[15,1]])
penal = 3 
niter = 200

solidsopt.SIMP(length, height, nx, ny, dirs, positions, niter, penal, plot=True)
```
![Picture 1](/example1.png)
|:--:|
| <b>Figure 1. Result.</b>|

{{< callout emoji="ℹ️">}}
  It is important to realize that the parameter **positions** are related to the values of **nx** and **ny**. **dirs** is a list of lists of [x,y] direction and **positions** are a list of lists of [row,col].
{{< /callout >}}

```python
import numpy as np
import solidsopt

length = 60
height = 60
nx = 60
ny= 60
dirs = np.array([[0,-1], [0,1], [1,0]])
positions = np.array([[61,30], [1,30], [30, 1]])
penal = 3 
niter = 200

solidsopt.SIMP(length, height, nx, ny, dirs, positions, niter, penal, plot=True)
```

![Picture 1](/example2.png)
|:--:|
| <b>Figure 2. Result.</b>|