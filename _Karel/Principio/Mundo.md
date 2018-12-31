---
layout: G-Article
title: Mundo de Karel
author: rivel_co
tags: [Introducción]
Hide_Tags: true
olimpiada: [OMIPS]
subject: [Karel pascal]
---

Al igual que todos Karel vive en un lugar particular, su mundo puede verse como una gran cuadricula, donde cada linea horizontal es una *calle* y cada linea vertical es una *avenida*. En otras palabras las calles corren de *este a oeste* y las avenidas de *norte a sur*. El mundo de Karel es ese recuadro blanco muy grande y lleno de cuadritos grises que se encuentra en la parte derecha de la pantalla de [Karel.js](https://omegaup.com/karel.js/ "Karel.js"){: target="_blank"}.

[<picture>
	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Karel/Mundo.jpg">
	<img class="Imagen" src="{{ site.iP-Sources }}/Multimedia/Karel/MundoC.jpg" alt="Mundo">
</picture>]({{ site.iP-Sources }}/Multimedia/Karel/MundoC.jpg){: data-lightbox="image-1"}

{: #ListaContenido}
- Ubicación en el mundo
- Paredes
- Ubicación de Karel
- Carga y respaldo de mundos
- Modificación del mundo

## Ubicación en el mundo

Podemos referirnos a las intersecciones del mundo como las coordenadas de un plano cartesiano donde no hay coordenadas negativas. En #iP verás las coordenadas indicadas en un recuadro gris, por ejemplo, la esquina inferior izquierda se representa como `0, 0` y a menudo le llamamos *origen*.

Karel también puede **orientarse** en el mundo pues existen puntos cardinales bien definidos, hacia arriba es el **norte**, análogamente hacia abajo es el **sur**. Del mismo modo y viendo la pantalla de frente a la imagen, la izquierda corresponde al **oeste** y la derecha al **este**. Karel puede orientarse hacia cualquiera de estos cuatro puntos cardinales. Decimos que Karel está orientado al norte cuando *la flecha* apunta al norte. Es **importante** saber que Karel **no puede orientarse a puntos intermedios** como el suroeste, noroeste, etc.

Karel puede desplazarse por las calles y avenidas siempre y cuando **estén despejadas**. También puede quedarse ubicado en cualquier intersección de ellas. Es **importante** notar que en la pantalla obtenemos una **vista superior** (<span>como aérea</span>) del mundo.

El mundo puede tener un tamaño variable, ese tamaño está dado por la cantidad de *filas o calles* y *avenidas o columnas*. Puedes modificar el tamaño del mundo en los espacios designados para ello que están en la barra de opciones en la parte superior de la pantalla. Puedes también mover el mapa del mundo *"arrastrando"* la pantalla con el mouse.

## Paredes

Igual que en el mundo real, en el mundo de Karel las paredes sirven para delimitar espacios, Karel **no puede** atravesar paredes. Es decir, las paredes pueden obstruir el paso de calles y avenidas. Para ubicar una pared en el mundo basta con hacer un click sobre la calle o avenida a bloquear y para quitarla hacer otro click sobre la pared ya ubicada. 

También podemos agregar paredes muy largas haciendo click en uno de los "cuadritos" grises donde queremos que la pared empiece y luego otro click en el punto donde queremos que termine. Verás que se marca en rojo el lugar donde se pondrá la nueva pared. Para quitar paredes podemos aplicar ese mismo proceso. 

[<picture>
	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Karel/Paredes.jpg">
	<img class="Imagen" src="{{ site.iP-Sources }}/Multimedia/Karel/ParedesC.jpg" alt="Paredes">
</picture>]({{ site.iP-Sources }}/Multimedia/Karel/ParedesC.jpg){: data-lightbox="image-1"}

## Ubicación de Karel

Puedes ubicar a Karel en cualquier intersección del mundo y con cualquiera de las cuatro posibles orientaciones. Sólo tienes que ubicar el apuntador del mouse en donde quieres ubicarlo y con el click derecho un menú contextual aparecerá, en él seleccionas la orientación que quieres y listo.

[<picture>
	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Karel/Situar.jpg">
	<img class="Imagen" src="{{ site.iP-Sources }}/Multimedia/Karel/SituarC.jpg" alt="Posicionar">
</picture>]({{ site.iP-Sources }}/Multimedia/Karel/SituarC.jpg){: data-lightbox="image-1"}

## Carga y respaldo de mundos

Para agilizar el uso de mundos, *Karel.js* permite **guardar** y **cargar** mundos ya hechos, éstos son guardados con formato `.in` en el destino que tú establezcas. Estas opciones las puedes encontrar en la barra de herramientas ubicada en la parte superior de la pantalla, dentro de la pestaña `Mundo` y en la opción `Guardar .in`. Para cargar un mundo que ya tienes guardado puedes usar la opción de `Abrir .in`.

[<picture>
	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Karel/GuardarMundo.jpg">
	<img class="Imagen" src="{{ site.iP-Sources }}/Multimedia/Karel/GuardarMundoC.jpg" alt="Carga y respaldo">
</picture>]({{ site.iP-Sources }}/Multimedia/Karel/GuardarMundoC.jpg){: data-lightbox="image-1"}

## Modificación del mundo

Es **importante** saber que en un mundo los elementos como la posición y orientación de Karel y el número y ubicación de zumbadores **pueden cambiar** durante la ejecución de un programa, **excepto** por las paredes y cantidad de filas y columnas, que siempre estarán igual que la primera vez que se creó el mundo. De hecho, durante la ejecución de un programa **sólo Karel** puede modificar el mundo. Después de terminar la ejecución de un programa puedes presionar el botón de <i class="fas fa-redo-alt"></i> y el mundo volverá a su estado original y podrás editarlo otra vez.

> Si buscas la versión sobre *Karel Azul* que se instalaba en la computadora, aún puedes encontrarlo [acá]({{ site.baseurl }}/Karel/Azul/Principio/Mundo/ "Karel Azul &vert; #iP Code").

<div class="Nav">
	<a href="{{ site.baseurl }}/Karel/Principio/Karel/" title="Karel el robot &vert; #iP Code">Tema anterior</a> | <a href="{{ site.baseurl }}/Karel/Principio/Zumbadores/" title="Zumbadores &vert; #iP Code">Tema siguiente</a>
</div>