---
title: "Como subir paquete a PyPI"
date: 2023-11-07T11:48:52-05:00
draft: false
---

En este post se mostrará el paso a paso de como subir un paquete para [Python](https://www.python.org/) en [PyPI](https://pypi.org/).

### Paso 1 

Antes de subir el paquete hay que tener una cuenta en [PyPI](https://pypi.org/) y Organizar el proyecto de la siguiente manera

```
├───mi_proyecto
│   ├───mi_modulo.py
│   ├───README.md
│   ├───setup.py
```

### Paso 2

Crear un archivo `setup.py`, este tiene la función de describir el paquete y como se debe de empaquetar. Ejemplo:

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

Tener en cuenta que se puede crear un archivo `MANIFEST.in` para añadir o excluir cualquier archivo que no sea incluido por `setup.py`.

### Paso 3

Empaqueta el proyecto usando `setuptools`. Inicia una terminal en la carpeta del proyecto y ejecuta el comando:

```bash
python .\setup.py sdist
```

Esto creará un archivo fuente tarball en un directorio `dist` dentro de tu proyecto.

### Paso 4

Instala el paquete `twine`, que es una herramienta para subir paquetes a PyPI. Puedes instalarlo utilizando pip:

```bash
pip install twine
```

### Paso 5

Antes de subir el proyecto se puede verificar con el siguiente comando:

```bash
twine check dist/*
```

O se puede utilizar el dominio de pruebas [testpypi](https://test.pypi.org/) para verificar que todo este correcto, tener en cuenta que hay que crear una cuenta. Para subir el proeyecto a este dominio se utiliza el comando:

```bash
twine upload --repository-url https://test.pypi.org/legacy/ dist/*
```

### Paso 6

Sube el paquete a PyPI ejecutando el siguiente comando para subir tu paquete a PyPI. Deberás ingresar tu nombre de usuario y contraseña de PyPI cuando se te solicite:

```bash
twine upload dist/*
```