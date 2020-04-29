---
layout: G-Article
title: Mundo de Karel
date: 2020-01-04 12:00:00
author: rivel_co
tags: [Introducción]
hide_tags: true
olimpiada: [OMIPS]
subject: [Karel pascal]
prevTopic: "Karel el Robot, /Karel/Principio/Karel/"
nextTopic: "Zumbadores, /Karel/Azul/Principio/Zumbadores/"
---

Al igual que todos Karel vive en un lugar particular, su mundo puede verse como una gran cuadricula, donde cada linea horizontal es una *calle* y cada linea vertical es una *avenida*. En otras palabras las calles corren de *este a oeste* y las avenidas de *norte a sur*. Karel puede desplazarse por las calles y avenidas siempre y cuando **estén despejadas**. También puede quedarse ubicado en cualquier intersección (<span>o esquina</span>) de ellas. Es **importante** notar que en la pantalla obtenemos una **vista superior** (<span>como aérea</span>) del mundo. Un mundo puede tener como máximo **cien avenidas**  y **cien calles**, todas están numeradas e indexadas (<span>numeradas iniciando</span>) en **1**.

> [Una versión más reciente de este artículo está disponible acá]({{ site.baseurl }}/Karel/Principio/Mundo/ "Mundo de Karel Karel.js &vert; iP Code")

> Para futura referencia se manejarán las intersecciones del mundo como las coordenadas de un plano cartesiano, donde no hay coordenadas negativas ni mayores a 100

El mundo lo puedes encontrar en la pestaña de **Mundo** del simulador **Karel Azul**.

[<picture>
	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Karel/Azul/Mundo.jpg">
	<img class="Imagen" src="{{ site.iP-Sources }}/Multimedia/Karel/Azul/MundoC.jpg" alt="Mundo">
</picture>]({{ site.iP-Sources }}/Multimedia/Karel/Azul/MundoC.jpg){: data-lightbox="image-1"}

{: #ListaContenido}
- Puntos cardinales
- Paredes
- Ubicación de Karel
- Carga y respaldo de mundos
- Modificación del mundo

## Puntos cardinales

(<s>¿En qué momento entraron los puntos cardinales?</s>) Para que la orientación de Karel sea más sencilla de entender, su mundo tiene puntos cardinales bien definidos, hacia arriba es el **norte**, análogamente hacia abajo es el **sur**. Del mismo modo, y viendo la pantalla de frente a la imagen, la izquierda corresponde al **oeste** y la derecha al **este**. <br>
Como ya se había mencionado, Karel puede orientarse (<span>voltear a ver</span>) hacia cualquiera de estos cuatro puntos cardinales. Es **importante** saber que Karel **no puede orientarse a puntos intermedios** como el suroeste, noroeste, etc.

## Paredes

Igual que en el mundo real, en el mundo de Karel las paredes sirven para delimitar espacios, Karel **no puede** atravesar (<span>pasar caminando</span>) paredes. Es decir, las paredes pueden obstruir el paso de calles y avenidas.<br>
Para ubicar una pared en el mundo, basta con hacer un click sobre la calle o avenida a bloquear, y para quitarla, hacer otro click sobre la pared ya ubicada.

[<picture>
	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Karel/Azul/Paredes.jpg">
	<img class="Imagen" src="{{ site.iP-Sources }}/Multimedia/Karel/Azul/ParedesC.jpg" alt="Paredes">
</picture>]({{ site.iP-Sources }}/Multimedia/Karel/Azul/ParedesC.jpg){: data-lightbox="image-1"}

## Ubicación de Karel

Para mayor facilidad, puedes ubicar a Karel en cualquier intersección del mundo y con cualquiera de las cuatro posibles orientaciones. <br>
Sólo tienes que ubicar el apuntador del mouse en donde quieres ubicarlo y con el click derecho un menú contextual aparecerá.

[<picture>
	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Karel/Azul/Situar.jpg">
	<img class="Imagen" src="{{ site.iP-Sources }}/Multimedia/Karel/Azul/SituarC.jpg" alt="Posicionar">
</picture>]({{ site.iP-Sources }}/Multimedia/Karel/Azul/SituarC.jpg){: data-lightbox="image-1"}

## Carga y respaldo de mundos

Para agilizar el uso de mundos en Karel, el simulador de la **OMI** permite **guardar** y **cargar** mundos ya hechos, éstos son guardados con formato `.mdo` en el destino que tú establezcas. <br>
Estas opciones las puedes encontrar en la barra de herramientas ubicada en la parte superior de la pantalla.

[<picture>
	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Karel/Azul/GuardarMundo.jpg">
	<img class="Imagen" src="{{ site.iP-Sources }}/Multimedia/Karel/Azul/GuardarMundoC.jpg" alt="Carga y respaldo">
</picture>]({{ site.iP-Sources }}/Multimedia/Karel/Azul/GuardarMundoC.jpg){: data-lightbox="image-1"}

## Modificación del mundo

Es **importante** saber que en un mundo todos sus elementos (<span>como la posición y orientación de Karel</span>) **pueden cambiar** durante la ejecución de un programa, **excepto** por las paredes, que siempre estarán igual que la primera vez que se creó el mundo. De hecho, durante la ejecución de un programa **sólo karel** puede modificar el mundo. Después de terminar la ejecución de un programa, el mundo volverá a su estado original.