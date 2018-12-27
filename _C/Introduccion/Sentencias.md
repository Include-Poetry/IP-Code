---
layout: G-Article
title: Sentencias en C++
author: rivel_co
tags: [Ciclos, Condicionales]
Hide_Tags: true
olimpiada: [OMI]
subject: [C++]
---

Las sentencias nos permiten modificar la manera en que el código se ejecuta, además de que nos facilitan la resolución de muchos problemas, haciéndolos más sencillos de resolver al tener herramientas más eficaces para prever más situaciones y casos de problemas. Su uso es muy sencillo y tiene además muchos usos.

{: #ListaContenido}
- Comentarios
- Selección - if y else
- Selección - switch
- Cíclica - while
- Cíclica - do while
- Cíclica - for
- Sentencias de salto

## Comentarios

Los comentarios nos permiten agregar mensajes en el código que el compilador ignorará, siendo que el mensaje escrito, es decir, el *comentario* está hecho para darnos referencias y retro alimentaciones a nosotros como programadores y desarrolladores del programa. En un código de *C++* tenemos dos tipos de comentario.

**Comentarios en línea**
<br>
Para agregar un comentario en línea debemos agregar dos *slash* seguidos, uno detrás del otro `//` lo que está a la derecha de este símbolo será ignorado por el compilador.

<textarea class="cpp">
#include &lt;iostream&gt;
using namespace std;

int main(){
   cout << "Hola mundo, desde #iP";//Mensaje de #iP
   return 0;
}</textarea>

Nota que la instrucción `cout` y `return` sí serán tomadas en cuenta por el compilador, sin embargo el comentario que agregamos no se considerará, aunque lo podremos ver en el editor. Estos comentarios se llaman así porque marcan como comentario toda la línea en que se encuentran, pero sólo después del `//`

**Comentarios de varias líneas**
<br>
Si queremos hacer un comentario más extenso, que ocupe varias líneas del código, podemos agregar varios comentarios en línea, por ejemplo:

<textarea class="cpp">
#include &lt;iostream&gt;
using namespace std;

int main(){
   //Este es un primer programa
   //donde mostramos el mensaje de "Hola mundo"
   //pero desde #iP
   cout << "Hola mundo, desde #iP";//Mensaje de #iP
   return 0;
}</textarea>

Sin embargo, puede resultar tedioso poner muchos `//` si vamos a comentar una parte muy grande del programa, y para esto tenemos los comentarios *de varias líneas* que marcarán como tal a todo lo que esté entre `/*` y `*/`. El mensaje anterior escrito con estos comentarios sería así:

<textarea class="cpp">
#include &lt;iostream&gt;
using namespace std;

int main(){
   /*Este es un primer programa
   donde mostramos el mensaje de "Hola mundo"
   pero desde #iP*/
   cout << "Hola mundo, desde #iP";
   return 0;
}</textarea>

Como recordarás, *la práctica y la organización hacen al maestro*, mantener nuestros códigos ordenados es muy importante, tanto como lo es agregar comentarios, puedes usarlos para especificar qué estabas haciendo en las líneas difíciles, cómo lograste descifrar el problema, qué método implementaste o qué problema estabas realizando. Todo lo que puedas necesitar para que si un día vuelves a ver un viejo código tuyo, recuerdes cómo lo hiciste.

<textarea class="cpp">
// Problema de "Hola mundo"
// Realizado por #iP
#include &lt;iostream&gt;
using namespace std;

int main(){
   cout << "Hola mundo, desde #iP";
   return 0;
}</textarea>

## Selección - if y else

demos traducir esta sentencia literalmente como un "*si*" condicional. Esta sentencia evalúa algo que regrese un valor booleano, si ese valor es verdadero entonces ejecuta sus acciones. Su sintaxis general es así:

<textarea class="output">
if ( valor_boolano ) { acciones; }</textarea>

Donde `if` es una palabra de control, indica al compilador que sigue una evaluación.
<br>
Un `valor_booleano` puede ser cualquier cosa que regrese un verdadero o falso, como una *comparación*, una *variable booleana* o una *función booleana*.
<br>
Las `acciones` son cualquier instrucción que queramos realizar.
<br>
Un ejemplo completo sería:

<textarea class="cpp">
// Sentencia if
#include &lt;iostream&gt;
using namespace std;

int main(){
   int T = 14;
   if ( T > 3 ){
      cout << "T es mayor que tres\n";
   }
   bool A = false;
   if ( A ){
      cout << "A es verdadera";
   }
   return 0;
}</textarea>

En el ejemplo anterior la sentencia de la línea 7 realizará la acción entre sus llaves, debido a que la variable `T` en efecto es mayor que $$ 3 $$. La sentencia de la línea 11 no realizará sus acciones pues la variable `A` tiene como valor `false`.
<br>
También puede evaluar con los operadores de conjunción y disyunción, `&&` y `||`

<textarea class="cpp">
// Sentencia if y operadores && y ||
#include &lt;iostream&gt;
using namespace std;

int main(){
   int N = 32, I;
   if ( N == 23 || N > 21 ){
      N += 18;
   }
   I = N;
   if ( N > 40 && N < 60 ){
      I = 10;
   }
   cout << N << " " << I;
   return 0;
}</textarea>

Al final de la ejecución del anterior programa nuestras variables quedarán así `N = 50` e `I = 10`. <span>Prueba a ejecutarlo en tu *IDE* favorito</span>.

La sentencia `if` puede ser utilizada agregando un `else` al final de su bloque. Las acciones del bloque de éste último serán ejecutadas si el valor booleano evaluado *no* es verdadero. De hecho, la traducción inmediata de `else` es *sino*.

<textarea class="cpp">
// Sentencia if con else
#include &lt;iostream&gt;
using namespace std;

int main(){
   int A = 12;
   if ( A > 13 ){
      cout << "La variable A es mayor a 13";
   }
   else{
      cout << "La variable A no es mayor a 13";
   }
   return 0;
}</textarea>

En este caso como `A` no es mayor $$ 13 $$ sólo se mostrará el mensaje `La variable A no es mayor a 13`. De haber sido mayor ese mensaje nunca se habría mostrado, sólo se habría mostrado el mensaje de la línea 8.

## Selección - switch

A diferencia de `if` esta sentencia no trabaja directamente con un valor *booleano* sino que trabaja con uno de los valores que conformarían a ese valor. Seguramente esto no ha quedado muy claro, así que vamos a revisarlo por partes. Lo primero es su estructura.

<textarea class="cpp">
// Estructura de switch
switch ( x ){
   case y:
      // Acciones
      break;
   case z:
      // Acciones
      break;
   default:
      // Acciones
      break;
}</textarea>

`x` debe ser una variable tipo `int` o `char`, no de otro tipo.
<br>
`y` `z` sólo pueden ser un *número entero* o *un carácter*. No una variable.
<br>
En la parte de acciones, es decir, entre cada `case` y `break` irán las acciones a realizar de ese *caso*. Nota que después de el valor del caso van dos punto `:` y después de `break` va el punto y coma `;`

El funcionamiento de `switch` es muy sencillo, si el valor que está en el paréntesis (en el ejemplo representado por `x`) es igual al valor de alguno de los casos (en el ejemplo representados por `y` y `z`) entonces se ejecutan las instrucciones de ese caso. Si ningún caso es igual a el valor del paréntesis, entonces se ejecutan los comandos de la sección `default`.

Pueden haber tantos casos como gustes, y dentro de cada caso pueden haber las acciones que tú decidas. Un ejemplo real sería:

<textarea class="cpp">
// Uso switch
#include &lt;iostream&gt;
using namespace std;

int main(){
   int T = 46;
   char A = 'N';
   switch ( T ){
      case 34:
         cout << "T vale 34";
         break;
      case 45:
         cout << "T vale 45";
         break;
      case 98:
         cout << "T vale 98";
         break;
      default:
         cout << "T vale " << T;
         break;
   }
   cout << "\n";
   switch ( A ){
      case 'T':
         cout << "A tiene la letra 'T'";
         break;
      case 'N':
         cout << "A tiene la letra 'N'";
         break;
      case 'a':
         cout << "A tiene la letra 'a'";
         break;
      default:
         cout << "A tiene la letra " << A;
         break;
   }
   return 0;
}</textarea>

Ejecuta el anterior código y pon mucha atención a la salida que produce y el por qué produce esa salida. Prueba y cambia los valores de las variables y los casos.

## Cíclica - while

Imagina que queremos imprimir (mostrar en pantalla) los números del $$ 0 $$ hasta cierto número que indique el usuario. Es decir, que debemos leer un número del teclado y luego mostrar en pantalla una sucesión del $$ 0 $$ hasta ese número. Si supiéramos de antemano cuál será el valor de ese número, podríamos poner la sucesión manualmente en un `cout`, aunque sería algo aburrido y tardado de hacer, más si el número *meta* es un número grande, como $$ 100 $$. Es aquí donde podemos usar una sentencia *cíclica*.

La sentencia `while` repite las acciones que abarca y en el mismo orden, mientras el valor booleano que evalúa sea verdadero. Su estructura es la siguiente.

<textarea class="cpp">
// Estructura de while
while ( valor_booleano ){
   // Acciones a repetir
}</textarea>

Recuerda que por `valor_booleano` debemos entender cualquier expresión que nos devuelva un valor `true` o `false`, como puede ser una *comparación* o una *variable o función booleana*. También podemos usar operadores de *conjunción* y *disyunción*. Ahora, imagina el siguiente ejemplo:

<textarea class="cpp">
// Uso de while
#include &lt;iostream&gt;
using namespace std;

int main(){
   int T = 10;
   while ( T > 0 ){
      cout << "Hola\n";
   }
   return 0;
}</textarea>

¿Cuántas veces se mostrará el mensaje "*hola*"? No es necesario pensarlo muchas veces si nos damos cuenta de que la variable `T` siempre va a ser mayor a $$ 0 $$, esto haría que el programa nunca terminara, pues se quedaría *ciclado*, es decir, la ejecución estaría en un ciclo interminable. Aquí está el factor principal que debemos tener en cuenta al utilizar una estructura cíclica, el asegurarnos de que *termine en algún momento*. En el ejemplo anterior para que ese ciclo termine la variable `T` tiene que cambiar. Podemos hacer lo siguiente:

<textarea class="cpp">
// Uso de while
#include &lt;iostream&gt;
using namespace std;

int main(){
   int T = 10;
   while ( T > 0 ){
      cout << "Hola\n";
      T--;
   }
   return 0;
}</textarea>

De esta manera, la ejecución sería algo así:<br>
Se declara la variable `T` con valor de $$ 10 $$.<br>
Al llegar al `while` se checa la condición que contiene. Como `T` es mayor a cero entonces se *entra* al ciclo.<br>
Se muestra el mensaje "*Hola*" y se da un salto de línea.<br>
Ahora se le resta $$ 1 $$ a la variable `T`, dejándola con valor de $$ 9 $$.<br>
Como ya se terminó de ejecutar el bloque de `while`, se vuelve a checar la condición, como `T = 9` aún es más grande de $$ 0 $$ y por lo tanto se vuelve a ejecutar el *ciclo*.

¿Cuántas veces se mostrará el mensaje "*hola*"? ¿Por qué pasa así? Prueba ahora con este código:

<textarea class="cpp">
// Uso de while
#include &lt;iostream&gt;
using namespace std;

int main(){
   int T = 10;
   while ( T > 0 ){
      cout << T-- << " ";
   }
   cout << "\n";
   int A = 10;
   return 0;
   while ( A > 10 ){
      cout << --A << " ";
   }
   return 0;
}</textarea>

¿Recuerdas la diferencia entre `T--;` y `--T;`?

## Cíclica - do while

En base al siguiente segmento de código:

<textarea class="cpp">
int T = 5;
while ( T > 10 ){
   cout << "Mensaje\n";
   T++;
}</textarea>

¿Cuántas veces se mostrará la palabra "*Mensaje*"? En efecto, no se mostrará ninguna vez, pues `T` no fue mayor de $$ 10 $$ al llegar al `while`. Si hubiéramos querido que primero se ejecutara lo que hay en las líneas 3 y 4 hubiéramos tenido que usar la estructura `do{} while()` justo así:

<textarea class="cpp">
// Estructura do while
int T = 5;
do {
   cout << "Mensaje\n";
   T++;
} while( T > 10 );</textarea>

Nota que primero ponemos la palabra reservada `do`, luego entre llaves lo que queremos realizar en el ciclo, y después de esas llaves la palabra reservada `while` seguido y entre paréntesis de su valor booleano de control, que en este ejemplo fue una comparación.
<br>
Nota también que `T` no fue mayor a 10 en ningún momento, sin embargo las instrucciones se realizaron una vez porque nosotros así lo indicamos, al poner que primero *ejecutara* (`do`) y luego checara si volvería a hacerlo (`while`).

## Cíclica - for

La última sentencia cíclica (<s>y mi favorita</s>) es la estructura `for`. Ésta es un poco diferente a las dos anteriores, su estructura es así:

<textarea class="cpp">
// Estructura for
for ( b1; b2; b3 ){
   // Acciones a repetir
}</textarea>

<span>Es importante que sepas que al poner <code>b1</code>, <code>b2</code> y <code>b3</code>, no se hace referencia a una variable en sí, sólo es para referencia en la explicación</span><br>
Primero tenemos que poner la palabra reservada `for`, indica que sigue ese ciclo.<br>
En donde está *b1* irá la (o las) variable de control, típicamente es un entero. <br>
En donde está *b2* irá el valor booleano de control del ciclo.<br>
En donde está *b3* irá la (o las) modificaciones a la (o las) variables de control.<br>
Para que quede bien claro, un ejemplo completo es:

<textarea class="cpp">
// Estructura for
for ( int T=0; T < 10; T++ ){
   cout << T << " ";
}</textarea>

Nota que nuestra variable de control se declaró ahí adentro, puedes declararla ahí o si ya la tienes declarada antes no hay ningún problema. Lo que sí es muy importante es que tiene que estar ya inicializada.<br>
El valor booleano de control en este ejemplo es una condición, que nos dice que mientras `T` sea menor que $$ 10 $$ se realizarán las instrucciones que están en esas llaves.<br>
La modificación que le estamos haciendo a `T` es sumarle $$ 1 $$. Esta adición se realizará cada vez que se repita el ciclo.

La ejecución anterior sería: <br>
Se llega a `for` y se declara la variable `T` inicializada en $$ 0 $$.<br>
Como `T` es menor a $$ 10 $$, el valor booleano de control toma valor de verdadero y el ciclo empieza.<br>
Se muestra el valor de `T` seguido por un espacio en blanco. El valor mostrado es $$ 0 $$.<br>
Se termina el bloque de `for` por lo que se regresa a la línea 2 y se modifica el valor de `T` al sumarle $$ 1 $$. Ahora esta variable vale $$ 1 $$.<br>
Se compara de nuevo `T < 10`, y una vez más el valor es verdadero, por lo que se vuelve a repetir el ciclo.

Es útil saber que en un momento dado se puede prescindir de siquiera escribir lo que va en el bloque de *b1*, (aunque sí tenemos que poner el punto y coma), por ejemplo si declaré e inicialicé antes la variable de control.<br>
También podemos no poner nada en el bloque de *b3*, por ejemplo si vamos a modificar la variable de control en alguna parte dentro del ciclo.<br>
También podemos no utilizar la variable de control en el bloque de *b2*, pero siempre siempre debe haber algo ahí que devuelva un valor booleano.<br>
Debido a esto podemos escribir un programa como este:

<textarea class="cpp">
// Estructura for
#include &lt;iostream&gt;
using namespace std;

int main(){
   int T = 3;
   for (; T < 10; T++){
      cout << T << " ";
   }
   cout << "\n";
   int a = 10;
   for (; a < 15;){
      cout << T << " ";
      a+=2;
   }
   cout << "\n";
   bool S = true;
   T = 0;
   for (; S ;){
      cout << T << " ";
      T++;
      S = T < 10;
   }
   return 0;
}</textarea>

Analiza la ejecución de el código anterior. ¿Por qué en un momento se muestra en una línea `10 10 10`?

> A las repeticiones que se realizan en un ciclo les llamamos **iteraciones**, que viene de la palabra [iterar](http://dle.rae.es/?id=ME7n9y2){: target="_blank"}

## Sentencias de salto

Las sentencias de salto nos permiten modificar la forma en la que se ejecuta una estructura.

`break`<br>
Esta sentencia hace que al momento de que la ejecución pasa por ella, se *salga* de la sentencia cíclica en la que está metida sin importar el valor booleano de control. Por ejemplo:

<textarea class="cpp">
// Sentencia break
#include &lt;iostream&gt;
using namespace std;

int main(){
   int A = 0;
   while ( A < 10 ){
      cout << "Algo\n";
      if ( A == 3 ){
         break;
      }
      A++;
   }
   return 0;
}</textarea>

En este caso sólo se mostrará $$ 4 $$ veces la palabra *Algo*, y eso será cuando `A` tenía los valores $$ 0, 1, 2, 3 $$ pues cuando vale $$ 3 $$ mostrará ese valor, para luego hacer que se cumpla la condición de la línea 9, esto ocasionará que se ejecute el `break` de la línea 10 y que por lo tanto, se salga del ciclo.<br>
Seguramente también recuerdas que encontramos `break` anteriormente en la estructura `switch` ¿Notas su funcionamiento ahí también? Aunque `switch` no es una estructura cíclica puede verse afectada por `break`.

`continue`<br>
Esta sentencia se *brinca* una iteración, justo la iteración en la que se aplicó esta sentencia. No se sale del ciclo completo, sino que sólo no hace una repetición.

<textarea class="cpp">
// Sentencia continue
#include &lt;iostream&gt;
using namespace std;

int main(){
   for (int T=1; T <= 10; T++){
      if ( T == 4 ){
         continue;
      }
      cout << T << " ";
   }
   return 0;
}</textarea>

En este ejemplo se estaría mostrando el valor de `T`, pero cuando su valor sea $$ 4 $$, es decir, cuando la condición del `if` de la línea 7 se cumpla, se *saltará* lo que había después y se seguirá con el resto de las iteraciones. En este caso este programa mostraría la salida `1 2 3 5 6 7 8 9 10 `.

`goto`<br>
Esta para el funcionamiento de esta sentencia, necesitamos declarar previamente una *etiqueta*. Esta etiqueta se compone de un nombre válido seguido de dos puntos, va ubicada en cualquier parte del código. Una etiqueta no lleva un *tipo* que la preceda, sólo es el nombre válido y dos puntos. Al momento de que la ejecución pase por la sentencia `goto` se redirigirá hacia la línea donde está esa etiqueta y se seguirá desde ahí.

<textarea class="cpp">
// Sentencia goto
#include &lt;iostream&gt;
using namespace std;

int main(){
   int T = 0;
 goto MiEtiqueta;
   cout << "Hola ";
   char letra;
 MiEtiqueta:
   cout << "Otro mensaje ";
 OtraEtiqueta:
   cout << T++ << " ";
   if ( T < 10 ){
      goto OtraEtiqueta;
   }
   return 0;
}</textarea>

El anterior programa mostraría la salida `Otro mensaje 0 1 2 3 4 5 6 7 8 9 `. El mensaje de la línea 8 no se mostraría, sin embargo la variable `letra` sí se declaró. No se puede inicializar en una parte del código que sea saltado por un `goto`, de hacerse una inicialización será ignorada.

<textarea class="cpp">
// Sentencia goto
#include &lt;iostream&gt;
using namespace std;

int main(){
   int T = 0;
 goto MiEtiqueta;
   cout << "Hola ";
   T = 5;
   char letra;
 MiEtiqueta:
   cout << "Otro mensaje ";
 OtraEtiqueta:
   cout << T++ << " ";
   if ( T < 10 ){
      goto OtraEtiqueta;
   }
   letra = 'L';
   cout << letra;
   return 0;
}</textarea>

La salida al final será `Otro mensaje 0 1 2 3 4 5 6 7 8 9 L`.

<div class="Nav">
   <a href="{{ site.baseurl }}/C++/Introduccion/Punteros/">Tema anterior</a> | <a href="{{ site.baseurl }}/C++/Estructuras/Arreglos/">Tema siguiente</a>
</div>