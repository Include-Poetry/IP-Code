---
layout: G-Article
title: Funciones prototipo
date: 2020-10-19 20:00:00
author: EdithGaspar
tags: [Funciones]
hide_tags: true
olimpiada: [OMIPS]
subject: [Karel pascal]
prevTopic: "Declaración de funciones en Karel, /Karel/Funciones/Declaracion/"
nextTopic: "Idea de recursión, /Karel/Recursion/"
---

Otra forma de definir funciones en Karel es utilizando las **funciones prototipo** las cuales son una forma de "pre-declarar" la existencia de una función.

{: #ListaContenido}
- Orden de declaración de funciones
- Implementación
- En Karel Java

## Orden de declaración de funciones

Supongamos que en nuestro código queremos definir dos funciones: una que se llame `AvanzayZumbador` y otra de nombre `gira-derecha` las cuales contienen los siguientes comandos:

<div class="karelBlock">
<textarea class="karelp">
iniciar-programa
	define-nueva-instruccion AvanzayZumbador como inicio
		mientras frente-libre hacer avanza;
		deja-zumbador;
		repetir 2 veces gira-izquierda;
		avanza;
		deja-zumbador;
		gira-izquierda;
		avanza;
		deja-zumbador;
	fin;
	define-nueva-instruccion gira-derecha como inicio
		repetir 3 veces gira-izquierda;
	fin;
	inicia-ejecucion
		apagate;
	termina-ejecucion
finalizar-programa</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span>
</div>

Nótese que en este ejemplo de código Karel no hará ninguna acción, sólo se apagará, ya que las funciones fueron declaradas después de `iniciar-programa` sin ser llamadas dentro de la **función principal**, es decir, después de `inicia-ejecucion`.

Una vez que tenemos las funciones definidas, podemos llamar a la función `AvanzayZumbador` para que Karel realice las instrucciones indicadas en ella:

<div class="karelBlock">
<textarea class="karelp">
iniciar-programa
	define-nueva-instruccion AvanzayZumbador como inicio
		mientras frente-libre hacer avanza;
		deja-zumbador;
		repetir 2 veces gira-izquierda;
		avanza;
		deja-zumbador;
		gira-izquierda;
		avanza;
		deja-zumbador;
	fin;
	define-nueva-instruccion gira-derecha como inicio
		repetir 3 veces gira-izquierda;
	fin;
	inicia-ejecucion
		AvanzayZumbador;
		apagate;
	termina-ejecucion
finalizar-programa</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span>
</div>

Ahora imaginemos que es necesario que Karel *corrija su rumbo*, para esto tendríamos que hacer una modificación en la función `AvanzayZumbador` ya que es la función que estamos llamando desde la función principal. Por ejemplo, si en lugar de que Karel gire dos veces hacia la izquierda después de que deje el primer zumbador queremos que gire a la derecha, entonces podríamos sustituir la instrucción de la línea **5** `repetir 2 veces gira-izquierda` por `gira-derecha`. En este caso estaríamos llamando a una **función secundaria** desde otra **función secundaria**, es decir, estaríamos llamando a la función `gira-derecha` desde la función `AvanzayZumbador`. Esto se vería así:

<div class="karelBlock">
<textarea class="karelp">
iniciar-programa
	define-nueva-instruccion AvanzayZumbador como inicio
		mientras frente-libre hacer avanza;
		deja-zumbador;
		gira-derecha;
		avanza;
		deja-zumbador;
		gira-izquierda;
		avanza;
		deja-zumbador;
	fin;
	define-nueva-instruccion gira-derecha como inicio
		repetir 3 veces gira-izquierda;
	fin;
	inicia-ejecucion
		AvanzayZumbador;
		apagate;
	termina-ejecucion
finalizar-programa</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span>
</div>

De este modo Karel haría lo que se indica en la función llamada `AvanzayZumbador`, comenzando por *avanzar*, *dejar un zumbador* y después la nueva instrucción `gira-derecha` para posteriormente continuar con el resto de la función. Pero aquí pasa algo extraño. Si tratas de ejecutar este código, notarás que el compilador te notificará el error *"Función no definida: gira-derecha"*. Esto ocurre porque al compilar el código, éste se va compilando **línea por línea** y al llegar a la **línea 5** el compilador "se da cuenta" de que intentaste llamar a una función que no está declarada en las líneas de código anteriores que ya revisó, en este caso la función `gira-derecha` no está declarada en las líneas **1**, **2**, **3**, y **4**.

## Implementación

Justo para evitar este tipo de errores es necesario usar la **función prototipo**, la cual permite llamar a una función desde otra función que fue declarada en líneas anteriores. Pero claro, para que pueda funcionar correctamente, se tiene que declarar la función prototipo **líneas antes** de declarar la función desde donde se le va a llamar. Para hacerlo usamos la sentencia de control `define-prototipo-instruccion` seguido del nombre de la función que queremos "pre-declarar", en nuestro ejemplo sería la función `gira-derecha` y se implementaría así:

<div class="karelBlock">
<textarea class="karelp">
iniciar-programa
	define-prototipo-instrucción gira-derecha;

	define-nueva-instruccion AvanzayZumbador como inicio
		mientras frente-libre hacer avanza;
		deja-zumbador;
		gira-derecha;
		avanza;
		deja-zumbador;
		gira-izquierda;
		avanza;
		deja-zumbador;
	fin;
	define-nueva-instruccion gira-derecha como inicio
		repetir 3 veces gira-izquierda;
	fin;
	inicia-ejecucion
		AvanzayZumbador;
		apagate;
	termina-ejecucion
finalizar-programa</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span>
</div>

Ahora puedes compilar y ejecutar el código y Karel podrá completar su tarea. Como podrás notar, lo único que debes hacer es escribir `define-prototipo-instrucción gira-derecha` sin escribir *lo que contiene* la función, porque en líneas más abajo vas a definirla completamente. `define-prototipo-instrucción` nos sirve para "presentar" a una función líneas antes de su declaración como tal, para que cuando se compile el código, el compilador "sepa" que existe esa función y que en *algún lugar* está definida. De esta forma ya podrás llamar a una función secundaria desde otras funciones sin importar el orden de declaración.

Utilizar las **funciones prototipo** pueden ser de gran utilidad cuando tienes demasiadas funciones en tu código y estas se llaman entre sí, pues de esta manera no es necesario que las definas en el órden en el que van siendo ejecutadas.

## En Karel Java

Si tu código lo escribes en la sintaxis de Java no es necesario utilizar las funciones prototipo ya que el compilador "busca" la función en las líneas de código posteriores. <span>¿Quieres hacer la prueba?</span> ejecuta este código:

<div class="karelBlock">
<textarea class="karelp">
{*Para ver el código en la sitaxis de Java da clic en el botón Java ubicado en la parte inferior derecha*}
</textarea>
<div class="karelBlock">
<textarea class="karelj">
class program {
	define AvanzayZumbador(){
		while(frontIsClear) move();
		putbeeper();
		GiraDerecha();
		move();
		putbeeper();
		turnleft();
		move();
		putbeeper();
	}
	define GiraDerecha(){
		iterate(3) turnleft();
	}
	program () {
		AvanzayZumbador();
		turnoff();
	}
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>
