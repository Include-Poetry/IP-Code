---
layout: G-Article
title: Contenedor queue
author: rivel_co
tags: [STL, Cola]
Hide_Tags: true
categories: [C++, OMI]
---

La clase `queue` es un contenedor que brinda la usabilidad de una estructura FIFO.

{: #ListaContenido}
- Funcionamiento
- Eficiencia
- Funciones miembro
- Funciones no miembro
- Ejemplo general

## Funcionamiento

*FIFO* es el acrónimo de las palabras en inglés *First In First Out*, que podemos traducir como *El primero en entrar, es el primero en salir*. A este tipo de estructura se le conoce en español como *cola*, pues su funcionamiento es precisamente como cuando hacemos *cola* o *fila* en algún lugar, por ejemplo, la que hacemos en la caja registradora del supermercado.

Si aún no te queda muy claro, cuando hacemos una cola, estamos *metiendo* datos a una estructura, todos los datos son ingresados uno detrás del otro en el orden que van llegando, cuando queremos sacar uno, sacamos el que está hasta el frente, es decir, el primero que llegó.

## Eficiencia

Ingresar un elemento | constante | $$ O(l) $$
Eliminar un elemento | constante | $$ O(l) $$

## Funciones miembro

| Función			| Definición															|
|:------------------|:----------------------------------------------------------------------|
| (constructor)		| Construye un contenedor `queue`, es lo que nos permite *declararlo*.	|
| (destructor)		| Destruye el `queue`														|
| Operador `=`		| Asigna valores al contenedor											|
|                                 **Acceso a elementos**                                    |
| `front`			| Accede al primer elemento del contenedor								|
| `back`			| Accede al último elemento del contenedor								|
|                                     **Capacidad**                                         |
| `empty`			| Checa si el contenedor está vacío										|
| `size`			| Regresa el número de elementos en el contenedor						|
|                                   **Modificadores**                                       |
| `push` 			| Inserta un elemento al final del contenedor 							|
| `pop`				| Elimina el primer elemento del contenedor 							|
| `swap` 			| Intercambia el contenido de dos contenedores 							|

## Funciones no miembro

| Función           | Definición                                                            |
|:------------------|:----------------------------------------------------------------------|
| Operadores `==`, `!=`, `<`, `<=`, `>`, `>=` | Compara lexicográficamente los valores del contenedor |

## Ejemplo general

<textarea class="editor">
#include &lt;iostream&gt;
#include &lt;queue&gt; // Libreria
using namespace std;

int main(){

	queue&lt;int&gt; cola;
	// Declaración de cola para elementos tipo 'int'

	cola.push(3);
	cola.push(14);
	cola.push(97);
	// Se ingresan datos

	cout << cola.front() << '\n';
	// Se muestra el primer elemento de la cola

	cout << cola.back() << '\n';
	// Se muestra el último elemento de la cola

	cout << cola.size() << '\n';
	// Se obtiene la cantidad de elementos almacenados

	cola.pop();
	// Se elimina el primer elemento de la estructura

	if (cola.empty()){
		// Se checa si la estructura está vacía
		cout << "La estructura esta vacia\n";
	} else {
		cout << "La estructura no esta vacia\n";
	}

	queue&lt;int&gt; otra;
	otra.push(32);
	otra.push(12);
	otra.push(1);

	cola.swap(otra);
	// Se intercambian contenidos

	cout << cola.size() << " " << otra.size() << '\n';
	
	return 0;
}</textarea>

<textarea class="output">
/* Salida */
3
97
3
La estructura no esta vacia
3 2</textarea>

<div class="Nav">
	<a href="{{ site.baseurl }}/C++/STL/String/">Tema anterior</a> | <a href="{{ site.baseurl }}/C++/STL/Stack/">Tema siguiente</a>
</div>