---
layout: G-Article
title: Para empezar a probar
date: 2020-04-05 23:00:00
author: rivel_co
tags: [Introducción]
Hide_Tags: true
olimpiada: [OMI]
subject: [C++]
---

Para que puedas comenzar a poner a prueba los temas que se describen aquí, he decidido crear este artículo donde puedas encontrar la *plantilla* de un programa clásico. A medida que avances en los temas sabrás qué hace y significa a mayor profundidad cada parte de la plantilla. Mientras tanto te servirá para hacer tus primeras pruebas.

{: #ListaContenido}
- Código base
- Haciendo pruebas
- Dónde modificar

## Código base

Para empezar con casi cualquier programa en programación competitiva utilizando `C++` podemos partir de un código que tiene lo más sencillo e indispensable:

<textarea class="cpp">#include&lt;iostream&gt;
using namespace std;

int main(){
    // Instrucciones aquí
    return 0;
}</textarea>

Conforme avances con los temas verás que la primer línea corresponde a la declaración de una [librería]({{ site.baseurl }}/C++/Introduccion/Librerias/ "Librerías &vert; IP Code"){:target="_blank"}, la segunda es una línea de declaración de sintaxis, en la cuarta estaremos declarando la [función]({{ site.baseurl }}/C++/Introduccion/Funciones/ "Funciones &vert; IP Code"){:target="_blank"} principal llamada `main`, en la quinta línea hay un [comentario]({{ site.baseurl }}/C++/Introduccion/Sentencias/ "Sentencias &vert; #IP Code"){:target="_blank"} que dice que las instrucciones van en ese lugar, la sexta línea tiene un `return 0;` clásico para terminar la función y con ello el programa.

## Haciendo pruebas

Para comenzar a hacer pruebas vamos a necesitar casi todo el tiempo ver algún resultado en pantalla, que nuestro programa nos muestre lo que está haciendo o cómo está funcionando. También vamos a necesitar ingresar datos a nuestro programa con los que trabajará. 

Para poder ver algo de nuestro programa debemos usar la función `cout << `. Si queremos mostrar texto, algún letrero, palabra control o similar, debemos usar comillas después de la función, por ejemplo `cout << "Todo funciona aqui";`. Nota que al final se agrega un `;`. Si queremos mostrar el valor de una [variable]({{ site.baseurl }}/C++/Introduccion/Variables/ "Variables &vert; IP Code"){:target="_blank"} (ya verás qué es una variable) solamente hay que poner el nombre de la variable sin comillas, por ejemplo `cout << contador;`. Si queremos realizar un salto de línea lo que tenemos que hacer es agregar un `endl` como sigue `cout << endl;`.

De la misma forma podemos utilizar todos estos tipos de salida al mismo tiempo en una misma línea solamente no hay que olvidar utilizar `<<` entre cada tipo de salida. Por ejemplo `cout << "El valor de equis es: " << x << endl;` de esta forma se muestra el texto `El valor de equis es: ` seguido del valor de la variable `x` y un salto de línea. Lo siguiente que se imprima se mostrará en una línea nueva.

Para ingresar un valor a nuestro programa, podemos utilizar la función `cin >>`. Si queremos ingresar el valor de la variable `aux` desde el teclado, podemos hacer algo como `cin >> aux;`. Una vez que terminemos de ingresar el valor hay que presionar la tecla `Enter`. Esto último se hace cuando ya se está ejecutando el programa, cuando la pantalla negra de la consola aparece, no mientras se edita el código. Aprenderás más sobre la entrada y salida de datos en la sección de [operadores]({{ site.baseurl }}/C++/Introduccion/Operadores/ "Operadores &vert; IP Code"){:target="_blank"}.

## Dónde modificar

Cuando quieras probar algún método o función de los siguientes temas, puedes modificar el código base agregando lo que quieres probar justo en donde está el comentario `// Instrucciones aquí`. Puedes quitar ese comentario, lo importante es que lo que pruebes esté ubicado entre la línea de `int main(){` y la de `return 0;`, a menos de que se indique otra cosa.

Por ejemplo, si quieres intentar probar los ejemplos de la sección de [variables]({{ site.baseurl }}/C++/Introduccion/Variables/ "Variables &vert; IP Code"){:target="_blank"}, encontrarás pequeños fragmentos de código como:

<textarea class="cpp">
int T=1401, variable=1, a;
float pi=3.14, decimal, otra=0.23;
char letra='C', mas;
bool dicho=true, bandera=false;</textarea>

En tu código de prueba puedes reemplazar la línea del comentario con el texto del ejemplo:

<textarea class="cpp">#include&lt;iostream&gt;
using namespace std;

int main(){
    int T=1401, variable=1, a;
    float pi=3.14, decimal, otra=0.23;
    char letra='C', mas;
    bool dicho=true, bandera=false;
    return 0;
}</textarea>

Luego puedes probar a poner algo como un `cout` para ver en la pantalla el valor de una de esas variables declaradas, por ejemplo:

<textarea class="cpp">#include&lt;iostream&gt;
using namespace std;

int main(){
    int T=1401, variable=1, a;
    float pi=3.14, decimal, otra=0.23;
    char letra='C', mas;
    bool dicho=true, bandera=false;
    cout << pi << " " << T << endl;
    return 0;
}</textarea>

De esa forma obtendrás en pantalla una salida igual a `3.14 1401`. De igual forma puedes probar a hacer asignaciones de valores desde el teclado, utilizando `cin`.

Cuando quieras probar tu código deberás compilarlo y ejecutarlo adecuadamente, esto lo puedes aprender en la sección de [compilador]({{ site.baseurl }}/C++/Introduccion/Compilador/ "Compilador &vert; IP Code"){:target="_blank"}.

> **Nota 1**: A los pequeños fragmentos de código que por sí solos no son un programa o código fuente completo le llamamos *snippet*.

> **Nota 2**: Es común referirnos a la acción de mostrar algo en la pantalla como *imprimir*. Por lo que *mostrar un mensaje* e *imprimir un mensaje* denotan la misma acción.

### Cita esta página

{% include citeThis.html titulo=page.title fecha=page.date link=page.url %}

<div class="Nav">
    <a id="navLeft" href="{{ site.baseurl }}/C++/Introduccion/Compilador/" title="Compilador C++ &vert; #iP Code">
        Tema anterior
        <span>Compilador C++</span>
    </a>
    <a id="navRight" href="{{ site.baseurl }}/C++/Introduccion/Librerias/" title="Librerías en C++ &vert; #iP Code">
        Tema siguiente
        <span>Librerías en C++</span>
    </a>
</div>