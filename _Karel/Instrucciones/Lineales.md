---
layout: G-Article
title: Instrucciones lineales en Karel
tags: [Instrucciones]
Hide_Tags: true
categories: [C++, OMI]
---

El funcionamiento de todo programa puede verse tan simple como **tomar una serie de instrucciones e ir haciendo lo que cada una indica**. <br>
Imaginemos ahora, que nos dan instrucciones a nosotros para realizar una tarea, y detallan esas instrucciones en una hoja de papel, podríamos tomar a esa hoja como el **código** de un programa y a nosotros como el robot que seguirá ese código. <br>
Las instrucciones que se realizan en exactamente el mismo orden en el que están escritas, **que no requieren regresar ni adelantarnos** en los pasos, son **instrucciones lineales**.

{: #ListaContenido}
- Comandos básicos
- Avanzar
- Girar a la izquierda
- Coger un zumbador
- Dejar un zumbador
- Apagarse

## Comandos básicos

En el caso de Karel, una instrucción o **comando** lineal, no es diferente a lo que se decía arriba, y podemos decir además, que es algo que Karel **tratará de hacer sin importar nada** (<s>sin pensar</s>).

Se puede decir que hay **5 acciones** (<span>o comandos</span>) que Karel naturalmente sabe hacer, y que aunque parezcan pocas siempre le han bastado para resolver sus problemas; `avanza`, `gira-izquierda`, `coge-zumbador`, `deja-zumbador` y `apagate`.

> La palabra [comando](https://es.wikipedia.org/wiki/Comando_%28inform%C3%A1tica%29){: target="_blank"} viene del inglés *command* que significa **orden o instrucción**.

> Con la versión de la OMI sabemos que hemos introducido un comando correctamente porque su color se hace azul.

## Avanzar

Cuando Karel recibe la instrucción `avanza`, se desplaza una calle o una avenida hacia adelante, es decir, se mueve **un paso hacia la dirección a la que está orientado**.<br>
Karel avanzará todas las veces que tú le indiques siempre y cuando **le sea posible**.

[<picture>
	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Karel/Avanza.gif">
	<img class="Imagen" src="{{ site.iP-Sources }}/Multimedia/Karel/AvanzaC.gif" alt="Avanza">
</picture>]({{ site.iP-Sources }}/Multimedia/Karel/AvanzaC.gif){: data-lightbox="image-1"}

Sintaxis:

<textarea class="eKarel">
avanza;</textarea>

Karel, aunque hábil, no puede atravesar paredes, así que de intentarlo, mostrará un mensaje de error.

## Gira a la izquierda

Durante la ejecución de un programa **Karel se orienta girando**. Toma en cuenta que sólo puede girar hacia la izquierda, y sólo dando giros de exactamente 90°, de no ser así Karel quedaría orientado en una posición intermedia, cosa que, como ya habíamos dicho, no puede pasar.

[<picture>
	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Karel/KGira.gif">
	<img class="Imagen" src="{{ site.iP-Sources }}/Multimedia/Karel/KGiraC.gif" alt="Gira-izquierda">
</picture>]({{ site.iP-Sources }}/Multimedia/Karel/KGiraC.gif){: data-lightbox="image-1"}

Sintaxis:

<textarea class="eKarel">
gira-izquierda;</textarea>

> A diferencia de la instrucción `avanza`, **no hay nada** que pueda impedir a Karel girar.

## Coger un zumbador

Karel puede tomar un zumbador si así se requiere, al tomarlo lo guarda en su mochila. En el mundo lo podemos ver porque disminuye en uno la cantidad de zumbadores en esa posición y aumenta la cantidad en la mochila.<br>
Por cada instrucción `coge-zumbador` Karel toma un zumbador, y así sucesivamente hasta que ya no pueda hacerlo o se indique hacer otra cosa.

[<picture>
	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Karel/KCoge.gif">
	<img class="Imagen" src="{{ site.iP-Sources }}/Multimedia/Karel/KCogeC.gif" alt="Coge-zumbador">
</picture>]({{ site.iP-Sources }}/Multimedia/Karel/KCogeC.gif){: data-lightbox="image-1"}

Sintaxis:

<textarea class="eKarel">
coge-zumbador;</textarea>

> Karel no puede tomar un zumbador de donde no hay <s>(lógicamente)</s>.

## Dejar un zumbador

Así como puede tomar, Karel también puede dejar zumbadores en una posición. Lo podemos notar en el mundo porque aumenta en uno la cantidad de zumbadores en esa posición y disminuye la cantidad en la mochila. <br>
Por cada instrucción `deja-zumbador` Karel deja un zumbador, y así sucesivamente hasta que ya no pueda hacerlo o se indique hacer otra cosa.

[<picture>
	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Karel/KDeja.gif">
	<img class="Imagen" src="{{ site.iP-Sources }}/Multimedia/Karel/KDejaC.gif" alt="Deja-zumbador">
</picture>]({{ site.iP-Sources }}/Multimedia/Karel/KDejaC.gif){: data-lightbox="image-1"}

Sintaxis:

<textarea class="eKarel">
deja-zumbador;</textarea>

> Karel no puede dejar un zumbador si ya no tiene en la mochila (<s>lógicamente</s>).

## Apagarse

La instrucción que Karel siempre deberá realizar al final es apagarse, después de esta instrucción Karel no hará nada más, por lo que debe dejarse hasta el final de nuestro programa.<br>
Karel no puede "reiniciarse" si no es volviendo a iniciar la ejecución, porque como seguramente ya notaste, no tiene una instrucción de "enciende". Así, una vez que se apaga termina la ejecución.

Sintaxis:

<textarea class="eKarel">
apagate;</textarea>

> No importa si hay comandos después de `apagate`, al llegar a éste, la ejecución terminará.

<div class="Nav">
	<a href="{{ site.baseurl }}/Karel/Principio/Simulador/">Tema anterior</a> | <a href="{{ site.baseurl }}/Karel/Instrucciones/Condicionales/">Tema siguiente</a>
</div>