---
layout: G-Article
title: Instrucciones cíclicas en Karel
author: rivel_co
tags: [Instrucciones, Ciclos]
Hide_Tags: true
olimpiada: [OMIPS]
subject: [Karel pascal]
---

Seguramente ya te has imaginado lo [tedioso](http://dle.rae.es/?id=ZJf6SDH){: target="_blank"} que resultaría hacer caminar 100 veces a Karel con lo que hasta ahora sabemos, pues habría que escribir 100 veces el comando `avanza;`, cosa que resulta además poco práctico.<br>
Para hacer una o varias acciones una determinada cantidad de veces, utilizamos instrucciones repetitivas o cíclicas.
	
{: #ListaContenido}
- Sentencia mientras
- Sentencia repetir
- Ejemplos

## Sentencia mientras

Tomemos en cuenta primeramente que existen varios tipos de repeticiones, es decir, que las realizamos bajo diferentes circunstancias, por ejemplo, cuando llueve usamos un paraguas, pero sólo **mientras** llueve, pues una vez que ya terminó de llover, deja de ser necesario. <br>
Para Karel, esta idea queda muy clara, y de hecho estructura muy bien este tipo de repeticiones.

Imaginemos que Karel está en algún lugar desconocido del mundo, y que queremos llevarlo hasta la pared que tenga a su frente, como no sabemos qué tan lejos está la pared de Karel, tampoco podemos saber cuántas veces debemos avanzar, puede que pongamos de menos y no llegue o puede que pongamos de más y choque contra la pared. <span>Entonces, ¿cómo saber cuántas veces avanzar?</span><br>
Es ahí donde llega la sentencia "mientras" a auxiliarnos. Tiene la siguiente estructura:

<textarea class="output">
mientras condición hacer acción-a-realizar;</textarea>
	
Comienza con la palabra de control `mientras` que le dice al compilador que sigue una sentencia repetitiva, seguido de una **condición**, luego la palabra de control `hacer` y finalmente **las acciones a realizar**. <br>
¿Recuerdas las [condiciones]({{ site.baseurl }}/Karel/Instrucciones/Condicionales/#condiciones-disponibles){: target="_blank"} que Karel puede evaluar? Pues aquí las volvemos a usar, para decirnos que **mientras** esa condición se cumpla, Karel realizará las acciones dichas. Por ejemplo:

<textarea class="karelp">
mientras no-orientado-al-norte hacer gira-izquierda;</textarea>

Con la línea anterior nos aseguramos de que Karel se oriente al norte, pues estará girando mientras no tenga esa orientación <span>(muy útil, ¿verdad?)</span>. <br>
A estas alturas seguramente has deducido cómo resolver el problema inicial:

<textarea class="karelp">
mientras frente-libre hacer avanza;</textarea>

<span>¿Y qué hay de las [condiciones agrupadas]({{ site.baseurl }}/Karel/Instrucciones/Condicionales/#condiciones-agrupadas){: target="_blank"}?</span> Las podemos utilizar de la misma manera que con la sentencia `si`, utilizando una clausula `o`, una clausula `y`, e incluso también la clausula `no` según nos convenga.

## Sentencia repetir

Ahora pensemos la situación en la que conocemos **exactamente** la cantidad de veces que hay que realizar algo, pero son demasiadas veces como para poner las acciones esa cantidad de veces. <br>
Es entonces cuando usamos la sentencia `repetir`.

<textarea class="output">
repetir número veces acción-a-realizar;</textarea>

Si la [diseccionamos](http://dle.rae.es/?id=Du8Lirp){: target="_blank"} también, encontraremos varias partes.<br>
La palabra de control `repetir`. <br>
La cantidad de veces que se repetirán las acciones. Esa cantidad puede ser cualquier número mayor a 0.<br>
La palabra de control `veces`. <br>
Las acciones a realizar. <br>
Viéndolo en un ejemplo quedaría como sigue.

<textarea class="karelp">
repetir 12 veces coge-zumbador;</textarea>

Con el código anterior Karel tomará exactamente 12 zumbadores de la posición sobre la que está. <br>
¿Y qué pasaría si no hay tal cantidad de zumbadores ahí? <br>
En ese caso se mostraría un mensaje de error, pues Karel **no puede tomar zumbadores de donde no hay**. Es por eso que hay que ser muy cuidadosos con el uso de la sentencia `repetir`.

## Ejemplos

`mientras` sencillo

<textarea class="karelp">
mientras izquierda-bloqueada hacer avanza;</textarea>

`repetir` sencillo:

<textarea class="karelp">
repetir 3 veces gira-izquierda;</textarea>

`mientras` compuesto:

<textarea class="karelp">
mientras izquierda-bloqueada y frente-libre hacer avanza;</textarea>

`mientras` con bloque:

<textarea class="karelp">
mientras algun-zumbador-en-la-mochila hacer
inicio
	si frente-libre entonces avanza;
	deja-zumbador;
fin;	
</textarea>

`repetir` con bloque:

<textarea class="karelp">
repetir 8 veces
inicio
	avanza;
	gira-izquierda;
	repetir 2 veces deja-zumbador;
fin;
</textarea>

<div class="Nav">
	<a href="{{ site.baseurl }}/Karel/Instrucciones/Condicionales/" title="Condicionales &vert; #iP Code">Tema anterior</a> | <a href="{{ site.baseurl }}/Karel/Funciones/" title="Funciones &vert; #iP Code">Tema siguiente</a>
</div>