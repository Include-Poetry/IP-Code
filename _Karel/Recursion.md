---
layout: G-Article
title: Recursión en programación
---

La idea y uso de la recursión entre otras cosas, ha permitido a la informática ser la potencia que es actualmente, así es que sí, se podría decir que **es una de las ideas centrales de la computación**.<br>
La recursión como técnica de resolver problemas es tan útil que la utilizamos en la vida cotidiana sin siquiera darnos cuenta, comprender el funcionamiento de la recursión es un arma **[invaluable](http://dle.rae.es/?id=M27S7Oj){: target="_blank"} e [imprescindible](http://dle.rae.es/?id=L6eq745){: target="_blank"}** en la informática.

(<span>En este apartado no se explicará la recursión en un lenguaje de programación en especial, sino la idea general de ella en la programación</span>)

{: #ListaContenido}
- Definición
- Matrioskas
- Fin de la recursión
- Condición de la recursión
- Más recursión

## Definición

Se podrían dar muchas versiones de lo que es la recursión, sin embargo, partiremos de la más sencilla y útil para esta explicación, que es la segunda que nos da el DRAE:

> [Recursivo, va](http://dle.rae.es/?id=VXkDTwd){: target="_blank"}<br>
> Dicho especialmente de un proceso: Que se aplica de nuevo al resultado de haberlo aplicado previamente.

Es decir, es la acción de aplicar un procedimiento a una cosa, y después, al resultado de eso volver a aplicar el procedimiento otra vez. <br>
De esta manera podemos solucionar un problema si lo vemos como un conjunto de problemas más pequeños.

<span>¿Qué nos dice esto?</span><br>
Para explicarlo mejor tomemos el ejemplo de las matrioskas. Una matrioska es un juguete artesanal de origen ruso, lo genial de estas muñecas es que están huecas por dentro, y dentro de cada matrioska hay una aún más pequeña, y dentro de ésta, otra, y así sucesivamente, hasta llegar a la matrioska más pequeña que ya no tiene otra dentro de ella. Seguro has visto una alguna vez.

## Matrioskas

Imagina que tienes la muy importante tarea de sacar todas las matrioskas que viven dentro de la más grande de ellas. <br>
Para abrir todas las matrioskas, primero debemos de abrir, (<s>lógicamente</s>) la primera, y seguir con las demás. Es decir, del primer gran problema de abrirlas todas, empezamos por un problema más sencillo, abrir la primera. Después, podemos ver como otro problema también pequeño, abrir la segunda. Así no lo vemos todo junto como tener que abrirlas todas. <span>Eso puede sonar, además como algo muy tardado</span>. <br>
Para ello, y como buen programador, imaginas la tarea a realizar como si fuera un programa:

<textarea class="output">
definir-nuevo-procedimiento "matrioskas" como
inicio
	abrir-matrioska;
	sacar-nueva-matrioska;
	matrioskas;
fin;</textarea>

Siguiendo el funcionamiento del anterior procedimiento, primero tienes una matrioska, la abres, sacas la matrioska en su interior, y a continuación ejecutas el procedimiento "matrioskas". (<span>[¿Esto no tiene sentido para ti?]({{ site.baseurl }}/Karel/Funciones/){: target="_blank"}</span>). <br>
<span>¿Qué pasa cuando ejecutamos de nuevo el procedimiento "matrioskas"?</span> Tomaríamos la matrioska, la abriríamos, sacaríamos la muñeca en su interior y volveríamos a aplicar el procedimiento anterior. Esto se vería más o menos así:

[<picture>
	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Recursividad/02.gif">
	<img class="Imagen" src="{{ site.iP-Sources }}/Multimedia/Recursividad/02.gif" alt="Recursividad">
</picture>]({{ site.iP-Sources }}/Multimedia/Recursividad/02.gif){: data-lightbox="image-1"}

<span>Genial ¿no?</span> Sólo que hay un problema, (<s>no sólo que muy seguramente no tenemos esa barba</s>), las matrioskas en el mundo real <span>no son infinitas</span>. Así que en algún momento no podremos seguir sacando matrioskas, es decir **no podremos seguir realizando el procedimiento "matrioskas"**.

## Fin de la recursión

En nuestra misión de abrir todas las matrioskas y aplicada en el mundo real (donde las matrioskas no son infinitas) nos detuvimos al llegar a la muñeca más pequeña pues dentro de ella ya no hay más muñecas. Sin embargo, un robot, o una computadora, (<span>como Karel</span>) no sabe por sí solo cuando detenerse. Recuerda que (<s>hasta ahora</s>) una máquina no sabe nada si tú no se lo programas.

> En la recursión una de las cosas más importantes (<s>por no decir que la más importante</s>) es su final.

<span>¿Por qué es tan importante saber detenerse?</span> Como en todo, el exceso no es bueno. En el caso de Karel ¿recuerdas lo que pasaba cuando le decíamos que avanzara sin importar nada? en el momento en que llegaba a una pared y trataba de atravesarla, fallaba, o como cuando tomaba o dejaba zumbadores **sin consideración**.

¿Notaste dónde empieza la recursión en el procedimiento anterior? La recursión empieza por una cosa que llamaremos **llamada recursiva** que es el momento en el que se vuelve a llamar una función dentro de sí misma. En el procedimiento que declaramos la llamada recursiva está en la línea 5.

Sin embargo una función nunca, **nunca** debe declararse si no es controlada por una condición. Es decir, toda llamada recursiva debe ser realizada dentro de una condición. En el proceso anterior, ¿dónde debemos poner la condición y qué condición debe ser evaluada?.

## Condición de la recursión

La condición en toda recursión debe tener siempre en cuenta **qué es lo que está buscando**. Es decir, el porqué se realiza la recursión. Volviendo a nuestro ejemplo de las muñecas rusas, queríamos llegar a la más pequeña, ¿y cómo íbamos a saber que era la más pequeña? pues porque dentro de ella **ya no iba a haber otra matrioska**.

Por lo tanto, ejecutamos el procedimiento "matrioska" siempre y cuando se pueda o sea necesario seguir ejecutándolo, una vez que hayamos cumplido nuestro cometido podemos dejar de hacer eso. Viéndolo así, seguro ya te imaginas dónde y qué condición hay que ubicar. 

<textarea class="output">
definir-nuevo-procedimiento "matrioskas" como
inicio
	abrir-matrioska
	sacar-nueva-matrioska
	si tiene-otra-muñeca-dentro entonces matrioskas
fin</textarea>

Toma en cuenta que lo anterior **no es un código real**, sólo es una manera general e informal de expresar un procedimiento y que puede ser fácilmente traducido a un lenguaje de programación real. Es decir, es un *pseudocódigo*. Es por ello que puede que hayas tenido otra manera de expresar la condición de la recursión pero la idea debe ser la misma.

## Más recursión

> Cuando buscas "recursión" en google ¿cuál es el sentido de que te diga "*Quizás quisiste decir: **recursión***"?

> ¿Te gustó el gif de las matrioskas interminables? Las [animaciones recursivas](http://giphy.com/search/recursive){: target="_blank"} siempre son geniales.

> No lo olvides, la idea básica de la recursión es **aplicar un proceso a una cosa, y después, al resultado de eso volver a aplicar ese proceso otra vez** y seguir haciéndolo hasta lograr lo que buscamos.

<div class="Nav">
	<a href="{{ site.baseurl }}/Karel/Problemas/">Tema anterior</a> | <a href="{{ site.baseurl }}/Karel/Recursion/Simple/">Tema siguiente</a>
</div>