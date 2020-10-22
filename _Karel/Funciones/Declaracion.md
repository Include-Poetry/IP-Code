---
layout: G-Article
title: Declaración de funciones en Karel
date: 2020-01-04 12:00:00
author: rivel_co
tags: [Funciones]
hide_tags: true
olimpiada: [OMIPS]
subject: [Karel pascal]
prevTopic: "Instrucciones cíclicas, /Karel/Instrucciones/Ciclicas/"
nextTopic: "Funciones prototipo, /Karel/Funciones/Prototipo/"
---

<span>¡Por fin ha llegado la hora de programar!</span> Sólo nos falta saber cómo empezar, y para ello tenemos que conocer lo que es una función. Lo primero que hay que saber, es que existen varios tipos de funciones:

{: #ListaContenido}
- Función principal
- Funciones secundarias
- Ejemplos en la función principal
- Ejemplos de funciones secundarias

## Función principal

La **función principal** es la parte del código por donde empieza a realizarse la ejecución, es lo primero que busca el compilador cuando queremos que ejecute nuestro código, por lo tanto **siempre** debe estar presente en nuestros programas. En el simulador de Karel, podemos encontrar la función principal al iniciar a hacer un nuevo programa. Para esto nos dirigimos a la pestaña de `Código` en la parte superior de la pantalla principal de Karel.js y a continuación en el botón nuevo. Ahí podemos seleccionar uno de tres versiones de lenguaje para Karel. En #iP sólo hablamos de la versión de Java y Pascal.

<div class="karelBlock">
<textarea class="karelp">
iniciar-programa
	inicia-ejecucion
		apagate;
	termina-ejecucion
finalizar-programa</textarea>
<textarea class="karelj">
class program{
    program(){
        turnoff();
    }
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Al seleccionar uno de los lenguajes se añadirá al *editor* un código como el de arriba, según hayas escogido Pascal o Java. En ambos casos los comandos de las líneas **1** y **5** marcan el inicio y el fin del programa, todo lo que está entre ellas es nuestro programa. En las líneas **2** y **4** encontramos los límites de nuestra función principal, es decir, al ejecutar nuestro programa comenzará con lo que hay justo debajo del `inicia-ejecucion` o del `program()`. En este ejemplo Karel sólo se apagaría.

## Funciones secundarias

Una función secundaria o [subrutina](https://es.wikipedia.org/wiki/Subrutina){: target="_blank"} es una parte del código que puede ser [invocada](http://dle.rae.es/?id=M4evQMl){: target="_blank"} desde cualquier parte del programa, esta parte del código tiene un nombre específico o **nombre de la función** y es refiriéndonos a ese nombre como ejecutamos sus comandos. En Karel para declarar una función nueva, hay que usar la siguiente estructura:

<div class="karelBlock">
<textarea class="karelp">
define-nueva-instruccion MiFuncion como inicio
	avanza;
	gira-izquierda;
fin;</textarea>
<textarea class="karelj">
define MiFuncion(){
	move();
    turnleft();
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Donde `define-nueva-instruccion` y `define` son sentencias de control que dicen que se está declarando una nueva función. `MiFuncion` es el nombre de la función que estamos creando en este ejemplo. Puede ser cualquiera pero no puede llevar espacios pero sí puede llevar guiones y números. En el caso de Pascal sí puede llevar acentos, pero en Java no. No puede ser un comando o instrucción que ya exista en el compilador. Tampoco podemos repetir nombres de instrucciones.

En el caso de Pascal, `como` es una palabra de control que le dice al compilador que está por definirse las instrucciones que conformarán esa función. Nota que para Java hay que poner un par de paréntesis que indican *argumento vacío*.

Al igual que con las sentencias condicionales y cíclicas, usamos bloques cuando hablaremos de más de una instrucción o podemos omitirlas si sólo usaremos una. En nuestro ejemplo a nuestra función de nombre "MiFuncion" la conforman dos instrucciones, `avanza | move()` y `gira-izquierda | turnleft()`, es por ello que se usan bloques de `inicio` y `fin` o llaves en Java `{}`.

> Ninguna función que declaremos puede estar antes de `iniciar-programa | class program{` o después de `finalizar-programa`, tampoco podemos declarar una función dentro de otra función, sea la principal o una secundaria. Tampoco debemos declararla después de la función de donde es llamada, es decir, si llamamos a la función en la línea 10, es porque ya la declaramos líneas arriba.

Para ejecutar la instrucción que acabamos de declarar, hay que llamarla por su nombre desde la parte del  programa que queremos que se ejecute. Podemos llamar una instrucción secundaria **desde cualquier parte** <span>(excepto por lo mencionado arriba)</span>. En el siguiente ejemplo llamamos a nuestra función secundaria desde la función principal, en la línea 7.

<div class="karelBlock">
<textarea class="karelp">
iniciar-programa
	define-nueva-instruccion MiFuncion como inicio
		avanza;
		gira-izquierda;
	fin;
	inicia-ejecucion
		MiFuncion;
		apagate;
	termina-ejecucion
finalizar-programa</textarea>
<textarea class="karelj">
class program {
	define MiFuncion(){
    	move();
        turnleft();
    }
    program () {
    	MiFuncion();
        turnoff();
    }
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

## Ejemplos en la función principal

Recuerda que cuando corremos un código compilado, siempre siempre va a empezar la ejecución por la primera instrucción de la función principal. Algunos ejemplos de instrucciones en la función principal son:

<div class="karelBlock">
<textarea class="karelp">
iniciar-programa
	inicia-ejecucion
		repetir 3 veces avanza;
		repetir 2 veces gira-izquierda;
		avanza;
		gira-izquierda;
		apagate;
	termina-ejecucion
finalizar-programa</textarea>
<textarea class="karelj">
class program {
    program () {
    	iterate(3) move();
        iterate (2) turnleft();
        move();
        turnleft();
        turnoff();
    }
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

<div class="karelBlock">
<textarea class="karelp">
iniciar-programa
	inicia-ejecucion
		si frente-libre entonces avanza;
		repetir 3 veces gira-izquierda;
		avanza;
		mientras junto-a-zumbador hacer avanza;
		apagate;
	termina-ejecucion
finalizar-programa</textarea>
<textarea class="karelj">
class program {
    program () {
    	if (frontIsClear) move();
        iterate (3) turnleft();
        move();
        while (nextToABeeper) move();
        turnoff();
    }
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

¿Notaste lo que hace Karel al girar tres veces a la izquierda?

<div class="karelBlock">
<textarea class="karelp">
iniciar-programa
	inicia-ejecucion
		mientras frente-libre hacer avanza;
		si junto-a-zumbador entonces coge-zumbador;
		avanza;
		apagate;
	termina-ejecucion
finalizar-programa</textarea>
<textarea class="karelj">
class program {
    program () {
        while (frontIsClear) move();
        if (nextToABeeper) pickbeeper();
        move();
        turnoff();
    }
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

¿Encontraste el error en el código anterior?

## Ejemplos de funciones secundarias

<div class="karelBlock">
<textarea class="karelp">
iniciar-programa
	define-nueva-instruccion AvanzayGira como inicio
		avanza;
		gira-izquierda;
	fin;
	inicia-ejecucion
		mientras frente-libre hacer AvanzayGira;
		apagate;
	termina-ejecucion
finalizar-programa</textarea>
<textarea class="karelj">
class program {
	define AvanzayGira(){
    	move();
        turnleft();
    }
    program () {
        while (frontIsClear) AvanzayGira();
        turnoff();
    }
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

<div class="karelBlock">
<textarea class="karelp">
iniciar-programa
	define-nueva-instruccion gira-derecha como inicio
		repetir 3 veces gira-izquierda;
	fin;
	inicia-ejecucion
		avanza;
		avanza;
		gira-derecha;
		si frente-libre entonces avanza sino gira-izquierda;
		apagate;
	termina-ejecucion
finalizar-programa</textarea>
<textarea class="karelj">
class program {
	define GiraDerecha(){
    	iterate(3) turnleft();
    }
    program () {
    	move();
        move();
        GiraDerecha();
        if (frontIsClear) move(); else turnleft();
        turnoff();
    }
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Y aquí una de las primeras implementaciones de las funciones secundarias y facilitadora del desarrollo de muchos programas, la función de `gira-derecha`. <span>¿Ya notaste por qué funciona?</span>

> ¡Felicidades! Ya sabes como empezar a hacer tus propios programas para Karel.
