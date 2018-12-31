---
layout: G-Article
title: Contenedor list
author: rivel_co
tags: [STL, Listas]
Hide_Tags: true
olimpiada: [OMI]
subject: [C++]
---

La clase `list` es un contenedor que soporta la inserción y eliminación de elementos desde cualquier parte del mismo.

{: #ListaContenido}
- Funcionamiento
- Eficiencia
- Funciones miembro
- Funciones no miembro

## Funcionamiento

Imagina un elemento `list` como un vector, pero que se pueden insertar y remover elementos de cualquier parte del contenedor en un tiempo muy eficiente.

Sin embargo, la desventaja de esta estructura, es que aunque es muy rentable en tiempo, es más costosa en memoria.

## Eficiencia

Insertar o remover un elemento | constante | $$ O(l) $$

## Funciones miembro

| Función			| Definición															|
|:------------------|:----------------------------------------------------------------------|
| (constructor)		| Construye un contenedor `list`, es lo que nos permite *declararlo*.	|
| (destructor)		| Destruye el `list`														|
| Operador `=`		| Asigna valores al contenedor											|
| `get_allocator`	| Regresa el asignador asociado											|
|                                 **Acceso a elementos**                                    |
| `front`			| Accede al primer elemento del contenedor								|
| `back`			| Accede al último elemento del contenedor								|
|                                     **Iteradores**                                        |
| `begin` `cbegin`	| Devuelve un iterador al principio del contenedor 						|
| `end` `cend`		| Devuelve un iterador al final del contenedor 							|
| `rbegin` `crbegin`| Devuelve un iterador reverso al principio del contenedor 				|
| `rend` `crend`	| Devuelve un iterador reverso al final del contenedor 					|
|                                     **Capacidad**                                         |
| `empty`			| Checa si el contenedor está vacío										|
| `size`			| Regresa el número de elementos en el contenedor						|
| `max_size`		| Regresa el máximo número posible de elementos							|
|                                   **Modificadores**                                       |
| `clear`			| Limpia el contenido del contenedor									|
| `insert`			| Inserta elementos en el contenedor									|
| `erase`			| Borra elementos														|
| `push_back`		| Agrega un elemento al final del contenedor							|
| `pop_back`		| Quita el último elemento del contenedor								|
| `push_front`		| Agrega un elemento al principio del contenedor						|
| `pop_front`		| Quita el primer elemento del contenedor								|
| `resize`			| Cambia la cantidad de elementos almacenados							|
| `swap`			| Intercambia el contenido												|
|                                    **Operaciones**                                        |
| `merge` 			| Mezcla dos listas ordenadas 											|
| `splice` 			| Mueve elementos de otra lista 										|
| `remove` `remove_if` | Elimina elementos que cumplan con cierto criterio 					|
| `reverse` 		| Invierte el orden de los elementos 									|
| `unique` 			| Remueve elementos duplicados consecutivos 							|
| `sort` 			| Ordena los elementos 													|

## Funciones no miembro

| Función           | Definición                                                            |
|:------------------|:----------------------------------------------------------------------|
| Operadores `==`, `!=`, `<`, `<=`, `>`, `>=` | Compara lexicográficamente los valores del contenedor |

<div class="Nav">
	<a href="{{ site.baseurl }}/C++/Estructuras/STL/Stack/" title="Stack STL &vert; #iP Code">Tema anterior</a> | <a href="{{ site.baseurl }}/C++/Estructuras/STL/Pair/" title="Pair STL &vert; #iP Code">Tema siguiente</a>
</div>