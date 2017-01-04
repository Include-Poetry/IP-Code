---
layout: G-Article
title: Tipos de variables en C++
---

En la vida diaria construimos y hacemos todo tipo de cosas, desde comida hasta computadoras, sin embargo, no utilizamos los mismos componentes para todas nuestras creaciones, si queremos hacer un pastel usamos harina, leche, mantequilla... que no son los mismos componentes que usaríamos si quisiéramos construir una casa (<s>a menos de que vivamos en el universo de Hansel y Gretel</s>) pues cada componente tiene características que son enfocadas a un cierto uso. En la programación pasa exactamente lo mismo.

{: #ListaContenido}
- Concepto de variable
- Idea de tipos de variable
- Variables básicas en C++
- Declaración de variables
- Limitaciones de las variables básicas
- Memoria y números binarios
- Tipos especiales de variable
- Parámetros signed y unsigned
- Código ASCII
- Conversiones de tipos
- Uso responsable de memoria

## Concepto de variable

Si ya has visto algo de *álgebra*, seguramente ya conoces lo que es una [variable](http://dle.rae.es/?id=bNTTsak){: target="_blank"}. Una variable en sí es algo muy sencillo de concebir, es **algo que puede variar**. Con esa *variación* por lo general nos referimos a un valor, por ejemplo, el valor de un dolar en pesos mexicanos. Sin embargo, puede no ser solamente un número, sino también una palabra.

> Consideraremos a una variable como algo cuyo valor puede variar

## Idea de tipos de variable

Cuando nos referimos a *tipos de variables* en realidad nos estamos refiriendo a distintos tipos de valores que una variable puede tener. Nota que no sólo decimos "distintos valores", sino *distintos tipos de valores*. Por ejemplo, imagina que, como muy a menudo, quieres hacer un pastel, necesitarás *mantequilla*, *azúcar*, *huevos*, *harina*, *cocoa*, *levadura*, *maicena* y *sal*.<br>
Sin embargo, cada ingrediente puede interpretarse distinto. Por ejemplo, al hablar de harina, puede ser de trigo, de maíz, de avena, etc.

De esta manera podemos interpretar cada ingrediente como tipo de variable, y cada tipo de ingrediente como su valor, como decir `harina trigo`, refiriéndonos a que estamos hablando de una variable tipo `harina` con valor de `trigo`. Nota que no puede haber algo como `harina NataDulce`, porque `NataDulce` es un valor posible de una variable tipo `mantequilla`.

## Variables básicas en C++

Así como en la cocina encontramos distintos tipos de variable, que pueden tener distintos tipos de valores. Las variables básicas en C/C++ son:

`int` Para valores tipo números enteros, por ejemplo $$ 5, 231, -3432 $$.<br>
`float` Para valores tipo números no enteros, o con decimales, por ejemplo $$ 3.14, 823.23, -0.231 $$.<br>
`char` Para valores tipo carácter. Un carácter es un *símbolo*, como los que usamos para escribir, por ejemplo 'T', 'c', 'r', '/', '5'. En este último caso el 5 será considerado como sólo un carácter, como sólo un símbolo y no un número.<br>
`bool` Para valores tipo booleanos, es decir, de *afirmativo* o *negativo*, *cierto* o *falso*.

## Declaración de variables

Cuando queremos utilizar algo, es de buena educación **pedirlo primero**, en C/C++ pasa exactamente lo mismo, aunque aquí es obligatorio. Cuando queremos usar una variable necesitamos primero **declararla**, y para hacer esto tomamos un formato como sigue:

<textarea class="output">
tipo-de-variable nombre-de-variable[=valor]</textarea>

Nota que lo que está entre corchetes es opcional, puedes o no dar el valor a la variable al mismo tiempo que la declaras. Podemos además declarar varias variables del mismo tipo separándolas con comas. Si quisiéramos declarar variables como las básicas, sería así:

<textarea class="editor">
int T=1401, variable=1, a;
float pi=3.14, decimal, otra=0.23;
char letra='C', mas;
bool dicho=true, bandera=false;</textarea>

Una variable puede tener cualquier nombre conformado por letras y/o números, que no incluya espacios, símbolos especiales, sea una palabra reservada del compilador (como el tipo de variable), ya lo tenga otra variable o función, o sea enteramente compuesta por números. *Sí hay distinción de mayúsculas y minúsculas* por lo que `int Variable` es diferente de `int variable`.
<br>
Nota que después de declarar una serie de variables de un mismo tipo hay que poner un `;`

En nuestro ejemplo, la variable `a`, `decimal` y `mas` que son las que no *inicializamos* es decir, que no les dimos nosotros un valor inicial, tienen un valor *aleatorio* que la computadora les ha dado. Este valor no es un valor *manipulable*, o al menos no hay que tratarlo como si lo fuera, pues es un valor que nosotros no conocemos. No hay problema si no inicializamos al momento de declarar una variable, siempre y cuando no la usemos hasta que no le hayamos dado un valor nosotros mismos. En cuanto nosotros ya le hayamos dado un valor podemos decir que ya está *inicializada*.

## Limitaciones de las variables básicas

Cada tipo de variable tiene ciertas limitaciones que nos llevan a modificar nuestras declaraciones y que siempre debemos tener en cuenta, por ejemplo:

`int` Almacena típicamente cualquier número entero $$ x $$ donde $$ -2 147 483 648 \le x \le 2 147 483 647 $$<br>
`float` Almacena típicamente cualquier número $$ x $$ donde $$ 1.18e^{-38} \le x \le 3.40e^{38} $$ con una precisión científica de $$ 7 $$ dígitos después del punto decimal.<br>
`char` Almacena sólo $$ 1 $$ carácter de los $$ 256 $$ posibles del código ASCII<br>
`bool` Almacena sólo un valor `true` o `false`

De esta manera, si necesitáramos una variable entera mayor a $$ 2 147 483 647 $$ una simple variable `int` no nos bastaría. Sin embargo, y para esto tenemos otras variables, con alcances mayores. Aunque hay un factor muy importante a considerar para saber qué variables usar, además claro, del tipo de valor que queremos guardar; **la memoria**.

## Memoria y números binarios

Sabemos de antemano que cuando hablamos de la memoria de una computadora o celular, nos referimos a la capacidad de almacenar archivos, programas, etc. Pero ¿te has preguntado por qué es así? Es decir ¿cómo es que un archivo ocupa espacio en un dispositivo? La respuesta detrás de esto está muy ligada a las variables de las que estamos hablando. Una variable, al igual que un archivo, necesita *estar registrada* en alguna parte, y ahí donde está ocupará espacio, y esto es así porque la computadora *recuerda* las características que estamos guardando.

Es decir, si tú declaras una variable `int T=1;` la computadora *anota* en alguna parte, que estarás usando una variable de tipo `int`, llamada `T` y que además tiene un valor de $$ 1 $$. Ahora, ya mencionamos que la computadora no puede recordar el valor de una variable de este tipo cuando es mayor a $$ 2 147 483 647 $$ pero <span>¿por qué es así? ¿No te parece un número demasiado específico?</span>

La capacidad de *almacenamiento* o más bien de *asignación* de una variable de un determinado tipo está basada en el espacio que la computadora dedica a cada tipo de variable, y también a la manera en que se guardan los valores en la memoria de una computadora.

Los equipos informáticos de hoy en día, utilizan el sistema *binario*, nosotros usamos el decimal, tenemos $$ 10 $$ posibles dígitos, mientras que el binario sólo tiene $$ 2 $$, el $$ 1 $$  y el $$ 0 $$. Si estudiamos un poco el sistema binario, notaremos que se basa en potencias de $$ 2 $$. [Aquí](https://es.wikipedia.org/wiki/Sistema_binario){: target="_blank"} podrás encontrar de manera explicita el funcionamiento de este sistema, si no lo conoces dale una leída y después continúa aquí.

La memoria de la computadora tiene también unidades de medida, seguro estás familiarizado con algunas de ellas, como el *megabyte* y el *gigabyte*. La unidad más chica es el *bit*, su valor puede ser $$ 0 $$ o $$ 1 $$ Un conjunto ordenado de $$ 8 $$ bits representa un *byte* por lo que se podría ver como $$ 10010110 $$, es decir como un número de $$ 8 $$ dígitos, donde cada dígito puede ser $$ 1 $$ o $$ 0 $$.

Cada tipo de variable tiene un tamaño en bits, de esta manera, si quisiéramos saber cuál es el valor que una determinada variable puede tener basta con hacer la operación $$ 2^n $$ donde $$ n $$ es el tamaño en bits que la computadora asigna a cada uno. Los tamaños de las variables básicas son:

`int` Tamaño de $$ 32 $$ bits, por lo que su valor máximo es $$ 2^{32}=4294967296 $$ sin embargo, como tiene valores positivos y negativos esa cantidad se reduce a la mitad a los negativos y la mitad a los positivos y el cero.<br>
`float` Tamaño de $$ 32 $$ bits, su tamaño final se ve reducido por los signos y precisión extra de $$ 7 $$ dígitos.<br>
`char` Tamaño de $$ 8 $$ bits, su tamaño máximo es $$ 2^8 = 256 $$<br>
`bool` Tamaño de $$ 8 $$ bits, pero sólo es evaluado como `true` o `false`

## Tipos especiales de variable

Su declaración es igual a las ya mencionadas, pero su uso es más especial por los valores que pueden tomar. (En el segundo caso la declaración sería `long long T=123;`)

`short` Para valores enteros. Tamaño de $$ 16 $$ bits.<br>
`long long` Para valores enteros. Tamaño de $$ 64 $$ bits.<br>
`double` Para valores decimales, exactitud de $$ 15 $$ dígitos después del punto decimal. Valores $$ x $$ donde $$ 2.23e^{-308} \le x \le 1.79e^{308}  $$

## Parámetros signed y unsigned

Como hemos estado viendo, los valores de las variables se ven reducidos de su máximo posible en bits porque usamos signos positivo y negativo. Si sólo usáramos signos positivos tendríamos más espacio para valores más grandes, de la totalidad de sus bits. Para hacer esto usamos los parámetros `signed` y `unsigned`.

`signed int T=1;` Es el parámetro por defecto, no es necesario escribirse. Indica que la variable puede tener valores *signados*.<br>
`unsigned int T=14;` Indica que la variable sólo tendrá valores positivos, su valor máximo es $$ 2^n $$ donde $$ n $$ es el tamaño en bits de la variable, en este caso $$ 32 $$.

Nota que el parámetro va antes del tipo de variable, y ese parámetro afectará a todas las variables declaradas en esa línea.

## Código ASCII

Al principio se mencionó que una variable tipo `char` puede almacenar sólo caracteres, sin embargo, después se habla de un valor máximo de $$ 256 $$ <span>¿Es a caso una contradicción?</span> La verdad es que no. Una variable de este tipo lo que almacena en sí es un número con base decimal, un *código* que está asociado a un carácter. Este es el llamado *código ASCII*.

<a href="{{ site.iP-Sources }}/Multimedia/C/ASCII.png" data-lightbox="image-1">
    <picture>
    	<source media="(min-width: 700px)" srcset="{{ site.iP-Sources }}/Multimedia/C/ASCII.png">
    	<img class="Imagen" src="{{ site.iP-Sources }}/Multimedia/C/ASCII.png" alt="Código ASCII">
    </picture>
</a>

Por lo que cuando hacemos esto `char letra='C';` en realidad es igual que hacer `char letra=65;`, sin embargo, en definitiva es más sencillo sólo poner la letra y no tener que recordar su código.

## 	Conversiones de tipos

Seguramente te preguntaste qué pasa si a una variable tipo entero le das un valor decimal, es decir, si haces algo como `int C=9.21;`, o le asignas un carácter. Hay distintas combinaciones y por lo tanto distintas reacciones.

`int C=9.21;` Aquí se guardará sólo la parte entera de la asignación. Es decir será como poner `int C=9;`<br>
`int var='T';` Cuando damos un carácter como valor a una variable tipo entero, lo que se guardará en realidad será su código ASCII, en este caso `84`<br>
`bool algo=23;` Se interpretará como `true` cuando se asigne a una variable tipo booleana cualquier valor distinto de $$ 0 $$, cuando se le da este valor se tomará como de tipo `false`. Cabe decir que el compilador interpreta `false = 0` y `true = 1`<br>
`int T=true;` Se tomarán los valores `false = 0` y `true = 1`

Nota que aunque el compilador no nos marque un error al hacer algo como lo de arriba, esto es algo *no recomendable*. Los primeros dos casos pueden darse en algunas situaciones, pero sólo cuando sea forzosamente necesario, los últimos dos son mucho menos comunes y de hecho sería muy extraño verse en una situación que te forzara a hacer algo así.

## 	Uso responsable de memoria

Podríamos utilizar siempre variables tipo `long long` y así no preocuparnos mucho por los valores que pueda tener una variable de este tipo, sin embargo, esto usaría más memoria de la que suele ser necesaria. Por lo general las variables básicas signadas son suficientes para la mayoría de los problemas, y sólo hay que utilizar las especiales cuando las necesitemos, no es bueno el uso indiscriminado de memoria.

Si sabemos cuanto mide cada variable, y sabemos cuántas variables declaramos, podemos calcular cuál sería el requerimiento de espacio que necesite un programa que escribamos. Ten en cuenta que ese espacio no es el que medirá tu código fuente, o el archivo ejecutable, sino el que requerirá *la ejecución del programa*.

Si declaramos $$ 100 $$ variables tipo `int`, $$ 50 $$ tipo `char` y $$ 20 $$ tipo `double` estaremos ocupando en total $$ 100 \cdot 32 + 50 \cdot 8 + 20 \cdot 64 = 4880 $$ bits, es decir $$ 610 $$ bytes.

<div class="Nav">
	<a href="{{ site.baseurl }}/C++/Introduccion/Compilador/">Tema anterior</a> | <a href="{{ site.baseurl }}/C++/Introduccion/Librerias/">Tema siguiente</a>
</div>