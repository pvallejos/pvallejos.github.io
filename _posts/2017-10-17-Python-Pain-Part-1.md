---
layout: post
title: Python al dolor Capitulo 1
---

Introduccion a Python: ventajas, variables, comentarios, consola, tipo de datos, tipo de operadores.

# Antes de comenzar
La serie de Python al dolor ofrece la ayuda y la enseñanza necesaria en poco tiempo para poder dominar uno de los lenguajes de scripting mas usados en la actualidad. 

### Nota
El libro guia que ocuparé para realizar estos post es `Python para todos`, lo puedes descargar desde aqui [https://vay3t.github.io/books/pythonparatodos.pdf](https://vay3t.github.io/books/pythonparatodos.pdf){:target="_blank"}

# Ventajas
* Facilidad de uso
* Multiplataforma
* Multiparadigma
* Alto nivel
* Proposito general
* Simplicidad
* Codigo reutilizable
* Lenguaje interprete (No necesita compilacion)
* Posee entorno interactivo
* Programas compactos
* Entorno de ejecucion (detecta problemas en el codigo e indica en que linea se produce)
* Legibilidad
* Sintaxis amigable
* Abundantes modulos estandars
* Amplia comunidad

# Consola Python
Python posee una consola para poder interactuar con el lenguaje de forma directa sin necesidad de ejecutar un archivo.

```
root@vay3t:~# python
Python 2.7.12 (default, Nov 19 2016, 06:48:10) 
[GCC 5.4.0 20160609] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

# Variables
Una variable está formada por un espacio de memoria principal de un computador y un nombre simbolico que esta asociado a ese espacio. Puede almacenar cualquier tipo de datos y puede ser llamado por el nombre dado cuando uno lo estime conveniente.

```
>>> valor1 = 1
>>> valor2 = 3
>>> respuesta = valor1 + valor2
>>> respuesta
4
```

# Comentario
El comentario sirve para poder escribir en el codigo, pero sin afectar a este. Como su nombre lo indica, sirve para comentar. Como ejemplo real, en ocaciones, cuando el codigo es muy complejo, el comentario sirve para que otro programador vea el codigo y lo entienda mas facilmente. Se usa un hashtag para poder iniciarlo, todo lo que esta despues del hastag es ignorado por el programa. Tambien sirven las comillas triples, pero estas hay que cerrarlas.

```
>>> 1 + 1 # Esto es un comentario
2
>>> 2 + 2 """Esto es otro comentario"""
4
```

# Tipos de datos
Tenemos varios tipos de datos como: cadenas, enteros, flotantes, complejos, enteros largo, listas, tuplas, booleanos y diccionarios. Con el metodo `type` se puede saber que tipo de dato es con el que estamos trabajando como se muestra en los ejemplos.

* Cadena `str`: 
La cadena o tambien llamado string es un conjunto de caracteres, por ejemplo, `a` y `h` son dos caracteres, pero cuando las unimos forman la cadena `ah` 

```
>>> type("hola mundo")
<type 'str'>
```


* Entero `int`: 
Es un numero entero que puede ser positivo o negativo

```
>>> type(1)
<type 'int'>
```


* Flotante `float`: 
Es otra forma de llamar a un numero decimal

```
>>> type(1.2)
<type 'float'>
```


* Complejo `complex`: 
Es un numero complejo. Entiendase que numero complejo es `j es igual a raiz de -1`

```
>>> type(3j)
<type 'complex'>
```


* Entero largo `long`: 
Cuando usamos `int` tenemos un limite del tamaño del numero, con `long` superamos ese limite y podremos usar un numero tan grande como es capaz de soportar nuestro ordenador

```
>>> type(23L)
<type 'long'>
```


* Lista `list`: 
Es un conjunto de elementos, el elemento puede ser cualquier tipo de dato, incluso una lista (una lista dentro de otra lista). La cualidad que tiene es que puede ser modificado (mas delante se explicará con mas detalle)

```
>>> type([1,2,3])
<type 'list'>
```


* Tupla `tuple`: 
Al igual que la lista, es un conjunto de elementos, y tambien elemento puede ser cualquier tipo de dato, con la diferencia de que la tupla no puede modificarse.

```
>>> type((1,2,3))
<type 'tuple'>
```


* Booleano `bool`: 
Es un tipo de dato logico, puede ser `True` o `False`

```
>>> type(True)
<type 'bool'>
```


* Diccionario `dict`: 
Parecido a las listas, con la diferencia que este posee dos partes en cada elemento, la la clave y el valor. Mas delante se explicara con mas detalle

```
>>> type({"ssh":22})
<type 'dict'>
```


# Operadores aritmeticos
El orden de los operadores aritmeticos de mayor prioridad a menor (Una forma rapida de poder aprender esto es con las letras iniciales de cada operacion formar la palabra PAPOMUDAS), es:

* PArentencis
* POtencia
* MUltiplicacion
* Division
* Adicion
* Sustracion 

| Operador | Descripción | Ejemplo |
|---|:---|:---|
| `+` | Suma | `>>> 3 + 2` (resp es 5) |
| `-` | Resta | `>>> 4 - 7` (resp es -3) |
| `-` | Negación | `>>> -7` (resp es -7) |
| `*` | Multiplicación | `>>> 2 * 6` (resp es 12) |
| `**` | Exponente | `>>> 2 ** 6` (resp es 64) |
| `/` | División | `>>> 3.5 / 2` (resp es 1.75) |
| `//` | División entera | `>>> 3.5 // 2` (resp es 1.0) |
| `%` | Módulo | `>>> 7 % 2` (resp es 1) |

# Operadores logicos
`and` y `or` trabajan con dos operandos y retornan un valor lógico basadas en las denominadas tablas de verdad. El operador `not` actúa sobre un operando. Estas tablas de verdad son conocidas y usadas en el contexto de la vida diaria, por ejemplo: "si hace sol Y tengo tiempo, iré a la playa", "si NO hace sol, me quedaré en casa", "si llueve O hace viento, iré al cine"

Operador | Descripción | Ejemplo
|---|:---|:---|
`and` | ¿se cumple a y b? | `>>> True and False` (resp es False)
`or` | ¿se cumple a o b? | `>>> True or False` (resp es True)
`not` | No a | `>>> not True` (resp es False)
 
# Operadores relacionales
Los operadores relacionales se usan para comparar 2 valores y saber si son iguales, distintos, etc

Operadores | Descripción | Ejemplo
|---|:---|:---|
`==` | ¿son iguales a y b? | `>>> 5 == 3` (resp es False)
`!=` | ¿son distintos a y b? | `>>> 5 != 3` (resp es True)
`<` | ¿es a menor que b? | `>>> 5 < 3` (resp es False)
`>` | ¿es a mayor que b? | `>>> 5 > 3` (resp es True)
`<=` | ¿es a menor o igual que b? | `>>> 5 <= 5` (resp es True)
`>=` | ¿es a mayor o igual que b? | `>>> 5 >= 3` (resp es True)
