---
layout: G-Article
title: Greedy
author: rivel_co
tags: [Greedy, Método]
Hide_Tags: true
olimpiada: [OMI]
subject: [C++]
---

Esta es una técnica que resulta útil y sospechosamente sencilla de implementar al momento de resolver un problema. Probar que un problema tiene las características necesarias para realizar una *greedy* no es nada trivial. La traducción de *greedy* es codicioso y justamente se usa este término por el razonamiento que utiliza.

{: #ListaContenido}
- Características de una solución greedy
- Un problema clásico
- Usos indirectos de greedy
- Greedy no siempre es la respuesta
- Conclusión

## Características de una solución greedy

Decimos que un problema se resuelve con una solución *greedy* cuando cumple con una condición específica: si a cada paso que damos en la construcción de la *mejor solución* de un problema, tomamos la decisión que en ese momento parezca la mejor, entonces al final habremos formado la mejor solución. Esto quiere decir que además el problema tiene que tener la característica de tener subestructuras óptimas, es decir, si dividimos el problema en subproblemas y resolvemos cada uno de la mejor manera entonces al final habremos resulto todo el problema de la mejor forma también.

Muchos problemas parecen tener estas características, pero es el principio principal de *greedy* el que es poco frecuente de aplicar. No siempre tomar la mejor decisión en el momento actual nos llevará a la mejor solución de todas las posibles.

## Un problema clásico

El problema clásico de uso de esta metodología es lo siguiente: se tiene una cantidad ilimitada de monedas de $$d$$ diferentes denominaciones, por ejemplo $$1, 2, 5, 10$$. El problema consiste en saber cuál es la cantidad más chica de monedas que hay que tomar para representar una cantidad $$x$$.

Un algoritmo greedy nos llevará a pensar que lo mejor es tomar la mayor cantidad posible de monedas de la mayor denominación que sea menor a $$x$$. Una vez que ya no podamos usar más esa denominación entonces tomamos de la que sigue (más chica), cuando ya no se pueda tomamos de la que sigue y así hasta terminar. Por ejemplo, si queremos representar $$x = 47$$ primero trataremos de tomar todo lo posible de la mayor denominación ($$10$$), podremos tomar hasta $$4$$ monedas, luego seguimos con la denominación inmediatamente más chica ($$5$$), de la cual tomamos sólo una moneda. Pasamos a la denominación de $$2$$ y tomamos una moneda también. Habremos tomado en total $$6$$ monedas, ésta es la respuesta óptima.

Este problema clásico cumple con todo lo necesario, tiene subproblemas óptimos y la mejor respuesta en cada estado nos lleva a la mejor respuesta de todo el problema. Si queremos representar $$47$$ de forma óptima y primero usamos $$1$$ moneda de $$10$$, nos quedará por representar $$37$$, de aquí ahora tenemos el problema de representar de forma óptima ese $$37$$, su respuesta contribuirá directamente a la del problema total y nos dará una respuesta global.

## Usos indirectos de greedy

El problema [10340 - All in All de UVa](https://uva.onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=1281){:target="_blank"} nos presenta de forma breve la siguiente situación: Se reciben pares de cadenas de caracteres, la cadena `A` seguida de la cadena `B`. Hay que responder si es posible transformar a `B` en `A` únicamente borrando caracteres. Se distingue entre mayúsculas y minúsculas. En caso de que `B` se pueda convertir en `A` con estas reglas, hay que imprimir `Yes`, en caso contrario hay que imprimir `No`. Un caso de ejemplo puede ser `A = "Diana"` y `B = "DinosauriosNadandoAlegres"`. En este caso, la respuesta debe ser `Yes`.

Aquí podemos proponer una solución siguiendo un principio *greedy*, si tomamos el caracter `A[x]` y lo buscamos en `B` desde `B[0]` y no lo encontramos entonces definitivamente no podemos formar `A` usando a `B`. Si lo encontramos en la posición `B[y]` y ahora buscamos el caracter `A[x+1]` entonces no debemos buscar antes de `B[y]` sino después y esto es justamente para que se mantenga el orden de los caracteres.

Entonces, si buscamos en orden siempre estaremos asegurándonos que los caracteres de `A` que se encuentren en `B` estén dispuestos en exactamente el mismo orden. Si están dispuestos en el mismo orden y podemos encontrar todos los caracteres de `A` entonces en efecto `B` se puede transformar en `A` únicamente borrando caracteres y sin alterar el orden de las letras.

## Greedy no siempre es la respuesta

En ocasiones un problema parece que puede ser respondido utilizando *greedy*, sin embargo, es muy importante analizar bien los posibles casos, muchas veces (muchas) no se puede seguir un razonamiento de "la mejor respuesta en este estado me llevará a la mejor repuesta del problema". Toma como ejemplo el siguiente problema:

Queremos comprar un pan de cada una de las $$y$$ categorías de pan de una tienda. En cada categoría el precio de sus panes específicos varía. Llevamos un presupuesto de $$x$$ cantidad de dinero y queremos gastar lo más que se pueda de ese presupuesto. De entrada recibimos la cantidad de categorías $$y$$ y el presupuesto $$x$$, en las siguientes $$y$$ líneas recibimos un entero que representa la cantidad $$y_i$$ de panes de esa línea, luego siguen $$y_i$$ enteros representando el precio de cada pan en particular. La salida debe ser la cantidad máxima de dinero que se puede gastar comprando un pan de cada categoría, se debe imprimir `-1` si esto no es posible. Una entrada de ejemplo es:

<textarea class="plain-text">
4 30
4 6 2 8 4
3 1 7 5
2 8 10
3 7 9 4</textarea>

Una respuesta greedy del problema anterior iría escogiendo el precio más alto de cada categoría (para gastar lo más posible). Entonces el algoritmo trataría de seleccionar los panes de precio $$8, 7, 10, 9$$ dando un total de $$34$$. Como esto excede del total a comprar entonces el algoritmo regresaría `-1`. Si únicamente cuidamos que el último elemento a comprar sea lo suficientemente pequeño para que ajuste el presupuesto, aún así tendríamos una respuesta incorrecta de $$29$$. La respuesta correcta de este problema es $$30$$.

> Recuerda que no podemos estar parchando problemas para casos especiales que nunca acaban, al final el código será una cosa indescifrable que será casi imposible de corregir y entender.

Como puedes notar, el algoritmo greedy no aplica aquí, aunque con algunos ejemplos especiales podría parecer que sí, esto es muy importante de tener en cuenta al momento de tratar de implementar este tipo de métodos.

## Conclusión

Es de suma importancia identificar las subestructuras óptimas y el principio de "mejor decisión a cada paso forma la mejor decisión global". En ocasiones algunos problemas pueden parecer resueltos con *greedy* cuando en realidad no es así, es importante realizar diversos casos y razonar el funcionamiento y las condiciones de cada problema en particular.

Algunos competidores inexpertos evalúan los problemas que requieren de *greedy* como *muy fáciles*. Esto no es necesariamente cierto, como ya se decía la cosa se complica cuando queremos demostrar que este método es adecuado porque el problema cumple con todas las características. A menudo se confunde con *greedy* un algoritmo que en realidad se resuelve con [DP]({{ site.baseurl }}/C++/Metodos/DP/ "DP - #iP Code"){:target="_blank"}. Cuando esto es así lo que se obtiene del evaluador es un **WA**, no un **TLE**, pues normalmente las soluciones greedy son muy rápidas.

<div class="Nav">
    <a id="navLeft" href="{{ site.baseurl }}/C++/Metodos/Busquedas/Profundidad/Matrices/" title="Busqueda en amplitud &vert; #iP Code">
        Tema anterior
        <span>Busqueda en amplitud</span>
    </a>
    <a id="navRight" href="{{ site.baseurl }}/C++/Metodos/DP/" title="Dynamic Programming &vert; #iP Code">
        Tema siguiente
        <span>Dynamic Programming</span>
    </a>
</div>