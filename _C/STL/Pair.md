---
layout: G-Article
title: Estructura pair
author: rivel_co
tags: [STL, Listas]
Hide_Tags: true
categories: [C++, OMI]
---

La estructura `pair` es una plantilla que permite almacenar dos variables en un sólo objeto.

{: #ListaContenido}
- Funcionamiento
- Eficiencia
- Funciones miembro
- Funciones no miembro
- Ejemplo general

## Funcionamiento

Al ser una estructura, nos permite de manera muy sencilla almacenar dos variables, bajo un mismo nombre. Su funcionamiento puede ser implementado fácilmente con `struct` sin embargo, sigue siendo un método práctico y fácil de implementar.

## Eficiencia

Acceder a un elemento | constante | $$ o(l) $$

## Funciones miembro

| Función			| Definición												|
|:------------------|:----------------------------------------------------------|
| (constructor) 	| Construye un nuevo elemento `pair`						|
| Operador `=`		| Asigna contenidos 										|
| `swap`			| Intercambia contenidos de dos elementos `pair`			|

## Funciones no miembro

| Función			| Definición												|
|:------------------|:----------------------------------------------------------|
| `make_pair`		| Crea un elemento `pair` definido por dos argumentos		|
| Operadores `==`, `!=`, `<`, `<=`, `>`, `>=` | Compara lexicográficamente los valores del contenedor |

## Ejemplo general

<textarea class="editor">
#include &lt;iostream&gt;
#include &lt;algorithm&gt; // Librería
using namespace std;

int main(){

	pair<int, int> dupla;

	dupla.first = 4;
	dupla.second = 10;

	cout << dupla.second << " " << dupla.first << '\n';

	pair<int, char> otro;

	otro.first = 89;
	otro.second = 'T';

	cout << otro.first << " " << otro.second << '\n';
	
	return 0;
}</textarea>

<textarea class="output">
/* Salida */
10 4
89 T</textarea>

<div class="Nav">
	<a href="{{ site.baseurl }}/C++/STL/List/">Tema anterior</a> | <a href="{{ site.baseurl }}/C++/Recursion/">Tema siguiente</a>
</div>