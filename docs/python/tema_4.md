# TEMA 4

## LISTAS

Una lista es una secuencia mutable, ordenada de elementos duplicados.  
Puede almacenar muchos tiposde datos  

**CREAR**  
Podemos crear listas con `lista = []` o con `lista = list()`  

**FUNCIONES**  
Podemos saber el tamaño de una lista con `len(lista)`  
Podemos acceder usando `lista[n]`  
También, podemos cortar una lista con `lista[start:end]`

- Ejemplo:

~~~python
lista = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

lista[:] # Devuelve todos los elementos de la lista
print(lista[2:6]) # Devuelve los elementos desde el índice 2 al 5
print(lista[:6]) # Devuelve desde el primer elemento hasta el índice 5
print(lista[::2]) # Devuelve desde el primer hasta el último de dos en dos
print(lista[-3:]) # Devuelve desde el índice -3 hasta el final
print(lista[::-1]) # Devuelve la lista en orden inverso
~~~

**MANIPULAR LISTAS**  
Añadir elementos al final > `lista.append(element)`  
Añadir en una posición específica > `lista.insert(n,element)`  
Modificar elementos > `lista[n] = "new_element"`  
Eliminar un elemento > `del lista[n]`  
Eliminar elementos (slicing) > `del lista[start:end]`  
Eliminar último elemento > `lista.pop()`  
Eliminar según su valor > `lista.remove(dato)`  
Eliminar todos los elementos > `lista.clear()`  

**RECORRER**  

- Recorrer listas únicas:  

~~~python
for e in lista:
    print(e)

for i in range(len(lista)):
    print(lista[i])
~~~

- Recorrer 2 listas a la vez con `zip()`  

~~~python
compra = ['Agua', 'Aceite', 'Arroz']
detalles = ['mineral natural', 'de oliva virgen', 'basmati']

for producto, detalle in zip(compra, detalles):
    print(producto, detalle)
~~~

- Encontrar un índice de un valor:

~~~python
lista = ['banana', 'orange', 'mango', 'lemon']
print(lista.index('orange')) #1
~~~

- Comprobar si un valor está en la lista

~~~python
lista = ['banana', 'orange', 'mango', 'lemon']

if 'banana' not in lista:
    print('No, banana no está en la lista!')
else:
    print('Si, banana si está en la lista!')
~~~  

**FUNCIONES DE LISTAS**  
`lista.sort()` > Ordena esa lista.  
`lista2 = sorted(lista)` > Crea una nueva lista ordenada (Conserva ambas).  
`lista =lista1 + lista 2` > Crea una nueva lista de la unificación (Conserva todas).  
`lista1.extend(lista2)` > Modifica la primera lista además de conservar la segunda.  
`lista2 = lista.copy()` > Crea una copia.  
`lista.reverse()` > Invierte la lista modificandola.
`lista2 = lista[::-1]` > Crea una nueva lista invertida (Conserva ambas).  
`lista2 = list(reserved(lista1))` > Crea una nueva lista invertida (Conserva ambas)  
`lista.count(valor)` > Cuenta cuantas veces aparece cierto valor en una lista.  
`lista2 = lista.split(',')` > Transforma una cadena a lista usando un separador.  
`lista2 = lista.rsplit(',')` > Transforma una cadena a lista usando un separador desde la derecha.  
`'separador'.join(lista)` > Transforma una lista a cadena.  

- También se pueden aplicar funciones matemáticas a las listas si solo contienen números.  
- Las listas se comparan elemento por elemento  

**COMPRESIONES DE LISTA**
Me dio mucha pereza ver esto

**LISTAS MULTIDIMENSIONALES**  
Son listas dentro de otras listas y se accede con `for`

~~~python
for fila in tabla:
    for elemento in fila:
        print(elememento,end=" ")
    print()
~~~

## RANGOS

