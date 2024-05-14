---
title: "How to upload a package in PyPI"
date: 2023-11-07T11:48:52-05:00
draft: false
---

This post will show the step-by-step process of how to upload a package for [Python](https://www.python.org/) to [PyPI](https://pypi.org/).

### Step 1

Before uploading the package, you need to have an account on [PyPI](https://pypi.org/) and organize the project as follows:

```
├───mi_proyecto
│   ├───mi_modulo.py
│   ├───README.md
│   ├───setup.py
```

### Step 2

Create a `setup.py` file, which describes the package and how it should be packaged. For example:

```python
from setuptools import setup

with open('README.md', 'r', encoding='utf-8') as f:
    long_description = f.read()
	
setup(
    name='nombre_del_paquete',
    version='0.1',
    description='Descripción de tu paquete',
	long_description=long_description,
    long_description_content_type="text/markdown",
    author='Tu Nombre',
    author_email='tu@email.com',
    url='URL de tu proyecto en GitHub o sitio web',
    packages=['nombre_del_paquete'],
)

```

Keep in mind that you can create a `MANIFEST.in` file to include or exclude any files not covered by `setup.py`.

### Step 3

Package the project using `setuptools`. Open a terminal in the project folder and run the command:

```bash
python .\setup.py sdist
```

This will create a source tarball file in a `dist` directory within your project.

### Step 4

Install the `twine` package, a tool for uploading packages to PyPI. You can install it using pip:

```bash
pip install twine
```

### Step 5

Before uploading the project, you can verify it with the following command:

```bash
twine check dist/*
```

O se puede utilizar el dominio de pruebas [testpypi](https://test.pypi.org/) para verificar que todo esté correcto, tener en cuenta que hay que crear una cuenta. Para subir el proyecto a este dominio se utiliza el comando:

```bash
twine upload --repository-url https://test.pypi.org/legacy/ dist/*
```
### Step 6

Upload the package to PyPI by running the following command. You'll need to enter your PyPI username and password when prompted:

```bash
twine upload dist/*
```