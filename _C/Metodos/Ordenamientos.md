---
layout: G-Article
title: Introducción a ordenamientos
author: rivel_co
tags: [Algoritmo, Ordenamientos, Introducción]
Hide_Tags: true
olimpiada: [OMI]
subject: [C++]
---

Una gran cantidad de problemas, de muchos tipos, requieren para su solución que los datos se encuentren en orden. La utilidad de trabajar con información ordenada es inmensa, en ocasiones no sólo facilita la solución de un problema, sino que además puede llegar a ser la única solución.

{: #ListaContenido}
- Principio del ordenamiento
- Utilidad del ordenamiento
- Posiciones compartidas

## Principio del ordenamiento

Es importante aclarar la definición de ordenamiento que usaremos aquí:

Datos ordenados
 : Conjunto de datos que guardan entre ellos una relación conocida en base a determinada característica, y se ubican en una posición específica del conjunto en base a dicha característica.

Con lo anterior, podemos notar que podemos ordenar cualquier conjunto de muchísimas formas, siempre y cuando podamos cuantificar cada característica. Por ejemplo, si nuestro conjunto es un determinado número de pasteles, podemos ordenarlos de acuerdo a su peso, comenzando por ubicar el pastel de menor peso y terminando con el de peso mayor, o al revés. En este caso hacemos uso de ***valores numéricos***.

Es importante saber cuantificar las características de una forma que nos permita ubicar fácilmente cada dato del conjunto. Por ejemplo, si queremos ordenar los pasteles en base a su sabor, nos encontraremos con datos como `vainilla, chocolate, napolitano, rompope`. Esta información puede parecer inservible para ordenar datos, dado que puede parecer ilógico decir que un determinado sabor va antes que otro. Sin embargo, aún en estos casos podemos aplicar un criterio útil y sencillo, como el ***orden alfabético***. Si aplicamos ese criterio, podemos ordenar los valores de la forma `chocolate, napolitano, rompope, vainilla`.

## Utilidad del ordenamiento

Seguramente ya te habrás preguntado <span>¿de qué sirve en la práctica ordenar los datos?</span> Los datos ordenados facilitan mucho operaciones de búsqueda, por ejemplo. Y esto tiene sentido, de forma cotidiana lo aplicamos cuando buscamos un contacto en la agenda del teléfono. Normalmente conocemos el nombre del contacto a buscar (*valor buscado*) y sabemos que nuestra agenda aplica un criterio alfabético para ordenar los contactos. Entonces, si buscamos a alguien cuyo nombre comienza con `Z`, sabemos que se encontrará al final de la agenda, si buscamos a alguien cuyo nombre empieza con `B`, sabemos que lo encontraremos al inicio.

Entonces, trabajar con datos ordenados nos ayuda a encontrar más fácilmente un determinado elemento del conjunto.

Otra gran utilidad es que en un conjunto de datos ordenados, cada dato guarda una ***relación conocida*** según su posición en el conjunto. Esta es información muy valiosa en muchos problemas, si conocemos, por ejemplo, que hemos ordenado un conjunto de números diferentes en orden creciente, entonces podemos saber que determinado numero en el conjunto es menor que el número siguiente y mayor que el número anterior.

## Posiciones compartidas

En el caso planteado en el párrafo anterior, es importante recordar que los números son todos diferentes, es decir, es como ordenar el conjunto `3, 6, 8, 1, 32, 0` a la forma `0, 1, 3, 6, 8, 32`. Sin embargo, muy a menudo nos encontraremos con datos que pueden no ser del todo diferentes, por ejemplo, el conjunto `8, 3, 6, 0 ,9 ,2, 3, 9` quedaría ordenado de forma creciente así `0, 2, 3, 3, 6, 8, 9, 9`. Podemos notar que hay datos repetidos, y que por lo tanto, en nuestro criterio de ordenamiento son iguales.

En este caso, podemos escoger un nuevo criterio de ordenamiento o no. Si el criterio que aplicamos es ***eficiente***, entonces no importará que los datos tengan valores iguales en el ordenamiento, pues no se alterará nuestro procedimiento ni resultado final de la tarea.

<div class="Nav">
    <a href="{{ site.baseurl }}/C++/Metodos/Recursion/" title="Recursión &vert; #iP Code">Tema anterior</a> | <a href="{{ site.baseurl }}/C++/Metodos/Ordenamientos/Bubble-sort/" title="Bubble sort &vert; #iP Code">Tema siguiente</a>
</div>