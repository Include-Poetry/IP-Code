---
layout: G-Article
title: Instrucciones lineales en Karel
author: rivel_co
tags: [Instrucciones]
Hide_Tags: true
olimpiada: [OMIPS]
subject: [Karel pascal]
---

El funcionamiento de todo programa puede verse tan simple como **tomar una serie de instrucciones e ir haciendo lo que cada una indica**. Imaginemos ahora, que nos dan instrucciones a nosotros para realizar una tarea y detallan esas instrucciones en una hoja de papel, podríamos tomar a esa hoja como el **código** de un programa y a nosotros como el robot que seguirá ese código. Las instrucciones que se realizan en exactamente el mismo orden en el que están escritas, **que no requieren regresar ni adelantarnos** en los pasos, son **instrucciones lineales**.

{: #ListaContenido}
- Comandos básicos
- Avanzar
- Gira a la izquierda
- Coger un zumbador
- Dejar un zumbador
- Apagarse

## Comandos básicos

En el caso de Karel, una instrucción o **comando** lineal, no es diferente a lo que se decía arriba y podemos decir además, que es algo que Karel **tratará de hacer sin importar nada** (<s>sin pensar</s>).

Se puede decir que hay **5 acciones** (<span>o comandos</span>) que Karel naturalmente sabe hacer y que aunque parezcan pocas siempre le han bastado para resolver sus problemas, en Pascal son `avanza`, `gira-izquierda`, `coge-zumbador`, `deja-zumbador` y `apagate`, para Java son `move()`, `turnleft()`, `takebeeper()`, `putbeeper` y `shutdown()`.

> La palabra [comando](https://es.wikipedia.org/wiki/Comando_%28inform%C3%A1tica%29){: target="_blank"} viene del inglés *command* que significa **orden o instrucción**.

> En #iP los comandos los verás indicados de color azul claro, tanto en Pascal como en Java.

## Avanzar

Cuando Karel recibe la instrucción `avanza | move()`, se desplaza una calle o una avenida hacia adelante, es decir, se mueve **un paso hacia la dirección a la que está orientado**. Karel avanzará todas las veces que tú le indiques siempre y cuando **le sea posible**.

[<picture>
	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Karel/Avanza.gif">
	<img class="Imagen" src="{{ site.iP-Sources }}/Multimedia/Karel/AvanzaC.gif" alt="Avanza">
</picture>]({{ site.iP-Sources }}/Multimedia/Karel/AvanzaC.gif){: data-lightbox="image-1"}

Sintaxis:

<div class="karelBlock">
<textarea class="karelp">
avanza;</textarea>
<textarea class="karelj">
move();</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Karel, aunque hábil, no puede atravesar paredes, así que de intentarlo, mostrará un mensaje de error.

## Gira a la izquierda

Durante la ejecución de un programa **Karel se orienta girando**. Toma en cuenta que sólo puede girar hacia la izquierda y sólo dando giros de exactamente 90°, de no ser así Karel quedaría orientado en una posición intermedia, cosa que, como ya habíamos dicho, no puede pasar.

[<picture>
	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Karel/KGira.gif">
	<img class="Imagen" src="{{ site.iP-Sources }}/Multimedia/Karel/KGiraC.gif" alt="Gira-izquierda">
</picture>]({{ site.iP-Sources }}/Multimedia/Karel/KGiraC.gif){: data-lightbox="image-1"}

Sintaxis:

<div class="karelBlock">
<textarea class="karelp">
gira-izquierda;</textarea>
<textarea class="karelj">
turnleft();</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

> A diferencia de la instrucción `avanza | move()`, **no hay nada** que pueda impedir a Karel girar.

## Coger un zumbador

Karel puede tomar un zumbador si así se requiere, al tomarlo lo guarda en su mochila. En el mundo lo podemos ver porque disminuye en uno la cantidad de zumbadores en esa posición y aumenta la cantidad en la mochila.Por cada instrucción `coge-zumbador | pickbeeper()` Karel toma un zumbador y así sucesivamente hasta que ya no pueda hacerlo o se indique hacer otra cosa.

[<picture>
	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Karel/KCoge.gif">
	<img class="Imagen" src="{{ site.iP-Sources }}/Multimedia/Karel/KCogeC.gif" alt="Coge-zumbador">
</picture>]({{ site.iP-Sources }}/Multimedia/Karel/KCogeC.gif){: data-lightbox="image-1"}

Sintaxis:

<div class="karelBlock">
<textarea class="karelp">
coge-zumbador;</textarea>
<textarea class="karelj">
pickbeeper();</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

> Karel no puede tomar un zumbador de donde no hay <s>(lógicamente)</s>.

## Dejar un zumbador

Así como puede tomar, Karel también puede dejar zumbadores en una posición. Lo podemos notar en el mundo porque aumenta en uno la cantidad de zumbadores en esa posición y disminuye la cantidad en la mochila. Por cada instrucción `deja-zumbador | putbeeper()` Karel deja un zumbador y así sucesivamente hasta que ya no pueda hacerlo o se indique hacer otra cosa.

[<picture>
	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Karel/KDeja.gif">
	<img class="Imagen" src="{{ site.iP-Sources }}/Multimedia/Karel/KDejaC.gif" alt="Deja-zumbador">
</picture>]({{ site.iP-Sources }}/Multimedia/Karel/KDejaC.gif){: data-lightbox="image-1"}

Sintaxis:

<div class="karelBlock">
<textarea class="karelp">
deja-zumbador;</textarea>
<textarea class="karelj">
putbeeper();</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

> Karel no puede dejar un zumbador si ya no tiene en la mochila (<s>lógicamente</s>).

## Apagarse

La instrucción que Karel siempre deberá realizar al final es apagarse, después de esta instrucción Karel no hará nada más, por lo que debe dejarse hasta el final de nuestro programa. Karel no puede "reiniciarse" si no es volviendo a iniciar la ejecución, porque como seguramente ya notaste, no tiene una instrucción de "enciende". Así, una vez que se apaga termina la ejecución.

Sintaxis:

<div class="karelBlock">
<textarea class="karelp">
apagate; {* también con acento: *} apágate;</textarea>
<textarea class="karelj">
turnoff();</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

> No importa si hay comandos después de `apagate | turnoff()`, al llegar a éste, la ejecución terminará.

<div class="Nav">
	<a href="{{ site.baseurl }}/Karel/Principio/Simulador/" title="Simulador Karel.js &vert; #iP Code">Tema anterior</a> | <a href="{{ site.baseurl }}/Karel/Instrucciones/Condicionales/" title="Instrucciones condicionales &vert; #iP Code">Tema siguiente</a>
</div>