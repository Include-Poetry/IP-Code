---
layout: G-Article
title: Operadores y entrada/salida de datos
author: rivel_co
tags: [Operadores]
Hide_Tags: true
olimpiada: [OMI]
subject: [C++]
---

Para manipular variables y conocer algunas de sus características utilizamos *operadores*, también tenemos la entrada y salida de datos, para mostrar y recibir información en la pantalla y del teclado respectivamente.

{: #ListaContenido}
- Operadores aritméticos
- Incremento y decremento
- Operadores lógicos
- Operadores de conjunción y disyunción
- Operador coma
- Operador ternario condicional
- Entrada y salida de datos

## Operadores aritméticos

Los operadores aritméticos son como los que utilizamos en *matemáticas*, así como la suma, la resta, etc.

**Asignación**
<br>
Una asignación es dar un valor a una variable, es decir, asignarle un valor. Para hacer esto usamos el símbolo de igual `=` y para usarlo en una sentencia sería como lo hemos manejado en las declaraciones de variables `int a=55;` además podemos dar asignaciones de una variable a otra como `a=b;` en este caso `a` y `b` tendrán el mismo valor, siendo que a la primera se le asignó el valor de la segunda, es decir, la asignación se realiza de derecha a izquierda. Después de toda asignación va `;`

**Suma**
<br>
Suma los valores implicados. Esta operación debe hacerse para hacer una asignación, es decir, necesitamos asignar el valor de esa suma a alguna parte, por ejemplo `T = 3 + 4;` También podemos hacer lo mismo con variables `T = a + 2;` este procedimiento no cambia el valor de `a` sino sólo el de `T` No hay que olvidar el `;` al final.

**Resta**
<br>
Resta los valores en orden de derecha a izquierda. Es necesario hacer una asignación para este proceso `A = 8 - 9;`

**Multiplicación**
<br>
Multiplica los valores implicados. Es necesario hacer una asignación para este proceso `A = 42 * 9;`

**División**
<br>
Divide los valores en orden de izquierda a derecha (<span>como habitualmente</span>). Es necesario hacer una asignación para este proceso `A = 8/2;`

**Módulo**
<br>
Obtiene el módulo del primer argumento dividido por el segundo. El símbolo para el módulo es `%` El *módulo* de dos números es el residuo inmediato de realizar la división de estos, por ejemplo $$ 6/4 $$ al hacer manualmente esa división veremos que el $$ 4 $$ *cabe* una vez en el $$ 6 $$ y *sobran* $$ 2 $$. Si aplicamos $$ 6\mod4 $$ obtendríamos ese $$ 2 $$. Otros ejemplos son $$ 4\mod5 = 4, 8\mod2 = 0 $$. Es necesario hacer una asignación para este proceso `A = 3%7;`. (<span>Nota que la sintaxis en el compilador es usando <code>%</code> la palabra <code>mod</code> sólo es para el lenguaje matemático</span>).

**Uso de paréntesis**
<br>
Podemos (y es necesario) usar paréntesis en operaciones aritméticas, justo como lo hacemos en matemáticas, por esto `T = (9+5)/7;` equivaldrá a $$ \frac{9+5}{7} = 2 $$

**Operadores a nivel asignación**
<br>
Si queremos por ejemplo aumentar el valor de una variable en tres unidades, podemos hacer `T = T + 3;` De esta forma le damos a `T` el valor que tenía más $$ 3 $$. Esto funciona pero (<s>personalmente creo que</s>) es más práctico usar las operaciones a nivel asignación, que consiste en poner antes del signo igual el signo del procedimiento a realizar, por ejemplo, la operación anterior se expresaría como `T += 3;` Lo que se hace es sumar a la variable de la izquierda todo lo que hay después del igual. `T *= 2;` sería como `T = T*2;`, también podemos hacer algo como `T -= 5+3;` Que sería como poner `T = T - (5+3);`. Puedes hacer esto con todos los operadores aritméticos.

## Incremento y decremento

El operador `++` y el operador `--` incrementan en uno y disminuyen en uno el valor de una variable respectivamente. El primer operador es como decir `a += 1;` y el segundo `a -= 1;` Nota que siempre incrementan o decrementan exactamente en una unidad.

El orden en el que se ubica el operador es muy importante, puede ser `T++;` o `++T;` lo mismo para el operador `--`. En el caso `A=4; T=A++;` la variable `A` terminará con un valor de $$ 5 $$ mientas que la variable `T` tendrá un valor de $$ 4 $$. Es decir, es como si se hubiera hecho `A=4; T=A; A++;`

Cuando ponemos el operador antes de la variable sucede distinto, al final del caso `A=4; T=++A;` la variable `A` mantendrá un valor de $$ 4 $$ mientras que la variable `T` tendrá un valor de $$ 5 $$, por lo que es como haber hecho `A=4; T=A+1;`.

## Operadores lógicos

Los operadores lógicos nos permiten saber algunas características de una variable en base a compararlas frente a alguna otra variable o valor. Nos devuelve un valor booleano (de cierto o falso).

**Mayor que**
<br>
Devuelve verdadero si el primer valor es más grande que el segundo `bool t = 3 > 6;` en este caso la comparación usando `>` nos daría como resultado `false` pues $$ 3 $$ no es mayor que $$ 6 $$

**Menor que**
<br>
Devuelve verdadero si el primer valor es más chico que el segundo, usa el operador `<`. Por ejemplo `bool C = 3 < 6;` tiene como valor final `true`

**Igual que**
<br>
Devuelve verdadero si los valores comparados son iguales, usa el operador `==` (<span>nota que son dos símbolos de igual, si sólo usas uno sería una asignación</span>). Por ejemplo `bool R = 5 == 8;` da como valor final `false`

**Diferente de**
<br>
Devuelve verdadero si los valores comparados son diferentes, usa el operador `!=`. Por ejemplo `bool F = 4 != -1;` devolvería `true` De hecho puedes usar el operador `!` con otros operadores lógicos. Devuelve verdadero si lo que está a la derecha del `!` es falso. Por ejemplo `!(4 > 5)` devolvería verdadero.

**Mayor o igual que**
<br>
Devuelve verdadero si el primer elemento es mayor o igual al segundo, usa el operador `>=`. Por ejemplo `bool A = 3 >= 8;` devuelve `false`

**Menor o igual**
<br>
Devuelve verdadero si el primer elemento es menor o igual al segundo, usa el operador `<=`. Por ejemplo `bool I = 3 <= 3;` devuelve `true`

## Operadores de conjunción y disyunción

Estos operadores nos permiten agrupar operadores lógicos y de esta manera hacer comparaciones más específicas.

**Conjunción**
<br>
Utilizan el operador `&&` que podríamos traducir como '*y*'. Devuelve verdadero cuando ambas comparaciones son verdaderas, por ejemplo `bool T = 4 < 6 && 3 >= 3;` daría un valor de `true` pues `4 < 6` es verdadero al igual que `3 >= 3`, sin embargo `bool T = 5 > 3 && 2 <= -1;` devuelve `false` pues aunque la primera comparación es verdadera la segunda no lo es, y para que la expresión completa sea verdadera ambas comparaciones deben serlo.

**Disyunción**
<br>
Utiliza el operador `||` que podríamos traducir como '*o*'. Devuelve verdadero cuando una de las dos comparaciones o ambas son verdaderas, por ejemplo `bool F = 4 < 6 || 7 < 2;` devuelve `true`, pues aunque la segunda comparación es falsa la segunda sí es verdadera.

## Operador coma

Este operador es literalmente `,` se utiliza para dar un orden a un par de procedimientos, por ejemplo `int a = (b=5, b+2);` de esta forma primero se le da a la variable `b` (que consideramos previamente declarada) el valor de $$ 5 $$ luego a la variable `a` se le da valor de `b+2` es decir $$ 7 $$.


## Operador ternario condicional

Este operador, como su nombre lo indica, es [ternario](http://dle.rae.es/?id=ZaQPxZN){: target="_blank"} por lo que está conformado por tres partes. Podríamos verla como una pequeña función que devuelve un valor en base a una comparación. Utiliza el operador `?` una expresión se vería así `(4 > 2) ? 78 : 21` en donde primero tenemos una comparación, luego tenemos el operador en sí, después de él un número que es el que la expresión devuelve si la comparación es verdadera, si no lo es devuelve el valor después de `:`. Como la expresión devuelve un valor es necesario asignar ese valor a alguna variable.

Una expresión completa de este tipo se ve así `int T = (4 > 5) ? 21 : 32;` después de esto la variable `T` tendrá un valor de $$ 32 $$ pues la comparación no fue verdadera.

## Entrada y salida de datos

Es importante recalcar que los que se mostrarán a continuación no son operadores, son objetos llamados *streams*, es una palabra en inglés cuya traducción directa al español es *corriente* o *flujo*, nosotros no le vemos mucho sentido con este significado, pero podríamos relacionarlo con el flujo de datos. Más típicamente nos referiremos a ellas como funciones.

Para utilizar la siguiente entrada y salida estándar de datos, debemos de agregar primero la línea `using namespace std;` Esto es debido a que que para el uso de *streams* se necesita de una notación particular, que podemos abarcar añadiendo la línea mencionada justo después de nuestras librerías. También debes saber que para utilizar las siguientes funciones debes tener declarada la librería `iostream` pues es ésta librería la que las abarca.

`cin`
<br>
Esta función trabaja junto con el operador de *extracción* que es `>>`, juntos se escribe como `cin>>`. Al decir extracción es porque se *extraen* datos de la entrada estándar de la computadora, es decir el teclado. Usándolo podemos dar un valor a una variable durante la ejecución de un programa, se usa así `cin >> variable;`. Es decir, al usarlo la computadora esperará a que introduzcas un valor con el teclado y ese valor se cargará a la variable especificada. Toma en cuenta que el valor que ingreses debe concordar con el tipo de variable, como lo especificamos antes.

También podemos hacer varias extracciones o lecturas con el mismo `cin`, usando varios operadores, es decir `cin >> a >> b;` pedirá primero el valor de `a` y luego el valor de `b`;

`cout`
<br>
Esta función trabaja junto con el operador de *inserción* es decir `<<`, juntos se vería así `cout<<`. Nota que estamos haciendo una inserción, pero ésta no es de nosotros a la computadora, sino al revés. Es decir, con esta función la computadora muestra en pantalla algo. Por ejemplo al declarar `cout << a;` donde `a` es una variable de cualquier tipo, estaremos mostrando en pantalla el valor de esa variable, no su nombre.

Si queremos mostrar un mensaje sólo tenemos que ponerlo entre comillas, así `cout << "Mensaje a mostrar";`. No olvides el `;` al final. Si queremos mostrar varias cosas en la misma salida, sólo hay que hacer varias inserciones. `cout << "Valor de la variable A " << A;` Nota que primero mostramos un mensaje y luego mostramos la variable, el nombre de la variable no va entre comillas. Nota también que antes de cerrar el mensaje puse un espacio extra, de no haber este espacio, el valor de `A` habría sido mostrado justo después de la letra 'A', que era la última del mensaje, es decir, *todo pegado*.

Por lo tanto si queremos mostrar varias variables en una misma salida, y para que sea fácilmente leída, debemos agregar espacios en blanco (como si fuera un mensaje) entre cada variable es decir `cout << a << " " << b;`. De no ponerlos los valores saldrían pegados.

Para mostrar un salto de línea podemos usar el carácter especial `\n`, que es interpretado como un salto de línea, cuando lo agregues no se mostrará ese texto, sino que solamente se mostrará un espacio. También podemos usar `endl` como si fuera una variable.

> `cout << "Este es un mensaje.\nFin.";` y `cout << "Este es un mensaje." << endl << "Fin.";`
> <br>
> Ambos mostrarán la siguiente salida y sin comillas:
> <br>
> "Este es un mensaje.<br>
> Fin."

Es más confiable usar `\n` además genera ejecuciones más rápidas.

<div class="Nav">
	<a href="{{ site.baseurl }}/C++/Introduccion/Funciones/" title="Funciones &vert; #iP Code">Tema anterior</a> | <a href="{{ site.baseurl }}/C++/Introduccion/Punteros/" title="Punteros &vert; #iP Code">Tema siguiente</a>
</div>