---
title: "How to generate code documentation?"
date: 2024-01-10T11:48:52-05:00
draft: false
math: true
---

In this post, we will explain how to generate documentation for a Python module using [Sphinx](https://www.sphinx-doc.org/en/master/).

## Requirements

{{% steps %}}

### Install Sphinx and the Markdown Builder

```sh
$ pip install sphinx
$ pip install sphinx-markdown-builder
```


### After installing these packages and navigating to the project's root, execute the following commands.


```sh
$ mkdir docs
$ cd docs
$ sphinx-quickstart
```

### Inside the docs folder, go to `/docs/source/conf.py` and make the following modifications:

At the beginning of the script, copy and paste:


```python
import os
import sys

sys.path.insert(0, os.path.abspath('/path/to/project/folder/'))
```
Copy and replace the extensions list:

```python
extensions = [
    'sphinx.ext.autodoc',
    'sphinx_markdown_builder'
]
```

### Exit the `/docs` folder and run:

```sh
$ sphinx-apidoc -o docs/source .
$ sphinx-build -b markdown docs/source docs/build
```
{{% /steps %}}


