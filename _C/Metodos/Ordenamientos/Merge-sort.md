---
layout: G-Article
title: Merge sort
date: 2020-01-04 12:00:00
author: rivel_co
tags: [Algoritmo, Ordenamiento, Arreglos]
hide_tags: true
olimpiada: [OMI]
subject: [C++]
prevTopic: "Bubble sort, /C++/Metodos/Ordenamientos/Bubble-sort/"
nextTopic: "Búsquedas, /C++/Metodos/Busquedas/"
---

Como habrás notado, la eficiencia es un factor muy importante al momento de escoger cualquier algoritmo. En el caso del ordenamiento, un algoritmo eficientes es ***Merge sort*** también llamado *ordenamiento por mezclas*

{: #ListaContenido}
- Idea del funcionamiento
- Implementación
- Complejidad

## Idea del funcionamiento

Para estos ejemplos estaremos trabajando con un conjunto de $$N=8$$ como sigue `6, 2, 3, 7, 5, 1, 4, 8` y lo estaremos ordenado de forma ascendente. Como su nombre lo indica, el algoritmo mezcla los datos a ordenar, de una forma en que al finalizar, los datos queden de la forma deseada. Para esto primero divide todo el conjunto inicial, en dos conjuntos, o subconjuntos, luego vuelve a dividir esos nuevos conjuntos en dos, y así recursivamente hasta llegar a conjuntos de un solo elemento. Como puedes notar, este procedimiento es recursivo.

Una vez que identificamos cada dato individual como un conjunto, comenzamos a mezclar, tomamos los primeros dos conjuntos y ponemos primero en el dato más chico que hay entre todos los datos del conjunto. La primera vez, que nuestros conjuntos son unitarios, habrá que poner primero el dato más chico, luego el mayor. Una vez que terminamos con esto, tendremos conjuntos de dos elementos. Y una vez más, hacemos mezclas. Como sabemos, en estos conjuntos de dos elementos, sus elementos se encuentran ordenados. 

Entonces recursivamente vamos mezclando los conjuntos para formar nuevos conjuntos ordenados, que contienen los elementos de los conjuntos que se unieron. La forma de mezclar es ir poniendo primero el dato más chico de cada conjunto, hasta mezclemos totalmente ambos grupos. Al finalizar, tendremos un conjunto de $$N$$ elementos, y habremos terminado de ordenarlos todos.

La siguiente animación muestra este algoritmo en acción:

<a href="https://commons.wikimedia.org/wiki/File:Merge-sort-example-300px.gif#/media/File:Merge-sort-example-300px.gif"><img src="https://upload.wikimedia.org/wikipedia/commons/c/cc/Merge-sort-example-300px.gif" alt="Merge-sort-example-300px.gif"></a>

## Implementación

Existen muchísimas maneras de hacer la implementación del *Merge Sort*, aquí utilizaremos dos colas, en donde se irán almacenando nuestros subarreglos. Para facilitar el código se utilizarán las plantillas de la *STL* para colas (`queue`) y pilas (`stack`).

Lo primero que tenemos que realizar es la división recursiva de los conjuntos. Para realizar esto primero tenemos que definir el punto medio del conjunto, para eso usaremos la "formula" de `(inicio+fin)/2`, donde `inicio` es la locación del arreglo en donde está nuestro primer valor y `fin` es la última locación en donde hay un valor. Para hacer la división recursiva, primero llamaremos a la función recursiva desde el inicio hasta la mitad, y luego desde la locación siguiente a la mitad y hasta el final del conjunto. Hay que recordar, que cada vez que pasamos los nuevos parámetros en la recursión, nuestros límites de `inicio` y `fin` se acercan más y más, en el momento en que sean el mismo valor, habremos terminado de *fragmentar* nuestro conjunto, por lo que estaremos con conjuntos unitarios.

<textarea class="cpp">
void MergeSort (int inicio, int fin){
    if (inicio == fin) return;      // Terminamos de dividir los conjuntos
    
    int mitad=(inicio+fin)/2;       // Creamos la mitad en base a los limites
        
    MergeSort(inicio, mitad);       // Llamada recursiva para dividir la primer mitad
    MergeSort(mitad+1, fin);        // Llamada recursiva para dividir la segunda mitad
}</textarea>

En cuanto el flujo de la ejecución termine con la llamada recursiva para dividir la segunda mitad, entonces podemos pasar a meter en las colas los elementos de cada nuevo subconjunto. En cada subconjunto estaremos ordenando cada mitad definida en la recursión. En la llamada `cola1` meteremos los elementos de los conjuntos de la izquierda, los que van desde el `inicio` hasta `mitad` y en la llamada `cola2` meteremos los conjuntos de la derecha, los que van desde `mitad+1` hasta `fin`. Esto lo realizamos fácilmente con dos ciclos `for`.

<textarea class="cpp">
for (int i=inicio; i<=mitad; i++){      // Metemos los elementos del conjunto de la izquierda
    cola1.push(arreglo[i]);
}
for (int i=mitad+1; i<=fin; i++){       // Metemos los elementos del conjunto de la derecha
    cola2.push(arreglo[i]);
}</textarea>

Damos por entendido el hecho de que en la estructura `arreglo` tenemos los datos que estamos ordenando. Ahora es necesario empezar a ***mezclar***. Para esto, definimos una variable control con la que llevaremos la cuenta de qué locación estamos ordenando. La locación de nuestro arreglo en donde empezaremos a ubicar nuestros elementos ordenados. Esta variable que lleva la cuenta de la posición la llamaremos `pos` y comenzará siendo igual al límite de `inicio`, pues ese es el comienzo de locación en donde comenzamos a tomar los datos.

Entonces, para realizar las mezclas, habrá que *vaciar* todos los elementos que metimos en las colas, pues ahí hay una copia de los elementos a ordenar, cuando terminemos de sacar todos los elementos de la pila, sabremos que es porque todos esos elementos se han ordenado. Sabemos que la velocidad a la que se vacían los elementos de cada cola, es distinta entre ellas, pues cada estructura contiene elementos diferentes. Sin embargo, si ya hemos terminado de vaciar una de las colas y se encuentra vacía, entonces podemos proceder a vaciar todos los elementos de la otra cola. Recuerda que con *vaciar* nos referimos a tomar el primer elemento de la cola en cuestión y ponerlo en la posición `pos` del arreglo. 

No olvidemos que tenemos que seguir un criterio para ordenar, por ejemplo, para hacer nuestro ordenamiento ascendente, pondremos en la posición `pos` el elemento más chico de cada cola. Como cada vez que se rellenen las colas, lo estaremos haciendo ingresando el elemento más chico primero (por la naturaleza recursiva del ordenamiento) podemos estar seguros de que el elemento más chico de cada cola se encuentra al frente. Entonces comparamos los elementos al frente de cada cola y ubicamos en la posición `pos` el elemento más chico.

Una vez que hayamos ubicado cada nuevo elemento tomado de las colas, sea cual sea, tenemos que actualizar el valor de `pos`, darle un valor una unidad mayor, para que se actualice el lugar donde se pondrá el nuevo elemento a guardar ya ordenado. Lo anterior lo podemos ver en este fragmento de código:

<textarea class="cpp">
// Comenzamos a mezclar los subconjuntos
int pos=inicio;             // Definición del auxiliar de ubicaciones
    
while (!cola1.empty() || !cola2.empty()){   // Estaremos extrayendo elementos mientras sea posible
    if (cola2.empty()){                     // Si la cola2 ya está vacía
        arreglo[pos]=cola1.front();         // entonces tomamos de la cola1
        cola1.pop();                        
    } else
    if (cola1.empty()){                     // Sino, revisamos si cola1 está vacía, de ser así
        arreglo[pos]=cola2.front();         // tomamos de cola2
        cola2.pop();
    } else                                  // Sino, entonces ambas colas tienen elementos
    if (cola1.front() < cola2.front()){     // Aplicamos nuestro criterio de ordenamiento
        arreglo[pos]=cola1.front();         // Ubicamos según sea el caso, tomando de cola1
        cola1.pop();
    } else {
        arreglo[pos]=cola2.front();         // O tomando de cola 2
        cola2.pop();
    }
    pos++;   // En este punto ya habremos ubicado un elemento, entonces actualizamos la posición
}</textarea>

Podemos mezclar todo lo anterior en una sola función `MergeSort` en donde todo ensambla de la siguiente manera:

<textarea class="cpp">
void MergeSort (int inicio, int fin)
{
    if (inicio == fin) return;
    
    int mitad=(inicio+fin)/2;
        
    MergeSort(inicio, mitad);
    MergeSort(mitad+1, fin);
    
    for (int i=inicio; i<=mitad; i++){
        cola1.push(arreglo[i]);
    }
    for (int i=mitad+1; i<=fin; i++){
        cola2.push(arreglo[i]);
    }
    
    int pos=inicio;
    
    while (!cola1.empty() || !cola2.empty()){
        if (cola2.empty()){
            arreglo[pos]=cola1.front();
            cola1.pop();
        } else
        if (cola1.empty()){
            arreglo[pos]=cola2.front();
            cola2.pop();
        } else
        if (cola1.front() < cola2.front()){
            arreglo[pos]=cola1.front();
            cola1.pop();
        } else {
            arreglo[pos]=cola2.front();
            cola2.pop();
        }
        pos++;
    }
    return;
}</textarea>

Puedes probar a mostrar el arreglo completo cada que terminas una mezcla, es decir cada que sales del ciclo `while`. De esa forma podrás ver como los datos se van ordenando en subconjuntos, y entenderás con mayor detalle como funciona el algoritmo (y como funciona la recursión).

## Complejidad

Definir la complejidad del algoritmo *Merge sort* no es tan sencillo como definir la de *Bubble sort*, por ejemplo, dado que es un poco más complicado visualizar la forma en la que recorremos los elementos a ordenar, sin embargo, dividimos nuestro conjunto en mitades hasta llegar a conjuntos unitarios. Cada llamada recursiva tiene una complejidad $$O(n)$$  y se requiere un total de $$O(log n)$$ llamadas recursivas para dividir totalmente el conjunto, por esto, podemos decir que el algoritmo *Merge sort* es de complejidad $$O(n log n)$$, en el peor de los casos.

Hay varias acciones que podemos tomar para optimizar el algoritmo, por ejemplo, si estamos por mezclar dos subconjuntos, el subconjunto `A` y el subconjunto `B` y el elemento más grande del subconjunto `A` es menor o igual que el elemento más chico de `B`, entonces podemos ahorrarnos el paso de mezclar y simplemente decir que `A` va antes de `B` y *unirlos* de esa forma.