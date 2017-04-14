---
layout: G-Article
title: Funciones en C++
---

Es hora de abrir nuestro *IDE* favorito porque estamos a sólo un paso de comenzar a escribir nuestros propios programas. Sólo nos falta saber cómo comenzar. Una función es una parte del código que puede ser llamado desde cualquier parte del mismo, esta parte lleva un nombre específico y al invocarse se ejecuta la parte del código que abarca.

{: #ListaContenido}
- Declaración
- Llamada a funciones
- Función principal
- Orden de declaración

## Declaración

Una función tiene como objetivo *hacer algo* (<s>lógicamente</s>), ya sea realizar un procedimiento y terminar con su ejecución o al terminar su ejecución *devolver* algo a donde fue llamada. Es como por ejemplo, que alguien te mandara a la tienda a *saludar* a la persona que atiende. Una vez que lo has hecho regresas a tu casa y listo, no hay nada *que devolver*. Sin embargo, si te mandaran a *comprar* algo, cuando regresaras traerías contigo lo que compraste, es decir, al final de tu ejecución (comprar algo) tendrías un valor que devolver, en este caso lo que compraste.

Una función también puede llevar consigo un parámetro o valor que se le *manda* cuando es llamada. Si volvemos a nuestro ejemplo de ir a comprar algo, necesitarías para esa ejecución llevar un parámetro contigo, en este caso sería *dinero*, pues sin él no podrías realizar tu ejecución de ir a comprar. En el caso de sólo ir a saludar no necesitarías llevar algo contigo para realizar esa ejecución.

Si lo vemos de manera general, necesitas saber lo que devuelves (sea algo o nada), y lo que necesitas para realizar la ejecución (sea algo o nada). Para C/C++ además necesitarás un nombre para referirte a esa función, en nuestro ejemplo ficticio también le daremos nombre. Nota que lo que haces en cada ejemplo es distinto, por lo que son *funciones* distintas. Llamaremos a la función de ir a saludar como `TiendaSaludar` y a la función de comprar `TiendaComprar`. La declaración de éstas sería más o menos así:

<textarea class="output">
nada TiendaSaludar(nada){
	Ir-a-saludar;
}
algo TiendaComprar(algo){
	Ir-a-comprar;
}</textarea>

Empezamos hablando de *lo que devuelves* luego el *nombre* de la función, luego lo que *necesitas* y entre llaves lo que haces en cada función. Las mismas reglas que aplican para los nombres de variables aplican para los nombres de funciones. Las cosas que devuelves o necesitas son tipos de datos como los que ya vimos, pero esta vez agregaremos el tipo `void` que significa *vacío* o *nada*.

Si una función debe devolver algo, es importante que al final de su función lo devuelva, para esto usamos la expresión `return` seguido de lo que estamos regresando y finalizando con `;`.
<br>
Toma en cuenta que en algunos casos necesitaremos más de un parámetro para hacer la ejecución de una función, estos parámetros pueden ser de distintos tipos, y deberán declararse en el paréntesis como si fueran variables nuevas, y en el mismo orden con el que se *pasaron* desde el lugar de donde la función fue llamada. (<span>Si no te queda muy claro aún, espera a la explicación de las llamadas a función</span>). La declaración real de una función es algo así:

<textarea class="editor">
int funcion(void){
	char b;
	return 5;
}</textarea>

Nota que la función devuelve un entero, al final devolvió $$ 5 $$ que sí es un entero. También pudo haber regresado una variable, siempre y cuando sea del mismo tipo del valor que devolverá. Nota también que esta función no necesitó un parámetro para funcionar, es por eso que entre el paréntesis se puso `void`. La función lo único que hizo fue declarar una variable tipo carácter y después regresar $$ 5 $$.

<textarea class="editor">
void funcion(int a, int b){
	char letra;
	bool otra;
}</textarea>

Esta función no devuelve nada, y necesitó de dos parámetros, que aunque en el ejemplo no se utilizaron sí se muestra como deben de declararse. En esta función sólo se declararon dos variables, una tipo carácter y otra tipo booleana. No se usa `return` puesto que la función se supone que no devuelve nada.

Es importante que sepas que cuando una función llega a la instrucción `return` ésta termina. Si hay código después de esto, ya no se ejecutará.

## Llamada a funciones

Para llamar a una función debemos considerar dos cosas, *lo que devuelve* y *los parámetros que necesita*. Si por ejemplo se llama a una función que no devuelve nada, puede llamarse directamente por su nombre en cualquier parte del código. Si se llama a una función que devuelve un valor, ese valor deberá ser *cargado* a alguna parte, por ejemplo a una variable que sea del mismo tipo del valor que devuelve la función.

Cuando llamamos a una función que no necesita parámetros, podemos poner en su paréntesis `void` o dejarlo en blanco. Si necesita de algunos parámetros, dentro del paréntesis irán esos valores, en el mismo orden en el que deberán declararse en la función invocada.

<textarea class="editor">
int valor=FuncionGenial();</textarea>

En este ejemplo suponemos que la función `FuncionGenial` regresa un entero y no necesita de un parámetro;

<textarea class="editor">
OtraFuncion(5, 'T');</textarea>

En este ejemplo suponemos que la función no devuelve nada y necesita como parámetro dos valores, el primero tipo entero y el segundo tipo carácter.

## Función principal

Cuando compilamos un código fuente en C/C++, el compilador, una vez que haya comprobado que todo está bien escrito y que sabe como ejecutar cada parte del código, buscará la función principal, es por esta función por donde empezará a ejecutar el programa. Seguramente ya habrás notado que en este lenguaje de programación se utilizan muchas palabras del vocabulario inglés, por lo que no es de extrañarnos que la función principal se llame `main` pues su traducción inmediata al español es precisamente *principal*.

Es importante saber que no se supone que se llame a ella en alguna parte del programa, sólo es por donde el compilador inicia su ejecución. La función `main` siempre devuelve un entero y no necesita valores externos para funcionar. Su declaración sería así. (<span>Una vez que compiles el siguiente código habrás creado oficialmente tu primer programa, y no puede ser un genial primer-programa si no es: </span>)

<textarea class="editor">
#include &lt;iostream&gt;
using namespace std;

int main(void){
   cout << "Hola mundo";
   return 0;
}</textarea>

Nota que al final estamos cumpliendo con el hecho de que debe devolver un entero, lo más adecuado es que ese entero sea $$ 0 $$ pues ese valor es muy específico y al final de la ejecución le indicará al compilador que todo ha salido bien. En este caso sólo mostramos el famoso mensaje `Hola mundo` usando `cout`, por lo que también tuvimos que agregar la librería `iostream` y la línea `using namespace std;`. Dentro de una función puede haber cualquier procedimiento, incluyendo las llamadas a otras funciones. Todo programa que escribas debe tener la función `main`. Una vez que ya la tienes podemos compilar y ejecutar.

## Orden de declaración

El orden en el que declaramos las funciones es importante, pues no podemos llamar a una función si no la hemos declarado previamente. Imagina el siguiente ejemplo:

<textarea class="editor">
int main(void){
   int valor=FuncionSec();
   return 0;
}

int FuncionSec(void){
   int a=5;
   return a;
}</textarea>

En este caso no podríamos compilar ese programa, porque la función `FuncionSec` está declarada después de donde es llamada. Para solucionar esto podemos hacer una de dos cosas, la primera es declarar la función `FuncionSec` antes de `main`

<textarea class="editor">
int FuncionSec(void){
   int a=5;
   return a;
}

int main(void){
   int valor=FuncionSec();
   return 0;
}</textarea>

La otra forma es usando *funciones prototipo*. Para esto hacemos la declaración sólo de la parte superior de la función, es decir, lo que regresa, el nombre de la función y los parámetros que necesita, después de esto va `;`. De la siguiente manera.

<textarea class="editor">
int FuncionSec(void);

int main(void){
   int valor=FuncionSec();
   return 0;
}

int FuncionSec(void){
   int a=5;
   return a;
}</textarea>

Nota que de todas formas declaramos la función completa más adelante, pero declaramos el prototipo antes de donde se hace la llamada.

<span>¡Hey! ¡Oficialmente ya estás programando!</span>

<div class="Nav">
	<a href="{{ site.baseurl }}/C++/Introduccion/Variables/">Tema anterior</a> | <a href="{{ site.baseurl }}/C++/Introduccion/Operadores/">Tema siguiente</a>
</div>
