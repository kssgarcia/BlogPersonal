---
title: SolidsOpt references
weight: 3
next: /docs
prev: /docs/getting-started
---

## solidsopt.optimize

### `BESO(length, height, nx, ny, dirs, positions, niter, t, ER, volfrac, plot=False)`

Performs Evolutionary Structural Optimization (ESO) based on stiffness for a beam structure.

**Parameters:**

- `length`: The length of the beam.
- `height`: The height of the beam.
- `nx`: The number of elements in the x direction.
- `ny`: The number of elements in the y direction.
- `dirs`: List of directions.
- `positions`: List of positions.
- `niter`: The number of iterations for the ESO process.
- `t`: Threshold for error.
- `ER`: The increment of RR for each iteration.
- `volfrac`: The volume fraction for the optimal structure.
- `plot`: If True, plot the initial and optimized mesh. Defaults to False.

**Returns:**

- `ELS`: ndarray: The optimized elements of the structure.
- `nodes`: ndarray: The optimized nodes of the structure.

### `ESO_stiff(length, height, nx, ny, dirs, positions, niter, RR, ER, volfrac, plot=False)`

Performs Evolutionary Structural Optimization (ESO) based on stiffness for a beam structure.

**Parameters:**

- `length`: The length of the beam.
- `height`: The height of the beam.
- `nx`: The number of elements in the x direction.
- `ny`: The number of elements in the y direction.
- `dirs`: List of directions.
- `positions`: List of positions.
- `niter`: The number of iterations for the ESO process.
- `RR`: The relative stress threshold for removing elements.
- `ER`: The increment of RR for each iteration.
- `volfrac`: The volume fraction for the optimal structure.
- `plot`: If True, plot the initial and optimized mesh. Defaults to False.

**Returns:**

- `ELS`: ndarray: The optimized elements of the structure.
- `nodes`: ndarray: The optimized nodes of the structure.

### `ESO_stress(length, height, nx, ny, dirs, positions, niter, RR, ER, volfrac, plot=False)`

Performs Evolutionary Structural Optimization (ESO) based on stress for a beam structure.

**Parameters:**

- `length`: The length of the beam.
- `height`: The height of the beam.
- `nx`: The number of elements in the x direction.
- `ny`: The number of elements in the y direction.
- `dirs`: List of directions.
- `positions`: List of positions.
- `niter`: The number of iterations for the ESO process.
- `RR`: The relative stress threshold for removing elements.
- `ER`: The increment of RR for each iteration.
- `volfrac`: The volume fraction for the optimal structure.
- `plot`: If True, plot the initial and optimized mesh. Defaults to False.

**Returns:**

- `ELS`: ndarray: The optimized elements of the structure.
- `nodes`: ndarray: The optimized nodes of the structure.

### `SIMP(length, height, nx, ny, dirs, positions, niter, penal, plot=False)`

Performs Solid Isotropic Material with Penalization (SIMP) for topology optimization.

**Parameters:**

- `length`: The length of the beam.
- `height`: The height of the beam.
- `nx`: The number of elements in the x direction.
- `ny`: The number of elements in the y direction.
- `dirs`: List of directions.
- `positions`: List of positions.
- `niter`: The number of iterations for the SIMP process.
- `penal`: Penalization factor used in the SIMP method.
- `plot`: If True, plot the initial and optimized mesh. Defaults to False.

**Returns:**

- `rho`: ndarray: The optimized density distribution of the structure.


## solidsopt.models

### `CNN_model(input_shape)`

Load the CNN model architecture

**Parameters:**

- `input_shape`: The shape of the input image

**Returns:**

- `model`: tensorflow.keras.models.Model
  - Model architecture

### `UNN_model(input_shape)`

Load the U-NET model architecture

**Parameters:**

- `input_shape`: The shape of the input image

**Returns:**

- `model`: tensorflow.keras.models.Model
  - Model architecture

### `ViT_model(input_shape)`

Load the ViT model architecture with CNN decoder

**Parameters:**

