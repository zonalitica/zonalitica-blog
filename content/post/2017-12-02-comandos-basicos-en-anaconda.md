---
title: Comandos Básicos en Anaconda
author: Alberto Negron
date: '2017-12-02'
slug: comandos-basicos-en-anaconda
categories:
  - data science
  - Python
tags:
  - Anaconda
  - python
description: ''
featured: ''
featuredalt: ''
featuredpath: ''
linktitle: ''
---

Como les comente en el anterior [post]({{< ref "post/2017-12-01-introduccion-a-anaconda.md" >}}) Anaconda es un ecosistema que nos permite instalar y administar multiple versiones de *Python* junto con más de 1000 paquetes y todas sus dependencias.

Quiero aclarar que estos comandos se llevan a cabo en el terminal o línea de comando pero los mismos también se puede ejecutar directamente en Anaconda usando la versión gráfica (**anaconda-navigator**) y unos cuantos clicks.


### Comandos Básicos

| Tarea          | Comando       |
| -------------|-------------|
| Verificar versión de *conda* está instalada      | `conda info`| 
| Actualizar coda a la versión mas reciente      | `conda update conda`      | 
| Instalar un paquete incluido en Anaconda | `conda install PACKAGENAME`      |
| Ejecutar un paquete después de instalación, ej. Spyder | `spyder`
| Actualizar un paquete | `conda update PACKAGENAME` |
| Perdir ayuda para un comando | `COMMANDLINE --help` |

### Ambientes

| Tarea          | Comando       |
| -------------|-------------|
| Crear un nuevo ambiente llamado py27, instalar Python 2.7.14     | `conda create --name py27 python=2.7.14`| 
| Activar ambiente (Windows)     | `activate py27`      | 
| Activar ambiente (macOS,Linux) | `source activate py27`      |
| Desactivar ambiente (Windows)   |`deactivate`|
| Desactivar ambiente (macOS,Linux) |`source deactivate`|
| Hacer una copia exacta de un ambiente | `conda create --clone py35 --name py35-2`
| Listar todos los paquetes instalados en al ambiente activo | `conda list`
| Listar todos los cambios hechos en el ambiente activo | `conda list --revisions` |
| Restaurar ambiente activo a una versión anterior |`conda install --revision 2`|
| Salvar un ambiente en un archivo de texto |`conda list --explicit > backup-env.txt`|
| Eliminar un ambiente|`conda env remove --name py27`|
| Crear un ambiente a partir de un archivo de texto|`conda env create --file backup-env.txt`|
| Crear un ambiente *bio-env* e instalar **biopython**|`conda create --name bio-env biopython`|


### Paquetes

| Tarea          | Comando       |
| -------------|-------------|
| Usar `conda` para buscar por un paquete    | `conda search PACKAGENAME`| 
| Instalar un nuevo paquete (ej. Jupyter)     | `conda install jupyter`      | 
| Instalar un paquete en un ambiente distinto | `conda install --name py27 pandas`      |
| Actualizar paquete en ambiente activo    | `conda update scikit-learn`| 
| Instalar un nuevo paquete (ej. Jupyter)     | `conda install jupyter`      | 
| Instalar un paquete directamente de PiPy | `pip install boltons`      |
| Instalar un paquete directamente de un canal específico | `conda install --channel conda-forge boltons`      |
| Eliminar un paquete ambiente específico | `conda remove --name py27 boltons toolz`      |

Guarden este post en sus favoritos!





