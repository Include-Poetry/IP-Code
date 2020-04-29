---
layout: G-Article
title: Contenedor Vector
date: 2020-01-04 12:00:00
author: rivel_co
tags: [STL, Vector]
hide_tags: true
olimpiada: [OMI]
subject: [C++]
prevTopic: "STL, /C++/Estructuras/STL/"
nextTopic: "String en STL, /C++/Estructuras/STL/String/"
---

El elemento `vector` es un contenedor que funciona como un arreglo de tamaño dinámico.

{: #ListaContenido}
- Funcionamiento
- Eficiencia
- Funciones miembro
- Funciones no miembro
- Ejemplo general

## Funcionamiento

Los elementos dentro de `vector` son almacenados de manera contigua (<span>como en un arreglo</span>) por lo tanto, se puede acceder a cada elemento usando *iteradores* o también los punteros regulares que usamos en los arreglos `[ ]`, de esta manera, podemos decir que podemos *hacer referencias* a un `vector`, de manera muy similar a como lo hacemos en un arreglo estático.

La capacidad de `vector` es manejada de manera automática, por lo que crece o disminuye según sea necesario. Es decir, cuando declaramos un arreglo tradicional, declaramos también la capacidad de éste. Con un contenedor `vector` no es necesario especificar el tamaño. Pues crece o se minimiza según se vaya necesitando.

La capacidad total de un contenedor de este tipo, es variada, pero puede ser solicitada usando la función `capacity()`


## Eficiencia

Para acceso aleatorio a un elemento | constante| $$ O(l) $$
Insertar o remover un elemento al final del contenedor | constante | $$ O(l) $$
Insertar o remover un elemento | lineal en función de la distancia a la que esté del final | $$ O(n) $$


## Funciones miembro

| Función						| Definición																							|
|:------------------------------|:------------------------------------------------------------------------------------------------------|
| (constructor)					| Construye un contenedor `vector`, es lo que nos permite *declararlo*.									|
| (destructor)					| Destruye el `vector`																					|
| Operador `=`					| Asigna valores al contenedor																			|
| `get_allocator`				| Regresa el asignador asociado																			|
| 												**Acceso a elementos**																	|
| `at`							| Accede al elemento especificado del contenedor con comprobación de límites							|	
| Operador `[]`					| Accede al elemento especificado																		|
| `front`						| Accede al primer elemento del contenedor																|
| `back`						| Accede al último elemento del contenedor																|
| 													**Iteradores**																		|
| `begin` `cbegin` 				| Devuelve un iterador al principio del contenedor 														|
| `end` `cend` 					| Devuelve un iterador al final del contenedor 															|
| `rbegin` `crbegin` 			| Devuelve un iterador reverso al principio del contenedor 												|
| `rend` `crend` 				| Devuelve un iterador reverso al final del contenedor 													|
| 													**Capacidad**																		|
| `empty` 						| Checa si el contenedor está vacío 																	|
| `size` 						| Regresa el número de elementos en el contenedor 														|
| `max_size` 					| Regresa el máximo número posible de elementos 														|
| `reserve` 					| Reserva almacenamiento 																				|	
| `capacity` 					| Regresa el número de elementos que pueden ser almacenados en el contenedor con el espacio actual 		|			
| `shrink_to_fit` (C++11) 		| Reduce a memoria usada liberando el espacio no utilizado 												|
| 													**Modificadores**																	|
| `clear`						| Limpia el contenido del contenedor																	|
| `insert`						| Inserta elementos en el contenedor																	|
| `erase`						| Borra elementos																						|
| `push_back`					| Agrega un elemento al final del contenedor															|
| `pop_back`					| Quita el último elemento del contenedor																|
| `resize`						| Cambia la cantidad de elementos almacenados															|
| `swap`						| Intercambia el contenido																				|

## Funciones no miembro

| Función           						  | Definición                                                            |
|:--------------------------------------------|:----------------------------------------------------------------------|
| Operadores `==`, `!=`, `<`, `<=`, `>`, `>=` | Compara lexicográficamente los valores del vector 					  |

## Ejemplo general

<textarea class="cpp">
#include &lt;iostream&gt;
#include &lt;vector&gt; // Librería del contenedor
using namespace std;
	
int main(){
	/* --- Declaración --- */
    vector&lt;int&gt; v; // Declaración del vector, en este caso tipo entero
    vector&lt;int&gt; segundo {12, 5, 3, 14, 98, 56, 23, 45}; // Declaración e inicialización (requiere c++11)

    /* --- Asignación --- */
    v = segundo; // Copia de "segundo" en "v"
    // Sólo puede ser entre vectores, los valores del primer 
    // contenedor se sobreescribirán para poner los del segundo
    v.assign(4, 87);
  	// Borra todos los valores en v y almacena 4 veces el valor 87

    /* --- Acceso a elementos --- */
    cout << segundo.front() << '\n'; // Primer elemento
    cout << segundo.back() << '\n'; // Último elemento
    cout << segundo[3] << '\n'; // Cuarto elemento (específico)
    cout << segundo.at(1) << '\n'; // Segundo elemento (seguro)


    /* --- Recorrer el vector -- */
    for (int i : v) // Para todos los elementos dentro de v
    	cout << i << " "; // i tiene que ser del mismo tipo que los valores del vector
    // Este método sólo es compatible en C++11

    cout << '\n';

    // Método tradicional como en un arreglo normal 
    for (int i = 0; i < v.size(); i++)
    	cout << v[i] << " ";
    cout << '\n';

    // O de manera más confiable, usando .at()
    for (int i = 0; i < v.size(); i++)
    	cout << v.at(i) << " ";
    cout << '\n';

    /* --- Sobre capacidad --- */
    if (v.empty()) // Devuelve true si está vacío
    	cout << "v esta vacio\n";
    cout << v.size() << " " << segundo.size() << '\n'; // Cantidad de objetos en los contenedores
    cout << v.max_size() << '\n'; 
    // Maxima cantidad de elementos posibles en el vector v
    cout << v.capacity() << '\n';
    // Regresa el numero de elementos que se pueden almacenar con la memoria declarada

    /* --- Modificador clear --- */
    v.clear();
    // Borra todos los elementos del vector
    cout << v.size() << '\n';

    /* --- Modificador insert --- */
    v.insert(v.begin(), 14);
    // Inserta el 14 en el inicio del vector 
    v.insert(v.begin(), 25);
    // Inserta ahora el 25 también al inicio
    for (int i : v) cout << i << " ";
    cout << '\n';

    v.insert(v.begin()+2, segundo.begin(), segundo.end());
    // Inserta en v, después del segundo elemento, el contenido
    // de 'segundo' desde el inicio hasta el fin
    for (int i : v) cout << i << " ";
    cout << '\n';

    v.insert(v.begin(), 3, 200);
    // Se inserta 3 veces el 200 al inicio del contenedor
    for (int i : v) cout << i << " ";
    cout << '\n';

    int arreglo[] = { -12, -32, 99};
    v.insert(v.end(), arreglo, arreglo+2);
    // Se insertan al final del vector, los elementos de
    // 'arreglo', desde el inicio hasta el segundo elemento
    for (int i : v) cout << i << " ";
    cout << '\n';

    /* --- Modificador erase --- */
    segundo.erase(segundo.begin());
    // Eliminación del primer valor del vector
    for (int i : segundo) cout << i << " "; 
    cout << '\n';

    segundo.erase(segundo.begin()+2);
    // Eliminación del tercer arreglo del vector
    for (int i : segundo) cout << i << " ";
    cout << '\n';

    segundo.erase(segundo.begin()+1, segundo.begin()+4);
    // Eliminación de un intervalo
    // El último elemento del intervalo no se borra
    for (int i : segundo) cout << i << " ";
    cout << '\n';

    /* --- Modificador push_back --- */
    segundo.push_back(32);
    // Inserta al final del contenedor, el entero 32
    int variable = 15;
    segundo.push_back(variable);
    // Inserta al final la variable 'variable'
    for (int i : segundo) cout << i << " ";
    cout << '\n';

    /* --- Modificador pop_back --- */
    segundo.pop_back();
    // Elimina el elemento del final
    for (int i : segundo) cout << i << " ";
    cout << '\n';

    /* --- Modificador resize --- */
    segundo.resize(3);
    // Se borran todos los elementos dejando sólo los primeros 3
    for (int i : segundo) cout << i << " ";
    cout << '\n';

    segundo.resize(6);
    // Cambia el tamaño a 6, si hay menos elementos entonces 
    // rellena con 0
    for (int i : segundo) cout << i << " ";
    cout << '\n';

    /* --- Modificador swap -- */
    for (int i : v) cout << i << " ";
    cout << '\n';
    for (int i : segundo) cout << i << " ";
    cout << '\n';
    // Se muestran los contenidos
    v.swap(segundo);
    // Se intercambian contenidos 
    for (int i : v) cout << i << " ";
    cout << '\n';
    for (int i : segundo) cout << i << " ";
    cout << '\n';

    return 0;
}</textarea>

Salida del anterior programa.

<textarea class="output">
12
45
14
5
87 87 87 87 
87 87 87 87 
87 87 87 87 
4 8
1073741823
8
0
25 14 
25 14 12 5 3 14 98 56 23 45 
200 200 200 25 14 12 5 3 14 98 56 23 45 
200 200 200 25 14 12 5 3 14 98 56 23 45 -12 -32 
5 3 14 98 56 23 45 
5 3 98 56 23 45 
5 23 45 
5 23 45 32 15 
5 23 45 32 
5 23 45 
5 23 45 0 0 0 
200 200 200 25 14 12 5 3 14 98 56 23 45 -12 -32 
5 23 45 0 0 0 
5 23 45 0 0 0 
200 200 200 25 14 12 5 3 14 98 56 23 45 -12 -32 </textarea>

No olvides examinar cuidadosamente el programa anterior y su comportamiento en tu *IDE* favorito.