- `input_shape`: The shape of the input image

**Returns:**

- `model`: tensorflow.keras.models.Model
  - Model architecture


## solidsopt.Utils.beams

### `beam(L=10, H=10, E=206800000000.0, v=0.28, nx=20, ny=20, dirs=array([], dtype=float64), positions=array([], dtype=float64), n=1)`

This function selects the appropriate beam function to call based on the value of n.

**Parameters:**

- `L`: Beam’s length, by default 10
- `H`: Beam’s height, by default 10
- `F`: Vertical force, by default -1000000
- `E`: Young’s modulus, by default 206.8e9
- `v`: Poisson’s ratio, by default 0.28
- `nx`: Number of elements in the x direction, by default 20
- `ny`: Number of elements in the y direction, by default 20
- `n`: Selector for the beam function to call, by default 1

**Returns:**

- `ndarray`: Nodes array returned by the selected beam function

### `beam_1(L=10, H=10, E=206800000000.0, v=0.28, nx=20, ny=20, dirs=array([], dtype=float64), positions=array([], dtype=float64))`

Make the mesh for a quadrilateral model with cantilever beam’s constraints.

**Parameters:**

- `L`: Length of the beam, by default 10
- `H`: Height of the beam, by default 10
- `E`: Young’s modulus, by default 206.8e9
- `v`: Poisson’s ratio, by default 0.28
- `nx`: Number of elements in the x direction, by default 20
- `ny`: Number of elements in the y direction, by default 20
- `dirs`: An array with the directions of the loads, by default empty array. `[[0,1],[1,0],[0,-1]]`
- `positions`: An array with the positions of the loads, by default empty array. `[[61,30], [1,30], [30, 1]]`

**Returns:**

- `nodes`: Array of nodes
- `mats`: Array of material properties
- `els`: Array of elements
- `loads`: Array of loads

### `beam_2(L=10, H=10, E=206800000000.0, v=0.28, nx=20, ny=20, dirs=array([], dtype=float64), positions=array([], dtype=float64))`

Make the mesh for a quadrilateral model with simply supported beam’s constraints.

**Parameters:**

- `L`: Length of the beam, by default 10
- `H`: Height of the beam, by default 10
- `E`: Young’s modulus, by default 206.8e9
- `v`: Poisson’s ratio, by default 0.28
- `nx`: Number of elements in the x direction, by default 20
- `ny`: Number of elements in the y direction, by default 20
- `dirs`: An array with the directions of the loads, by default empty array. `[[0,1],[1,0],[0,-1]]`
- `positions`: An array with the positions of the loads, by default empty array. `[[61,30], [1,30], [30, 1]]`

**Returns:**

- `nodes`: Array of nodes
- `mats`: Array of material properties
- `els`: Array of elements
- `loads`: Array of loads

## solidsopt.Utils.solver

### `adjacency_nodes(nodes, els)`

Create an adjacency matrix for the elements connected to each node.

**Parameters:**

- `nodes`: Array with models nodes.
- `els`: Array with models elements.

**Returns:**

- `adj_nodes`: Adjacency elements for each node.

### `center_els(nodes, els)`

Calculate the center of each element.

**Parameters:**

- `nodes`: Array with models nodes.
- `els`: Array with models elements.

**Returns:**

- `centers`: Centers of each element.

### `del_node(nodes, els, loads, BC)`

Restrict nodes dof that aren’t been used and free up the nodes that are in use.

**Parameters:**

- `nodes`: Array with models nodes
- `els`: Array with models elements
- `loads`: Array with models loads
- `BC`: Boundary conditions nodes

**Returns:**

### `del_nodeESO(nodes, els)`

Restrict nodes dof that aren’t been used.

**Parameters:**

- `nodes`: Array with models nodes
- `els`: Array with models elements

**Returns:**

### `density_filter(centers, r_min, rho, d_rho)`

Perform the sensitivity filter.

**Parameters:**

