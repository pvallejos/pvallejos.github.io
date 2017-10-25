---
layout: post
title: Python al dolor Capitulo 3
---

Mi primer programa en Python, que es una Funcion, biblioteca math y sentencias de decision

# Mi primer programa en python
Para crear nuestro primer programa en python necesitamos de un editor de texto (en mi caso prefiero sublime-text pero recomiendo el IDE PyCharms) y la terminal para poder ejecutar nuestros programas. Los programas en python tienen como extencion `.py`. En nuestro editor de texto escribimos y lo guardamos como `holamundo.py`, el `print` sirve para poder mostrar en pantalla algun mensaje:

```python
print "Hola mundo!"
```

Vamos a nuestra terminal y lo ejecutamos colocando primero la palabra python y luego el nombre del archivo:

```
root@vay3t:~# python holamundo.py 
Hola mundo!
```

* `raw_input()` Esta funcion lo que hace es pedir al usuario que ingrese algun dato, pero lo guarda como un `str`. En este caso este script (programa) lo guardaré como `saludo.py` (Lo siguiente escrito se hará en el editor de texto)

```python
nombre = raw_input("Ingrese nombre: ")
print "Hola " + nombre
```

Veamos que es lo que hace el programa:

```
root@vay3t:~# python saludo.py
Ingrese nombre: Vay3t
Hola Vay3t
```

### Ejemplo de programa

Necesitamos un programa que calcule el perimetro y el area de un cuadrado, el lado del cuadrado lo tenemos que ingresar por pantalla. El problema que tenemos es que `raw_input()` guarda la variable como un `str` pero para eso podemos forzar el tipo de variable de la siguiente forma como se muestra en el programa. Para despues imprimir o mostrar la variable en pantalla necesito transformarlo a `str` para luego unirlo con otro `str`, en python no se puede unir 2 tipos de valores distintos. El programa sera guardado como `calcCuadrado.py`:

```python
print "=== Calculadora de Perimetro y Area de un Cuadrado ==="
lado = raw_input("Ingrese lado: ")
area = float(lado) ** 2
perimetro = float(lado) * 4
print "El Area del cuadrado es: " + str(area)
print "El Perimetro del cuadrado es: " + str(perimetro)
```

Salida:

```
root@vay3t:~# python calcCuadrado.py 
=== Calculadora de Perimetro y Area de un Cuadrado ===
Ingrese lado: 4
El Area del cuadrado es: 16.0
El Perimetro del cuadrado es: 16.0
```


# Funciones
Tal y como las calculadoras científicas, Python provee un número de funciones que podemos utilizar. A estas funciones se les llama nativas, built-in en inglés. En el siguiente ejemplo, se muestra el uso de dos funciones nativas: valor absoluto `abs` y potencia `pow`, en el caso de la potencia `pow` tiene la siguiente estructura: `pow(base,exponente)`.

```
>>> abs(2)
2
>>> abs(-2)
2
>>> pow(2, 3)
8
>>> pow(3, 2)
9
```

En posts anteriores conocimos que para Python los números pueden ser de tres tipos, enteros `int`, enteros largos `long`, y números no enteros `float`. Sin embargo, a través de funciones podemos cambiar fácilmente el tipo de número con el que Python trabaja, utilizando las funciones presentadas en la siguiente tabla:

| Nombre | Descripción |
|---|:---|
`int(x)` | Recibe un número y lo convierte a un entero, si el número no puede ser contenido en 4 bits, se guarda como `long`, en caso de recibir un `float`, el resultado se trunca, no se aproxima.
`long(x)` | Recibe un número y lo convierte a un entero largo, (sin importar que pueda ser representado como `int`), en caso de recibir un `float`, el resultado se trunca, no se aproxima.
`float(x)` | Recibe un número y lo convierte a un flotante, en caso de recibir un `float`, el resultado es el mismo `float`.

### Creando nuestra propia funcion
Muchas veces necesitamos alguna funcion, pero esta, no existe en Python, para eso se nos da la facilidad de programar nuestra propia funcion para asi usarla mas adelante. Es un bloque de código que tiene un nombre asociado y ejecuta una serie órdenes retornando un valor, Además puede ser invocado n veces desde el programa

```python
def funcion(argumentos):
	< Codigo >

funcion(argumentos)
```

Viendo un ejemplo mas concreto podremos entender mejor lo que es una funcion. En el ejemplo se ve que se usa la palabra `return`. El `return` es muy parecido al `print` con la diferencia que `return` no imprime en pantalla, sinó que lo guarda para luego usarse mas tarde. Crearemos un script llamado `sumas.py`

```python
def suma(x,y):
	respuesta = x + y
	return respuesta

resultado = suma(3,4)
print resultado
```

Salida:

```
root@vay3t:~# python sumas.py
7
```

# Biblioteca math
Podemos extender la funcionalidad de Python agregándole funciones importadas. Estas no vienen nativamente con el intérprete, sino que se encuentran en bibliotecas para que sean consultadas por él. A estas bibliotecas de Python se les conoce como módulos. Uno de los módulos que nos será de utilidad es `math`, que contiene muchas de las funciones matemáticas y trigonométricas que usamos. La siguiente tabla lista algunas de las funciones que podemos destacar:

Nombre | Descripción
|---|:---|
`sin(x)` | Seno de x, con x expresado en radianes
`cos(x)` | Coseno de x, con x expresado en radianes
`tan(x)` | Tangente de x, con x expresado en radianes
`exp(x)` | Número e elevado a x
`log(x)` | Logaritmo natural (base e) de x
`log10(x)` | Logaritmo en base decimal de x
`sqrt(x)` | Raíz cuadrada de x
`degrees(x)` | Convierte a grados un ángulo x expresado en radianes
`radians(x)` | Convierte a radianes un ángulo x expresado en grados


