---
layout: G-Article
title: Recursión con parámetros en Karel
---

¿Has notado que con Karel no usamos números? Es decir, sí, los usamos pero sólo para la estructura `repetir`, con otra cosa no. Pero siendo más claros, no podemos contar contar alguna cosa y tener presente ese número (de lo que ya contamos) para usarlo de diversas formas ¿o sí? <br>
Ya aprendimos que con recursión podemos contar, más bien dicho podemos repetir un conjunto de acciones la misma cantidad de veces que hicimos la llamada recursiva, pero nunca vemos de manera más práctica y concisa las repeticiones de la recursión. Para poder lograr esto la recursión simple ya no nos alcanza. Sin embargo, Karel tiene otra habilidad que nos salva en estos casos: la recursión con parámetros.

{: #ListaContenido}
- Parámetros; la idea de variable
- Parámetros en Karel
- Expresión sucede
- Expresión precede
- Aumentar o disminuir más de 1
- Expresión si-es-cero
- Expresión no si-es-cero

## Parámetros; la idea de variable

Cuando en la escuela, te pones a resolver un problema de matemáticas, como por ejemplo, *Zita ayer tenía 15 libros, pero esta mañana ha comprado 3 más, ¿cuántos libros tiene ahora?*, (<s>vaya problema difícil</s>) encontramos y manejamos los números que nos dan en el problema con toda naturalidad, esos **datos** que nos da el problema son los que nos hacen mucho más sencillo resolverlo, a esos datos les llamaremos **parámetros**. Lo que el DRAE tiene para decirnos sobre los parámetros es:

> **[parámetro](http://dle.rae.es/?id=Rrl8oAZ){: target="_blank"}**: <br>
> 1- m. Dato o factor que se toma como necesario para analizar o valorar una situación. <br>
> 2- m. Mat. Variable que, en una familia de elementos, sirve para identificar cada uno de ellos mediante su valor numérico.

Como puedes ver, en nuestro ejemplo de los libros de Zita, se nos dan los datos necesarios para poder analizar su situación, esos datos podemos verlos como *variables* de nuestro problema, que al final mediremos con un valor numérico, es decir, diremos cuántos libros tiene ella en total.

<span>Pero, un momento, ¿qué es una variable?</span> Como su nombre lo indica, es algo que varía, en este caso (<s>así como en las matemáticas</s>) nos referimos a que es su valor el que varía, es decir, el que puede cambiar, ser diferente, ser [variable](http://dle.rae.es/?id=bNTTsak){: target="_blank"}.

Recuerda que en la programación no diseñamos soluciones para un caso específico de un problema, sino que debemos diseñar soluciones para **todos** los casos de un problema. Por ellos es poco común que manejemos los datos de un problema como algo [constante](http://dle.rae.es/?id=AQymQN7){: target="_blank"}, que nunca cambia y siempre es igual, no. Hay que ver los datos del problema como algo que es variable y nuestra solución debe adaptarse a eso. De esta forma, si Zita nos preguntara cuántos libros tiene ella en total, nosotros consideraríamos lo siguiente:

<textarea class="output">
libros-de-ayer + libros-de-hoy = libros-en-total</textarea>


Para el caso mencionado nuestras variables tendrían valores como sigue: `libros-de-ayer = 15`; `libros-de-hoy = 3`; dando un total de **18 libros**. Dicho de otro modo `libros-en-total = 15+3 = 18` (<span>bien por ti, Zita</span>).

## Parámetros en Karel

¿Notaste que en la pila de llamadas cada que se llamaba una función, al registrarse su nombre se ponía justo delante unos paréntesis vacíos? Seguro te preguntaste el porqué de esos paréntesis. En realidad, esos paréntesis están ahí para mostrar **el valor de un parámetro**. <span>¿Pero qué parámetro?</span> Hasta ahora no hemos declarado ningún parámetro en realidad, no le hemos dicho a el compilador que vamos a usar alguno, pero él ya está listo para el caso en el que lo necesitemos. Para declarar un parámetro tenemos que hacerlo de la siguiente manera:

<textarea class="eKarel">
iniciar-programa
	define-nueva-instruccion UnaNueva(x) como
	inicio
		avanza;
		gira-izquierda;
	fin;
	inicia-ejecucion
		UnaNueva(0);
		apagate;
	termina-ejecucion
finalizar-programa</textarea>

Si ejecutas esta función, verás como en la *pila de llamadas* junto a el nombre de la función ya aparece el valor de su parámetro entre paréntesis, que en este caso es 0. Hay algunas cosas **muy muy importantes** que debes recordar sobre los parámetros en Karel.

> En la función principal siempre debes llamar a la función dándole un valor numérico **entero y mayor o igual a 0**.

> Al declarar la función y poner algo entre los paréntesis, lo que ponemos ahí es el **nombre del parámetro**.

> Las mismas reglas para los nombres de funciones aplican para el nombre de los parámetros.

Es aconsejable que uses un nombre corto como nombre de las variables, (<span>muy corto, como sólo una letra</span>), de esta manera te es más sencillo escribirla y recordarla. <br>
Ahora, ya hemos declarado, un parámetro, (<span>genial</span>) pero <span>¿Para qué dijimos que nos servía?</span> El parámetro por sí solo no nos sirve de mucho en realidad, su poder está en **la manera en la que lo manipulamos**.

## Expresión sucede

En las matemáticas el poder de las variables está en que podemos modificar su valor, por ejemplo sumándole alguna determinada cantidad (u otra variable incluso). En el lenguaje de Karel, también podemos modificar el valor de sus parámetros, la manera de hacer esto es en realidad sencilla (<s>y poderosa</s>).

<textarea class="eKarel">
iniciar-programa
	define-nueva-instruccion UnaNueva(x) como
	inicio
		si frente-libre entonces
		inicio
			deja-zumbador;
			UnaNueva(sucede(x));
		fin;
	fin;
	inicia-ejecucion
		UnaNueva(0);
		apagate;
	termina-ejecucion
finalizar-programa</textarea>

Como puedes notar, en este código hemos agregado algo distinto al parámetro de la función `UnaNueva` que está en la línea 7. Hemos agregado la expresión `sucede`. <br>
El uso de esta expresión es en realidad muy sencillo, **aumenta en uno el valor de la variable o número que tiene dentro de su paréntesis**. Por ejemplo:

<textarea class="output">
sucede(variable) = variable+1
sucede(5) = 5+1 = 6</textarea>


Nota que está el nombre de la función, luego unos paréntesis, ahí dentro va la expresión (si aplica) y ya que ponemos la expresión va otra vez unos paréntesis y entre ellos la variable o valor al que queremos agregar uno más. <br>
Ahora sí, analicemos lo que sucede en la pila de llamadas cuando ejecutamos el código anterior en un mundo como este.

<video controls>
	<source src="{{ site.iP-Sources }}/Multimedia/Videos/E5/E5.mp4" type="video/mp4">
	<source src="{{ site.iP-Sources }}/Multimedia/Videos/E5/E5.webm" type="video/webm">
	Tu navegador no soporta este video :c
</video>

Como puedes ver, el valor de su parámetro comenzó siendo 0, porque así lo definimos cuando lo llamamos por primera vez desde la función principal, y fue incrementando cada vez que hacía la llamada recursiva desde la línea 7. Cuando ya no pudo seguir realizándose la recursión, debido a que el frente se había bloqueado, el parámetro tenía valor de 5. Prueba a dar distintos *valores iniciales al parámetro*.

> Es muy importante saber, que si tenemos dos funciones con parámetros en nuestro programa, por ejemplo `FuncionUno` y `FuncionDos` podemos llamar desde `FuncionUno` a la otra función dándole como valor inicial a su parámetro (al de `FuncionDos`) el valor del parámetro de `FuncionUno`. Prueba a intentarlo en tu simulador.

## Expresión precede

Así como en la vida conocemos la suma y la resta, también Karel conoce el principio de añadir y de quitar. Como ya vimos, añade con `sucede`. <br>
Para que Karel quite o disminuya un valor, utilizamos la expresión `precede`. Su funcionamiento es más o menos igual al de `sucede`, sólo que es [inverso](http://dle.rae.es/?id=M3NVLLY){: target="_blank"}.

<textarea class="eKarel">
iniciar-programa
	define-nueva-instruccion UnaNueva(x) como
	inicio
		si frente-libre entonces
		inicio
			deja-zumbador;
			UnaNueva(precede(x));
		fin;
	fin;
	inicia-ejecucion
		UnaNueva(8);
		apagate;
	termina-ejecucion
finalizar-programa</textarea>

La ejecución de este código se ve así:

<video class="VideoG" controls>
	<source src="{{ site.iP-Sources }}/Multimedia/Videos/E6/E6.mp4" type="video/mp4">
	<source src="{{ site.iP-Sources }}/Multimedia/Videos/E6/E6.webm" type="video/webm">
	Tu navegador no soporta este video :c
</video>

Nota que esta vez iniciamos con 8, y terminamos con tres, pues por cada llamada recursiva se le restaba uno a la variable. <br>
¿Qué habría pasado si empezamos con el cero? De haber empezado por el 0, al quitarle 1 por cada llamada habríamos llevado un [valor negativo](http://dle.rae.es/?id=QM8mhzM#NryQS8z){: target="_blank"}. Es decir, su valor sería incluso menor a 0. Karel **no sabe manejar números negativos**. Así que procura nunca llegar a una situación en la que tenga que usarlos.

## Aumentar o disminuir más de 1

Seguramente ya te has preguntado o incluso tratado de hacer que Karel aumente o disminuya más de uno a una variable. Esto es posible y en realidad es muy sencillo.  <br>
Primero tienes que verlo de la siguiente manera.

<textarea class="output">
NombreDeFuncion( valor ) </textarea>

Ahí tenemos una función con un parámetro, ese parámetro se llama (<span>para fines [prácticos](http://dle.rae.es/?id=TtEMsxJ#NIXOKao){: target="_blank"}</span>) `valor`. Todo bien hasta ahí, ahora vamos a incrementar ese valor en uno. La cosa se vería más o menos así.

<textarea class="output">
NombreDeFuncion( sucede(valor) )</textarea>

Esto a su vez, sería más o menos lo mismo que decir:

<textarea class="output">
NombreDeFuncion( 1+(valor) )</textarea>

Entonces, si queremos sumar más de uno, por ejemplo 2, es como querer que esto se viera así

<textarea class="output">
NombreDeFuncion( 1+( 1+(valor) ) )</textarea>

<span>Seguramente ya lo tienes</span>. Para hacer, entonces que Karel incremente 2 a su parámetro por cada llamada recursiva, un código completo se vería así. 

<textarea class="eKarel">
iniciar-programa
	define-nueva-instruccion UnaNueva(x) como
	inicio
		si frente-libre entonces
		inicio
			deja-zumbador;
			UnaNueva(sucede(sucede(x)));
		fin;
	fin;
	inicia-ejecucion
		UnaNueva(0);
		apagate;
	termina-ejecucion
finalizar-programa</textarea>

Lo mismo sería para restar 2, aunque claro, en lugar de `sucede` usaríamos `precede`. <span>¿Y si queremos sumarle 3? Seguro que ya lo tienes</span>.

## Expresión si-es-cero

¿Recuerdas cuando aprendimos lo que era una condición y vimos las condiciones que Karel puede evaluar? Pues ahora que ya estás aprendiendo sobre los parámetros estás listo para aprender la última condición que Karel conoce. <br>
A diferencia de nosotros, Karel no puede comparar dos números, decir si es más grande o más chico. Lo que sí puede hacer es decirnos si un valor es igual a 0. ¿Por qué 0? No estamos seguros en realidad, pero lo más probable es que es porque el cero es un número muy práctico. (<s>o tal vez a Karel le gusta mucho</s>). El valor que Karel puede evaluar es el de **una variable**. 

En realidad Karel también puede evaluar un número ya definido, pero el que nosotros le preguntemos, por ejemplo si 5 es igual a 0, es en realidad algo nada útil de nuestra parte, pues sabemos que el 5 nunca va a ser igual a 0 porque siempre va a ser igual a 5. De lo que no podemos estar seguros es de que una variable sea siempre igual o diferente a 0, es por eso que está de más decir que sólo evaluaremos variables.

Recuerda que estamos hablando de **una condición** aunque a diferencia de las demás parezca más bien una comparación en sí por como se lee. Pero no te confundas, un ejemplo te será más útil.

<textarea class="eKarel">
si si-es-cero(x) entonces avanza;</textarea>

De esta forma, si el valor de el parámetro `x` es igual a 0, Karel avanzará. En un programa completo podemos verlo así.

<textarea class="eKarel">
iniciar-programa
	define-nueva-instruccion UnaNueva(x) como
	inicio
		si si-es-cero(x) entonces
		inicio
			deja-zumbador;
			UnaNueva(precede(x));
		fin sino gira-izquierda;
	fin;
	inicia-ejecucion
		UnaNueva(3);
		apagate;
	termina-ejecucion
finalizar-programa</textarea>

Seguramente ya notaste que en este caso Karel nunca dejará un zumbador ni hará una llamada recursiva, pues la condición en la línea 4 no es verdadera, y esto se debe a que la función es llamada dando un valor de 3 al parámetro `x`. Y como 3 y 0 no son iguales, no se realizan las acciones de esa comparación, lo que pasará es que Karel girará a la izquierda, pues la condición no se cumplió.

> Nota que siendo `si-es-cero(x)` una condición puedes combinarla con cualquier otra condición como aprendiste en la sección de [instrucciones condicionales]({{ site.baseurl }}/Karel/Instrucciones/Condicionales/){: target="_blank"}.

## Expresión no si-es-cero

Cuando vimos por primera vez la cláusula `no`, parecía que usarla no tenía mucho sentido, sin embargo, ahora y dado a que no existe la condición `no-es-cero(x)` tenemos que usar la cláusula `no` forzosamente para evaluar cuando una variable **no** es igual a cero.

<textarea class="eKarel">
iniciar-programa
	define-nueva-instruccion UnaNueva(x) como
	inicio
		si no si-es-cero(x) entonces
		inicio
			deja-zumbador;
			UnaNueva(precede(x));
		fin;
	fin;
	inicia-ejecucion
		UnaNueva(3);
		apagate;
	termina-ejecucion
finalizar-programa</textarea>

Usando el código anterior, y poniendo zumbadores en la mochila de Karel, el código de arriba nos dará la siguiente ejecución.

<video class="VideoG" controls>
	<source src="{{ site.iP-Sources }}/Multimedia/Videos/E7/E7.mp4" type="video/mp4">
	<source src="{{ site.iP-Sources }}/Multimedia/Videos/E7/E7.webm" type="video/webm">
	Tu navegador no soporta este video :c
</video>

Como puedes ver, Karel deja 3 zumbadores mientras realiza llamadas recursivas, en las que cada vez le va restando uno al valor de su variable. Esa variable empezó siendo 3, pero al irle quitando, en un momento se hizo 0, cuando eso pasó la condición en la línea 4 dejó de cumplirse, y por lo tanto la recursión terminó.

> El uso de `si-es-cero` y  `si no si-es-cero` puede resultar confuso, pero con un poco de práctica te acostumbrarás.

> También puedes hacer comparaciones como `si-es-cero( sucede(x) )`

> Ya estas listo para comenzar con la sección de *Recursión con parámetros* de Karelotitlán.

<div class="Nav">
	<a href="{{ site.baseurl }}/Karel/Recursion/Simple/">Tema anterior</a>
</div>