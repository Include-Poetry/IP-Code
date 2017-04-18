---
layout: G-Article
title: Plantilla string
author: rivel_co
tags: [STL, Cadena, Variables, Variables compuestas]
Hide_Tags: true
categories: [C++, OMI]
---

La plantilla de clase `string` almacena y manipula secuencias de variables tipo `char`.

{: #ListaContenido}
- Funcionamiento
- Eficiencia
- Funciones miembro
- Funciones no miembro
- Ejemplos

## Funcionamiento

Imagina que con `string` generamos un arreglo de tamaño dinámico, es decir, cuyo tamaño no tenemos que declarar al inicio, y las variables que almacenan son de tipo `char`, de esta forma podemos escribir palabras fácilmente.

Los elementos en una plantilla tipo `string` son almacenados de manera contigua, de hecho, la palabra *string* se traduce al español como *cadena*. Imagina esta plantilla, como una cadena de caracteres.

## Eficiencia

La eficiencia de la plantilla `string` es muy aproximada a la de la clase `vector`.

Para acceso aleatorio a un elemento | constante| $$ O(l) $$
Insertar o remover un elemento al final del contenedor | constante | $$ O(l) $$
Insertar o remover un elemento | lineal en función de la distancia a la que esté del final | $$ O(n) $$


## Funciones miembro

| Función						| Definición																					|
|:------------------------------|:----------------------------------------------------------------------------------------------|
| (constructor)					| Construye un elemento `string`																|
| Operador `=`					| Asigna valores al `string`																	|
| `get_allocator`				| Regresa el asignador asociado																	|
| 														**Acceso a elementos**													|
| `at` 							| Accede al carácter especificado revisando límites 											|
| Operadores `[ ]` 				| Accede al carácter especificado 																|
| `front` 						| Accede al primer carácter 																	|
| `back` 						| Accede al último carácter 																	|
| `data` 						| Regresa un puntero al primer carácter del `string` 											|
| `c_str` 						| Devuelve una versión no modificable tipo arreglo del `string` para C estándar 				|
| 															**Iteradores**														|
| `begin` `cbegin`(C++11) 		| Devuelve un iterador al principio de la cadena 												|	
| `end` `cend`(C++11) 			| Devuelve un iterador al final de la cadena 													|	
| `rbegin` `crbegin`(C++11) 	| Devuelve un iterador reverso al principio de la cadena 										|	
| `rend` `crend`(C++11) 		| Devuelve un iterador reverso al final de la cadena 											|	
| 															**Capacidad**														|
| `empty` 						| Devuelve verdadero si la cadena está vacía													|
| `size` `length` 				| Devuelve el número de caracteres																|
| `max_size` 					| Regresa el máximo número de caracteres posibles												|
| `reserve` 					| Reserva almacenamiento																		|
| `capacity` 					| Regresa el número de caracteres que pueden ser almacenados en la memoria actual reservada		|
| `shrink_to_fit`(C++11) 		| Reduce el uso de memoria liberando la memoria no utilizada									|
| 															**Operaciones**														|
| `clear` 						| Limpia los contenidos 																		|
| `insert` 						| Inserta caracteres 																			|
| `erase` 						| Borra caracteres 																				|
| `push_back` 					| Agrega un carácter al final de la cadena 														|
| `pop_back`(C++11) 			| Borra el último carácter 																		|
| `append` 						| Agrega caracteres al final de la cadena 														|
| Operador `+=` 				| Agrega caracteres al final de la cadena 														|
| `compare` 					| Compara dos cadenas 																			|
| `replace` 					| Reemplaza una parte especificada de la cadena 												|
| `substr` 						| Devuelve una sub cadena 																		|
| `copy` 						| Copia caracteres 																				|
| `resize` 						| Cambia la cantidad de caracteres almacenados 													|
| `swap` 						| Intercambia contenidos de dos cadenas 														|
| 															**Búsqueda**														|
| `find` 						| Encuentra caracteres en la cadena 															|
| `rfind` 						| Encuentra la última coincidencia de una subcadena 											|
| `find_first_of` 				| Encuentra la primera coincidencia de caracteres 												|
| `find_first_not_of` 			| Encuentra la primera ausencia de caracteres 													|
| `find_last_of` 				| Encuentra la última coincidencia de caracteres 												|
| `find_last_not_of` 			| Encuentra la última ausencia de caracteres													|

## Funciones no miembro

| Función           						  | Definición        						                                        |
|:--------------------------------------------|:--------------------------------------------------------------------------------|
| Operadores `==`, `!=`, `<`, `<=`, `>`, `>=` | Compara lexicográficamente dos cadenas											|
| Operador `+`								  | Concatena dos cadenas o una cadena y una variable `char`						|
| 												**Entrada/salida**																|
| Operador `<<`								  | Ejecuta una salida de datos de una cadena										|	
| Operador `>>`								  | Ejecuta una entrada de datos a una cadena 										|
| 											**Conversiones numéricas**															|
| `stoi`(C++11) `stol`(C++11) `stoll`(C++11)  | Convierte una cadena en un entero signado 										|
| `stoul`(C++11) `stoull`(C++11) 			  | Convierte una cadena en un entero no signado 									|
| `stof`(C++11) `stod`(C++11) `stold`(C++11)  | Convierte una cadena a un número con punto decimal `float`						|
| `to_string`(C++11) 						  | Convierte un entero o decimal a tipo `string` 									|

## Ejemplos

**Asignaciones y entrada/salida**

<textarea class="editor">
#include &lt;iostream&gt;
#include &lt;string&gt; // Librería de la plantilla 'string'
using namespace std;

int main(){
	string cadena;
	string palabra;
	// Declaración

	cadena = "Hola mundo\n";
	palabra = cadena;
	// Asginación con operador '='
	// Pueden haber espacios en esta asignación.
	// También saltos de línea.
	cout << cadena << palabra;
	// Salida del valor de las cadena/

	cin >> cadena;
	// Asignación por entrada estándar
	// La asignación por entrada estándar omitirá los espacios
	// pues éstos se tomarán como final de la entrada.
	cout << cadena << '\n';

	cadena.assign(4, 'T');
	// Remplaza el contenido de 'cadena' con 4 caracteres 'T'
	cout << cadena << '\n';

	cadena.assign(palabra);
	// Equivalente a 'cadena = palabra'
	cout << cadena;

	cadena = "Otro texto";
	palabra.assign(cadena, 0, 7);
	// Reemplaza el contenido de 'palabra' por el contenido de
	// 'cadena', desde el índice 0 los siguientes 7 caracteres.
	// Recuerda que un espacio es también un carácter.
	cout << palabra << '\n';

	cadena.assign("Lorem ipsum");
	// Equivalente a 'cadena = "Lorem ipsum"'
	cout << cadena << '\n';

	return 0;
}</textarea>

<textarea class="output">
/* Entrada */
Nueva palabra</textarea>

<textarea class="output">
/* Salida */
Hola mundo
Hola mundo
Nueva
TTTT
Hola mundo
Otro te
Lorem ipsum</textarea>

**Acceso a elementos**

<textarea class="editor">
#include &lt;iostream&gt;
#include &lt;string&gt;
using namespace std;

int main(){
	string cadena;
	cadena = "Pastel genial";

	cout << cadena[0] << cadena[2] << cadena[8] << '\n';
	// Uso de operadores '[]' como un arreglo normal

	cout << cadena.at(7) << cadena.at(8) << cadena.at(9) << '\n';
	// Uso del selector 'at', es más seguro

	cout << cadena.front() << '\n';
	// Acceso al primer elemento

	cout << cadena.back() << '\n';
	// Acceso al último elemento
	
	return 0;
}</textarea>

<textarea class="output">
/* Salida */
Pse
gen
P
l</textarea>

**Capacidad**

<textarea class="editor">
#include &lt;iostream&gt;
#include &lt;string&gt;
using namespace std;

int main(){
	string cadena;
	
	if (cadena.empty()){ // Se revisa si está vacío
		cout << "Cadena vacia\n";
	}

	cadena = "Pay de queso";
	cout << cadena.length() << '\n';
	// Devuelve la cantidad de carácteres en la cadena

	cadena = "Galleta";
	cout << cadena.size() << '\n';
	// También devuelve la cantidad de carácteres

	cout << cadena.max_size() << '\n';
	// Devuelve la cantidad máxima de caracteres que puede alojar
	// la cadena con la memoria actual reservada

	cout << cadena.capacity() << '\n';
	// Devuelve la capacidad actual de alamacenamiento de la cadena
	// actual, es el tamaño más grande que se le ha asignado
	
	return 0;
}</textarea>

<textarea class="output">
/* Salida */
Cadena vacia
12
7
1073741820
12</textarea>

La salida anterior puede variar en la línea 5, según cada computadora.

**Operaciones**

<textarea class="editor">
#include &lt;iostream&gt;
#include &lt;string&gt;
using namespace std;

int main(){
	string cadena;
	
	/* --- Clear --- */
	cadena = "Tres leches";
	cadena.clear();
	// Elimina todo el contenido de la cadena
	cout << cadena.size() << '\n';

	/* --- Insert --- */
	cadena = "ael";
	cadena.insert(0, 1, 'P');
	// Insertad desde la posición 0, 1 vez el carácter 'P'
	cout << cadena << '\n';

	cadena.insert(2, "st");
	// Inserta desde la posición 2, el texto "st".
	// En este caso siempre se usa doble comilla
	cout << cadena << '\n';

	cadena.insert(6, " de tres leches", 0, 8);
	// Inserta en desde la locación 6 el texto " de tres leches"
	// desde la locación 0 los primeros 8 caracteres
	cout << cadena << '\n';

	/* --- erase --- */
	cadena.erase(0, 10);
	// Borra desde la locación 0 los primeros 10 caracteres
	cout << cadena << '\n';

	/* --- push_back --- */
	cadena.push_back('a');
	// Inserta un carácter al final de la cadena
	cout << cadena << '\n';

	/* --- pop_back --- */
	cadena.pop_back();
	// Elimina el carácter al final de la cadena
	cout << cadena << '\n';

	/* --- append --- */
	cadena.append(3, ' ');
	// Agrega 3 caracteres ' ' (espacios) al final de la cadena
	cout << cadena << '\n';

	cadena.append("leches");
	// Agrega la cadena 'leches'
	cout << cadena << '\n';

	string final = "leches";
	cadena.append(final, 4, 2);
	// Agrega la cadena 'leches' pero sólo a partir de la
	// locación 4 los primeros 2 caracteres
	cout << cadena << '\n';

	/* --- operador += --- */
	cadena = "Algo genial";
	cadena += " es hacer pan";
	// Se agrega la cadena ' es hacer pan' al final de 'cadena'
	cout << cadena << '\n';

	/* --- replace --- */
	cadena.replace(15, 5, "comer");
	// Remplaza desde la locación 15 los primeros 5 caracteres con
	// la cadena 'comer'
	cout << cadena << '\n';

	cadena.replace(0, 4, "Muy");
	cout << cadena << '\n';

	/* --- substr --- */
	string otra;
	otra = cadena.substr(10);
	// Genera una subcadena tomando los 10 caracteres ubicados a 
	// partir de la locacion 10
	cout << otra << '\n';

	otra = cadena.substr(5, 3);
	// Genera una cadena tomando los primeros 3 caracteres
	// a partir de la locación 5
	cout << otra << '\n';

	/* --- resize --- */
	cadena = "Chocolate";
	otra = "Fresa";

	int tam = 8;

	cadena.resize(tam);
	// Se cambia el tamaño de la cadena, el tamaño nuevo es 
	// menor al tamaño anterior, por lo que sólo se espera
	// como parámetro un número entero
	cout << cadena << '\n';

	otra.resize(tam, 'x');
	// El tamaño nuevo es mayor al tamaño actual, por lo que 
	// además del entero, hay que ingresar el carácter de relleno
	cout << otra << '\n';

	/* --- swap --- */
	cout << cadena << '\n' << otra << '\n';

	cadena.swap(otra);
	// Se intercambia el contenido de las dos cadenas
	cout << cadena << '\n' << otra << '\n';

	return 0;
}</textarea>

<textarea class="output">
/* Salida */
0
Pael
Pastel
Pastel de tres
tres
tresa
tres
tres   
tres   leches
tres   lecheses
Algo genial es hacer pan
Algo genial es comer pan
Muy genial es comer pan
 es comer pan
eni
Chocolat
Fresaxxx
Chocolat
Fresaxxx
Fresaxxx
Chocolat
</textarea>

**Búsquedas**

<textarea class="editor">
#include &lt;iostream&gt;
#include &lt;string&gt;
using namespace std;

int main(){
	string cadena;

	/* --- find --- */
	cadena = "Reposteria";
	
	cout << cadena.find("poste") << '\n';
	// Devuelve la locación donde empieza la primer coincidencia

	cout << cadena.find("e", 3) << '\n';
	// Devuelve la locación donde encuentra la primer coincidencia
	// después de la locación 3, incluyendo esa locación

	cout << cadena.find("choco") << '\n';;
	// Si no lo encuentra devuelve un entero mayor al tamaño de
	// la cadena, por eso siempre hay que revisar, por ejemplo

	int pos = cadena.find("pastel");
	if (pos < cadena.size()){
		cout << "Sub cadena encontrada\n";
	} else {
		cout << "Sub cadena no encontrada\n";
	}

	/* --- rfind --- */
	cadena = "Galletitita";

	cout << cadena.rfind("ti") << '\n';
	// Devuelve la locación de la última coincidencia

	cout << cadena.rfind("a", 3) << '\n';
	// Devuelve la locación donde encuentra la última coincidencia
	// después de la locación 3, incluyendo esa locación

	cout << cadena.rfind("choco") << '\n';;
	// Si no lo encuentra devuelve un entero mayor al tamaño de
	// la cadena

	/* --- find_first_of --- */
	cadena = "Pay de queso";
	string segunda = "e";

	cout << cadena.find_first_of(segunda) << '\n';
	// Devuelve la locación de la primer coincidencia

	segunda = "Otra";
	cout << cadena.find_first_of(segunda) << '\n';
	// Devuelve la locación se haya encontrado la primer coincidencia
	// de alguno de los caracteres que componen las cadenas.
	// En este caso la salida es '1', pues en la locación 1 de 'cadena'
	// está el primer carácter que también está en algún lado
	// de la cadena 'segunda'

	cout << cadena.find_first_of("e", 6) << '\n';
	// Devuelve la locación de la primer coincidencia después
	// de la locación 6, contando también ésta.

	segunda = "zzz";
	cout << cadena.find_first_of(segunda) << '\n';
	// Si no lo encuentra devuelve un entero mayor al tamaño de
	// la cadena

	/* --- find_first_not_of --- */
	cout << cadena.find_first_not_of("zrtwl") << '\n';
	// Devuelve la locación del primer carácter de 'cadena' que
	// no esté en la cadena con la que se compara

	/* --- find_last_of --- */
	cout << cadena.find_last_of("e") << '\n';
	// Devuelve la posición de la última coincidencia

	/* --- find_last_not_of --- */
	cout << cadena.find_last_not_of("yapdqeo") << '\n';
	// Devuelve la posición de la última no coincidencia

	return 0;
}</textarea>

<textarea class="output">
/* Salida */
2
6
4294967295
Sub cadena no encontrada
7
1
4294967295
5
1
9
4294967295
0
9
10
</textarea>

**Funciones no miembro**

<textarea class="editor">
#include &lt;iostream&gt;
#include &lt;string&gt;
using namespace std;

int main(){
	string c1,c2,c3;

	c1 = "Galletas";
	c2 = " con ";
	c3 = "crema";

	c1 += c2 + c3;
	// Se concatenan las cadenas en el orden que están puestas
	cout << c1 << '\n';

	c1 = "vainilla";
	c2 = "chocolate";
	c2 = "cajeta";

	if (c1 < c2){
		cout << c1 << " está primero en el diccionario que " << c2 << '\n'; 
	} else {
		cout << c2 << " está primero en el diccionario que " << c1 << '\n';
	}

	if (c2 == c3){
		cout << "Las cadenas son iguales\n";
	} else {
		cout << "las cadenas son diferentes\n";
	}

	// Se pueden aplicar todos los operadores lógicos con las cadenas.
	// Considera que 'A' será tomada como menor que 'a' pues está
	// primero en la tabla del código ASCII

	/* --- Conversiones --- */
	c1 = "203";
	c2 = "401";
	c3 = "1000";

	int a = stoi(c1);
	int b = stoi(c2);
	int c = stoi(c3);
	// Conversión de 'string' a 'int'

	c1 += c2 + c3;
	// Se concatenan
	a += b + c;
	// Se suman como números enteros

	cout << c1 << '\n';
	cout << a << '\n';

	c1 = "10.5";
	c2 = "21.2";
	c3 = "2.2";

	float A = stof(c1);
	float B = stof(c2);
	float C = stof(c3);
	// Conversión de 'string' a 'float'

	c1 += c2 + c3;
	// Se concatenan
	A += B + C;
	// Se suman como números decimales

	cout << c1 << '\n';
	cout << A << '\n';

	a = 213123;
	A = 3.141592;

	c1 = to_string(a);
	c2 = to_string(A);
	// Se convierten los números a tipo 'string'
	c3 = c1 + c2;
	// Se concatenan
	cout << c3 << '\n';

	return 0;
}</textarea>

<textarea class="output">
/* Salida */
Galletas con crema
cajeta está primero en el diccionario que vainilla
las cadenas son diferentes
2034011000
1604
10.521.22.2
33.9
2131233.141592</textarea>

No olvides probar los programas anteriores en tu IDE favorito, experimenta con ellos.

<div class="Nav">
	<a href="{{ site.baseurl }}/C++/STL/Vector/">Tema anterior</a> | <a href="{{ site.baseurl }}/C++/STL/Queue/">Tema siguiente</a>
</div>