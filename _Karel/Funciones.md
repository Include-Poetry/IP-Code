---
layout: G-Article
title: Funciones en Karel
---

<span>¡Por fin ha llegado la hora de programar!</span> Sólo nos falta saber cómo empezar, y para ello tenemos que conocer lo que es una función. Lo primero que hay que saber, es que existen varios tipos de funciones:

{: #ListaContenido}
- Función principal
- Funciones secundarias
- Ejemplos en la función principal
- Ejemplos de funciones secundarias

## Función principal

La **función principal** es la parte del código por donde empieza a realizarse la ejecución, es lo primero que busca el compilador cuando queremos que ejecute nuestro código, por lo tanto **siempre** debe estar presente en nuestros programas. <br>
En el simulador de Karel, podemos encontrar la función principal al iniciar a hacer un nuevo programa. Para esto nos dirigimos a la pestaña de **programa** y a continuación en el botón nuevo.

<textarea class="eKarel">
iniciar-programa
	inicia-ejecucion
		apagate;
	termina-ejecucion
finalizar-programa</textarea>

Los comandos de las líneas **1** y **5** marcan el inicio y el fin del programa, todo lo que está entre ellas es nuestro programa.<br>
En las líneas **2** y **4** encontramos los límites de nuestra función principal, es decir, al ejecutar nuestro programa comenzará con lo que hay justo debajo del `inicia-ejecucion`. En este ejemplo Karel sólo se apagaría.

## Funciones secundarias

Una función secundaria o [subrutina](https://es.wikipedia.org/wiki/Subrutina){: target="_blank"} es una parte del código que puede ser [invocada](http://dle.rae.es/?id=M4evQMl){: target="_blank"} desde cualquier parte del programa, esta parte del código tiene un nombre específico o **nombre de la función** y es refiriéndonos a ese nombre como ejecutamos sus comandos.

En Karel para declarar una función nueva, hay que usar la siguiente estructura:

<textarea class="eKarel">
define-nueva-instruccion MiFuncion como
inicio
	avanza;
	gira-izquierda;
fin;</textarea>

Donde `define-nueva-instruccion` es una sentencia de control que dice que se está declarando una nueva función.<br>
`MiFuncion` es el nombre de la función que estamos creando en este ejemplo. Puede ser cualquiera pero no puede llevar espacios o acentos, sí puede llevar guiones y números. No puede ser un comando o instrucción que ya exista en el compilador. Tampoco podemos repetir nombres de instrucciones.<br>
`como` es una palabra de control que le dice al compilador que está por definirse las instrucciones que conformarán esa función.<br>
Al igual que con las sentencias condicionales y cíclicas usamos bloques de instrucciones cuando hablaremos de más de una instrucción, o podemos omitirlas si sólo usaremos una. En nuestro ejemplo a nuestra función de nombre "MiFuncion" la conforman dos instrucciones, avanzar y girar a la izquierda, es por ello que se usan bloques de inicio y fin.<br>
Los nombres de las funciones que declaramos no se ponen en azul como el resto del código pero eso no significa que estén mal escritas.

> Ninguna función que declaremos puede estar antes de `iniciar-programa` o después de `finalizar-programa`, tampoco puede estar dentro de otra función, sea la principal o una secundaria. Tampoco debemos declararla después de la función de donde es llamada, pues cuando el compilador revise que se llama a esa función aún no conoce la función en sí.

Para ejecutar la instrucción que acabamos de declarar, hay que llamarla por su nombre desde la parte del  programa que queremos que se ejecute. Podemos llamar una instrucción secundaria **desde cualquier parte**.

<textarea class="eKarel">
iniciar-programa
	define-nueva-instruccion MiFuncion como
	inicio
		avanza;
		gira-izquierda;
	fin;
	inicia-ejecucion
		MiFuncion;
		apagate;
	termina-ejecucion
finalizar-programa</textarea>

En este ejemplo llamamos a nuestra función secundaria desde la función principal, en la línea 8.

> Prueba a ejecutar el código anterior y ver paso a paso lo que sucede con él.

## Ejemplos en la función principal

Recuerda que cuando corremos un código compilado, siempre siempre va a empezar a ejecutar por la primera instrucción de la función principal. Algunos ejemplos de instrucciones en la función principal son:

<textarea class="eKarel">
iniciar-programa
	inicia-ejecucion
		repetir 3 veces avanza;
		repetir 2 veces gira-izquierda;
		avanza;
		gira-izquierda;
		apagate;
	termina-ejecucion
finalizar-programa</textarea>

<textarea class="eKarel">
iniciar-programa
	inicia-ejecucion
		si frente-libre entonces avanza;
		repetir 3 veces gira-izquierda;
		avanza;
		mientras junto-a-zumbador hacer avanza;
		apagate;
	termina-ejecucion
finalizar-programa</textarea>

¿Notaste lo que hace Karel al girar tres veces a la izquierda?

<textarea class="eKarel">
iniciar-programa
	inicia-ejecucion
		mientras frente-libre hacer avanza;
		si junto-a-zumbador entonces coge-zumbador;
		avanza;
	termina-ejecucion
finalizar-programa</textarea>

¿Encontraste el error en el código anterior?

## Ejemplos de funciones secundarias

<textarea class="eKarel">
iniciar-programa
	define-nueva-instruccion AvanzayGira como
	inicio
		avanza;
		gira-izquierda;
	fin;
	inicia-ejecucion
		mientras frente-libre hacer AvanzayGira;
		apagate;
	termina-ejecucion
finalizar-programa</textarea>

¿Recuerdas el segundo ejemplo de la función principal?

<textarea class="eKarel">
iniciar-programa
	define-nueva-instruccion gira-derecha como
	inicio
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

Y aquí una de las primeras implementaciones de las funciones secundarias y facilitadora del desarrollo de muchos programas, la función de `gira-derecha`.<br>
<span>¿Ya notaste por qué funciona?</span>

> ¡Felicidades! Ya sabes como empezar a hacer tus propios programas para Karel.

<div class="Nav">
	<a href="{{ site.baseurl }}/Karel/Instrucciones/Ciclicas/">Tema anterior</a> | <a href="{{ site.baseurl }}/Karel/Problemas/">Tema siguiente</a>
</div>