---
title: Introducción a Anaconda
author: Alberto Negron
date: '2017-12-01'
slug: introduccion-a-anaconda
categories:
  - Python
  - data science
tags:
  - herramientas
  - python
  - Anaconda
description: ''
featured: ''
featuredalt: ''
featuredpath: ''
linktitle: ''
---

Mis aventuras con *Python* empezarón por allá en el 2010 y desde entonces he trabajado con esta herramienta de forma intermitente. Como algunos de ustedes saben *Python* viene en varias formas y colores, con esto quiero decir que distintas distribuciones que pueden ser instaladas en un momento dado.

Por lo general, la gente descarga *Python* de [python.org](https://www.python.org/downloads/) lo cual es más que suficiente para la mayoría de las tareas básicas pero la perspectiva cambia cuando se trata de usar paquetes con referencia a Data Science.

Recuerdo por allá en el 2011 cuando **Wes McKinney** lanzó las primeras versiones beta del paquete *Pandas*, era toda una odisea poder instalar esta librería en tu PC. Cuando no tenías todas las dependencias como por ejemplo *Numpy*, era que el compilador que estabas usando no era el adecuado pero si cambiabas el compilador entonces cientos de micro procesos en la máquina dejaban de funcionar lo cual se traducía a semanas enteras de frustración tratando de reparar todos los desastres hechos.

Algunas empresas como [Enthought](https://www.enthought.com/) empezaron a crear distribuciones "científicas" de *Python* que resolvían esto problemas pero cuya licencias de distribución eran algo restrictivas.

Posteriormente apareció [Anaconda](https://www.anaconda.com/) cuya distribución es una de las más populares hoy en día.

Pero qué es lo que *Anaconda* resuelve?

La clave del éxito de *Anaconda* es que resuelve todas las dependencias de más 1000 paquetes de python para Data Science y otras tareas. Permite al usuario tener múltiple versiones de python aisladas unas de otras, en otras palabras no hay conflictos entre versiones!!! algo imposible de imaginar hace unos años atrás.

Cuáles son las caraterísticas más importante de Anaconda?

1. Totalmente gratis,Libre, de código abierto, con una documentación bastante detallada.
2. Puede ser instalada en Windows, Linux in Mac
3. Permite instalar y administrar multiples entornos de Python
4. Viene con varios IDE pre-instalados como Jupyter y Spyder
5. Anaconda Navigator es una interfaz gráfica de usuario GUI (opcional)
6. Elimina problemas de dependencia de paquetes y control de versiones.
7. Facilita el compartir scripts o proyectos entre múltiples personas.
8. Ya mencione que es totalmente gratis?

Cómo instalar Anaconda?

La instalación de Anaconda es muy sencilla!

* Diríjase a este link [https://www.anaconda.com/download/](https://www.anaconda.com/download/) 
* Descarge la version de Python que desee. Mi recomendación es la 3.X.
* En cada versión tiene la opción de descargar la versión gráfica o la sólo la versión por línea de comando. Aquí la decisión es a juicio del facultativo.

![](/img/anaconda-versiones.png "Versiones de Ananconda")

* Una vez descargado puede instalarlo como cualquier otro programa.
* Ananconda puede ser instalado globalmente o sólo para el usuario local. Si usted no es el administrador entonces vaya por la segunda opción.

>NOTA: Durante la instalación, asegurate de marcar las siguientes 2 casillas durante la instalación. Esto te va a ahorrar tener que agregar manualmente Anaconda a tus *PATH* de variables de ambiente.

![](/img/ananconda_path_win.png "Anaconda PATH")


Una vez instalada Anaconda ejecute el siguiente comando desde la línea de comando para verificar que la instalación a finalizado correctamente. Ustedes deberían la versión de python 3.6 ó mayor.

```
altons@centaurus> conda info
Current conda install:

               platform : osx-64
          conda version : 4.3.30
       conda is private : False
      conda-env version : 4.3.30
    conda-build version : 1.14.1
         python version : 3.4.4.final.0
       requests version : 2.12.4
       root environment : /Users/altons/anaconda  (writable)
    default environment : /Users/altons/anaconda
       envs directories : /Users/altons/anaconda/envs
                          /Users/altons/.conda/envs
          package cache : /Users/altons/anaconda/pkgs
                          /Users/altons/.conda/pkgs
           channel URLs : https://repo.continuum.io/pkgs/main/osx-64
                          https://repo.continuum.io/pkgs/main/noarch
                          https://repo.continuum.io/pkgs/free/osx-64
                          https://repo.continuum.io/pkgs/free/noarch
                          https://repo.continuum.io/pkgs/r/osx-64
                          https://repo.continuum.io/pkgs/r/noarch
                          https://repo.continuum.io/pkgs/pro/osx-64
                          https://repo.continuum.io/pkgs/pro/noarch
            config file : None
             netrc file : /Users/altons/.netrc
           offline mode : False
             user-agent : conda/4.3.30 requests/2.12.4 CPython/3.4.4 Darwin/17.2.0 OSX/10.13.1
                UID:GID : 501:20
```

Felicitaciones!!!! Ya tienen Ananconda instalada y ahora están a un paso menos de sus proyectos de Data Science.

En el siguiente post hablaremos sobre los comando básicos de adminitración de Anancoda.


