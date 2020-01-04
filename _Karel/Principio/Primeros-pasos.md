---
layout: G-Article
title: Primeros pasos con Karel
author: rivel_co
tags: [Karel]
Hide_Tags: true
olimpiada: [OMIPS]
subject: [Karel pascal]
---

Para empezar a aprender a utilizar el simulador de [Karel el Robot]({{ site.baseurl }}/Karel/Principio/Karel/ "Karel el Robot &vert; IP Code"){: target="_blank"}, es importante que conozcas la estructura base de un programa de Karel, de esta forma irás aprendiendo mejor cada concepto y poniendo a prueba cada cosa mientras aprendes.

{: #ListaContenido}
- Simulador
- Código base
- Probando códigos
- Poniendo a prueba lo aprendido

## Simulador 

Los aspectos completos del simulador se han cubierto en un [artículo anterior]({{ site.baseurl }}/Karel/Principio/Simulador/ "Karel.js &vert; IP Code"){: target="_blank"}, si aún no lo has leído entonces es un buen momento de hacerlo. También tienes que recordar que puedes instalar en tu computadora la versión de [Karel azul]({{ site.baseurl }}/Karel/Azul/Principio/Simulador/ "Karel azul &vert; IP Code"){: target="_blank"}. Sin importar la opción que escojas es importante que conozcas bien tu simulador. Recuerda también que el simulador oficial en competencias es [Karel.js](https://omegaup.com/karel.js/ "Karel.js en omegaUp"){: target="_blank"}, por lo que es importante que ya te estés familiarizando con él.

En este artículo se discutirá el uso de Karel.js.

## Código base

El código base de todo programa de Karel es muy sencillo en esencia y depende de la sintaxis particular de Karel que estés usando.

<div class="karelBlock">
<textarea class="karelp">
iniciar-programa
    inicia-ejecucion
        { TODO poner codigo aqui }
        apagate;
    termina-ejecucion
finalizar-programa</textarea>
<textarea class="karelj">
class program {
    program () {
        // TODO poner codigo aqui
        turnoff();
    }
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Cuando inicias un nuevo programa en cualquiera de las sintaxis aparece un código como el anterior. En la línea 3 podrás encontrar un comentario que dice `TODO poner codigo aqui`. Eso nos quiere dar a entender que a partir de esa línea deberás escribir tu programa.

### El programa

Dentro del código se establece qué es lo que comprende el programa para Karel, en Karel Pascal se marca por las palabras `iniciar-programa` y `finalizar-programa`. En el caso de Karel Java se indica por lo que está dentro de `class program`. Todo lo que se encuentra dentro de estos bloques comprende el programa que Karel debe utilizar.

### Inicio de la ejecución

Cuando Karel comienza su ejecución, toma el código que se le ha dado, identifica el programa que debe utilizar y dentro de este programa encuentra la **función principal** que es la función por la que comienza la ejecución. En el caso de Karel Pascal se utilizan las palabras `inicia-ejecucion` y `termina-ejecucion`. En el caso de Karel Java se utiliza la función `program ()`. Esta es la función que siempre debe estar en todo programa y por aquí se empieza a ejecutar el código. 

Pueden existir [otras funciones]({{ site.baseurl }}/Karel/Funciones/ "Funciones en Karel &vert; IP Code"){: target="_blank"} que el usuario puede declarar, pero siempre debe estar esta función principal y de aquí se inicia siempre.

## Probando códigos

Cuando queremos probar algo que recién hemos aprendido sobre Karel, debemos escribir la instrucción o instrucciones que queremos probar dentro de la función principal y antes de que Karel se apague, es decir, justamente donde está el comentario que indica que ahí va el código.

Por ejemplo, si estamos revisando las instrucciones lineales de Karel en #iP entonces encontraremos un ejemplo como el que sigue:

<div class="karelBlock">
<textarea class="karelp">
avanza;</textarea>
<textarea class="karelj">
move();</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Si queremos probar lo que hace la instrucción anterior, entonces debemos irnos a la parte de código de nuestro simulador (Karel.js), identificar la función principal y escribir lo que queremos probar. En base al ejemplo anterior podemos tener algo como lo que sigue.

<div class="karelBlock">
<textarea class="karelp">
iniciar-programa
    inicia-ejecucion
        avanza;
        apagate;
    termina-ejecucion
finalizar-programa</textarea>
<textarea class="karelj">
class program {
    program () {
        move();
        turnoff();
    }
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Nota que hemos reemplazado el comentario con el `TODO` por la instrucción que hace que Karel avance una casilla en la orientación actual. Si queremos probar otra instrucción como girar a la izquierda, entonces podemos dar un salto de línea en donde íbamos y continuar.

<div class="karelBlock">
<textarea class="karelp">
iniciar-programa
    inicia-ejecucion
        avanza;
        gira-izquierda;
        apagate;
    termina-ejecucion
finalizar-programa</textarea>
<textarea class="karelj">
class program {
    program () {
        move();
        turnLeft();
        turnoff();
    }
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Y así podemos continuar editando nuestro código fuente para ir aplicando todos los conceptos de Karel al mismo tiempo que los vamos revisando en el sitio.

## Poniendo a prueba lo aprendido

Una vez que ya hemos revisado como empezar un programa y comenzar a escribir nuestros propios códigos, podremos ir aprendiendo cada tema de forma ordenada, pero no podemos estar seguros de que de verdad lo estamos aprendiendo si no lo ponemos a prueba.

Para poner a prueba tus conocimientos adquiridos, puedes resolver *mini problemas* en [omegaUp](https://omegaup.com/ "omegaUp"){:target="_blank"}. Estos problemas necesitan que pongas a prueba un conocimiento particular, en #iP puedes encontrar los problemas recomendados al final de cada artículo. Habrá problemas que son **únicamente de implementación** en donde bastará con aplicar *tal cual* el concepto revisado y otros en donde deberás aplicar una idea más creativa y menos obvia del concepto revisado, esta clase de problemas son más similares a los que encontrarías en una competencia. Los problemas aumentan de dificultad conforme bajas en la lista.

Para poder aprender como utilizar la plataforma de omegaUp, deberás leer [el artículo]({{ site.baseurl }}/Problemas/omegaUp/ "Cómo usar omegaUp &vert; IP Code"){: target="_blank"} que hemos escrito sobre ello o revisarlo directamente [desde omegaUp](https://blog.omegaup.com/category/omegaup/omegaup-101/ "Cómo usar omegaUp &vert; omegaUp"){: target="_blank"}. 

Una vez cubierto todo esto podrás comenzar a resolver problemas y a prepararte para tus siguientes competencias.

<div class="Nav">
    <a id="navLeft" href="{{ site.baseurl }}/Karel/Principio/Simulador/" title="Simulador Karel.js &vert; #iP Code">
        Tema anterior
        <span>Simulador Karel.js</span>
    </a>
    <a id="navRight" href="{{ site.baseurl }}/Karel/Instrucciones/Lineales/" title="Instrucciones lineales &vert; #iP Code">
        Tema siguiente
        <span>Instrucciones lineales</span>
    </a>
</div>