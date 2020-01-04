---
layout: G-Article
title: Karel el robot
author: rivel_co
tags: [Introducción]
Hide_Tags: true
olimpiada: [OMIPS]
subject: [Karel pascal]
---

En este sitio encontrarás el más completo manual y tutorial para aprender a programar a *Karel el robot*, donde además de encontrar de forma detallada todas las funciones del lenguaje, lo aprenderás con un enfoque especialmente diseñado para la [Olimpiada Mexicana de Informática](http://www.olimpiadadeinformatica.org.mx/){: target="_blank"} para [Primaria](http://www.olimpiadadeinformatica.org.mx/OMI/OMI_Primaria/Inicio.aspx){: target="_blank"} y [Secundaria](http://www.olimpiadadeinformatica.org.mx/OMI/OMI_Secundaria/Inicio.aspx){: target="_blank"}.

**Karel el robot** es una aplicación que simula un robot y su entorno. Dicho robot sigue instrucciones en su lenguaje, que tiene una sintaxis muy similar a un lenguaje de programación real, como *PASCAL*, o *Java*. Fue creado por [Richard E. Pattis en 1981](https://es.wikipedia.org/wiki/Karel_el_Robot){: target="_blank"} con un objetivo; enseñar a pensar de una manera **ordenada** y **eficiente**.

{: #ListaContenido}
- El simulador
- Karel

## El simulador

El lenguaje de este simulador, si bien, es bastante limitado a comparación de un lenguaje de programación real, da muy buenas bases para el diseño real de un programa y de hecho fue utilizado oficialmente desde el 2004 y hasta el 2016 como una de las pruebas de la **[Olimpiada Mexicana de Informática](http://www.olimpiadadeinformatica.org.mx "Olimpiada Mexicana de Informática"){: target="_blank"}** y actualmente como la prueba oficial de la **OMIP** y **OMIS**. <br>
Para ello, la **OMI** diseñó su propia versión del simulador. A la fecha y de forma oficial se utiliza [Karel.js](https://omegaup.com/karel.js/ "Karel.js"){: target="_blank"} para las competencias pero puedes descargar una versión antigua de su página oficial [aquí](http://www.cmirg.com/karelotitlan/Pantallas/descargas.aspx){: target="_blank"}.

El simulador, integra además un **[compilador](http://dle.rae.es/?id=A11NS9d){: target="_blank"}** del lenguaje particular de Karel. Un compilador es un programa que traduce de un lenguaje de programación a otro, por lo general es de un lenguaje **fácil de escribir para los humanos** a un lenguaje **fácil de entender para una máquina**. En este caso la máquina es Karel. Para que el compilador funcione correctamente es necesario que nuestro código esté escrito correctamente también, respetando la **sintaxis** del lenguaje con el que trabaja.

> Cada compilador tiene un conjunto de *palabras* especiales que le indican qué debe hacer

## Karel

A todo esto, nace la pregunta obligada (<s>¿por qué tanto alboroto?</s>) **¿quién es Karel?** Karel es (<s>obviamente</s>) el personaje principal de esta aplicación y es además el robot que programamos, es decir, quien cumple lealmente nuestras instrucciones, escritas debidamente en su lenguaje.

Karel tiene (<s>una muy práctica</s>) forma de flecha, hacia donde apunta la flecha es hacia donde *ve Karel*, quien además es fácil de identificar por su conocido color azul, con una descripción tan genial, seguro que te será muy sencillo reconocerlo.

Lo **más importante** de Karel, es que tiene una vida muy interesante y por lo tanto se enfrenta a muchos y muy variados problemas, es ahí donde entramos nosotros, para decirle **qué debe hacer** (<s>literalmente</s>).

Y para que no te quedes sin conocerlo, aquí un artístico retrato de él utilizado en la *OMI 2015*.

[<picture>
	<source media="(min-width: 800px)" width="90%" srcset="{{ site.iP-Sources }}/Multimedia/Karel/Karel.png">
	<img class="Imagen" width="90%" src="{{ site.iP-Sources }}/Multimedia/Karel/KarelC.png" alt="Karel-ccionista">
</picture>]({{ site.iP-Sources }}/Multimedia/Karel/KarelC.png){: data-lightbox="image-1"}

> La imagen fue obtenida de la página oficial de la **OMI** en facebook, [aquí el post original](https://www.facebook.com/olimpiadadeinformatica/posts/10152787483717478){: target="_blank"}

<div class="Nav">
    <a id="navRight" href="{{ site.baseurl }}/Karel/Principio/Mundo/" title="Alternative &vert; #iP Code">
        Tema siguiente
        <span>Mundo de Karel</span>
    </a>
</div>