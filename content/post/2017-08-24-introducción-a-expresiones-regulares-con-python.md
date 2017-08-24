---
title: Introducción a Expresiones Regulares con Python
author: Alberto Negron
date: '2017-08-24'
slug: introduccion-a-expresiones-regulares-con-python
categories:
  - Python
tags:
  - nlp
  - python
  - regex
description: ''
featured: ''
featuredalt: ''
featuredpath: ''
linktitle: ''
---

Este es el primer post de una serie de artículos sobre **NLP**. Para los que no conocen que es el procesamiento de lenguajes naturales  o **Natural Language Processing (NLP)** aquí les dejo una corta pero concisa definición:

>...es un campo de las ciencias de la computación, inteligencia artificial y lingüística que estudia las interacciones entre las computadoras y el lenguaje humano. El NLP se ocupa de la formulación e investigación de mecanismos eficaces computacionalmente para la comunicación entre personas y máquinas por medio de lenguajes naturales. El PLN no trata de la comunicación por medio de lenguajes naturales de una forma abstracta, sino de diseñar mecanismos para comunicarse que sean eficaces computacionalmente.**Wikipedia**

Uno de los pilares fundamentales del **NLP** son las expresiones regulares:

>En cómputo teórico y teoría de lenguajes formales una expresión regular, también conocida como regex, regexp o expresión racional es una secuencia de caracteres que forma un patrón de búsqueda, principalmente utilizada para la búsqueda de patrones de cadenas de caracteres u operaciones de sustituciones. Por ejemplo, el grupo formado por las cadenas Handel, Händel y Haendel se describe con el patrón "H(a|ä|ae)ndel". La mayoría de las formalizaciones proporcionan los siguientes constructores: una expresión regular es una forma de representar los lenguajes regulares (finitos o infinitos) y se construye utilizando caracteres del alfabeto sobre el cual se define el lenguaje. **Wikipedia**

Para digerir mejor la definición anterior piensen que una **regex** es: *Una secuencia de caracteres con una sintaxis especial que nos permite hallar ciertos patrones de caracteres en otras cadenas de texto*.

Algunas de las aplicaciones más comunes:

* Conseguir todos los enlaces web en documento como por ejemplo una página html.
* Extraer direcciones de correo
* Remover o reemplazar caracteres no deseados.

Las sintaxis más comunes en **regex** las pueden ver en la siguiente tabla:

| Patrón  | Corresponde   | Ejemplo   |
|---------|---------------|-----------|
|  \w+    | palabra       | 'Hola'    |
|  \d     | dígito        | 9         | 
|  \s     | espacio       | " "        |   
|  .\*    | wildcard      | 'receta23@'|  
|  + ó \* | greedy match  | 'aaabbbbbcccc'|  
|  \S     | no es espacio | 'sin_espacios'|
| [a-z]   | todas minusculas| 'pkfjfus'|

