---
title: "Como generar documentación de códigos"
date: 2024-01-10T11:48:52-05:00
draft: false
math: true
---

En este post se explicará cómo generar la documentación de un módulo de Python usando [Sphinx](https://www.sphinx-doc.org/en/master/).

## Requisitos


{{% steps %}}

### Instalar sphinx y el builder para markdown

```sh
$ pip install sphinx
$ pip install sphinx-markdown-builder
```

### Después de instalar estos paquetes y ubicarse en la raíz del proyecto, ejecutar los siguientes comandos.

```sh
$ mkdir docs
$ cd docs
$ sphinx-quickstart
```

### Dentro de la carpeta docs, ir a la ubicación `/docs/source/conf.py` y realizar las siguientes modificaciones:

Al inicio del script, copiar y pegar:


```python
import os
import sys

sys.path.insert(0, os.path.abspath('/path/to/project/folder/'))
```

Copiar y reemplazar la lista extensions

```python
extensions = [
    'sphinx.ext.autodoc',
    'sphinx_markdown_builder'
]
```

### Salir de la carpeta docs y ejecutar:

```sh
$ sphinx-apidoc -o docs/source .
$ sphinx-build -b markdown docs/source docs/build
```
{{% /steps %}}