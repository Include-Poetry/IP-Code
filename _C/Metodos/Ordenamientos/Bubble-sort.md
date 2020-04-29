---
layout: G-Article
title: Bubble sort
date: 2020-01-04 12:00:00
author: rivel_co
tags: [Ordenamiento, Algoritmo, Arreglos]
hide_tags: true
olimpiada: [OMI]
subject: [C++]
prevTopic: "Ordenamientos, /C++/Metodos/Ordenamientos/"
nextTopic: "Merge sort, /C++/Metodos/Ordenamientos/Merge-sort/"
---

Bubble sort (*ordenamiento burbuja*) es un método bastante sencillo e intuitivo de ordenar datos. Es muy útil para comenzar a comprender las formas en las que podemos ordenar la información, aunque dada su complejidad no es muy útil en casos muy demandantes.

{: #ListaContenido}
- Idea del funcionamiento
- Implementación
- Complejidad

## Idea del funcionamiento

Para poder entender cómo funciona el algoritmo, usaremos el conjunto desordenado de datos `7, 9, 3, 4, 8` y definiremos como $$N$$ la cantidad de datos a ordenar, en este ejemplo $$N=6$$.

La forma en la que funciona el algoritmo del *Bubble sort* es utilizando ***intercambios***. Por ejemplo, si queremos ordenar los datos de forma creciente, sabemos que hemos de dejar al principio (lado izquierdo) los valores más pequeños. Entonces vamos "tomando" pares de datos y dejando del lado izquierdo el valor más pequeño. Para esto *intercambiamos* las posiciones de los dos elementos en cuestión, y dejamos en la posición de la izquierda el valor más chico, y en el de la derecha el más grande. En base a nuestro ejemplo sería:

<textarea class="output">
7, 9, 3, 4, 8     // Conjunto original
7, 9, 3, 4, 8     // De haber seleccionado el par 7 y 9, el 7 se queda a la izquierda
7, 3, 9, 4, 8     // De haber seleccionado el par 9 y 3, el 3 se mueve a la izquierda
7, 3, 4, 9, 8     // De haber seleccionado el par 9 y 4, el 4 se mueve a la izquierda
7, 3, 4, 8, 9     // De haber seleccionado el par 9 y 8, el 8 se mueve a la izquierda</textarea>

Como podrás notar, para nuestro conjunto de $$N$$ datos, hemos realizado a penas $$N-1$$ movimientos y hemos llegado al final de los pares, pero el conjunto aún no está del todo ordenado, entonces habrá que realizar otra vez el algoritmo, comenzando por el primer par de nuevo. Es importante notar también, que después de haber recorrido todos los datos una vez, al final quedará el más grande de los datos en el extremo derecho, dado que siempre se habrá movido a la derecha con respecto al resto.

<textarea class="output">
7, 3, 4, 8, 9     // Después de los primeros N-1 pasos
3, 7, 4, 8, 9     // De haber seleccionado el par 7 y 3, el 3 se mueve a la izquierda
3, 4, 7, 8, 9     // De haber seleccionado el par 7 y 4, el 4 se mueve a la izquierda
3, 4, 7, 8, 9     // De haber seleccionado el par 7 y 8, el 7 se queda a la izquierda
3, 4, 7, 8, 9     // De haber seleccionado el par 8 y 9, el 8 se queda a la izquierda</textarea>

Aquí ya hemos terminado otra vez con todos nuestros pares, y afortunadamente el conjunto ha quedado ordenado, sin embargo, dos repeticiones no habrían bastado para el conjunto `9, 8, 7, 6, 5`.

Puedes observar el algoritmo en acción con la siguiente animación:

<a title="By Swfung8 (Own work) [CC BY-SA 3.0 (http://creativecommons.org/licenses/by-sa/3.0) or GFDL (http://www.gnu.org/copyleft/fdl.html)], via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File%3ABubble-sort-example-300px.gif" target="_blank"><img width="256" alt="Bubble-sort-example-300px" src="https://upload.wikimedia.org/wikipedia/commons/c/c8/Bubble-sort-example-300px.gif"/></a>

## Implementación

La implementación del Bubble sort en C++ es bastante sencilla

<textarea class="cpp">
for (int i = 0; i < N; i++){
    for (int j = 0; j < N - 1; j++){
        if (conjunto[j] > conjunto[j + 1]){
            tmp = conjunto[j];
            conjunto[j] = conjunto[j + 1];
            conjunto[j + 1] = tmp;
        }
    }
}</textarea>

Nota que estamos haciendo el recorrido de todos los pares una vez por cada dato del conjunto, esto es para asegurarnos de que al final todo quede bien ordenado. Es importante notar además, que con `conjunto[j + 1]` nos referimos al siguiente elemento, contiguo a `conjunto[j]` y que debido a esto se hace una corrección en el límite del ciclo interior, al hacerlo hasta `j < N -1` y así evitar salir del arreglo.

## Complejidad

Dado que estamos realizando $$N$$ recorridos por cada dato y son $$N$$ datos, entonces podemos decir que la complejidad del algoritmo de ordenamiento *bubble sort* es $$O(n^2)$$. Recuerda que cuando hablamos de complejidad tomamos el peor de los casos posibles, y se "redondea" al factor que tiene la tasa de crecimiento mayor.

Es sencillo notar que se pueden hacer algunas mejoras al algoritmo, se puede ***optimizar*** de varias maneras, de cualquier forma, para un caso muy grande, como $$100000$$ de datos, obtendremos un desempeño muy cercano al $$O(n^2)$$. Debido a esto, el algoritmo puede ser útil como explicación general de un algoritmo de ordenamiento, dado que es sencillo de entender y sencillo de codificar, pero resulta ser poco práctico para resolver problemas en los que se manejen grandes conjuntos de datos.