Probemos en el intérprete de Python la función `sin()`.

```
>>> sin(0)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'sin' is not defined
```

Podemos darnos cuenta que ocurrió un error. Esto fue debido a que no hemos indicado al intérprete que consulte el módulo `math`. Para esto debemos usar la sentencia `import` y en nombre del módulo.

```
>>> import math
>>> math.sin(0)
0.0
>>> sin(0)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'sin' is not defined
```

Podemos notar que a pesar de importar el módulo math ocurrió un error al invocar la función como lo hubiéramos hecho con las funciones nativas. Pero el error no ocurrió cuando especificamos explícitamente el nombre del módulo (separado con un punto del nombre de la función). Esto podemos corregirlo.

```
>>> from math import sin,cos
>>> cos(0)
1.0
>>> sin(0)
0.0
```

Con lo anterior, pudimos importar las funciones seno y coseno, lo que nos permite usarlas escribiendo sólo su nombre y los parámetros actuales correspondientes.

# Estructuras de decision

Las estructuras de control condicionales, son aquellas que nos permiten evaluar si una o más condiciones se cumplen, para decir qué acción vamos a ejecutar. La evaluación de condiciones, solo puede arrojar 1 de 2 resultados: verdadero o falso (`True` o `False`). Un ejemplo que podriamos usar para explicar mejor esto es el siguiente: SI el semaforo está en verde, cruzar la calle. SINO esperar a que esté en verde. Otro ejemplo para usar condiciones es el siguiente: SI tengo hambre Y dinero, comprar comida. 

Las estructuras de control de flujo condicionales, se definen mediante el uso de tres palabras claves reservadas, del lenguaje: `if` (si), `elif` (sino, si) y `else` (sino).

```python
if semaforo == "verde": 
    print "Cruzar la calle"
else: 
    print "Esperar"
```

Otro ejemplo que podriamos revisar es el siguiente, creamos un programa llamado `edades.py`:

```python
edad = 30

if edad <= 13:
	print "Menor"
elif edad > 13 and edad < 18:
	print "Adolecente"
elif edad >= 18 and edad < 30:
	print "Adulto joven"
elif edad >= 30 and edad < 60:
	print "Adulto"
elif edad >= 60:
	print "Adulto mayor"
```

Y en la salida:

```
root@vay3t:~# python edades.py
Adulto
```

# Creando un programa
Antes de crear un programa necesitamos responder una pregunta ¿Que problema resolvera nuestro programa?, en caso de ejemplo necesitamos crear una calculadora en donde se puedan ingresar 2 numeros y resolver operaciones matematicas. Para eso necesitamos diseñar el programa de la siguiente manera, primero creamos las funciones que vamos a usar en el programa. Estas funciones serán las encargadas de realizar el trabajo pesado, las operaciones fundamentales. Luego realizamos un menu de opciones donde sabremos que cosas queremos que haga nuestro programa. Y por ultimo aplicamos las opciones y llamamos las funciones.

```python
#!/usr/bin/python

# Difinir la funcion suma
def suma(x,y):
	respuesta = x + y
	return respuesta

# Difinir la funcion resta
def resta(x,y):
	respuesta = x - y
	return respuesta

# Difinir la funcion multiplicacion
def multiplicacion(x,y):
	respuesta = x * y
	return respuesta

# Difinir la funcion division
def division(x,y):
	respuesta = x / y
	return respuesta

# Menu de programa
print """
========== MENU =========
	a) Sumar
	b) Restar
	c) Multiplicar
	d) dividir
"""

# Entrada para ingresar opcion valida
opcion = raw_input("Elija opcion > ")

# Condicion para elegir la suma
if opcion == "a":
	print ">>> SUMA <<<"
	print ""
	numeroA = float(raw_input("Ingrese numero A "))
	numeroB = float(raw_input("Ingrese numero B "))
	# Operacion suma
	respuesta = suma(numeroA,numeroB)
	print "Respuesta: " , str(respuesta)

# Condicion para elegir la resta
elif opcion == "b":
	print ">>> RESTA <<<"
	print ""
	numeroA = float(raw_input("Ingrese numero A "))
	numeroB = float(raw_input("Ingrese numero B "))
	# Operacion resta
	respuesta = resta(numeroA,numeroB)
	print "Respuesta: " , str(respuesta)

# Condicion para elegir la multiplicacion
elif opcion == "c":
	print ">>> MULTIPLICACION <<<"
	print ""
	numeroA = float(raw_input("Ingrese numero A "))
	numeroB = float(raw_input("Ingrese numero B "))
	# Operacion multiplicacion
	respuesta = multiplicacion(numeroA,numeroB)
	print "Respuesta: " , str(respuesta)

# Condicion para elegir la division
elif opcion = "d":
	print ">>> DIVISION <<<"
	print ""
	numeroA = float(raw_input("Ingrese numero A "))
	numeroB = float(raw_input("Ingrese numero B "))
	# Condicion para que no nos arroje error el programa cuando dividamos por cero
	if numeroB == 0.0:
		print "El numero B no puede ser 0!"
	# En caso de que el numero B no sea 0 proceder con la division
	else:
		# Operacion division
		respuesta = division(numeroA,numeroB)
		print "Respuesta: " , str(respuesta)

# En caso de que ninguna de las opciones anteriores alla sido valida
# se realizará el else
else:
	print "Ingrese opcion valida"
```