Esto es sólo un abre-boca, para ver todas las opciones les recomiendo este [pdf](https://montcs.bloomu.edu/Information/Python/python-regex-cheatsheet.pdf)




# Módulo de Python para Regex: `re`

El módulo `re` cuenta con funciones para trabajar con expresiones regulares y cadenas. Las funciones más comunes son:

* `split`: divide una cadena en subcadenas.
* `findall`: devuelve una lista con las subcadenas que cumplen el patrón de la regex.
* `search`: busca coincidencias de un patrón en una cadena de texto.
* `match`: comprueba si una expresión regular tiene coincidencias con el comienzo de una cadena de texto.

La sintaxis básica para cada función es: `re.fun(regex,cadena)` y devuelve objetos de tipo `iterator`, `string` o `match`.

## Diferencia entre `search` y `match`


`search` ⇒  consigue un patrón en cualquier parte de la cadena y retorna un objecto de tipo `match.`

`match` ⇒  consigue un patrón al comienzo de una cadena y retorna un objecto de tipo `match`.

Ya hemos cubierto algo de teoría así que veamos algunos ejemplos:


```python
import re
```


```python
frase = "En un lugar de la Mancha, de cuyo nombre no quiero acordarme..."

# encontrar la primera letra
print(re.match(r"\w",frase)) # devuelve un objeto match
```

    <_sre.SRE_Match object; span=(0, 1), match='E'>



```python
# otra forma - (la anterior es la más común)
print(re.match(r"\D",frase))
```

    <_sre.SRE_Match object; span=(0, 1), match='E'>



```python
# encontrar la primera palabra
print(re.match(r"\w+",frase))
```

    <_sre.SRE_Match object; span=(0, 2), match='En'>



```python
# encontrar las dos primeras palabras
print(re.match(r"\w+\s\w+",frase))
```

    <_sre.SRE_Match object; span=(0, 5), match='En un'>


> **Nota**: Es muy importante iniciar las cadenas de regex con `r`. `r` es **raw string** en Python y significa que los caracteres en la cadena no tienen ninguna interpretación especial. Recuerden  las expresiones regulares a menudo utilizan caracteres de escape (como por ejemplo la barra invertida \\ ). Por ejemplo "\n" en Python se utiliza para indicar una nueva línea pero si usamos el `r` entonces se interpreta simplemente como "\n".




# Algunos ejercicios con `findall` y `split`

Hay algunos tópicos como los *brackets* que aún no hemos abordado pero no se preocupen que lo haremos pronto.

```python
sentencia = "Hola Mundo!!! Hace 22 grados centigrados, será Verdad? Mientras no Llegue a 40 grados estamos bien. "

# Dividir la sentencia usando signos de puntuación
print(re.split(r"[!.?]", sentencia)) # devuelve una lista
```

    ['Hola Mundo', '', '', ' Hace 22 grados centigrados, será Verdad', ' Mientras no Llegue a 40 grados estamos bien', ' ']



```python
# Hallar todas las palabras que empiezen con mayúsculas
print(re.findall(r"[A-Z]\w+", sentencia)) # también devuelve una lista
```

    ['Hola', 'Mundo', 'Hace', 'Verdad', 'Mientras', 'Llegue']



```python
# Hallar todas las palabras que terminen en 'o'
print(re.findall(r"\w*o\b", sentencia))
```

    ['Mundo', 'no']



```python
# Dividir la sentencia usando los espacios
print(re.split(r"\s+", sentencia))
```

    ['Hola', 'Mundo!!!', 'Hace', '22', 'grados', 'centigrados,', 'será', 'Verdad?', 'Mientras', 'no', 'Llegue', 'a', '40', 'grados', 'estamos', 'bien.', '']



```python
# Hallar todos los digitos en la sentencia
print(re.findall(r"\d+", sentencia))
```

    ['22', '40']


# Grupos


Los grupos nos permiten extraer un grupo de caracters. Una expresión regular puede tener múltiples grupos. `.group()` se utiliza para retornar la regex completa. `.group(1)` devuelve el primer subgrupo en la cadena y así sucesivamente. 

Algunos ejemplos:

```python
print(re.match(r"\w+",frase).group()) #devuelve un string
```

    En


```python
# grupos
email = "abcde574@gmail.com"
# extraer el usuario de la dirección de correos
print(re.match(r"(\w+)@.+",email).group(1))
```

    abcde574



```python
# extraer el dominio de la dirección de correos
print(re.match(r"\w+@(.+)",email).group(1))
```

    gmail.com



```python
# otra forma, cuando tenemos multiples grupos
print(re.match(r"(\w+)@(.+)",email).group(2)) 
```

    gmail.com



```python
# Extraer multiple grupos
print(re.match(r"(\w+)@(.+)",email).groups()) # retorna un objecto tuple
```

    ('abcde574', 'gmail.com')



```python
# Extraer toda la expresión
print(re.match(r"\w+@(.+)",email).group())
```

    abcde574@gmail.com


## Repeticiones

En regex podemos utilizar el `+` and `*` para especificar repeticiones en el patrón: 

    + -- 1 o mas ocurrencias 
    * -- 0 o mas ocurrencias 
    ? -- match 0 ó 1 ocurrencias

## Más a la izquierda & más largo

Un concepto importante en regex es que la búsqueda siempre consigue el primer patrón que está más a la izquierda (o más cercano al origen de la cadena) y segundo que intenta usar tantos caracteres como sea posible de la cadena. Por ejemplo `+` and `*` va tan lejos como sea posible, por eso se les conoce como 'greedy' o codiciosos.

Ejemplos:


```python
print(re.search(r'pi+', 'piiig').group())
```

    piii



```python
print(re.findall(r'a+', 'caaasa casa casaaaaaa'))
```

    ['aaa', 'a', 'a', 'a', 'a', 'aaaaaa']



```python
# Sólo caaasa y casa
print(re.findall(r'\w*a+sa\b', 'caaasa casa casaaaaaa'))
```

    ['caaasa', 'casa']


# Square Brackets

`[]` se utilizan para indicar un conjunto de caracteres, así pues `[abc]` coincide con `a` o `b` o `c`. `\w`, `\s` etc. funcionan dentro de los `[]` con la excepción del punto (`.`) que sólo significa un punto. Para problemas de extracción de emails los `[]` son una manera sencilla de agregar el `.` y `-`  a el conjunto de caracteres que pueden aparecer alrededor del `@`:

```python
lista_emails = ["alberto@abcd.com","victoria-b@dva.no","irma-m@ttt.c0m"]
# imprimir emails con '-'
for email in lista_emails:
    match = re.search(r'\w+[.-]+\w+@[\w.-]+', email)
    if match:
        print(match.group())
```

    victoria-b@dva.no
    irma-m@ttt.c0m


# `findall` and Groups

Los `( )` como mecanismo de grupos puede ser combinado con `findall()`. Si el patrón incluye 2 ó mas paréntesis entonces es vez de retornar una lista de cadenas, retorna una tupla de cadenas y unido con `findall()` entonces retorna una lista de tuplas. Creo que se entiende mejor con un ejemplo:

```python
enredo = 'pop rock alberto@abcd.com, Madrid Barsa victoria-b@dva.no patatas bravas! irma-m@ttt.c0m'
tuples = re.findall(r'([\w\.-]+)@([\w\.-]+)', enredo)
print(tuples)
```

    [('alberto', 'abcd.com'), ('victoria-b', 'dva.no'), ('irma-m', 'ttt.c0m')]



```python
for t in tuples:
    print(t[0])  ## username
    print(t[1])  ## dominio
```

    alberto
    abcd.com
    victoria-b
    dva.no
    irma-m
    ttt.c0m



# Opciones

Las funciones `re` que hemos abarcado hasta ahora pueden tomar parámetros extras que ayudan a modificar su comportamiento original. La opción se agregar como un argumento extra por ejemplo `re.search(pat, str, re.IGNORECASE)`.

Las opciones mas importantes:

* `IGNORECASE`: ignora mayúsculas y minúsculas, así pues `[a-z]` y `[A-Z]` son equivalentes.
* `DOTALL`: convierte todos los puntos a nueva línea
* `MULTILINE`: con cadenas de hechas de muchas líneas (imaginen un párrafo), esta opción permite allow `^` y `$` coincidir con el inicio y final de cada línea.

Creo que por ahora lo voy a dejar hasta aquí. Las expresiones regulares son un tema bien complejo y esto es sólo una introducción a los conceptos más sencillos.

En los siguientes posts cubriremos un poco más de regex en relación con **NLP**.

Suscríbanse al blog para que se mantengan informados!
