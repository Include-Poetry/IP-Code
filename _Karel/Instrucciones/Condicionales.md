---
layout: G-Article
title: Instrucciones condicionales en Karel
author: rivel_co
tags: [Instrucciones, Condicionales]
Hide_Tags: true
olimpiada: [OMIPS]
subject: [Karel pascal]
---

En ocasiones cuando queremos hacer algo ocurre un evento desafortunado por el cual ya no podemos realizarlo, como querer comprar un pastel tres leches y que ya no haya mas que pays <span>:c</span> Sin embargo, de no haber pasado eso, habríamos seguido nuestro plan sin problemas. Aunque, veamos el lado positivo, si no haya del sabor que queríamos podemos llevar otro. En otras palabras podríamos decir:

> Si hay pastel de tres leches entonces compro ese, sino compro un pay.

Esto lo conocemos como una **condición** y en el caso de la programación es **exactamente lo mismo**.

{: #ListaContenido}
- Estructura
- Condiciones disponibles
- Bloques de instrucciones
- Condiciones agrupadas
- Ejemplos

## Estructura

La estructura es de hecho bastante similar a la manera natural de decir una condición:

<div class="karelBlock">
<textarea class="karelp">
si {*condición*} entonces {*acción-a-realizar;*}</textarea>
<textarea class="karelj">
if (/*condición*/) /*acción-a-realizar;*/</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Podemos notar varias partes en el enunciado:  La palabra reservada del compilador `si | if` que le indica que está recibiendo una sentencia condicional.  La condición que debe evaluar para saber en base a qué decidir.  La palabra `entonces` que le dice al compilador que está por recibir lo que **tiene que hacer si esa condición se cumple**. También podemos agregar lo que Karel tendría que hacer en caso de que la condición **no se cumpla**.

<div class="karelBlock">
<textarea class="karelp">
si condición entonces acción-a-realizar sino acción-alternativa;</textarea>
<textarea class="karelj">
if (/*condición*/) /*acción-a-realizar;*/ else /*acción-a-realizar;*/</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Nota que podemos [prescindir](http://dle.rae.es/?id=U5RdD3G){: target="_blank"} de especificar un `sino | else`, pero no podemos poner un `sino |else` sin un `si | if` antes de él. (<span>Ni siquiera tendría sentido la oración</span>).

> En  Pascal el `;` se pone al final de la expresión completa, si mi condición no lleva un `sino` iría justo después de la acción a realizar, de llevarlo iría hasta el final de la acción del `sino`. En el caso de Java el `;` va luego de cada acción.

> En #iP notarás las palabras control de las sentencias condicionales marcadas de color morado.

## Condiciones disponibles

Como podrás imaginar, Karel no puede evaluar si hay o no pasteles de su sabor favorito y siendo que podrían haber una infinidad de posibles condiciones **hay ciertas condiciones especiales que Karel puede evaluar**.

> Nota que el tipo de [condición](http://dle.rae.es/?id=ABisSB6#17It2n4){: target="_blank"} que usamos aquí puede ser evaluada tan sólo con un **sí** o **no**, con un **verdadero** o **falso**.

Las condiciones que Karel puede evaluar, son las siguientes:

<div class="karelBlock">
<textarea class="karelp">
frente-libre;
frente-bloqueado;
izquierda-libre;
izquierda-bloqueada;
derecha-libre;
derecha-bloqueada;
junto-a-zumbador;
no-junto-a-zumbador;
algun-zumbador-en-la-mochila; 
algún-zumbador-en-la-mochila; {* acentuado *}
ningun-zumbador-en-la-mochila;
ningún-zumbador-en-la-mochila; {* acentuado *}
orientado-al-norte;
orientado-al-sur;
orientado-al-este;
orientado-al-oeste;
no-orientado-al-norte;
no-orientado-al-sur;
no-orientado-al-este;
no-orientado-al-oeste;</textarea>
<textarea class="karelj">
frontIsClear;
frontIsBlocked;
leftIsClear;
leftIsBlocked;
rightIsClear;
rightIsBlocked;
nextToABeeper;
notNextToABeeper;
anyBeepersInBeeperBag;
noBeepersInBeeperBag;
facingNorth;
facingSouth;
facingEast;
facingWest;
notFacingNorth;
notFacingSouth;
notFacingEast;
notFacingWest;</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Donde cada condición expresa lo que evalúa. La expresión: `si junto-a-zumbador` o `if (nexToABeeper)` es **verdadera** si Karel comparte su posición con un zumbador.

> En #iP verás las condiciones marcadas de color naranja.

## Bloques de instrucciones

<span>¿Qué pasa cuando queremos hacer más de una acción si una condición se cumple o no se cumple?</span> Con las estructuras anteriores sólo podíamos realizar una acción si se cumplía la condición, o sólo una si no, si queremos realizar más de una acción debemos usar **bloques de instrucciones** como sigue:

<div class="karelBlock">
<textarea class="karelp">
si junto-a-zumbador entonces inicio
	{* acciones a realizar *}
fin;</textarea>
<textarea class="karelj">
if (nextToABeeper){
	/* acciones a realizar */
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Como notarás, los bloques de instrucciones en Pascal los marcan las palabras `inicio` y `fin`. En Java utilizamos llaves, `{` al principio y `}` al final del bloque.

> En #iP las palabras control que delimitan los bloques los verás marcadas en verde.

> Podemos escribir las acciones a realizar al mismo nivel del `si | if` y podemos poner todas las acciones en una línea (<span>siempre y cuando no olvides los `;` al final de cada comando</span>) pero es aconsejable que dejes espacios para mantener todo ordenado y más fácil de entender. A estos espacios se les llama [identación](https://es.wikipedia.org/wiki/Indentaci%C3%B3n){: target="_blank"} o [sangrado](http://dle.rae.es/?id=XCq62r8#LTED7NG){: target="_blank"}.

## Condiciones agrupadas

Puede darse (<s>muy seguido</s>) que necesitemos considerar no sólo una condición, si ese es el caso podemos usar una simple clausula de conjunción o disyunción para agregar más. Una clausula de conjunción es `y` por ejemplo, una de disyunción es `o`. 

<div class="karelBlock">
<textarea class="karelp">
si junto-a-zumbador y frente-libre entonces avanza;
si junto-a-zumbador e izquierda-bloqueada entonces avanza;</textarea>
<textarea class="karelj">
if (nextToABeeper && frontIsClear) move();
if (nextToABeeper && leftIsBlocked) move();</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Karel avanzará si y sólo si **ambas condiciones se cumplen**, es decir en la primera línea, si Karel está junto a un zumbador **y** tiene el frente libre entonces avanzará. No importa si sólo una se cumple, **tienen que cumplirse ambas** para que la acción se realice. Nota que en pascal podemos usar `y` y `e` <span>para que se lea mejor</span>, pero en Java únicamente usamos `&&`.

Pero existe otro caso, el caso en el que tanto si se cumple una u otra condición se realice cierta acción. Ahí usamos las cláusulas de disyunción como sigue:

<div class="karelBlock">
<textarea class="karelp">
si junto-a-zumbador o izquierda-libre entonces deja-zumbador;
si frente-libre u orientado-al-este entonces avanza;</textarea>
<textarea class="karelj">
if (nestToABeeper || leftIsClear) putbeeper();
if (frontIsClear || facingEast) move();</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

En este caso, Karel dejará un zumbador si **una de las dos condiciones se cumple** es decir, en la primera línea si está junto a un zumbador **o** si tiene la izquierda libre. No importa si una no se cumple, **con que una de las dos se cumpla** se realizará la acción. Nota que en Pascal podemos usar `o` y `u`, en Java únicamente usamos `||`.

Está además la clausula `no` en Pascal y `!` en Java, que se considera verdadera cuando la condición a su lado **no** se cumple:

<div class="karelBlock">
<textarea class="karelp">
si no frente-bloqueado entonces avanza;</textarea>
<textarea class="karelj">
if (!frontIsClear) move();</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Karel avanzará si el frente **no** está bloqueado. <span>¿Pero qué no pude haber utilizado la condición `frente-libre`?</span> Sí, en este caso podemos utilizar la condición análoga, sin embargo, más adelante encontraremos casos en los que no hay una y tendremos que usar forzosamente la clausula `no | !`.

> En #iP encontrarás los caracteres de conjunción, disyunción y negación marcados de un color gris azulado.

## Ejemplos

Condición sencilla:

<div class="karelBlock">
<textarea class="karelp">
si frente-libre entonces avanza;</textarea>
<textarea class="karelj">
if (frontIsClear) move();</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Condición completa:

<div class="karelBlock">
<textarea class="karelp">
si frente-libre entonces avanza sino gira-izquierda;</textarea>
<textarea class="karelj">
if (frontIsClear) move(); else turnleft();</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Condición sencilla con bloque:

<div class="karelBlock">
<textarea class="karelp">
si junto-a-zumbador entonces inicio
	coge-zumbador;
	gira-izquierda;
fin;</textarea>
<textarea class="karelj">
if (nextToABeeper){
	pickbeeper();
	turnleft();
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Condición completa con bloque:

<div class="karelBlock">
<textarea class="karelp">
si junto-a-zumbador entonces inicio
	coge-zumbador;
	gira-izquierda;
fin sino inicio
	gira-izquierda;
	apagate
fin;</textarea>
<textarea class="karelj">
if (nextToABeeper){
	pickbeeper();
	turnleft();
} else {
	turnleft();
	turnoff();
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Condición agrupada sencilla con bloque:

<div class="karelBlock">
<textarea class="karelp">
si junto-a-zumbador y frente-libre entonces inicio
	coge-zumbador;
	avanza;
fin;</textarea>
<textarea class="karelj">
if (nextToABeeper && frontIsClear){
	pickbeeper();
	move();
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Condición agrupada completa con bloque:

<div class="karelBlock">
<textarea class="karelp">
si junto-a-zumbador y frente-libre entonces inicio
	coge-zumbador;
	avanza;
fin sino inicio
	deja-zumbador;
	apagate;
fin;</textarea>
<textarea class="karelj">
if (nextToABeeper && frontIsClear){
	pickbeeper();
	move();
} else {
	putbeeper();
	turnoff();
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Por si no te lo habías preguntado, puedes poner una condición dentro de otra, de hecho **puedes poner cualquier cosa dentro de un bloque**.

<div class="karelBlock">
<textarea class="karelp">
si junto-a-zumbador y frente-libre entonces inicio
	coge-zumbador;
	avanza;
fin sino inicio
	si frente-bloqueado entonces avanza;
	apagate;
fin;</textarea>
<textarea class="karelj">
if (nextToABeeper && frontIsClear){
	pickbeeper();
	move();
} else {
	if (frontIsBlocked) move();
	turnoff();
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

> Nota lo útil que es *identar* nuestros códigos para poder distinguir mejor entre un bloque de acciones y otro.

<div class="Nav">
	<a href="{{ site.baseurl }}/Karel/Instrucciones/Lineales/" title="Instrucciones lineales &vert; #iP Code">Tema anterior</a> | <a href="{{ site.baseurl }}/Karel/Instrucciones/Ciclicas/" title="Instrucciones cíclicas &vert; #iP Code">Tema siguiente</a>
</div>