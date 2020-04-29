---
layout: G-Article
title: Contenedor stack
date: 2020-01-04 12:00:00
author: rivel_co
tags: [STL, Pila]
hide_tags: true
olimpiada: [OMI]
subject: [C++]
prevTopic: "Queue en STL, /C++/Estructuras/STL/Queue/"
nextTopic: "List en STL, /C++/Estructuras/STL/List/"
---

La clase `stack` es un contenedor que brinda la usabilidad de una estructura FILO.

{: #ListaContenido}
- Funcionamiento
- Eficiencia
- Funciones miembro
- Funciones no miembro
- Ejemplo general

## Funcionamiento

*FILO* es un acrónimo de las palabras en inglés *First In, Last Out*, que podemos traducir como *El primero en entrar, es el primero en salir*. En español a esta estructura se le conoce *pila*.

Para visualizarlo mejor podemos pensar en una pila de platos, es decir, una serie de elementos *apilados*. Cuando ponemos un elemento lo ponemos sobre el anterior, y así sucesivamente. Cuando quitamos uno, quitamos el que está hasta arriba, por lo que el último que quitaremos sería el primero que pusimos.

## Eficiencia

Ingresar un elemento | constante | $$ O(l) $$
Eliminar un elemento | constante | $$ O(l) $$

## Funciones miembro

| Función			| Definición															|
|:------------------|:----------------------------------------------------------------------|
| (constructor)		| Construye un elemento tipo `stack`									|
| (destructor)		| Destruye un elemento tipo `stack`										|
| Operador `=`		| Asigna valores al contenedor											|
|                                 **Acceso a elementos**                                    |
| `top`				| Accede al elemento que está al final, es decir, el último en ingresar |
|                                     **Capacidad**                                         |
| `empty`			| Checa si el contenedor está vacío										|
| `size`			| Regresa el número de elementos en el contenedor						|
|                                   **Modificadores**                                       |
| `push`			| Inserta un elemento al inicio del contenedor 							|
| `pop`				| Elimina el primer elemento del contenedor 							|
| `swap`			| Intercambia el contenido de dos contenedores							|

## Funciones no miembro

| Función           | Definición                                                            |
|:------------------|:----------------------------------------------------------------------|
| Operadores `==`, `!=`, `<`, `<=`, `>`, `>=` | Compara lexicográficamente los valores del contenedor |

## Ejemplo general

<textarea class="cpp">
#include &lt;iostream&gt;
#include &lt;stack&gt; // Libreria
using namespace std;

int main(){

	stack&lt;int&gt; pila;
	// Declaración de pila para elementos tipo 'int'

	pila.push(3);
	pila.push(14);
	pila.push(97);
	// Se ingresan datos

	cout << pila.top() << '\n';
	// Se muestra el último elemento ingresado en la pila

	cout << pila.size() << '\n';
	// Se obtiene la cantidad de elementos almacenados

	pila.pop();
	// Se elimina el primer elemento de la estructura

	if (pila.empty()){
		// Se checa si la estructura está vacía
		cout << "La estructura esta vacia\n";
	} else {
		cout << "La estructura no esta vacia\n";
	}

	stack&lt;int&gt; otra;
	otra.push(32);
	otra.push(12);
	otra.push(1);

	pila.swap(otra);
	// Se intercambian contenidos

	cout << pila.size() << " " << otra.size() << '\n';
	
	return 0;
}</textarea>

<textarea class="output">
/* Salida */
97
3
La estructura no esta vacia
3 2</textarea>