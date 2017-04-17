---
layout: G-Article
title: Librerías para C++
tags: [Introducción, Librerías]
Hide_Tags: true
categories: [C++, OMI]
---

En ocasiones encontramos palabras cuyo significado no sabemos, pues para hablar un determinado idioma no necesitamos conocer todas las palabras existentes. Se podría decir que conocemos la mayoría y cuando encontramos una que no conocemos recurrimos a un *diccionario*, una vez que conocemos su significado podemos usarla. Lo mismo sucede con los compiladores, por eso cuando queremos usar una *función* o *método* que él desconoce, debemos primero decirle dónde aprender qué es.

{: #ListaContenido}
- Librería o biblioteca
- Declaración
- Librerías más usadas en C++
- Ejemplos

## Librería o biblioteca

Normalmente son llamadas *librerías* en español, aunque es técnicamente más apropiado llamarles *bibliotecas*, pues la palabra de la que surgen es de la palabra en inglés *library* cuya traducción inmediata es *biblioteca*, sin embargo esto no importa demasiado pues para quienes hablamos español, ambas palabras nos dan una idea muy similar. También hay quienes se refieren a ellas como *cabeceras* o en inglés *headers*.

Una librería es un archivo que el compilador puede leer, en él encuentra las *instrucciones de uso* de muchos y distintos métodos y funciones. Existen cientos de librerías, la mayoría de IDE ya las tienen incluidas, pero no las incluyen en todos los códigos fuente que se crean, con el propósito de que estos no sean demasiado grandes. Por esto debemos declarar en nuestro código fuente qué librerías necesitaremos.

## Declaración

Para declarar que usaremos una determinada librería debemos indicar que vamos a incluirla. Para incluir algo a nuestro archivo fuente usamos la expresión `#include`, después de esto y entre signos de menor que y mayor qué ponemos el nombre de la librería. De manera general sería:

> #include &lt;nombre_libreria&gt;

Si queremos incluir varias librerías deberemos declararlas en líneas separadas y todas con su respectivo `#include`. Debido a que el compilador primero debe conocer cómo usar los métodos de las librerías, es lo primero que debemos declarar en nuestros códigos fuente.

## Librerías más usadas en C++

Debes tener en cuenta que las librerías no son para todos los lenguajes, las librerías que se usan en un código fuente de *C* (es decir, un archivo con extensión `.c`) no puede compilar librerías diseñadas para *C++* (archivos con extensión `.cpp`). Aunque las declaraciones de librerías en ambos lenguajes es igual, éstas cambian. Aquí se hablará de algunas librerías para **C++** y algunas funciones que incluyen. (<span>Por el momento no importa si no sabes para qué son o cómo se usan</span>).

`iostream`
<br>
Es definitivamente la librería que más estaremos utilizando, pues es una muy completa, tiene muchas funciones sencillas que son muy utilizadas, al incluirla en la mayoría de los casos evitamos tener que incluir más librerías. Está especializada en la lectura y escritura de archivos.
<br>
`cout` `cin` `min()` `max()`

`cmath`
<br>
Declara un conjunto de funciones principalmente para operaciones matemáticas y transformaciones. Incluye funciones como:
<br>
`sin()` `cos()` `tan()` `exp()` `log()` `pow()` `sqrt()` `abs()`

`cstring`
<br>
Declara un conjunto de funciones principalmente para manipulación de elementos tipo `string`
<br>
`strcat()` `memcmp()` `strpbrk()` `strlen()` `memset()`

`ctime`
<br>
Declara un conjunto de funciones para obtener y manipular información de tiempo y fecha.
<br>
`clock()` `difftime()` `mktime()` `time()`

`algorithm`
<br>
Define una colección de funciones especialmente diseñadas para utilizarse en rangos de elementos. Además incluye la mayoría de los contenedores de la *STL*.
<br>
`find()` `count()` `swap()` `reverse()` `sort()` `merge()`

`bits/stdc++.h`
<br>
Esta es algo así como una *súper librería*. Incluye todas las librerías estándar y de STL, es decir, podrías sólo incluir esta siempre y no necesitarías incluir otra. Sin embargo funciona precompilando todas las librerías que incluye, sólo que lo hace en una sola línea, por lo que incluye librerías que podríamos no usar, esto hace que el tiempo de compilación sea mayor.
<br>
Puedes ver todas las librerías que se integran al agregar `bits/stdc++.h` viendo su código fuente [acá](https://gist.github.com/eduarc/6022859){:.Re target="_blank"}. Como notarás son demasiadas que muy probablemente no usaremos.
<br>
Debido a esto y aunque su uso es muy práctico, sugiero no utilizarla al hacer nuestros programas, es preferible que incorpores una a una las librerías que usaremos. Además no todos los compiladores y evaluadores soportan este fichero. Sin embargo es algo útil conocer y llegar a utilizar en pruebas, por ejemplo.

## Ejemplos

<textarea class="editor">
#include &lt;iostream&gt;
#include &lt;cmath&gt;
#include &lt;cstring&gt;
#include &lt;bits/stdc++.h&gt;</textarea>

<div class="Nav">
	<a href="{{ site.baseurl }}/C++/Introduccion/Compilador/">Tema anterior</a> | <a href="{{ site.baseurl }}/C++/Introduccion/Variables/">Tema siguiente</a>
</div>