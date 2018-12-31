---
layout: G-Article
title: Instrucciones condicionales en Karel
author: rivel_co
tags: [Instrucciones, Condicionales]
Hide_Tags: true
olimpiada: [OMIPS]
subject: [Karel pascal]
---

En ocasiones cuando queremos hacer algo ocurre un evento desafortunado por el cual ya no podemos realizarlo, como querer comprar un pastel tres leches y que ya no haya mas que pays <span>:c</span> <br>
Sin embargo, de no haber pasado eso, habríamos seguido nuestro plan sin problemas. Aunque, veamos el lado positivo, aunque no haya del sabor que queríamos podemos llevar otro.	En otras palabras podríamos decir:

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

<textarea class="output">
si condición entonces acción-a-realizar;</textarea>

Podemos notar varias partes en el enunciado: <br>
La palabra reservada del compilador `si` que le indica que está recibiendo una sentencia condicional. <br>
La condición que debe evaluar para saber en base a qué decidir. <br>
La palabra `entonces` que le dice al compilador que está por recibir lo que **tiene que hacer si esa condición se cumple**.

También podemos agregar lo que Karel tendría que hacer en caso de que la condición **no se cumpla**.

<textarea class="output">
si condición entonces acción-a-realizar sino acción-alternativa;</textarea>

Nota que podemos [prescindir](http://dle.rae.es/?id=U5RdD3G){: target="_blank"} de especificar un `sino`, pero no podemos poner un `sino` sin un `si` antes de él. (<span>Ni siquiera tendría sentido la oración</span>)

> El `;` se pone al final de la expresión completa, si mi condición no lleva un `sino` iría justo después de la acción a realizar, de llevarlo iría hasta el final de la acción del `sino`.

## Condiciones disponibles

Como podrás imaginar, Karel no puede evaluar si hay o no pasteles de su sabor favorito, y siendo que podrían haber una infinidad de posibles condiciones **hay ciertas condiciones especiales que Karel puede evaluar**.

> Nota que el tipo de [condición](http://dle.rae.es/?id=ABisSB6#17It2n4){: target="_blank"} que usamos aquí puede ser evaluada tan sólo con un **sí** o **no**, o con un **verdadero** o **falso**.

Las condiciones que Karel puede evaluar, son las siguientes:

- frente-libre
- frente-bloqueado
- izquierda-libre
- izquierda-bloqueada
- derecha-libre
- derecha-bloqueada
- junto-a-zumbador
- no-junto-a-zumbador
- algun-zumbador-en-la mochila
- ningun-zumbador-en-la mochila
- orientado-al-norte
- orientado-al-sur
- orientado-al-este
- orientado-al-oeste
- no-orientado-al-norte
- no-orientado-al-sur
- no-orientado-al-este
- no-orientado-al-oeste

Donde cada condición expresa lo que evalúa.

> La expresión: `si junto-a-zumbador` es **verdadera** si Karel comparte su posición con un zumbador.

## Bloques de instrucciones

<span>¿Qué pasa cuando queremos hacer más de una acción si una condición se cumple o no se cumple?</span> <br>
Con las estructuras anteriores sólo podíamos realizar una acción si se cumplía la condición, o sólo una si no, si queremos realizar más de una acción debemos usar **bloques de inicio y fin** como sigue:

<textarea class="output">
si junto-a-zumbador entonces
inicio
	acción;
	acción;
	...
fin;</textarea>

> **Nota:**<br>
> Podemos escribir `inicio` inmediatamente junto a `entonces`, y podemos poner todas las acciones en una línea, (<span>siempre y cuando no olvides los `;` al final de cada comando</span>) pero es aconsejable que dejes espacios para mantener todo ordenado y más fácil de entender. A estos espacios se les llama [identación](https://es.wikipedia.org/wiki/Indentaci%C3%B3n){: target="_blank"} o [sangrado](http://dle.rae.es/?id=XCq62r8#LTED7NG){: target="_blank"}.

## Condiciones agrupadas

Puede darse (<s>muy seguido</s>) que necesitemos considerar no sólo una condición, si ese es el caso podemos usar una simple clausula `y` para agregar más, por ejemplo:

<textarea class="karelp">
si junto-a-zumbador y frente-libre entonces avanza;</textarea>

Karel avanzará si y sólo si **ambas condiciones se cumplen**, es decir, si está junto a un zumbador **y** tiene el frente libre. No importa si sólo una se cumple, **tienen que cumplirse ambas** para que la acción se realice.

Pero existe otro caso, el caso en el que tanto si se cumple una u otra condición se realice cierta acción. Ahí usamos la cláusula `o` como sigue:

<textarea class="karelp">
si junto-a-zumbador o izquierda-libre entonces deja-zumbador;</textarea>

En este caso, Karel dejará un zumbador si **una de las dos condiciones se cumple** es decir si está junto a un zumbador **o** si tiene la izquierda libre. No importa si una no se cumple, **con que una de las dos se cumpla** se realizará la acción.

Está además la clausula `no`, que se considera verdadera cuando la condición **no** se cumple

<textarea class="karelp">
si no frente-bloqueado entonces avanza;</textarea>

Karel avanzará si el frente **no** está bloqueado.<br>
<span>¿Pero qué no pude haber utilizado la condición `frente-libre`?</span><br>
Sí, en este caso podemos utilizar la condición análoga, sin embargo, más adelante encontraremos casos en los que no hay una, y tendremos que usar forzosamente la clausula `no`.

## Ejemplos

Condición sencilla:

<textarea class="karelp">
si frente-libre entonces avanza;</textarea>

Condición completa:

<textarea class="karelp">
si frente-libre entonces avanza sino gira-izquierda;</textarea>

Condición sencilla con bloque:

<textarea class="karelp">
si junto-a-zumbador entonces
inicio
	coge-zumbador;
	gira-izquierda;
fin;</textarea>

Condición completa con bloque:

<textarea class="karelp">
si junto-a-zumbador entonces
inicio
	coge-zumbador;
	gira-izquierda;
fin sino
	inicio
		gira-izquierda;
		apagate
	fin;</textarea>

Condición agrupada sencilla con bloque:

<textarea class="karelp">
si junto-a-zumbador y frente-libre entonces
inicio
	coge-zumbador;
	avanza;
fin;</textarea>

Condición agrupada completa con bloque:

<textarea class="karelp">
si junto-a-zumbador y frente-libre entonces
inicio
	coge-zumbador;
	avanza;
fin sino 
	inicio
		deja-zumbador;
		apagate;
	fin;</textarea>

Por si no te lo habías preguntado, puedes poner una condición dentro de otra, de hecho **puedes poner cualquier cosa dentro de un bloque**.

<textarea class="karelp">
si junto-a-zumbador y frente-libre entonces
inicio
	coge-zumbador;
	avanza;
fin sino 
	inicio
		si frente-bloqueado entonces avanza;
		apagate;
	fin;</textarea>

> Nota lo útil que es *identar* nuestros códigos para poder distinguir mejor entre un bloque de acciones y otro.

<div class="Nav">
	<a href="{{ site.baseurl }}/Karel/Instrucciones/Lineales/" title="Instrucciones lineales &vert; #iP Code">Tema anterior</a> | <a href="{{ site.baseurl }}/Karel/Instrucciones/Ciclicas/" title="Instrucciones cíclicas &vert; #iP Code">Tema siguiente</a>
</div>