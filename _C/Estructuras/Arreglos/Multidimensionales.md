---
layout: G-Article
title: Arreglos multidimensionales
author: rivel_co
tags: [Variables compuestas, Arreglos, Matrices]
Hide_Tags: true
olimpiada: [OMI]
subject: [C++]
---

En C++ podemos concebir un arreglo como una variable que almacena a otras variables. Podemos hacer arreglos de cualquier tipo de variable, incluso de otros arreglos. Cuando hacemos que cada locación de un arreglo *contenga* otro arreglo, estamos hablando de arreglos de dos dimensiones que son más comúnmente llamados **matrices**.

{: #ListaContenido}
- Declaración de una matriz
- Arreglos de más de dos dimensiones
- Dimensiones máximas

## Declaración de una matriz

Como ya se decía, las matrices las podemos ver como un arreglo de arreglos o un arreglo de dos dimensiones. Un arreglo *sencillo* de enteros de tamaño $$N$$ se puede declarar como `int arr[N];`. Si queremos hacer un arreglo de de tamaño $$M$$ de arreglos de tamaño $$N$$ de enteros entonces habría que hacer algo como `int mat[M][N];`.

<textarea class="cpp">int arr[N]; // Declaración de un arreglo de una dimensión
int mat[M][N]; // Declaración de un arreglo de dos dimensiones o matriz</textarea>

Si buscamos una representación gráfica un arreglo y de una matriz entonces podríamos pensar en un arreglo como una lista (o un renglón) y una **matriz como una tabla**.

<textarea class="plain-text">arr -> {| 0 | 1 | 2 | 3 | 4 | 5 | ... | N |}
mat -> {| 0 | 1 | 2 | 3 | 4 | 5 | ... | N |
        | 0 | 1 | 2 | 3 | 4 | 5 | ... | N |
        | 0 | 1 | 2 | 3 | 4 | 5 | ... | N |
        | 0 | 1 | 2 | 3 | 4 | 5 | ... | N |
        ...
        | M | ...                         |} </textarea>

Nota que el arreglo `arr` está declarando $$N$$ variables y la matriz `mat` está declarando $$NM$$ variables, es decir, está declarando $$M$$ arreglos de tamaño $$N$$ cada uno. Nos referimos al primer arreglo como `mat[0][];` y al primer elemento del primer arreglo como `mat[0][0];`. Si queremos referirnos al quinto elemento del tercer arreglo sería `mat[2][4];`. Nótese que no podemos hacer algo como `cout << mat[x]` pues nos estaríamos refiriendo a todo un arreglo, no a un solo elemento. 

<textarea class="cpp">int mat[M][N];    // Declaración de una matriz de M x N
mat[0][0] = 56; // Asignación al primer elemento del primer arreglo
cin >> mat[x][y];   // Ingresamos un dato en el elemento y del arreglo x</textarea>

Nota que siempre puedes referirte a los arreglos como las columnas o como las filas de manera prácticamente indistinta, pero es **muy importante** que mantengas el mismo criterio en todo el programa. Si estás manejando `int mat[x][y]` como una matriz de $$x$$ columnas por $$y$$ filas tienes que manejarlo así siempre en tu implementación y del mismo modo, si quieres considerar esa misma matriz como una matriz de $$x$$ filas por $$y$$ columnas tienes que mantenerte así siempre. Lo mismo si quieres considerarlo como un arreglo de $$x$$ arreglos de tamaño $$y$$ o al revés.

## Arreglos de más de dos dimensiones

Siempre puedes declarar arreglos de más de dos dimensiones. Puedes agregar hasta 8 dimensiones en un mismo arreglo. Esta clase de implementaciones son útiles en diferentes situaciones, por ejemplo, si quieres representar un calendario en donde debas guardar algún dato para cada día de cada mes de algunos años, en este ejemplo puedes usar un arreglo de tres dimensiones.

<textarea class="cpp">// Declaración de un calendario como un arreglo de 3 dimensiones
// en este caso se estarían representando 80 años, cada uno con hasta 
// 12 meses y cada mes con hasta 31 días
int calendario[80][12][31];
calendario[49][3][10] = 105; // Aquí le asignamos un 105 al día 10 de marzo del año 50</textarea>

Nota que puedes seguir la misma forma de pensamiento que te propongo sobre verlo como un arreglo de arreglos de arreglos de alguna clase de variable. Nota que todos los elementos de estos arreglos multidimensionales de estos ejemplos son de tipo entero, aunque puedes hacerlo de cualquier otro tipo.

## Dimensiones máximas

No sólo hay que considerar que máximo podemos declarar un arreglo de ocho dimensiones. Tienes que recordar siempre la cantidad de memoria que estás utilizando. Ya se mencionaba antes que un arreglo de $$10^6$$ enteros de $$32$$ bits necesita alrededor de $$32$$ **mb** de memoria. Si declaras una matriz de $$1000 \times 1000$$ entonces estarías declarando $$10^6$$ variables también. Nota que no importa como manejes el tamaño de cada dimensión, lo que importa es el tamaño total del arreglo en cuestión. De la misma forma un arreglo de tres dimensiones de $$ 100 \times 100 \times 100$$ está declarando un millón de variables.

Es importante también que tengas en cuenta que es muy raro (demasiado improbable) que un problema requiera que declares un arreglo de muchas dimensiones con muchas variables en cada una. Si tu solución requiere una matriz de $$10000 \times 10000$$ entonces es muy probable que esa no sea una respuesta correcta.

<div class="Nav">
    <a id="navLeft" href="{{ site.baseurl }}/C++/Estructuras/Arreglos/" title="Arreglos lineales &vert; #iP Code">
        Tema anterior
        <span>Arreglos lineales</span>
    </a>
    <a id="navRight" href="{{ site.baseurl }}/C++/Estructuras/Operaciones-con-bits/" title="Operaciones con bits &vert; #iP Code">
        Tema siguiente
        <span>Operaciones con bits</span>
    </a>
</div>