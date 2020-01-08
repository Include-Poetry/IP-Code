---
layout: G-Article
title: Instrucciones cíclicas en Karel
author: rivel_co
tags: [Instrucciones, Ciclos]
Hide_Tags: true
olimpiada: [OMIPS]
subject: [Karel pascal]
---

Seguramente ya te has imaginado lo [tedioso](http://dle.rae.es/?id=ZJf6SDH){: target="_blank"} que resultaría hacer caminar 100 veces a Karel con lo que hasta ahora sabemos, pues habría que escribir 100 veces el comando `avanza; | move();`, cosa que resulta además poco práctico. Para hacer una o varias acciones una determinada cantidad de veces, utilizamos instrucciones repetitivas o cíclicas.
	
{: #ListaContenido}
- Sentencia mientras
- Sentencia repetir
- Ejemplos
- Problemas sugeridos

## Sentencia mientras

Tomemos en cuenta primeramente que existen varios tipos de repeticiones, es decir, que las realizamos bajo diferentes circunstancias, por ejemplo, cuando llueve usamos un paraguas, pero sólo **mientras** llueve, pues una vez que ya terminó de llover, deja de ser necesario. Para Karel, esta idea queda muy clara y de hecho estructura muy bien este tipo de repeticiones.

Imaginemos que Karel está en algún lugar desconocido del mundo y que queremos llevarlo hasta la pared que tenga a su frente, como no sabemos qué tan lejos está la pared de Karel, tampoco podemos saber cuántas veces debemos avanzar; puede que pongamos de menos y no llegue o puede que pongamos de más y choque contra la pared. <span>Entonces, ¿cómo saber cuántas veces avanzar?</span> Es ahí donde llega la sentencia "mientras" a auxiliarnos. Tiene la siguiente estructura:

<div class="karelBlock">
<textarea class="karelp">
mientras {*condición*} hacer {*acción-a-realizar;*}</textarea>
<textarea class="karelj">
while (/*condición*/) /* acción-a-realizar; */</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>
	
Comienza con la palabra de control `mientras | while` que le dice al compilador que sigue una sentencia repetitiva, seguido de una **condición**, luego en Pascal la palabra de control `hacer` y finalmente **las acciones a realizar**. ¿Recuerdas las [condiciones]({{ site.baseurl }}/Karel/Instrucciones/Condicionales/#condiciones-disponibles){: target="_blank"} que Karel puede evaluar? Pues aquí las volvemos a usar, para decirnos que **mientras** esa condición se cumpla, Karel realizará las acciones dichas. Por ejemplo:

<div class="karelBlock">
<textarea class="karelp">
mientras no-orientado-al-norte hacer gira-izquierda;</textarea>
<textarea class="karelj">
while (notFacingNorth) turnleft();</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Con la línea anterior nos aseguramos de que Karel se oriente al norte, pues estará girando mientras no tenga esa orientación <span>(muy útil, ¿verdad?)</span>. A estas alturas seguramente has deducido cómo resolver el problema inicial:

<div class="karelBlock">
<textarea class="karelp">
mientras frente-libre hacer avanza;</textarea>
<textarea class="karelj">
while (frontIsClear) move();</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

<span>¿Y qué hay de las [condiciones agrupadas]({{ site.baseurl }}/Karel/Instrucciones/Condicionales/#condiciones-agrupadas){: target="_blank"}?</span> Las podemos utilizar de la misma manera que con la sentencia `si | if`, utilizando una clausula `o`, `u`, `||`, una clausula `y`, `e`, `&&`, e incluso también la clausula `no | !` según nos convenga.

## Sentencia repetir

Ahora pensemos la situación en la que conocemos **exactamente** la cantidad de veces que hay que realizar algo, pero son demasiadas veces como para poner las acciones esa cantidad de veces. Es entonces cuando usamos la sentencia `repetir` en Pascal o `iterate` en Java..

<div class="karelBlock">
<textarea class="karelp">
repetir {*número*} veces {*acción-a-realizar;*}</textarea>
<textarea class="karelj">
iterate (/*número*/) /*acción-a-realizar;*/</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Si [diseccionamos](http://dle.rae.es/?id=Du8Lirp){: target="_blank"} la instrucción también, encontraremos varias partes. La palabra de control `repetir | iterate`. La cantidad de veces que se repetirán las acciones (indicado arriba como `número`). Esa cantidad puede ser cualquier número mayor a $$0$$. La palabra de control `veces` si estamos usando Pascal y las acciones a realizar. Viéndolo en un ejemplo quedaría como sigue.

<div class="karelBlock">
<textarea class="karelp">
repetir 12 veces coge-zumbador;</textarea>
<textarea class="karelj">
iterate (12) pickbeeper();</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Con el código anterior Karel tomará exactamente 12 zumbadores de la posición sobre la que está. ¿Y qué pasaría si no hay tal cantidad de zumbadores ahí? En ese caso se mostraría un mensaje de error pues Karel **no puede tomar zumbadores de donde no hay**. Es por eso que hay que ser muy cuidadosos con el uso de la sentencia `repetir | iterate`.

## Ejemplos

`mientras` sencillo

<div class="karelBlock">
<textarea class="karelp">
mientras izquierda-bloqueada hacer avanza;</textarea>
<textarea class="karelj">
while (leftIsBlocked) move();</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

`repetir` sencillo:

<div class="karelBlock">
<textarea class="karelp">
repetir 3 veces gira-izquierda;</textarea>
<textarea class="karelj">
iterate (3) turnleft();</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

`mientras` compuesto:

<div class="karelBlock">
<textarea class="karelp">
mientras izquierda-bloqueada y frente-libre hacer avanza;</textarea>
<textarea class="karelj">
while (leftIsBlocked && frontIsClear) move();</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

`mientras` con bloque:

<div class="karelBlock">
<textarea class="karelp">
mientras algun-zumbador-en-la-mochila hacer inicio
    si frente-libre entonces avanza;
    deja-zumbador;
fin;</textarea>
<textarea class="karelj">
while (anyBeepersInBeeperBag){
    if (frontIsClear) move();
    putbeeper();
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

`repetir` con bloque:

<div class="karelBlock">
<textarea class="karelp">
repetir 8 veces inicio
    avanza;
    gira-izquierda;
    repetir 2 veces deja-zumbador;
fin;</textarea>
<textarea class="karelj">
iterate (8){
    move();
    turnleft();
    iterate (2) putbeeper();
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

## Problemas sugeridos

<div id="omegaDiv">
    <ul id="omegaList">
        <li><i class="far fa-lightbulb"></i><span>Camino adelante</span><a href="https://omegaup.com/arena/problem/iP-Karel-Camino-adelante/" target="_blank" class="omegaBtn">Ver en omegaUp</a></li>
        <li><i class="far fa-lightbulb"></i><span>El hechizo de escape</span><a href="https://omegaup.com/arena/problem/iP-Karel-El-hechizo-de-escape/" target="_blank" class="omegaBtn">Ver en omegaUp</a></li>
        <li><i class="far fa-lightbulb"></i><span>Karel Pesh</span><a href="https://omegaup.com/arena/problem/iP-Karel-Karel-Pesh" target="_blank" class="omegaBtn">Ver en omegaUp</a></li>
        <li><i class="far fa-lightbulb"></i><span>Vaciando la mochila</span><a href="https://omegaup.com/arena/problem/iP-Karel-Vaciando-la-mochila/" target="_blank" class="omegaBtn">Ver en omegaUp</a></li>
    </ul>
</div>

<div class="Nav">
    <a id="navLeft" href="{{ site.baseurl }}/Karel/Instrucciones/Condicionales/" title="Instrucciones condicionales &vert; #iP Code">
        Tema anterior
        <span>Instrucciones condicionales</span>
    </a>
    <a id="navRight" href="{{ site.baseurl }}/Karel/Funciones/" title="Funciones en Karel &vert; #iP Code">
        Tema siguiente
        <span>Funciones en Karel</span>
    </a>
</div>