Secuencia inmutable de números enteros en sucesión aritmética.  
Su estructura es `range (inicio,fin,paso)` siendo `inicio` y `paso` opcionales.  
Podemos obtener su longiud con `len(range())` que mostrara la longitud del rango.  
Podemos convertilos en listas `lista(range(i,f,p))`  
Se puede usar para recorrer listas.  

**FUNCIONES**  
`n in (range(i,f,p))`  > Comprueba si un número esta en el rango.  
`max(range())` > Encuentra el número máximo.  
`min(range(i,f,p))` > Encuentra el número mínimo.  
`sorted(range(i,f,p))` > Ordena de menor a mayor.  
`sorted(range(i,f,-1))`> Ordena de mayor a menor.  

**ATRIBUTOS**  
Al ser un objeto con podemos:
`rango.start` > Indica el valor del inicio.  
`rango.stop` > Indica el valor del final.  
`rango.step` > Indica el valor del paso.  

## TUPLAS

`tupla = ()` > Crear tupla.  
`tupla = tuple(lista)` > Convierte una tupla a lista.  
`tupla[0]` > Acceso al primer elemento.  
`tupla[-1]` > Acceso al último elemento.  
`len(tupla)` > Longitud de la tupla.  
`tupla.index(valor)` > Muestra el índice de ese valor.  
`lista = list(tupla)` > Transforma una tupla a lista.
`sorted(tuplla)` > Crea una tupla ordenada (Conserva ambas).  
`tupla3 = tupla1 + tupla2` > Crea una tupla de una unificación (Conserva todas).  
`copia = tupla` > Crea una copia de la tupla.  
`tupla.count(valor)` > Obtienes la cantidad de veces que se repite ese valor.  
`tupla2 = tupla.split(',')` > Transforma una cadena a tupla usando un separador.  
`tupla2 = tupla.rsplit(',')` > Transforma una cadena a tupla usando un separador desde la derecha.  
`'separador'.join(tupla)` > Transforma una tupla a cadena.  

- No se puede añadir, elminar o modifcar elementos de una tupla.  
- Se puede usar `not in` y `in` con tuplas.  
- Tuplas de números puedes usar funciones matemáticas.  
- Puedes pasar los valores de la tupla variables con la asignación múltiple.  
  - Es posible también indicar que el inicio y final sean de un elemento y el centro de varios  
  `inicio, *general, fin = tupla`  
  - Aunque es muy versatil, pudiendo usar el `*` según la necesidad.  

**SLICING**  

~~~python
tupla = (0, 1, 2, 3, 4, 5, 6, 7, 8, 9)

tupla[:] # Devuelve todos los elementos de la tupla

print(tupla[2:6]) # Devuelve los elementos desde el índice 2 al 5

print(tupla[:6]) # Devuelve desde el primer elemento hasta el índice 5

print(tupla[::2]) # Devuelve desde el primer hasta el último de dos en dos

print(tupla[-3:]) # Devuelve desde el índice -3 hasta el final

print(tupla[::-1]) # Devuelve la tupla en orden inverso
~~~~  

**RECORRER**  

- Recorrer una única tupla.  

~~~python
tupla = ('banana', 'orange', 'mango', 'lemon')
for e in tupla:
print(e)
~~~~  

- Recorrer varias tuplas a la vez usando `zip()`

~~~python
compra = ('Agua', 'Aceite', 'Arroz')
detalles = ('mineral natural', 'de oliva virgen', 'basmati')
for producto, detalle in zip(compra, detalles):
print(producto, detalle)
~~~~  

**TUPLAS MULTIDIMENSIONALES**  

~~~python
tabla = ((1,2,3),(4,5,6),(7,8,9))

print(tabla[0][0]) # Acceso

for fila in tabla:
    for elemento in fila:
        print(elemento,end=" ")
    print()
~~~

~~~python
tupla=(((1,2,3),(1,2,3),(1,2,3)),(1,2,3),(1,2,3),(1,2,3)),((1,2,3),(1,2,3),
(1,2,3))

