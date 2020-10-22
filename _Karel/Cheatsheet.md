---
layout: G-Article
title: Karel pascal cheatsheet
date: 2020-01-04 12:00:00
author: rivel_co
tags: [Cheatsheet]
hide_tags: true
olimpiada: [OMIPS]
subject: [Karel pascal]
---

*Cheatsheet* de las funciones de Karel.js para que no batalles en recordarlas rápidamente.

{: #ListaContenido}
- Comentarios
- Comandos o acciones
- Condiciones
- Bloques de instrucciones
- Cláusula no
- Expresiones repetitivas
- Declarar una nueva función
- Función prototipo
- Estructura básica de recursión
- Recursión con parámetros

## Comentarios

<div class="karelBlock">
<textarea class="karelp">
{* este es un comentario *}</textarea>
<textarea class="karelj">
/* este es un comentario */</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

## Comandos o acciones

### Avanza un paso en la orientación actual

<div class="karelBlock">
<textarea class="karelp">
avanza;</textarea>
<textarea class="karelj">
move();</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

### Giro de 90° a la izquierda

<div class="karelBlock">
<textarea class="karelp">
gira-izquierda;</textarea>
<textarea class="karelj">
turnleft();</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

### Tomar un zumbador

<div class="karelBlock">
<textarea class="karelp">
coge-zumbador;</textarea>
<textarea class="karelj">
pickbeeper();</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

### Deja un zumbador

<div class="karelBlock">
<textarea class="karelp">
deja-zumbador;</textarea>
<textarea class="karelj">
putbeeper();</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

### Apagarse y terminar con el programa

<div class="karelBlock">
<textarea class="karelp">
apagate; {*también apágate *}</textarea>
<textarea class="karelj">
turnoff();</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

## Condiciones

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
algun-zumbador-en-la-mochila; {* algún-zumbador-en-la mochila; *}
ningun-zumbador-en-la-mochila; {* ningún-zumbador-en-la mochila; *}
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

## Bloques de instrucciones

<div class="karelBlock">
<textarea class="karelp">
inicio
    {* acciones aquí *}
fin;</textarea>
<textarea class="karelj">
{
    /* Acciones aquí */
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

### Expresión si

<div class="karelBlock">
<textarea class="karelp">
si {* condición *} entonces {* acción *};</textarea>
<textarea class="karelj">
if ( /*condición*/ ) /*acción*/;</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

<div class="karelBlock">
<textarea class="karelp">
si {* condición *} entonces {* acción1 *} sino {* acción2 *};</textarea>
<textarea class="karelj">
if ( /*condición*/ ) /* acción */; else /* acción */;</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

### Condiciones agrupadas

<div class="karelBlock">
<textarea class="karelp">
{* Verdadero si todas las condiciones se cumplen *}
si {*condición1*} y {*condición2*} e {*condición1*} entonces {*acción*};</textarea>
<textarea class="karelj">
/* Verdadero si todas las condiciones se cumplen */
if ( /*condición1*/ && /*condición2*/ ) /* acción */;</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

<div class="karelBlock">
<textarea class="karelp">
{* Verdadero si alguna de las condiciones se cumple *}
si {*condición1*} o {*condición2*} u {*condición1*} entonces {*acción*};</textarea>
<textarea class="karelj">
/* Verdadero si alguna de las condiciones se cumple */
if ( /*condición1*/ || /*condición2*/ ) /* acción */;</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

## Cláusula no

<div class="karelBlock">
<textarea class="karelp">
si no {*condición*} entonces {*acción*};</textarea>
<textarea class="karelj">
if (! /*condición*/) /* acción */;</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

## Expresiones repetitivas

### Sentencia mientras

<div class="karelBlock">
<textarea class="karelp">
mientras {* condición *} hacer {* acción *};</textarea>
<textarea class="karelj">
while ( /*condición*/ ) /* acción */;</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

### Sentencia repetir

<div class="karelBlock">
<textarea class="karelp">
repetir {* número o parámetro *} veces {* acción *};</textarea>
<textarea class="karelj">
iterate ( /* número o parámetro */ ) /*acción*/;</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

## Declarar una nueva función

<div class="karelBlock">
<textarea class="karelp">
define-nueva-instrucción miFuncion como inicio
    {* acciones de la función *}
fin;
{* también define-nueva-instrucción ... *}</textarea>
<textarea class="karelj">
define miFuncion(){
    /* acciones de la función */
}
/* Aquí no puede haber acentos */</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

## Función prototipo

<div class="karelBlock">
<textarea class="karelp">
define-prototipo-instruccion miFuncion;
</textarea>
<textarea class="karelj">
/*En Karel Java no son necesarias las funciones prototipo*/</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

## Estructura básica de recursión

<div class="karelBlock">
<textarea class="karelp">
define-nueva-instrucción miFuncion como inicio
    si {* condición *} entonces inicio
        {* acción1 *};
        miFuncion; {* Llamada recursiva *}
        {* acción2 *};
    fin;
fin;</textarea>
<textarea class="karelj">
define miFuncion(){
    if (/* condición */){
        /* acción1 */;
        miFuncion(); /* Llamada recursiva */
        /* acción2 */;
    }
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

## Recursión con parámetros

### Sumar 1 por llamada al parámetro

<div class="karelBlock">
<textarea class="karelp">
define-nueva-instrucción miFuncion(x) como inicio
    si {* condición *} entonces inicio
        {* acción1 *};
        miFuncion(sucede(x)); {* Llamada recursiva y parámetro*}
        {* acción2 *};
    fin;
fin;</textarea>
<textarea class="karelj">
define miFuncion(x){
    if (/* condición */){
        /* acción1 */;
        miFuncion(succ(x)); /* Llamada recursiva y parámetro */
        /* acción2 */;
    }
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

### Restar 1 por llamada al parámetro

<div class="karelBlock">
<textarea class="karelp">
define-nueva-instrucción miFuncion(x) como inicio
    si {* condición *} entonces inicio
        {* acción1 *};
        miFuncion(precede(x)); {* Llamada recursiva y parámetro*}
        {* acción2 *};
    fin;
fin;</textarea>
<textarea class="karelj">
define miFuncion(x){
    if (/* condición */){
        /* acción1 */;
        miFuncion(pred(x)); /* Llamada recursiva y parámetro */
        /* acción2 */;
    }
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

### Comparar con 0

<div class="karelBlock">
<textarea class="karelp">
define-nueva-instrucción miFuncion(x) como inicio
    si si-es-cero(x) entonces inicio
        {* acción *};
    fin;
fin;</textarea>
<textarea class="karelj">
define miFuncion(x){
    if (iszero(x)){
        /* acción */;
    }
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>
