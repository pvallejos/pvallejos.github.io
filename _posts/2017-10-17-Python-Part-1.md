---
layout: post
title: Python al dolor cap 1
---

Introduccion a Python

# Antes de comenzar
La serie de Python al dolor ofrece la ayuda y la enseñanza necesaria en poco tiempo para poder dominar uno de los lenguajes de scripting mas usados en la actualidad. 

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

```root@vay3t:~# python
Python 2.7.12 (default, Nov 19 2016, 06:48:10) 
[GCC 5.4.0 20160609] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> ```

# Tipos de datos
Tenemos varios tipos de datos como: cadenas, enteros, flotantes, complejos, enteros largo, listas, tuplas, booleanos y diccionarios. Con el metodo `type` se puede saber que tipo de dato es con el que estamos trabajando como se muestra en el ejemplo.

```
root@vay3t:~# python
Python 2.7.12 (default, Nov 19 2016, 06:48:10) 
[GCC 5.4.0 20160609] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> type("hola mundo")
<type 'str'>
>>> type(1)
<type 'int'>
>>> type(1.2)
<type 'float'>
>>> type(3j)
<type 'complex'>
>>> type(23L)
<type 'long'>
>>> type([1,2,3])
<type 'list'>
>>> type((1,2,3))
<type 'tuple'>
>>> type(True)
<type 'bool'>
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
| "+" | Suma | r = 3 + 2 # r es 5 |
| "-" | Resta | r = 4 - 7 # r es -3 |
| "-" | Negación | r = -7 # r es -7 |
| "*" | Multiplicación | r = 2 * 6 # r es 12 |
| "**" | Exponente | r = 2 ** 6 # r es 64 |
| "/" | División | r = 3.5 / 2 # r es 1.75 |
| "//" | División entera | r = 3.5 // 2 # r es 1.0 |
| "%" | Módulo | r = 7 % 2 # r es 1 |

# Operadores logicos

Operador | Descripción | Ejemplo
|---|:---|:---|
"and" | ¿se cumple a y b? | r = True and False # r es False
"or" | ¿se cumple a o b? | r = True or False # r es True
"not" | No a | r = not True # r es False
 
# Operadores relacionales
Los operadores relacionales se usan para comparar 2 valores y saber si son iguales, distintos, etc

Operadores | Descripción | Ejemplo
|---|:---|:---|
"==" | ¿son iguales a y b? | r = 5 == 3 # r es False
"!=" | ¿son distintos a y b? | r = 5 != 3 # r es True
"<" | ¿es a menor que b? | r = 5 < 3 # r es False
">" | ¿es a mayor que b? | r = 5 > 3 # r es True
"<=" | ¿es a menor o igual que b? | r = 5 <= 5 # r es True
">=" | ¿es a mayor o igual que b? | r = 5 >= 3 # r es True
