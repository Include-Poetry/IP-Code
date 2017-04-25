---
layout: G-Article
title: Zumbadores en Karel
author: rivel_co
tags: [Introducción]
Hide_Tags: true
olimpiada: [OMIPS]
subject: [Karel pascal]
---

Seguramente habrás notado en el menú contextual del mundo que podemos ubicar unas cosas llamadas **zumbadores**. Un zumbador [etimológicamente](http://definicion.de/etimologia/){: target="_blank"} hablando, es un aparato que emite un zumbido. En el mundo de Karel un zumbador no es algo muy diferente, además, es algo que Karel puede **tomar** y **dejar**. Al tomarlos, los guarda en una **mochila** de capacidad (<s>extrañamente</s>) **infinita**.

{: #ListaContenido}
- Zumbadores en el mundo

## Zumbadores en el mundo

En el mundo de Karel, los zumbadores son ubicados en las intersecciones, ahí pueden ubicarse hasta **infinitos** zumbadores, y pueden compartir intersección con Karel **sin** obstruir el paso. <br>
Los zumbadores los podemos ver en el mundo **como números** que indican la cantidad que hay en esa posición y están resaltados con un recuadro verde fosforescente.

> En el mundo de Karel no existen cantidades negativas de zumbadores

Aunque puede haber una cantidad infinita de zumbadores y la capacidad de la mochila de Karel es infinita también, Karel **no puede** tomar una cantidad infinita de zumbadores, pues **no terminaría nunca de hacerlo**.

Los zumbadores se ven de la siguiente manera en el mundo:

[<picture>
	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Karel/Zumbadores.jpg">
	<img class="Imagen" src="{{ site.iP-Sources }}/Multimedia/Karel/ZumbadoresC.jpg" alt="Mundo">
</picture>]({{ site.iP-Sources }}/Multimedia/Karel/ZumbadoresC.jpg){: data-lightbox="image-1"}

<div class="Nav">
	<a href="{{ site.baseurl }}/Karel/Principio/Mundo/">Tema anterior</a> | <a href="{{ site.baseurl }}/Karel/Principio/Simulador/">Tema siguiente</a>
</div>