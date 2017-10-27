---
layout: post
title: Python al dolor Capitulo 2
categories: Python
---

Colecciones en Python: Listas, Tuplas, Diccionarios y Conjuntos.

# Listas
Una lista es un conjunto de elementos, estos elementos estan ordenados desde el `0` hasta `n-1` donde `n` es la cantidad total de elementos que tiene una lista. Estos elementos pueden pertenecer a cualquier tipo de dato. En el ejemplo se muestra primero la posicion `pos` y la lista respectivamente (el numero 1 esta en la pocision 0 y asi)

```
>>> # pos    0 1 2 3 4 5 6 7 8
>>> lista = [1,2,3,4,5,6,7,8,9]
```

* `range(k)`
Crea una lista de 0 al numero anterior a `k` (es decir `k-1`) donde `k` es un numero entero. Concidentemente `k` es la cantidad de elementos que hay en la lista creada con range. tambien range es posible usarlo con numero de inicio hasta el numero `k-1`

```
>>> range(9)
[0, 1, 2, 3, 4, 5, 6, 7, 8]
>>> range(1,10)
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Tuplas
Una tupla es igual que una lista con la ligera diferencia que la tupla no puede ser modificada.

```
>>> tupla = (1,2,3,4,5)
```

### Anexos sobre listas y tuplas

* `L[k]` Accede a un elemento especifico de la lista o tupla segun la posicion `k`.En las listas es posible cambiarle un valor a la pocision usando `L[k] = value` donde `k` no puede ser mayor a la cantidad total menos 1 (`n-1`)

```
>>> lista = ["uno","tres","cuatro","cinco"]
>>> lista[2]
'cuatro'
>>> lista[3] = "seis"
>>> lista
['uno', 'tres', 'cuatro', 'seis']
>>> tupla = ("tres","dos","uno")
>>> tupla[2]
'uno'
```

* Conversion de tipos: Una variabla declarada como tupla puede ser convertida a lista y viceversa como se muestra en el ejemplo

```
>>> tupla = (1,2,3,4,5)
>>> tupla
(1, 2, 3, 4, 5)
>>> list(tupla)
[1, 2, 3, 4, 5]
>>> lista = [1,2,3,4,5]
>>> tuple(lista)
(1, 2, 3, 4, 5)
```

* Concatenacion simple: Usando el signo suma `+` se puede unir dos listas o tuplas

```
>>> lista1 = [1,2,3,4]
>>> lista2 = [5,6,7,8]
>>> lista1 + lista2
[1, 2, 3, 4, 5, 6, 7, 8]
>>> tupla1 = (1,2,3)
>>> tupla2 = (4,5,6)
>>> tupla1 + tupla2
(1, 2, 3, 4, 5, 6)
```

* Maximos y minimos: Tambien se pueden obtener los valores maximos y minimos de una lista o tupla

```
>>> lista = [6,4,3,7]
>>> max(lista)
7
>>> min(lista)
3
>>> tupla = (5,4,3,7,8)
>>> max(tupla)
8
>>> min(tupla)
3
```

* Contar elementos: Al igual que con los strings se pueden contar la cantidad de elementos que tiene una lista o tupla

```
>>> lista = ["hola",34,54,3.2,True]
>>> len(lista)
5
>>> tupla = ("adios",False,200,1.9)
>>> len(tupla)
4
```

### Metodos de la lista
Estos metodos son exclusivo de las listas. (no de las tuplas)

* `L.append(k)`
Añade el elemento `k` al final de la lista.

```
>>> lista = [1,2,3,4,5,6,7,8,9]
>>> lista.append(6)
>>> lista
[1, 2, 3, 4, 5, 6, 7, 8, 9, 6]
```


* `L.count(value)`
Muestra la cantidad de veces que se encontró value en la lista.

```
>>> lista = [1,2,3,4,5,6,7,8,9,6]
>>> lista.count(6)
2
```


* `L.extend(iterable)`
Añade los elementos del iterable (una lista) a la lista original.

```
>>> lista = [1,2,3,4,5,6,7,8,9,6]
>>> lista.extend([4,5])
>>> lista
[1, 2, 3, 4, 5, 6, 7, 8, 9, 6, 4, 5]
```


* `L.index(value)`
Indica la posición en la que se encontró la primera ocurrencia del valor `value`.

```
>>> # pos    0 1 2 3 4 5 6
>>> lista = [4,5,3,7,6,8,9]
>>> lista.index(6)
4
```


* `L.insert(index, elemento)`
Inserta el elemento en la posición index.

```
>>> lista = ["uno","tres","cuatro","cinco"]
>>> lista.insert(1,"dos")
>>> lista
['uno', 'dos', 'tres', 'cuatro', 'cinco']
```


* `L.pop([index])`
Muestra el valor en la posición index y lo elimina de la lista. Si no se especifica la posición, se utiliza el último elemento de la lista.

```
>>> lista = ["hola","mundo",5,3,"wifi",True]
>>> lista.pop(1)
'mundo'
>>> lista
['hola', 5, 3, 'wifi', True]
>>> lista.pop()
True
>>> lista
['hola', 5, 3, 'wifi']
```


* `L.remove(value)`
Eliminar la primera ocurrencia de value en la lista.

```
>>> lista = [1,2,3,4,5,6,7,8,9,6]
>>> lista.remove(6)
>>> lista
[1, 2, 3, 4, 5, 7, 8, 9, 6]
```


* `L.reverse()`
Invierte la lista. Esta función trabaja sobre la propia lista desde la que se invoca el método, no sobre una copia.

```
>>> lista = range(1,10)
>>> lista.reverse()
>>> lista
[9, 8, 7, 6, 5, 4, 3, 2, 1]
```


* `L.sort()`
Ordena la lista de menor a mayor.

```
>>> lista = [7,3,5,2,9,0]
>>> lista.sort()
>>> lista
[0, 2, 3, 5, 7, 9]
```


# Diccionarios
Parecido a las listas, con la leve diferencia que en cada elemento tiene 2 partes, una es la clave y la otra es el valor `D["clave":valor]`. Aca vemos un ejemplo de un diccionario donde sus claves son nombres de servicios y sus valores el numero de puerto.

```
>>> dictionary = {"ftp":21,"ssh":22,"http":80,"https":443}
```

### Metodos del diccionario


* `D.get(k)`
Busca el valor de la clave `k` en el diccionario. Es equivalente a utilizar `D[k]` pero al utilizar este método podemos indicar un valor a devolver por defecto si no se encuentra la clave, mientras que con la sintaxis `D[k]` , de no existir la clave se lanzaría una excepción.

```
>>> dictionary = {"ftp":21,"ssh":22,"http":80,"https":443}
>>> dictionary["ftp"]
21
>>> dictionary.get("asd")
>>> dictionary.get("http")
80
```


* `D.has_key(k)`
Comprueba si el diccionario tiene la clave `k`. Es equivalente a la sintaxis `k in D`.

```
>>> dictionary = {"ftp":21,"ssh":22,"http":80,"https":443}
>>> "https" in dictionary
True
>>> dictionary.has_key("https")
True
```


* `D.items()`
Muestra una lista de tuplas con pares clave-valor.

```
>>> dictionary = {"ftp":21,"ssh":22,"http":80,"https":443}
>>> dictionary.items()
[('ftp', 21), ('http', 80), ('ssh', 22), ('https', 443)]
```


* `D.pop(k)`
Borra la clave `k` del diccionario y muestra su valor.

```
>>> dictionary = {"ftp":21,"ssh":22,"http":80,"https":443}
>>> dictionary.pop("ftp")
21
>>> dictionary
{'http': 80, 'ssh': 22, 'https': 443}
```


* `D.keys()`
Muestra una lista de las claves del diccionario.

```
>>> dictionary = {"ftp":21,"ssh":22,"http":80,"https":443}
>>> dictionary.keys()
['ftp', 'http', 'ssh', 'https']
```


* `D.values()`
Muestra una lista de los valores del diccionario.

```
>>> dictionary = {"ftp":21,"ssh":22,"http":80,"https":443}
>>> dictionary.values()
[21, 80, 22, 443]
```


# Conjuntos
Python también dispone de conjuntos en forma nativa. Aquí “conjunto” se ha de entender como en su definición matemática: un grupo finito y sin orden de elementos únicos (no pueden existir dos elementos iguales en un conjunto). En Python se agrega otra restricción: los elementos deben ser además inmutables (no se pueden cambiar). Lo que hace le metodo `set()` es transformar una lista o tupla en un conjunto.

```
>>> cjto = set((1, 5, 0, 9, 3, 0, 2, 1))
>>> print cjto
set([0, 1, 2, 3, 5, 9])
```

### Metodos del conjunto

* `C.add(k)` Agrega un elemento al conjunto

```
>>> cjto = set((1, 5, 0, 9, 3, 0, 2, 1))
>>> cjto
set([0, 1, 2, 3, 5, 9])
>>> cjto.add(10)
>>> cjto
set([0, 1, 2, 3, 5, 9, 10])
```

* `C.discard(k)` Elimina un elemento del conjunto

```
>>> cjto = set((1, 5, 0, 9, 3, 0, 2, 1))
>>> cjto
set([0, 1, 2, 3, 5, 9])
>>> cjto.discard(9)
>>> cjto
set([0, 1, 2, 3, 5])
```

* `C1.union(C2)` Une 2 conjuntos

```
>>> cjto1 = set([1,2,3,4])
>>> cjto2 = set([3,4,5,6])
>>> cjto1.union(cjto2)
set([1, 2, 3, 4, 5, 6])
```

* `C1.intersection(C2)` Es el conjunto de elementos que estan en ambos conjuntos

```
>>> cjto1 = set([1,2,3,4])
>>> cjto2 = set([3,4,5,6])
>>> cjto1.intersection(cjto2)
set([3, 4])
```

* `C1.difference(C2)` Es el conjunto de elementos que pertenecen a C1 pero que no pertenezca ningun elemento del conjunto C2

```
>>> cjto1 = set([1,2,3,4])
>>> cjto2 = set([3,4,5,6])
>>> cjto1.difference(cjto2)
set([1, 2])
>>> cjto2.difference(cjto1)
set([5, 6])
```


* `C1.symmetric_difference(C2)` Es el conjunto de elementos que están en C1 o C2, pero no en ambos.

```
>>> cjto1 = set([1,2,3,4])
>>> cjto2 = set([3,4,5,6])
>>> cjto1.symmetric_difference(cjto2)
set([1, 2, 5, 6])
```
