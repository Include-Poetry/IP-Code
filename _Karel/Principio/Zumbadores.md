---
layout: G-Article
title: Zumbadores en Karel
date: 2020-01-04 12:00:00
author: rivel_co
tags: [Introducción]
Hide_Tags: true
olimpiada: [OMIPS]
subject: [Karel pascal]
---

Seguramente habrás notado que al hacer click derecho sobre el mundo podemos ubicar unas cosas llamadas **zumbadores**. Un zumbador [etimológicamente](http://definicion.de/etimologia/){: target="_blank"} hablando, es un aparato que emite un zumbido. En el mundo de Karel un zumbador no es algo muy diferente, principalmente, es algo que Karel puede **tomar** y **dejar**. Al tomar un zumbador Karel lo guarda en su **mochila** de capacidad (<s>extrañamente</s>) **infinita**.

{: #ListaContenido}
- Zumbadores en el mundo
- Ubicando zumbadores
- La mochila de Karel

## Zumbadores en el mundo

En el mundo de Karel, los zumbadores son ubicados en las intersecciones, ahí pueden ubicarse hasta **infinitos** zumbadores y pueden compartir intersección con Karel **sin obstruir el paso**. Los zumbadores los podemos ver en el mundo **como números** que indican la cantidad que hay en esa posición y están resaltados con un recuadro verde fosforescente.

> En el mundo de Karel no existen cantidades negativas de zumbadores

Aunque puede haber una cantidad infinita de zumbadores y la capacidad de la mochila de Karel es infinita también, Karel **no puede** tomar una cantidad infinita de zumbadores, pues **no terminaría nunca de hacerlo**.

[<picture>
	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Karel/Zumbadores.jpg">
	<img class="Imagen" src="{{ site.iP-Sources }}/Multimedia/Karel/ZumbadoresC.jpg" alt="Mundo">
</picture>]({{ site.iP-Sources }}/Multimedia/Karel/ZumbadoresC.jpg){: data-lightbox="image-1"}

En la imagen anterior puedes ver un mundo con zumbadores, por ejemplo en la posición `3,6` hay una cantidad infinita de zumbadores, en la `9, 3` hay 5 y en la posición `8, 5` Karel está junto a un zumbador.

## Ubicando zumbadores

Podemos ubicar $$1$$ zumbador en una posición haciendo click en el lugar donde lo queremos. Si haces 5 clicks entonces pondrás 5 zumbadores. También podemos poner el apuntador (<span>la flechita del mouse</span>) sobre un espacio y teclear el número de zumbadores que queremos poner ahí, si quieres poner más de $$9$$ entonces presionas la tecla `N` y luego escribes en el recuadro emergente la cantidad deseada. Para poner infinitos zumbadores puedes presionar la tecla `I` o dar click derecho sobre el lugar y seleccionar esa opción.

## La mochila de Karel

Karel guarda los zumbadores que recoge en su mochila, ésta puede estar vacía o tener hasta infinitos zumbadores dentro. Karel puede empezar en un mundo con una cantidad predeterminada de zumbadores en su mochila. Si quieres poner una cantidad determinada en la mochila antes de ejecutar un programa puedes hacerlo en el recuadro ubicado en la parte superior de la pantalla.

[<picture>
    <source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Karel/Mochila.jpg">
    <img class="Imagen" src="{{ site.iP-Sources }}/Multimedia/Karel/MochilaC.jpg" alt="Mundo">
</picture>]({{ site.iP-Sources }}/Multimedia/Karel/MochilaC.jpg){: data-lightbox="image-1"}

Karel no puede tener una cantidad negativa de zumbadores en la mochila y si ésta tiene una cantidad infinita dentro Karel no puede vaciarla nunca, pues nunca terminaría de retirar tantos zumbadores. Cuando guardas un mundo, los zumbadores se guardan con él.

> Si buscas la versión sobre *Karel Azul* que se instalaba en la computadora, aún puedes encontrarlo [acá]({{ site.baseurl }}/Karel/Azul/Principio/Zumbadores/ "Karel Azul &vert; #iP Code").

### Cita esta página

{% include citeThis.html titulo=page.title fecha=page.date link=page.url %}

<div class="Nav">
    <a id="navLeft" href="{{ site.baseurl }}/Karel/Principio/Mundo/" title="Mundo de Karel &vert; #iP Code">
        Tema anterior
        <span>Mundo de Karel</span>
    </a>
    <a id="navRight" href="{{ site.baseurl }}/Karel/Principio/Simulador/" title="Simulador Karel.js &vert; #iP Code">
        Tema siguiente
        <span>Simulador Karel.js</span>
    </a>
</div>