- `centers`: Array with the centers of each element.
- `r_min`: Minimum radius of the filter.
- `rho`: Array with the density of each element.
- `d_rho`: Array with the derivative of the density of each element.

**Returns:**

- `densi_els`: Sensitivity of each element with filter

### `optimality_criteria(nelx, nely, rho, d_c, g)`

Optimality criteria method.

**Parameters:**

- `nelx`: Number of elements in x direction.
- `nely`: Number of elements in y direction.
- `rho`: Array with the density of each element.
- `d_c`: Array with the derivative of the compliance.
- `g`: Volume constraint.

**Returns:**

- `rho_new`: Array with the new density of each element.
- `gt`: Volume constraint.

### `protect_els(els, nels, loads, BC)`

Compute a mask array with the elements that don’t must be deleted.

**Parameters:**

- `els`: Array with models elements
- `nels`: Number of elements
- `loads`: Array with models loads
- `BC`: Boundary conditions nodes

**Returns:**

- `mask_els`: Array with the elements that don’t must be deleted.

### `protect_elsESO(els, loads, BC)`

Compute a mask array with the elements that don’t must be deleted.

**Parameters:**

- `els`: Array with models elements
- `loads`: Array with models loads
- `BC`: Boundary conditions nodes

**Returns:**

- `mask_els`: Array with the elements that don’t must be deleted.

### `sensitivity_elsBESO(nodes, mats, els, mask, UC)`

Calculate the sensitivity number for each element.

**Parameters:**

- `nodes`: Array with models nodes
- `mats`: Array with models materials
- `els`: Array with models elements
- `mask`: Mask of optimal structure
- `UC`: Displacements at nodes

**Returns:**

- `sensi_number`: Sensitivity number for each element.

### `sensitivity_elsESO(nodes, mats, els, UC)`

Calculate the sensitivity number for each element.

**Parameters:**

- `nodes`: Array with models nodes
- `mats`: Array with models materials
- `els`: Array with models elements
- `UC`: Displacements at nodes

**Returns:**

- `sensi_number`: Sensitivity number for each element.

### `sensitivity_filter(nodes, centers, sensi_nodes, r_min)`

Perform the sensitivity filter.

**Parameters:**

- `nodes`: Array with models nodes
- `sensi_nodes`: Array with nodal sensitivity
- `centers`: Array with center of elements
- `r_min`: Minimum distance

**Returns:**

- `sensi_els`: Sensitivity of each element with filter

### `sensitivity_nodes(nodes, adj_nodes, centers, sensi_els)`

Calculate the sensitivity of each node.

**Parameters:**

- `nodes`: Array with models nodes
- `adj_nodes`: Adjacency matrix of nodes
- `centers`: Array with center of elements
- `sensi_els`: Sensitivity of each element without filter

**Returns:**

- `sensi_nodes`: Sensitivity of each node

### `sparse_assem(elements, mats, neq, assem_op, kloc)`

Assembles the global stiffness matrix using a sparse storing scheme

**Parameters:**

- `elements`: Array with the number for the nodes in each element.
- `mats`: Array with the material profiles.
- `neq`: Number of active equations in the system.
- `assem_op`: Assembly operator.
- `uel`: Python function that returns the local stiffness matrix.
- `kloc`: Stiffness matrix of a single element

**Returns:**

- `stiff`: Array with the global stiffness matrix in a sparse Compressed Sparse Row (CSR) format.

### `strain_els(els, E_nodes, S_nodes)`

Compute the elements strains and stresses.

**Parameters:**

- `els`: Array with models elements
- `E_nodes`: Strains at nodes.
- `S_nodes`: Stresses at nodes.

**Returns:**

- `E_els`: Strains at elements.
- `S_els`: Stresses at elements.

### `volume(els, length, height, nx, ny)`

Compute volume.

**Parameters:**

- `els`: Array with models elements.
- `length`: Length of the beam.
- `height`: Height of the beam.
- `nx`: Number of elements in x direction.
- `ny`: Number of elements in y direction.

**Returns:**

- `V`: float: Volume of the structure.

