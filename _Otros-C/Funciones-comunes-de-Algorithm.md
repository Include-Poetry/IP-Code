---
layout: G-Article
title: Funciones comunes de Algorithm
date: 2020-01-04 12:00:00
author: rivel_co
tags: [Algorithm, STL, Funciones]
olimpiada: [OMI]
subject: [C++]
---

Muchas veces podemos ahorrarnos tiempo de competencia si utilizamos las funciones que ya vienen por defeco en la [librería]({{ site.baseurl }}/C++/Introduccion/Librerias/ "Librerías para C++ &vert; #iP Code") `algorithm` (`#include<algorithm>`). Estas funciones son sencillas de utilizar y recordar. Es importante que sepas que lo recomendable es que tú ya sepas cómo implementar estas funciones desde cero y una vez que lo domines entonces uses estas funciones *sin remordimientos*.

{: #ListaContenido}
- sort
- min
- max
- binary_search
- Todas las funciones

## sort

La función `sort()` nos permite ordenar los elementos de un [arreglo]({{ site.baseurl }}/C++/Estructuras/Arreglos/ "Arreglos en C++ &vert; #iP Code") utilizando un determinado criterio. Esta función utiliza un algoritmo bastante eficiente para ordenar, tiene una complejidad de $$O(N log_2(N))$$. Una implementación equivalente puede ser [merge sort]({{ site.baseurl }}/C++/Metodos/Ordenamientos/Merge-sort/ "Merge sort &vert; #iP Code"). El uso de la función es como sigue.

<textarea class="cpp">
sort(elemento.inicio, elemento.fin, funcionCriterio);</textarea>

Nótese que con `elemento.inicio` y `elemento.fin` se hace referencia a apuntadores al inicio y fin del elemento que queremos ordenar y con `funcionCriterio` a una función hecha por nosotros que marcará el criterio de ordenamiento, esta función criterio puede o no ser indicada, si se omite entonces `sort()` ordenará de **menor a mayor**. Un uso típico de la función `sort()` es como sigue.

<textarea class="cpp">
#include &lt;iostream&gt;
#include &lt;algorithm&gt;
using namespace std;

int main(){
    int arr[] = {1, 5, 3, 0, 6, 7, 8, 4, 2, 9};
    
    sort(arr, arr+10);
    
    for (int i=0; i<10; i++){
        cout << arr[i] << endl;
    }
    
    return 0;
}</textarea>

Nótese que por tratarse de un arreglo podemos identificar el inicio con únicamente el nombre del arreglo y el fin con el nombre del arreglo más la cantidad de elementos a ordenar. Podemos ordenar también sólo una parte del arreglo, por ejemplo ordenar desde el cuarto elemento y hasta el octavo con la línea `sort(&arr[3], &arr[3]+5);`. Recuerda que la función recibe solamente [direcciones de memoria]({{ site.baseurl }}/C++/Introduccion/Punteros/ "Punteros &vert; #iP Code"), por eso el `&`.

Para utilizar un criterio distinto hay que crear una función que maneje ese nuevo criterio y posteriormente indicar esa función como argumento de `sort()`, por ejemplo para ordenar de mayor a menor podemos usar el siguiente código:

<textarea class="cpp">
#include &lt;iostream&gt;
#include &lt;algorithm&gt;
using namespace std;

bool mayorMenor(int a, int b){
    return a > b;
}

int main(){
    int arr[] = {1, 5, 3, 7, 6, 0, 8, 4, 2, 9};
    
    sort(arr, arr+10, mayorMenor);
    
    for (int i=0; i<10; i++){
        cout << arr[i] << endl;
    }
    
    return 0;
}</textarea>

Si queremos ordenar un objeto tipo `vector` debemos utilizar iteradores del mismo elemento, es decir usamos `sort(vec.begin(), vec.begin()+n);` donde `n` es un entero que representa la cantidad de elementos a ordenar.

## min

La función `min()` toma como argumentos **dos** elementos y regresa el menor de ellos. Siempre toma la parte numérica de los elementos, por lo que `'a' < 'z'`. También trabaja con decimales. Su implementación es como sigue:

<textarea class="cpp">
#include &lt;iostream&gt;
#include &lt;algorithm&gt;
using namespace std;

int main(){
    int a = 3, b = 10;
    
    cout << min(a, b); // Muestra 3
    
    return 0;
}</textarea>

## max

Funciona exactamente igual a `min()`, pero este regresa el mayor de dos elementos. 

## binary_search

Esta función realiza una búsqueda binaria sobre un arreglo **ordenado** de datos. Por definición esta función es muy eficiente. Se consideran a dos elementos `a` y `b` iguales si `(!(a<b) && !(b<a))`. Recuerda que se considera que el arreglo sobre el que se opera **ya está ordenado**. Devuelve un valor booleano, *true* si el elemento se encuentra, *false* sino. Su implementación es muy similar a `sort()`, como sigue:

<textarea class="cpp">
binary_search(arr, arr+n, x, funcionCriterio);</textarea>

El primer argumento es el apuntador al inicio del arreglo, luego el apuntador al último elemento, el tercer argumento es el elemento a buscar. Al final se puede agregar una función criterio porque `binary_sort()` opera por defecto sobre elementos en orden creciente.

Para el siguiente código lo que haremos es tomar un arreglo ya declarado, ordenarlo con `sort()` y luego realizar la búsqueda binaria de un elemento `x`. El siguinte cósigo tiene como salida un `64 esta en el arreglo`.

<textarea class="cpp">
#include &lt;iostream&gt;
#include &lt;algorithm&gt;
using namespace std;

int main(){
    int arr[] = {10, 21, 453, 64, 75, 123, 68, 32, 156, 35};
    int x; // Variable de consulta
    
    sort(arr, arr+10);
    x = 64;
    if (binary_search(arr, arr+10, x))
        cout << x << " esta en el arreglo";
    else 
        cout << x << " no esta en el arreglo";
    
    return 0;
}</textarea>

Si se quiere aplicar en un arreglo decreciente como `78, 13, 3, 0` debemos usar una función criterio. De forma completa su uso puede ser como sigue:

<textarea class="cpp">
#include &lt;iostream&gt;
#include &lt;algorithm&gt;
using namespace std;

bool funct(int a, int b){
    return a > b;
}

int main(){
    int arr[] = {10, 21, 453, 64, 75, 123, 68, 32, 156, 35};
    int x; // Variable de consulta
    
    sort(arr, arr+10, funct); // Ordenamos de forma decreciente
    x = 75;
    if (binary_search(arr, arr+10, x), funct)
        cout << x << " esta en el arreglo";
    else 
        cout << x << " no esta en el arreglo";

    
    return 0;
}</textarea>

## Todas las funciones

Como siempre, lo ideal en estos artículos meramente técnicos es que consultes la documentación oficial que es también la fuente de esta clase de contenidos. La documentación de esta librería la puedes encontrar [en la página de cplusplus.com](http://www.cplusplus.com/reference/algorithm/ "C++ Reference").