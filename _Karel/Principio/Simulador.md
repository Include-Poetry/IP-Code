---
layout: G-Article
title: Simulador Karel.js
author: rivel_co
tags: [Introducción]
Hide_Tags: true
olimpiada: [OMIPS]
subject: [Karel pascal]
---

En las competencias oficiales utilizamos [Karel.js](https://omegaup.com/karel.js/ "Karel.js"){: target="_blank"} para resolver los problemas. Antes se utilizaba [Karel Azul](http://www.cmirg.com/karelotitlan/Pantallas/descargas.aspx){: target="_blank"} pero la versión oficial hasta la fecha es Karel.js que tiene muchas mejoras respecto a su antecesor. En otros artículos se profundiza sobre el [mundo y sus opciones]({{ site.baseurl }}/Karel/Principio/Mundo/ "Mundo de Karel &vert; #iP Code") además de los [zumbadores]({{ site.baseurl }}/Karel/Principio/Zumbadores/ "Zumbadores de Karel &vert; #iP Code").

{: #ListaContenido}
- Lenguaje y código
- Ejecutando un programa
- Barra superior de botones
- Apartado de mensajes
- Pila de llamadas

## Lenguaje y código

En el simulador de *Karel.js* podemos escribir nuestro código en el recuadro que se ubica en la parte izquierda de la pantalla. Por el momento *Karel.js* puede operar en modalidad **Pascal** y modalidad **Java**. Estas son versiones del lenguaje que el simulador puede entender, como si pudiera *hablar* esos dos idiomas. La versión de *Ruby* aún está bajo desarrollo.

Para comenzar a escribir tu código puedes dirigirte a la pestaña de `Código` en la parte superior de la pantalla, ahí encontrarás las opciones para comenzar un código nuevo en alguno de los tres lenguajes mencionados. También está la opción de `Abrir` por si tienes algún código guardado que quieras trabajar ahí y la opción de `Guardar` para que salves el código que estás editando.

Cada que comiences un código nuevo *Karel.js* te pondrá algo así como una *plantilla* en el **editor de código**. Esa plantilla es ideal para que tú te pongas a escribir tu código rápidamente. Sólo puedes editar el código cuando no hay algún programa ejecutándose. Puedes asegurarte que no hay nada corriendo al presionar el botón con el símbolo <i class="fas fa-redo-alt"></i> en la parte superior derecha. 

## Ejecutando un programa

Para ejecutar un programa lo primero que tenemos que hacer es asegurarnos de que el código a ejecutar está bien escrito en el editor, para esto hay que **compilarlo**. Para compilar el código vamos a presionar el segundo botón (de izquierda a derecha) de la barra superior <i class="fas fa-th-large"></i>. Si hay algún problema con el código entonces aparecerá un mensaje en el recuadro inferior izquierdo del entorno.

Una vez que el código ya está compilado correctamente pasamos a presionar el botón <i class="fas fa-play"></i> (el tercero de izquierda a derecha). Con eso haremos que Karel comience a hacer lo que le hemos indicado en el código que escribimos y compilamos, es decir, Karel ejecutará el programa.

## Cinta de opciones

En la parte más superior de la pantalla encontramos una cinta que lleva cuatro pequeñas pestañas diferentes, como `Mundo` ([del que ya hablamos en otro lado]({{ site.baseurl }}/Karel/Principio/Mundo/ "Mundo de Karel &vert; #iP Code")), `Código` (del que hablamos arriba), `Opciones` y `Ayuda`.

En la pestaña de `Opciones` puedes encontrar una función para cambiar el *tema* del editor de código, personalmente sugiero un tema oscuro (alguno que diga *dark* en el nombre), pues resulta ser menos molesto para los ojos después de largas horas programando.

En la pestaña de `Ayuda` puedes encontrar el *Acerca de* de esta aplicación para que conozcas a los programadores detrás de ello. También está la parte de `Manual y trucos` <s>en donde tristemente no figuramos</s> donde puedes encontrar la primer versión de los manuales de Karel, la misma que está disponible con *Karel Azul*.

## Barra superior de botones

### Velocidad de ejecución

Con velocidad de ejecución nos referimos a el tiempo que Karel espera entre una acción y otra. Ese tiempo está dado en milisegundos (ms). En *Karel.js* podemos indicar la velocidad de ejecución en el apartado de `Retraso` de la parte superior. Por ejemplo, si indicamos un retraso de 1000 entonces Karel esperara 1 segundo entre una acción y otra. Si ponemos un valor de 50 entonces Karel hará las cosas mucho más rápido.

Modificar la velocidad de ejecución es muy útil cuando estamos viendo qué es lo que hace exactamente nuestro programa, en ocasiones servirá que Karel se mueva muy rápido y otras veces querremos que lo haga lento para apreciar cada detalle.

### Paso a paso

El botón *paso a paso* <i class="fas fa-forward"></i> es el cuarto de izquierda a derecha. Cada que presionamos este botón Karel realiza únicamente una operación, es decir, hace que Karel haga las cosas paso a paso, un click = un paso.

### Ver el futuro

Al presionar este botón *Karel.js* nos mostrará cómo queda el mundo al terminar de ejecutar todo nuestro programa. Esto es muy útil cuando Karel tiene muchas cosas que hacer y queremos ver el resultado final en un instante.

### Volver al inicio

Al presionar este botón el mapa del mundo se mueve automáticamente hasta la posición inicial en `1, 1`. Este botón es el quinto de izquierda a derecha y tiene una casita en él <i class="fas fa-home"></i>. 

### Ve a donde esté Karel

Este botón es el sexto y en él está Karel orientado al norte (<s>una flecha que apunta hacia arriba</s>). Al presionarlo aparece Karel en la vista del mapa del mundo actual, no importa dónde se encuentre él.

### Zumbadores en la mochila de Karel

En la barra donde están los demás botones, en la novena posición está el recuadro de `Mochila`, ahí podemos especificar cuántos zumbadores tiene Karel en su mochila al inicio de la ejecución. Puede tener cualquier cantidad, incluso infinito.

### Retraso

En este recuadro que está a la derecha del de la mochila (<s>y del cual ya hablamos más arriba</s>) podemos indicar el tiempo en milisegundos que Karel espera cada que realiza una acción. Mientras más pequeño sea este número más rápido actuará Karel en la ejecución (pero no significa que Karel sea muy rápido en el código). Podemos usar los botones de más y menos que están a la derecha para incrementar o disminuir el tiempo.

### Tamaño del mundo

A la derecha del recuadro de `Retraso` encontramos la opción de cambiar la cantidad de filas y columnas que hay en el mundo.

### Evaluador

El último botón de la barra de botones de la parte superior es para indicar parámetros y condiciones específicas de un programa. Esta opción es mucho más usada cuando estamos creando un problema y queremos especificar las condiciones del mundo pero también cuando estamos probando algún caso particular, donde Karel solamente pueda hacer $$100$$ veces la acción `avanza`, por ejemplo.

## Apartado de mensajes

En la esquina inferior izquierda de la pantalla encontramos un recuadro donde hay 2 pestañas, de forma predeterminada está abierta la pestaña de `Mensajes`, aquí se mostrarán indicaciones por parte del simulador, por ejemplo cuando hemos compilado un código correctamente, cuando Karel ha tenido un *accidente en su ejecución* o cuando hemos terminado con la ejecución de un programa.

## Pila de llamadas

La otra pestaña que se encuentra en la esquina inferior izquierda de la pantalla lleva por título `Pila` y hace referencia a la pila de llamadas de Karel. Esta pila de llamadas será vital cuando estés resolviendo problemas con recursión. Aquí es donde Karel va *"anotando"* cada función que realiza para que no se le olvide ninguna. 

> Si buscas la versión sobre *Karel Azul* que se instalaba en la computadora, aún puedes encontrarlo [acá]({{ site.baseurl }}/Karel/Azul/Principio/Simulador/ "Karel Azul &vert; #iP Code").

<div class="Nav">
    <a href="{{ site.baseurl }}/Karel/Principio/Zumbadores/" title="Zumbadores &vert; #iP Code">Tema anterior</a> | <a href="{{ site.baseurl }}/Karel/Instrucciones/Lineales/" title="Instrucciones lineales &vert; #iP Code">Tema siguiente</a>
</div>