for i in range(len(tupla)):
    for j in range(len(tupla[i])):
        for k in range(len(tupla[i][j])):
            print(tupla[i][j][k], end=" ")
        print()
    print()
~~~

## CONJUNTOS

Un conjunto es una sencuencia mutable, que alamacena objetos únicos  
sus elementos son inmutables y no importa el orden de los elementos.  

**FUNCIONES**  
`conjunto = {valores}` > Crea un conjunto.  
`conjunto = set([valores])` > Crea un conjunto.  
`lent(conjunto)` > Obtenemos la longitud del conjunto.  
`conjunto.add(valor)` > Añadimos un elemento al conjunto.  
`conjunto.remove(valor)` > Elimina un elemento del conjunto, si no existe da error.  
`conjunto.discard(valor)` > Elimina un elemento del conjunto, no da error.  
`conjunto.pop()` > Elimina un elemento aleatoriamente.  
`conjunto.clear()` > Elimina todos los elementos.  
`conjunto.sorted()` > Retorna una lista ordenada, no modifca el conjunto.
`cojunto2 = conjunto.cpy()` > Crea un copia del conjunto.  

- No se puede acceder a un elemento concreto.  
- No se puede modificar un elemento concreto.  
- Podemos usar `in` en los conjuntos.  
- Podemos pasarlo a cadena de texto.
- Podemos usar funciones matemáticas.

**RECORRER**  

- Recorrer un único conjunto

~~~python
conjunto = {'banana', 'orange', 'mango', 'lemon'}

for e in conjunto:
    print(e)
~~~

**TEORÍA DE CONJUNTOS**  

~~~python
A = {1, 3, 3, 4}
B = {1, 2, 8, 9}

print(A & B) #Unión (Todos)
print(A | B) #Intersección (Comunes)
print(A - B) #Diferencia (Elementos de A que no estén en B)
print(A ^ B) # Elementos no cumunes de A y B

print(A.union(B))
print(A.intersection(B))
print(A.difference(B))
print(A.symmetric_difference(B))
~~~

## DICCIONARIOS

Son colecciones de pares tipo clave-valor desordenado y mutable.  
Las claves son únicas e inmutables puede ser un `int`, `float` o `string`  
Los valores pueden ser objetos de tipos diferentes.  
Son mutables asi que se puede añadir, borrar y modficar elementos.  

**FUCIONES**  
`diccionario = {}` > Crear un diccionario.  
`diccionario = dict{key1="value1", }` > Crear un diccionario.  
`diccionario[key] = element` > Añade elementos al diccionario.  
`diccionario[key]` > Accede al valor del diccionario (Puede haber error).  
`diccionario.get(key)` > Accede al valor del diccionario (Nunca da error).  
`"key" in diccionario` > Verifica si la clave pertenece al diccionario.  
`len(diccionario)` > Longitud del diccionario.  
`diccionario.keys()` > Devuelve una lista con las keys.  
`diccionario.values()` > Devuelve una lista con los valores.
`diccionario.items()` > Devuelve clave y valor en forma de tupla.  
`del diccionario[key]` > Elimina un elemento del diccionario (Por su clave).  
`diccionario.pop(clave)` > Elimina un elemento del diccionario (Por su clave).  
`diccionario.clear` > Elimina todos los elementos.  
`dicc1 = dicc2 | dicc3` > Crea un nuevo diccionario de la unión de otros 2.  
`dicc1.update(dicc2)` > El primer diccionario se actualiza con la información del segundo.  
`dicc2 = dicc1.copy()` > Crear una copia del diccionario.  

**RECORRER**  

- Claves

~~~python
for clave in persona:
    print(clave)
~~~
  
- Valores

~~~python
for valor in persona.values():
    print(valor)
~~~

- Claves y valores

~~~python
for clave, valor in persona.items():
    print(clave, ":", valor)
~~~
