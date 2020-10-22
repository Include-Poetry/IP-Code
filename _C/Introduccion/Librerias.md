---
layout: G-Article
title: Librerías para C++
date: 2020-10-21 12:00:00
author: rivel_co
tags: [Introducción, Librerías]
hide_tags: true
olimpiada: [OMI]
subject: [C++]
prevTopic: "Para empezar a probar, /C++/Introduccion/Para-empezar-a-probar/"
nextTopic: "Variables, /C++/Introduccion/Variables/"
---

En ocasiones encontramos palabras cuyo significado no sabemos, pues para hablar un determinado idioma no necesitamos conocer todas las palabras existentes. Se podría decir que conocemos la mayoría y cuando encontramos una que no conocemos recurrimos a un *diccionario*, una vez que conocemos su significado podemos usarla. Lo mismo sucede con los compiladores, por eso cuando queremos usar una *función* o *método* que él desconoce, debemos primero decirle dónde aprender qué es.

{: #ListaContenido}
- Librería o biblioteca
- Declaración
- Librerías más usadas en C++
- Todas las librerías de C en C++
- Las librerías estándar para C++

## Librería o biblioteca

Normalmente son llamadas *librerías* en español, aunque es técnicamente más apropiado llamarles *bibliotecas*, pues la palabra de la que surgen es de la palabra en inglés *library* cuya traducción inmediata es *biblioteca*. Esto no importa demasiado pues para quienes hablamos español, ambas palabras nos dan una idea muy similar. También hay quienes se refieren a ellas como *cabeceras* o en inglés *headers*.

Una librería es un archivo que el compilador puede leer y en el que encuentra las *instrucciones de uso* de muchos y distintos **métodos y funciones**. Existen cientos de librerías, la mayoría de IDE ya las tienen incluidas, pero no las incluyen en todos los códigos fuente que se crean, con el propósito de que estos no sean demasiado grandes. Por esto debemos declarar en nuestro código fuente qué librerías necesitaremos.

> Una librería en C++ es un archivo en donde se define la función y uso de muchas funciones diferentes.

> Si incluimos una librería en nuestro programa entonces podemos usar rápida y fácilmente las instrucciones que se definen en ella.

## Declaración

Si vamos a usar una determinada librería en nuestro programa, debemos incluirla o declararla en nuestro código fuente. Para incluir algo a nuestro archivo fuente usamos la expresión `#include`, después de esto y entre signos de menor qué (`<`) y mayor qué (`>`) ponemos el nombre de la librería. De manera general sería:

<textarea class="output">
#include &lt;nombre_libreria&gt;</textarea>

Si queremos incluir varias librerías deberemos declararlas en líneas separadas y todas con su respectivo `#include`. Como el compilador debe de conocer cómo usar las funciones de una librería antes de que esas funciones sean llamdas en el código, lo primero que tenemos que hacer en nuestro código fuente es declarar las librerías que usaremos.

## Librerías más usadas en C++

Debes tener en cuenta que las librerías no son iguales en todos los lenguajes. Las librerías que se usan en un programa escrito en **C++** (archivo con extensión `.cpp`) no siempre pueden usarse en un programa escrito en **C** (archivo con extensión `.c`). Aunque la declaración de librerías es igual en C y C++, estas no siempre son intercambiables. Aquí se hablará de algunas librerías para **C++** y algunas funciones que incluyen.

### iostream

Es definitivamente la librería que más estaremos utilizando, pues es una muy completa, tiene muchas funciones sencillas que son muy utilizadas, al incluirla en nuestro código fuente generalmente evitamos tener que incluir más librerías. Está especializada en la lectura y escritura de archivos. Es exclusiva de C++.

<textarea class="cpp">
#include &lt;iostream&gt;
// Algunas funciones son
std::cout << a;   // Muestra el valor de a en la consola
std::cin << a;    // Ingresa un valor para a desde la consola
min(a, b)         // Regresa el minimo entre a y b
max(a, b)         // Regresa el máximo entre a y b</textarea>

### cmath

Declara un conjunto de funciones principalmente para operaciones matemáticas y transformaciones. Incluye funciones como `sin()`, `cos()`, `tan()`, `exp()`, `log()`, `pow()`, `sqrt()`, `abs()`. Se puede usar en C/C++.

<textarea class="cpp">
#include &lt;cmath&gt;
// Algunas funciones son
sin(x);       // Devuelve el valor de la función trigonométrica seno de la variable x
cos(x);       // Devuelve el valor de la función trigonométrica coseno de la variable x
tan(x);       // Devuelve el valor de la función trigonométrica tangente de la variable x
exp(x);       // Devuelve el valor de la función exponencial de la variable x, es decir e^x
log(x);       // Devuelve el valor de la función logaritmo de la variable x
pow(x, y);    // Devuelve el valor de la variable x elevadaa la potencia y
sqrt(x);      // Devuelve el valor de la raíz cuadrada de la variable x
abs(x);       // Devuelve el valor absoluto de la variable x</textarea>

### cstring

Declara un conjunto de funciones principalmente para manipulación de elementos tipo `string`. Algunas funciones que incluye son `strcat()` `memcmp()` `strpbrk()` `strlen()` `memset()`. Se puede usar en C/C++.

<textarea class="cpp">
#include &lt;cstring&gt;
// Algunas funciones son
strcat()      // Concatena cadenas
memcmp()      // Mueve bloques de memoria
strpbrk()     // Ubica caracteres en una cadena
strlen()      // Obtienes la longitud de una cadena
memset()      // Rellena un bloque de memoria
// Para conocer más funciones en strings y ejemplos revisa el articulo de Strings en STL</textarea>

### ctime

Declara un conjunto de funciones para obtener y manipular información de tiempo y fecha.
Incluye funciones como: `clock()` `difftime()` `mktime()` `time()`. Se puede usar en C/C++.

<textarea class="cpp">
#include &lt;ctime&gt;
// Algunas funciones son
clock()         // La puedes usar para contar el tiempo que dura la ejecución de un programa
difftime()      // Da la diferencia entre dos tiempos
mktime()        // Convierte entre tipos de variable de tiempo
time()          // Obtiene el tiempo actual</textarea>


### algorithm

Define una colección de funciones especialmente diseñadas para utilizarse en rangos de elementos. Además incluye la mayoría de los contenedores de la *STL*. Algunas funciones que incluye son: `find()` `count()` `swap()` `reverse()` `sort()` `merge()`. Exclusiva de C++.

<textarea class="cpp">
#include &lt;algorithm&gt;
// Algunas funciones son
find()      // Encuentra un valor en un rango de elementos
count()     // Cuenta el numero de apariciones de un valor en un rango
swap()      // Intercambia el valor de dos variables
reverse()   // Pone en orden inverso un rango de elementos
sort()      // Ordena un rango de elementos
merge()     // Mezcla dos rangos de elementos ya ordenados</textarea>

### bits/stdc++.h

Esta es algo así como una *súper librería*. Incluye todas las librerías estándar y de STL, es decir, podrías sólo incluir esta siempre y no necesitarías incluir otra. Sin embargo funciona precompilando todas las librerías que incluye, sólo que lo hace en una sola línea, por lo que incluye librerías que podríamos no usar, esto hace que el tiempo de compilación sea mayor.

Puedes ver todas las librerías que se integran al agregar `bits/stdc++.h` viendo su código fuente [acá](https://gist.github.com/eduarc/6022859){:.Re target="_blank"}. Como notarás son demasiadas que muy probablemente no usaremos.

Debido a esto y aunque su uso es muy práctico, sugiero no utilizarla al hacer nuestros programas, es preferible que incorpores una a una las librerías que usaremos. Además no todos los compiladores y evaluadores soportan este fichero. Sin embargo es algo útil conocer y llegar a utilizar en pruebas, por ejemplo.

<textarea class="cpp">
#include &lt;bits/stdc++.h&gt;</textarea>

## Todas las librerías de C en C++

Las librerías que se utilizaban en C han sido convertidas para que puedan usarse en C++, como se mostró en ejemplos anteriores. Las librerías en C utilizaban una extención `.h` al final del nombre, en C++ se excluye ese `.h` y en su lugar se añade una `c` al inicio del nombre de la librería. Por ejemplo, la librería de C `stdio.h` se puede usar en C++ con el nombre `<cstdio>`. Todas las librerías de C que han tenido esta conversión son:

<textarea class="cpp">
#include &lt;cassert&gt;
#include &lt;cctype&gt;
#include &lt;cerrno&gt;
#include &lt;cfloat&gt;
#include &lt;ciso646&gt;
#include &lt;climits&gt;
#include &lt;clocale&gt;
#include &lt;cmath&gt;
#include &lt;csetjmp&gt;
#include &lt;csignal&gt;
#include &lt;cstdarg&gt;
#include &lt;cstddef&gt;
#include &lt;cstdio&gt;
#include &lt;cstdlib&gt;
#include &lt;cstring&gt;
#include &lt;ctime&gt;</textarea>

## Las librerías estándar para C++

Existen otras librerías que son estándar en C++, algunas de ellas son solamente compatibles con *C++11*, entonces considera esto cuando quieras compilar tu codigo o quieras enviar un código que incluya alguna de estas librerías a un evaluador. Entonces todas las liberías estándar de C++ incluyendo las de C++11 son:

<textarea class="cpp">
#include &lt;algorithm&gt;         // Algoritmos de la plantilla estándar
#include &lt;chrono&gt;            // Librería para usar mediciones de tiempo
#include &lt;complex&gt;           // Librería para usar números complejos
#include &lt;exception&gt;         // Exepciones estándar
#include &lt;functional&gt;        // Objetos para funciones
#include &lt;initializer_list&gt;  // Para inicilizar listas
#include &lt;iterator&gt;          // Para definir iteradores
#include &lt;limits&gt;            // Calcula límites numéricos
#include &lt;locale&gt;            // Librería para localizaciones
#include &lt;memory&gt;            // Elementos de memoria
#include &lt;new&gt;               // Para uso dinámico de memoria
#include &lt;numeric&gt;           // Operaciones numéricas generales
#include &lt;random&gt;            // Funciones para obtener cosas aleatorias
#include &lt;ratio&gt;             // Librería para proporciones
#include &lt;regex&gt;             // Para manejar expresiones regulares
#include &lt;stdexcept&gt;         // Clases de exepciones
#include &lt;string&gt;            // Crea y maneja elementos string
#include &lt;system_error&gt;      // Gestión de errores del sistema
#include &lt;tuple&gt;             // Librería para objetos tipo tuple
#include &lt;typeinfo&gt;          // Obtener información sobre tipos de datos
#include &lt;type_traits&gt;       // Tipos de traits
#include &lt;utility&gt;           // Componentes variados de utilería
#include &lt;valarray&gt;          // Para arreglos de elementos numéricos</textarea>
