---
layout: post
title: Python al dolor Capitulo 2
---

Listas y Diccionarios en Python.

# Listas
Una lista es un conjunto de elementos, estos elementos estan ordenados desde el `0` hasta `n-1` donde `n` es la cantidad total de elementos que tiene una lista. Estos elementos pueden pertenecer a cualquier tipo de dato.

```
>>> # pos    0 1 2 3 4 5 6 7 8
>>> lista = [1,2,3,4,5,6,7,8,9]

```

* `range(k)`
Crea una lista de 0 al numero anterior a `k` (`k-1`) donde `k` es un numero entero. Concidentemente `k` es la cantidad de elementos que hay en la lista creada con range. tambien range es posible usarlo con numero de inicio hasta el numero `k-1`

```
>>> range(9)
[0, 1, 2, 3, 4, 5, 6, 7, 8]
>>> range(1,10)
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Metodos de la lista

* `L.append(elemento)`
Añade un elemento al final de la lista.

```
>>> lista = [1,2,3,4,5,6,7,8,9]
>>> lista.append(6)
>>> lista
[1, 2, 3, 4, 5, 6, 7, 8, 9, 6]
```

* `L.count(value)`
Devuelve el número de veces que se encontró value en la lista.

```
>>> lista = [1,2,3,4,5,6,7,8,9,6]
>>> lista.count(6)
2
```

* `L.extend(iterable)`
Añade los elementos del iterable (una lista) a la lista.

```
>>> lista = [1,2,3,4,5,6,7,8,9,6]
>>> lista.extend([4,5])
>>> lista
[1, 2, 3, 4, 5, 6, 7, 8, 9, 6, 4, 5]
```

* `L.index(value)`
Devuelve la posición en la que se encontró la primera ocurrencia del valor.

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
Devuelve el valor en la posición index y lo elimina de la lista. Si no se especifica la posición, se utiliza el último elemento de la lista.

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

```
>>> dictionary = {"ftp":21,"ssh":22,"http":80,"https":443}
```

### Metodos del diccionario

* `D.get(k)`
Busca el valor de la clave `k` en el diccionario. Es equivalente a utilizar `D[k]` pero al utilizar este método podemos indicar un valor a devolver por defecto si no se encuentra la clave, mientras que con la sintaxis `D[k]` , de no existir la clave se lanzaría una excepción.

```
>>> dictionary["ftp"]
21
>>> dictionary["asd"]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'asd'
>>> dictionary.get("asd")
>>> dictionary.get("http")
80
```

* `D.has_key(k)`
Comprueba si el diccionario tiene la clave `k`. Es equivalente a la sintaxis `k in D`.

```
>>> "https" in dictionary
True
>>> dictionary.has_key("https")
True
```

* `D.items()`
Devuelve una lista de tuplas con pares clave-valor.

```
>>> dictionary.items()
[('ftp', 21), ('http', 80), ('ssh', 22), ('https', 443)]
```

* `D.keys()`
Devuelve una lista de las claves del diccionario.

```
>>> dictionary.keys()
['ftp', 'http', 'ssh', 'https']
```

* `D.pop(k)`
Borra la clave `k` del diccionario y devuelve su valor.

```
>>> dictionary = {"ftp":21,"ssh":22,"http":80,"https":443}
>>> dictionary.pop("ftp")
21
>>> dictionary
{'http': 80, 'ssh': 22, 'https': 443}
```

* `D.values()`
Devuelve una lista de los valores del diccionario.

```
>>> dictionary.values()
[21, 80, 22, 443]
```
