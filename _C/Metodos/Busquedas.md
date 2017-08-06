---
layout: G-Article
title: Introducción a búsquedas
author: rivel_co
tags: [Búsquedas, Introducción, Algoritmo]
Hide_Tags: true
olimpiada: [OMI]
subject: [C++]
---

La definición más simple de ***búsqueda***, es literalmente determinar si un elemento se encuentra en un determinado conjunto. Este concepto se puede expandir hasta ser definida como una relación posible de estados.

{: #ListaContenido}
- Preparando el terreno
- Componentes de la búsqueda
- Tipos de búsquedas
- Realización de una búsqueda

## Preparando el terreno

El primer aspecto importante en la búsqueda de datos, es la forma en la que se ***almacenan*** e ***indexan***.

### Almacenamiento

A pesar de que la [STL]({{ site.baseurl }}/C++/STL/ "STL"){: target="_blank"} nos brinda una gran cantidad de contenedores para todo tipo de dato, normalmente lo más recomendable y práctico, es utilizar [arreglos]({{ site.baseurl }}/C++/Introduccion/Arreglos/ "Arreglos"){: target="_blank"} convencionales. 

> Recuerda que normalmente los problemas del estilo de la OMI retan tu capacidad de crear, implementar y modificar algoritmos, más que el manejo de estructuras.

Generalmente la desventaja principal de utilizar arreglos, es la capacidad de almacenaje. Digamos que un arreglo puede contener cómodamente ***un millón de locaciones***, que es una cantidad típicamente más que suficiente para la mayoría de los problemas, claro está, que no para todos.

Otra posible desventaja, es que probablemente queramos almacenar datos y procesarlos de forma específica al retirarlos o al ingresarlos, como en el caso de las [pilas]({{site.baseurl}}/C++/Esructuras/Pila/ "Implementación de pila"){: target="_blank"} o de las [colas]({{site.baseurl}}/C++/Estructuras/Cola/ "Implementación de cola"){: target="_blank"}. Aún para ese tipo de estructuras sencillas, lo más recomendable es usar arreglos.

### Indexación

La cosa no sólo es en dónde se guardan los datos, sino ***cómo*** se guardan:

> [Indexar](http://dle.rae.es/?id=LNTIjYS "En la RAE"){: target="_blank"}: <br>
> 2.- tr. Registrar ordenadamente datos e informaciones, para elaborar su índice.

A diferencia de lo que se puede pensar, al decir *ordenadamente* en la definición, no necesariamente estamos hablando de un orden de mayor a menor por ejemplo, sino cualquier organización intencional, conocida y con un propósito específico. Según sea el problema en cuestión, será el orden establecido para los datos que almacenamos.

## Componentes de la búsqueda

Existen dos principales componentes en una búsqueda, que nos ayudan en la definición más general de búsqueda:

### Estados

Entendamos por estado cada punto o situación de una búsqueda, por ejemplo, en el caso en el que te encuentras buscando un determinado edificio en la ciudad, para lograrlo, utilizas un GPS que te dirige desde tu posición actual, hasta la posición en que se encuentra el edificio. Tu posición en el primer momento define el ***estado inicial***. De la misma forma, la posición del edificio define el ***estado final*** pues es el último punto al que se quiere llegar. Ambos *estados* se componen de una ubicación geográfica en un mapa, por lo que existen muchísimos posibles estados, de hecho, mientras te desplazas desde tu ubicación hasta el edificio estarás modificando tu ***estado actual***.

> Los estados nos permiten conocer las características específicas que describen un punto en la búsqueda.

Otro punto muy importante es la ***relación entre estados***. Decimos que un estado es ***inmediato*** o ***adyacente*** a otro si es posible ir de uno a otro en sólo un movimiento válido. Sabremos cuáles son las reglas para relacionar dos estados en base a las reglas de cada problema en particular. Por ejemplo, la siguiente figura expresa un mapa de carreteras entre las ciudades $$A, B, C, D, E, F$$, nota que si te encuentras en la ciudad $$A$$ no puedes llegar *de la nada* a la ciudad $$C$$, al menos no por carretera. Sin embargo, sí puedes llegar por carretera a la ciudad $$B$$ y a la $$E$$. En otras palabras, el estado correspondiente a la ciudad $$A$$ es inmediato o adyacente a el estado correspondiente a la ciudad $$B$$ y $$E$$, y no lo es para la ciudad $$C$$ ni $$D$$ ni $$F$$. No obstante, es posible llegar llegar a la ciudad $$C$$ si atravesamos la ciudad $$B$$ o la ciudad $$E$$ y $$D$$.

[![Mapa de ciudades por carretera]({{ site.iP-Sources }}/Multimedia/C/Fig1.png "Mapa de ciudades y carreteras")]({{ site.iP-Sources }}/Multimedia/C/Fig1.png "Mapa de ciudades y carreteras"){: data-lightbox="image-1"}

### Condiciones de validez

En toda búsqueda, dos estados se relacionan entre sí de forma inmediata si estos cumplen determinadas condiciones. Volviendo al ejemplo de las ciudades y carreteras, nota que hemos definido que el estado relacionado a la ciudad $$A$$ no es inmediato al relacionado a la ciudad $$C$$ en base a las reglas de las carreteras existentes, de haber dicho, por ejemplo, que puedes volar de una ciudad a otra, entonces todas las ciudades y sus estados correspondientes serían inmediatos entre sí. A esto es a lo que se hace referencia cuando se dice que la relación entre estados está dada por las reglas de cada problema.

> Para poder relacionar dos estados de forma inmediata o no inmediata, se tienen que cumplir las reglas declaradas por el problema.

### Podas

Una poda es una situación de descarte de estados, este descarte se realiza en base a las reglas del problema. Por ejemplo, usando nuestro mapa de ciudades y carreteras, podemos agregar una nueva regla, como "*podemos atravesar una ciudad siempre y cuando ésta no esté conectada a más de dos ciudades distintas*", entonces para ir de la ciudad $$A$$ a la ciudad $$C$$, podemos tomar el camino a través de las ciudades $$E$$ y $$D$$ pero no el camino atravesando por la ciudad $$B$$, pues no cumple con la nueva regla. En nuestra búsqueda de caminos a la ciudad $$C$$, podemos evitar los caminos que requieran pasar por la ciudad $$B$$, o en otras palabras, podemos podar los caminos que requieran del estado relacionado a la ciudad $$B$$. 

> Las podas posibles de una búsqueda son creadas en base a las reglas del problema y hacen que nuestra búsqueda sea más rápida, pues evitamos estados innecesarios.

###  Estado final

El estado final de una búsqueda es aquél en el que ya no es necesario seguir revisando más estados, pues habremos terminado nuestro problema. Por ejemplo, una vez que llegamos a la ciudad $$C$$, no es necesario ver el resto de las ciudades que están conectadas a ella, pues ya estamos ahí y hemos cumplido con nuestro objetivo. Es importante siempre considerar nuestro estado final para poder realizar búsquedas finitas y efectivas.

## Tipos de búsquedas

Existen muchos tipos de búsquedas, que pueden ser utilizadas en distintos y específicos tipos de problema. Dos muy frecuentes son los siguientes:

### Búsqueda de valores

Es un tipo muy común y el más sencillo de todos. Es utilizada para determinar si un elemento pertenece a un conjunto de datos, por ejemplo decir si existen números primos en un determinado conjunto de números. Para resolver lo anterior, tendrás que buscar entre todos los números del conjunto aquellos que cumplan con la definición de número primo, y para ello deberás considerar sus divisores y de hecho, puedes hacer varias podas.

### Búsquedas de posibilidades

Otra búsqueda muy común es aquella que determina si algo es posible o no. Por ejemplo, en el caso de nuestro mapa de ciudades y carreteras, puedes decir si es posible ir de una ciudad a otra en base a ciertas reglas. Para esto deberás ir relacionando de forma válida cada estado y realizando podas hasta llegar (o no) a la ciudad de destino. 

## Realización de una búsqueda

Una vez que has identificado qué tipo de búsqueda es necesaria en el problema, puedes pasar a la representación de los componentes de la búsqueda.

### Datos de la búsqueda

Son los datos que conforman nuestra entrada, por ejemplo el conjunto de números en el que deberás buscar si hay números primos o no. Aquí es donde importa muchísimo la forma en la que almacenas e indexas los datos, recuerda siempre hacerlo de una forma que puedas comprender qué significa cada elemento y la forma que lo indexaste. Mientras más sencillo sea tu método de almacenamiento e indexación, más sencillo te será manipular los datos y resolver el problema.

### Estados

Resulta muy útil crear una [clase]({{ site.baseurl }}/C++/Estructuras/Class/ "Clases"){: target="_blank"} o una [estructura]({{ site.baseurl }}/C++/Estructuras/Struct/ "Estructuras"){: target="_blank"} para expresar las características que conforman un estado. Por ejemplo en nuestro problema de las ciudades y el máximo número de ciudades conectadas, podemos dar como definición de estado algo como sigue:

<textarea class="editor">
struct estado{
    char id;
    int conexiones;
};</textarea>

De esta forma, en un mismo tipo `estado` puedes guardar el caracter de identificación de una ciudad y la cantidad de conexiones que tiene.

### Podas y condiciones de validez

Estas dos partes son comúnmente expresadas como simples condiciones, en donde si determinadas situaciones se cumplen, entonces no se realice el procesamiento de ese estado (poda) o que sí se realice (condiciones de validez). En otros problemas particulares, determinar una poda o condición de validez requiere de métodos más complejos y elaborados, sin embargo siempre son del mismo principio.

## Conclusión

Las ***búsquedas*** nos permiten determinar si un elemento ***se encuentra*** en un determinado conjunto, como también si un determinado procedimiento ***es posible***, todo se realiza gracias a la ***relación entre los estados*** que definen a una búsqueda, y estos estados se ***relacionan*** en base a las ***reglas*** de cada problema. Podemos acelerar una búsqueda utilizando ***podas*** que es el descarte de estados en base de las reglas. Para poder considerar un estado como parte de una solución, ese estado deberá cumplir con ciertas ***reglas de validez***. Finalizamos nuestra búsqueda cuando llegamos al ***estado final***, que puede estar o no, inmediatamente relacionado al ***estado inicial***, en donde todo comienza.

<div class="Nav">
    <a href="{{ site.baseurl }}/C++/Metodos/Ordenamientos/Merge-sort/">Tema anterior</a> | <a href="{{ site.baseurl }}/C++/Metodos/Busquedas/Lineales/">Tema siguiente</a>
</div>