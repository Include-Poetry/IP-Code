---
layout: G-Article
title: Recursión simple en Karel
---
Ya que sabemos lo que es la [recursión]({{ site.baseurl }}/Karel/Recursion/){: target="_blank"} es momento de aprender cómo aprovecharla en Karel, conocer su correcta declaración y uso principal.

{: #ListaContenido}
- Idea de la pila
- Pila de llamadas
- La pila y la recursión
- Recursión para contar
- Notas

## Idea de la pila

Seguramente al escuchar (<s>o leer</s>) la palabra "pila", lo primero que pienses sea en una pila eléctrica, como las que usa el control de la televisión para funcionar. Sin embargo, nosotros como buenos programadores, conocemos otro significado para esa palabra, que no es muy diferente en realidad a lo que ya sabemos.

En la antigüedad, existió un muy ingenioso físico llamado **Alessandro Volta**, este hombre un día, y gracias años de experimentación e investigación, logró construir la primer batería. Esta invención suya se dio a conocer como la **pila voltaica**, y consistía de pares de pequeños discos de cobre y zinc apilados uno encima de otro. Su invento lucía algo así:

[<picture>
	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/Karel/PilaVolta.jpg">
	<img class="Imagen" src="{{ site.iP-Sources }}/Multimedia/Karel/PilaVolta.jpg" alt="Pila voltaica">
</picture>]({{ site.iP-Sources }}/Multimedia/PilaVolta.jpg){: data-lightbox="image-1"}

<span>¿Ya has notado la idea?</span> El secreto de la idea aquí, se encuentra en la palabra [apilar](http://dle.rae.es/?id=3AOy8Wo){: target="_blank"}, que seguro te suena familiar, como también lo es ahora la palabra **pila**. Como *una pila de platos*. En donde hay un plato arriba de otro.

El funcionamiento básico de una pila (<s>y ya no hablamos de la pila de Volta</s>) es muy sencillo, imagina la pila de platos, pones sobre una mesa el primer plato, luego sobre éste pones otro, y luego otro y otro más. Cuando quieres tomar un plato de esta pila que ya armaste, tomas el que está hasta arriba, no el que quedó hasta abajo. Es decir **el último en poner es el primero que se tomará**. Y del mismo modo, cuando hayamos tomado todos los platos, y sólo quede uno, será el que estaba hasta abajo, que es el que pusimos primero, entonces también podemos decir que **el primero en poner será el último en quitar**.

> En una pila podemos decir que: <br>
> **El primero en entrar es el último en salir** y que **el último en entrar será el primero en salir**

## Pila de llamadas

¿Has notado para qué sirve el rectángulo blanco que se encuentra en la esquina inferior izquierda de la pantalla de ejecución del simulador de Karel el robot? Seguramente has notado que está ahí, aunque entender su funcionamiento y motivo de estar ahí es un poco más profundo. Para entenderlo mejor vamos a analizar lo que pasa cuando ejecutamos un programa que tiene una función declarada por nosotros.

<video controls>
	<source src="{{ site.iP-Sources }}/Multimedia/Videos/E1/E1.mp4" type="video/mp4" />
	<source src="{{ site.iP-Sources }}/Multimedia/Videos/E1/E1.webm" type="video/webm" />
	Tu navegador no soporta este video :c
</video>

Es muy importante que notes que la ejecución que se realiza aquí, es paso a paso, para ver línea a línea lo que está sucediendo. <br>
La ejecución es muy sencilla, el programa arranca con la instrucción `avanza` en la línea 8, después pasa a la línea 9 en donde se indica que hay que ejecutar la instrucción `nueva`, que es la que declaramos, entonces la ejecución sigue por la línea 4, que es en donde está la primer acción de `nueva`, el programa sigue con el `avanza` de la línea 5 y una vez que llega al final de la instrucción en la línea 6, se regresa a la línea 10 que es en donde iba **antes de que la instrucción `nueva` fuera llamada**. (Si algo no tiene sentido para ti, vuelve a analizar el código, recordar la sección de [funciones]({{ site.baseurl }}/Karel/Funciones/){: target="_blank"} puede ser muy útil.)

Karel funciona entonces sin problemas y termina con su ejecución con normalidad. Sin embargo, aquí hay una habilidad muy especial de Karel que estamos olvidando y que fue **clave** para que todo marchara bien. Esa habilidad es la capacidad de **recordar dónde se había quedado** para volver ahí una vez terminada la ejecución de esa instrucción. A el lugar donde Karel guarda y recuerda dónde se había quedado le llamaremos **pila de llamadas**. Nosotros la vemos en ese rectángulo blanco.

Es por esto que cuando la ejecución llega a la línea 9 en la pila de llamadas se guarda el nombre de la función y la línea desde la que fue llamada. Cuando termina de ejecutar esa función, Karel toma **la última cosa guardada en la pila** y continúa desde ahí.

## La pila y la recursión

Primero veamos la manera correcta de realizar una llamada recursiva con Karel. En estos casos, podemos tomar como recursión el hecho de **llamar a una función desde sí misma**. Es decir, tener una función y como una instrucción dentro de ella está el realizar la función misma. <span>¿No queda muy claro?</span> Analiza el siguiente código.

<textarea class="eKarel">
iniciar-programa
	define-nueva-instruccion avanzando como
	inicio
		avanza;
		si frente-libre entonces
		inicio
			avanzando;
		fin;
	fin;
	inicia-ejecucion
		avanzando;
		apagate;
	termina-ejecucion
finalizar-programa</textarea>

Como puedes ver, declaramos una nueva instrucción llamada `avanzando`, en la cual avanzamos, luego checamos que el frente esté libre, y de ser así entonces volvemos a llamar a la función `avanzando`. Recuerda que en toda recursión debemos poner una condición que la detenga. En este caso nuestra recursión termina cuando ya no tenemos el frente libre. <br>
Pero no olvidemos a la pila de llamadas, lo que sucede con ella en la recursión es muy importante.

<video controls>
	<source src="{{ site.iP-Sources }}/Multimedia/Videos/E2/E2.mp4" type="video/mp4">
	<source src="{{ site.iP-Sources }}/Multimedia/Videos/E2/E2.webm" type="video/webm">
	Tu navegador no soporta este video :c
</video>

La acción empieza en la línea 11 cuando desde la función principal se llama a `avanzando` que es la instrucción que declaramos, entonces se guarda en la pila que se llamó a `avanzando` desde la línea 11, ahora la ejecución continúa por la línea 4, en donde avanza Karel, después pasa a la línea 5, evalúa si el frente está libre y como sí lo está, vuelve a llamar a la función `avanzando` en la línea 7, entonces se guarda en la pila que se llamó a la instrucción `avanzando` pero esta vez desde la línea 7. Vuelve a repetir este proceso hasta que ya no tiene el frente libre.

<span>¿Y qué pasa cuando el frente ya no está libre?</span> Cuando revisa por cuarta vez si el frente está libre, ya no lo está, entonces la condición no se cumple y **no se ejecuta otra llamada**, sino que sigue por la línea 8, que es el final del `si`, luego sigue con la línea 9 que no es más que el final de la instrucción. Entonces Karel revisa la pila y toma el **último elemento** que puso (<span>recuerda que es una pila</span>), así se da cuenta que se había quedado en la línea 7 antes de que se llamara por última vez a la instrucción, sin embargo, sólo sale del `si` y luego de la instrucción, y repite esto varias veces.

<span>¿Y cuántas veces se repite eso?</span> Pues **la misma cantidad de veces que se llamó a la función**, para al terminar de vaciar la pila regrese a la línea 11 que fue en donde se llamó por primera vez. Al final de esta ejecución Karel habrá avanzado hasta llegar a la pared que tiene en frente. <br>
<span>Genial, pero pude hacer eso con un ciclo `mientras` ¿por qué molestarme en usa recursión?</span>

## Recursión para contar

¿Notaste que durante la ejecución algo tuviera alguna relación con la pila de llamadas? Si pones atención, notarás que Karel avanzó la misma cantidad de veces que se llamó a la instrucción `avanzando`. Exactamente la misma cantidad, pues cada que se llamaba a la instrucción Karel avanzaba. Siendo así, podemos utilizar esto a nuestro favor. Hagamos una pequeña modificación al código que usamos arriba.

<textarea class="eKarel">
iniciar-programa
	define-nueva-instruccion avanzando como
	inicio
		avanza;
		si frente-libre entonces
		inicio
			avanzando;
			deja-zumbador;
		fin;
	fin;
	inicia-ejecucion
		avanzando;
		apagate;
	termina-ejecucion
finalizar-programa</textarea>

Al ejecutar lo anterior tendremos a Karel haciendo esto:

<video controls>
	<source src="{{ site.iP-Sources }}/Multimedia/Videos/E3/E3.mp4" type="video/mp4">
	<source src="{{ site.iP-Sources }}/Multimedia/Videos/E3/E3.webm" type="video/webm">
	Tu navegador no soporta este video :c
</video>

Si analizamos lo ocurrido, podemos ver que Karel ha puesto 3 zumbadores en la posición en donde estaba cuando la recursión terminó. Esto se debe a que Karel cada que llamaba a la instrucción `avanzando` desde la línea 7, dejaba pendiente continuar con la línea 8, en donde dejaría un zumbador. Estos zumbadores no los deja inmediatamente después de avanzar un paso, sino hasta el final, cuando toma de la pila las líneas que había dejado pendientes para ejecución.

Sin embargo, aunque Karel avanzó 4 veces en total, no dejó 4 zumbadores. Esto es porque solamente dejó pendientes 3 veces dejar un zumbador, según la línea 8. Seguro que ya sabes dónde hay que modificar para hacer que Karel deje la cantidad exacta de zumbadores. Ten en cuenta que esta tarea se puede resolver de muchas maneras distintas, prueba a modificar en tu simulador.

Hagamos ahora otro ejemplo, imagina que Karel inicia siempre sobre un montón de zumbadores, tiene infinitos zumbadores en la mochila además y se te pide que gire a la izquierda la misma cantidad de veces que zumbadores sobre los que está. Es decir, si está sobre 3 zumbadores gire 3 veces y luego se apague. Prueba a resolverlo primero en el tu simulador y luego continúa con la explicación aquí.

<video controls>
	<source src="{{ site.iP-Sources }}/Multimedia/Videos/E4/E4.mp4" type="video/mp4">
	<source src="{{ site.iP-Sources }}/Multimedia/Videos/E4/E4.webm" type="video/webm">
	Tu navegador no soporta este video :c
</video>

Como puedes notar, Karel gira la misma cantidad de veces que la cantidad de zumbadores sobre los que estaba. Al final de esta ejecución ya no quedan zumbadores en la posición, pero seguro que puedes hacer que los deje de nuevo.

## Notas

> Pon mucha atención a las condiciones iniciales de los mundos de estos ejemplos, han sido las ideales para que Karel pudiera realizar el trabajo esperado.

> Recuerda que lo más aconsejable es que vayas realizando en tu simulador las practicas de ejemplo de aquí a la vez que analizas las explicaciones.

> Pon a prueba lo que has aprendido haciendo los problemas de la sección de recursión de Karelotitlán.

<div class="Nav">
	<a href="{{ site.baseurl }}/Karel/Recursion/">Tema anterior</a> | <a href="{{ site.baseurl }}/Karel/Recursion/Parametros/">Tema siguiente</a>
</div>