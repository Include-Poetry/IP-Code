---
layout: G-Article
title: Instalación y uso de Karel el robot
author: rivel_co
tags: [Introducción]
Hide_Tags: true
olimpiada: [OMIPS]
subject: [Karel pascal]
---

Lo primero que tenemos que hacer es conseguir la última versión del simulador desde la página oficial de Karel, <span>es decir [acá](http://www.cmirg.com/karelotitlan/Pantallas/descargas.aspx){: target="_blank"}</span>. <span>[¿Ya no recuerdas qué es Karel el robot?]({{ site.baseurl }}/Karel/Principio/Karel/){: target="_blank"}</span>

La versión que usaremos para entrenar es la versión **azul** de Karel. Las otras versiones son para desarrollar y probar problemas, y mundos para ellos. No los usaremos por ahora.

> No olvides que también puedes usar la [versión en línea](https://omegaup.com/karel.js/){: target="_blank"}, pero es más recomendable que lo tengas instalado en tu equipo.

{: #ListaContenido}
- Instalación
- Mundo
- Programa
- Ejecutar
- Ayuda

## Instalación

Una vez que lo hayas descargado, ejecuta el archivo de instalación, primero el instalador te dirá lo que está instalando, es decir el programa `Karel OMI V2011`.

Después de pedirá el lugar donde el simulador será instalado. <span>Está bien si dejas la ubicación [predeterminada](http://dle.rae.es/?id=TxXcrju){: target="_blank"} y sólo presionas el botón de `Next >`</span>.

A continuación se te ofrecerá la opción de crear un acceso directo en el escritorio, esto es para que puedas encontrarlo desde la pantalla principal  de tu computadora más fácilmente. <span>Tampoco hay problema si no seleccionas esta casilla</span>.

Ahora sólo queda confirmar la configuración de instalación y dejar que se instale el programa de "Karel el robot". Al finalizar presiona el botón `Finish`, Karel estará instalado ya en tu equipo.

Una vez instalado el programa, podemos abrirlo. Lo encontrarás fácilmente en el inicio de tu computadora, o en el escritorio si así lo escogiste. Al abrirlo lo primero que encontrarás será una pantalla azul con algunas opciones en la parte superior.

[<picture>
	<source media="(min-width=700px)" srcset="{{ site.iP-Sources }}/Multimedia/Simulador/Principal.jpg">
	<img class="Imagen" width="100%" src="{{ site.iP-Sources }}/Multimedia/Simulador/Principal.jpg">
</picture>]({{ site.iP-Sources }}/Multimedia/Simulador/Principal.jpg){: data-lightbox="image-1"}

## Mundo

En la parte superior de la ventana se encuentran cuatro pestañas. La primera de ellas es la de Mundo. En ella se encuentra el entorno donde Karel se desenvuelve. <s>Sí, su mundo</s>. Y debajo de la tira de pestañas están algunas opciones para ese mundo.

[<picture>
	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Simulador/Mundo.jpg">
	<img class="Imagen" width="100%" src="{{ site.iP-Sources }}/Multimedia/Simulador/Mundo.jpg">
</picture>]({{ site.iP-Sources }}/Multimedia/Simulador/Mundo.jpg){: data-lightbox="image-1"}

**Nuevo**: Te permite crear un mundo nuevo, si ya hiciste modificaciones a tu mundo lo borra todo y crea uno en blanco. <span>Ten cuidado, esta opción no pide confirmación</span>. <br>
**Guardar**: Cuando creas un mundo tienes la posibilidad de guardarlo para usarlo después. Al usar esta opción el programa te pedirá que escojas una ubicación y un nombre para el archivo que será el mundo que hiciste. <br>
**Abrir**: Aquí puedes seleccionar un mundo guardado previamente para volverlo a abrir en el editor. <br>
**Guardar como**: <span>¿Cuál es la diferencia al botón de `Guardar`?</span> Si ya guardaste un mundo y lo sigues editando, y ahora quieres guardarlo como un archivo nuevo (<span>sin reemplazar el respaldo anterior</span>) usa esta opción.

**Zumbadores en la mochila**: Aquí puedes definir la cantidad inicial que Karel llevará en su mochila. No olvides que puede cambiar durante la ejecución del programa, la cosa aquí es que el número que definas ahí será la cantidad con la que Karel empieza. <br>
<span>¿Y el botón de infinito?</span> Si lo que quieres es hacer que Karel empiece con una cantidad [infinita](http://dle.rae.es/?id=LWs5qiN){: target="_blank"} de zumbadores, no escribas nada, sólo presiona este botón.

Por último en la pestaña de mundo puedes encontrar unas flechas. Con ellas puedes desplazar la pantalla por el mundo, sin embargo así no mueves a Karel, sólo la vista que tú tienes del mundo.

## Programa

Aquí es en donde <span>la magia ocurre</span> pues es donde escribimos nuestro código que pasará a ser el programa que controle a Karel.

[<picture>
	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Simulador/Programa.jpg">
	<img class="Imagen" width="100%" src="{{ site.iP-Sources }}/Multimedia/Simulador/Programa.jpg">
</picture>]({{ site.iP-Sources }}/Multimedia/Simulador/Programa.jpg){: data-lightbox="image-1"}

**Nuevo**: Para empezar a escribir tu código, comienza presionando este botón. Insertará cinco líneas de código que servirán como base para nuestros programas. <br>
**Abrir**: Cuando hayas guardado un código que ya hayas hecho, puedes volver a abrirlo en el editor con esta opción. <br>
**Guardar**: Aquí puedes guardar tu código en un archivo de texto. Al igual que con el mundo, al usar esta opción te pedirá seleccionar una ubicación y un nombre para el archivo. <br>
**Guardar como**: Al igual que en el mundo, permite guardar un archivo en un lugar y bajo un nombre nuevo. <br>
**Compilar**: Al [compilar](http://dle.rae.es/?id=A11NS9d){: target="_blank"} nuestro código, todo lo que escribimos es traducido a un lenguaje que Karel puede entender, para poder realizar correctamente lo que le pedimos. Recuerda que para ello todos los comandos e instrucciones que pusimos deben de estar escritos **correctamente**, de otra manera no se podrá realizar la *traducción* y el programa nos devolverá un error de compilación, mostrando un mensaje donde dice en qué parte del código algo está mal escrito. Si todo está en orden, se mostrará un mensaje diciendo "*Programa compilado*".

> No olvides que el simulador nos permite saber cuando escribimos mal un comando, cada palabra debe estar de color azul para que  esté correctamente escrita. Sin embargo sólo al tratar de compilar podremos saber de otros errores como la falta de un punto y coma o una equivocada organización de los comandos de una instrucción. (<s>No se puede todo en la vida :c</s>)

<span>¿Y qué significa la última opción?</span>. Al final de la tira de opciones podemos ver un pequeño recuadro donde escogemos entre "Pascal" o "Java", esto es el tipo de sintaxis con el que escribimos nuestro programa (<span>como el "idioma" en que estamos escribiendo</span>). Ambos términos hacen referencia a los lenguajes de programación real que llevan precisamente esos nombres. Aquí manejaremos la sintaxis tipo "Pascal".

> Es muy muy importante que recuerdes y entiendas que siempre siempre antes de querer ejecutar un programa, tienes que **compilarlo**.

## Ejecutar

Siguiendo con nuestra [analogía](http://dle.rae.es/?id=2Vt6TRt){: target="_blank"} esta ventana es donde <span>vemos cómo ocurre la magia</span>.

[<picture>
	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Simulador/Ejecutar.jpg">
	<img class="Imagen" width="100%" src="{{ site.iP-Sources }}/Multimedia/Simulador/Ejecutar.jpg">
</picture>]({{ site.iP-Sources }}/Multimedia/Simulador/Ejecutar.jpg){: data-lightbox="image-1"}

Como podrás notar, del lado izquierdo está el código que compilamos, desde aquí **no podemos hacer modificaciones**. Del lado derecho y ocupando la mayor parte de la pantalla encontramos el mundo de Karel, **tampoco podemos hacer modificaciones en él desde aquí**. <br>
<span>¿Entonces para qué están ahí?</span> El objetivo de estos recuadros es que podemos ver lo que hace Karel **al mismo tiempo** que vemos la línea del código que hace que haga eso. <span>Así podemos ver qué está pasando y porqué está pasando eso</span>.

En la parte superior podemos encontrar varias opciones: <br>
**Adelante**: Al presionar este botón se ejecuta la siguiente línea de código, se señala en la línea del programa y lo vemos en el mundo. <span>Es como verlo un paso a la vez.</span> <br>
**Correr**: Con esta opción el código corre todo de manera automática. A diferencia de "*Adelante*" aquí sólo tenemos que presionar una vez para que se ejecute todo el código. <br>
**Detener**: Si ya estás usando la opción de "*Correr*", y necesitas detener la ejecución por un momento (<s>como pausarlo</s>), usa este botón. Puedes [reanudar](http://dle.rae.es/?id=VHq0Zj1){: target="_blank"} después. <br>
**Inicializar**: Si en algún momento quieres detenerlo todo y volver a empezar desde el principio, después de detener la ejecución, usa este botón. Tanto el código, como el mundo volverá a su estado inicial.

Tal vez ya hayas notado que aquí tampoco podemos cambiar el número de zumbadores que Karel lleva en la mochila, pero es como ver el número de zumbadores en tiempo real que Karel va dejando o tomando.

<span>¿Qué es el retardo de ejecución?</span> El retardo de ejecución es cuánto tiempo hay de espera en la ejecución de cada comando cuando usamos la opción de "*correr*". Por lo tanto, mientras mayor sea el número aquí más tiempo se esperará para ejecutar cada instrucción, es decir **parecerá más lento**.

> Por si te lo habías preguntado, el motivo por el que aquí no podemos modificar nada "a mano" es porque aquí es donde vemos la ejecución. No podemos modificar las cosas mientras se ejecuta el código. Para ello hay que volver a la pestaña de "Programa" o a la de "Mundo", compilar y volver a ejecutar.

## Ayuda

Por último, la pestaña de ayuda contiene una guía de la sintaxis con la que estemos trabajando o tengamos seleccionada en la pestaña de "Programa". Te dice cuales son exactamente las palabras que tienes que utilizar para realizar una acción. Es muy útil cuando recién empezamos a utilizar Karel, te ayuda a recordar cuáles son los comandos que puedes utilizar y cómo debes de escribirlos.

<div class="Nav">
	<a href="{{ site.baseurl }}/Karel/Principio/Zumbadores/">Tema anterior</a> | <a href="{{ site.baseurl }}/Karel/Instrucciones/Lineales/">Tema siguiente</a>
</div>