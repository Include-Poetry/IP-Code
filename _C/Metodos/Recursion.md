---
layout: G-Article
title: Recursión en C++
date: 2020-01-04 12:00:00
author: rivel_co
tags: [Recursión]
hide_tags: true
olimpiada: [OMI]
subject: [C++]
prevTopic: "Unión y pertenencia, /C++/Estructuras/Grafos/Union-y-pertenencia/"
nextTopic: "Ordenamientos, /C++/Metodos/Ordenamientos/"
---

En la actualidad, se podría decir que ningún gran programa está hecho sin algo de *recursión*. Y esto es porque la recursión como técnica de resolver problemas es tan útil que la utilizamos en la vida cotidiana sin siquiera darnos cuenta, comprender el funcionamiento de la recursión es un arma *invaluable* e *imprescindible* en la informática.

{: #ListaContenido}
- Idea de recursión
- Problema recursivo
- Razonando una solución
- Generando la llamada recursiva
- Condición de salida
- Recuento de los hechos
- Otros ejemplos prácticos y cortos
- Conclusión

## Idea de recursión

En esta sección se explicará la recursión específicamente aplicada en el lenguaje *C++*, pero es requisito *indispensable* conocer el concepto de recursión, el cual podemos resumir de la forma:

> La idea básica de la recursión es **aplicar un proceso a una cosa, y después, al resultado de eso volver a aplicar ese proceso otra vez** y seguir haciéndolo hasta lograr lo que buscamos.

Es muy, *muy* recomendable que asientes bien el concepto de recursión, y qué mejor que en la [sección especialmente dedicada para ello]({{ site.baseurl }}/Karel/Recursion/){: target="_blank"}. Una vez que ya lo tengas entendido completamente, puedes seguir aquí.

## Problema recursivo

Como ya sabemos, en la recursión necesitaremos una *llamada recursiva*, que será la que desencadenará todo. Para esto, necesitamos llamar a una función dentro de la misma función. Recuerda que no podemos hacerlo desde la función principal `main`. Por lo tanto declararemos una nueva función.

Ahora, el punto más importante, <span>¿Qué queremos hacer en la recursión?</span> Vamos a crear un programa que sume todos los números enteros del $$ 1 $$ al $$ n $$, donde $$ n $$ es un número que ingresa el usuario. Dicho lo anterior podemos tener un esqueleto del programa como sigue: 

<textarea class="cpp">
#include &lt;iostream&gt;
using namespace std;

int suma( void ){

}

int main(){
	int n;
	cin >> n;

	int resultado = 0;

	cout << resultado;

	return 0;
}</textarea>

Nota que por el momento la función `suma` no realiza nada. Al final devolverá un entero, porque esperamos que nos regrese el resultado de nuestra suma. Tampoco se ha hecho ninguna llamada a función por el momento.  Por el momento nuestra función tampoco tiene parámetros. <br>
Toma en cuenta que queremos resolver este problema usando *recursión*.

## Razonando una solución

Primero sinteticemos los datos que tenemos.<br>
**Objetivo general**: Sumar todos los números enteros $$ x $$ donde $$ 1 \le x \le n $$ y además $$ n $$ es un número proporcionado por el usuario.<br>
**Consideraciones especiales**: Uso forzoso de recursión <br>
Ahora consideremos cómo resolvemos el problema manualmente, usando un razonamiento muy sencillo:<br>
**Método**: Como debemos sumar una serie de números enteros consecutivos, comenzamos siempre en $$ 1 $$, y después podemos simplemente ir sumando $$ 1 $$ al número anterior sumado, generando la serie $$ 1, 2, 3, 4... $$<br>
**Condición para recursión**: Sabemos que vamos a estar agregando un número siempre a un resultado, y vamos a estar haciendo eso, siempre y cuando el número a sumar no sea mayor a $$ n $$<br>
**Fin de recursión**: Siguiendo el razonamiento anterior, una vez que el número a sumar sea igual que el número final, agregaremos $$ n $$ al resultado y terminaremos ahí.

Ahora tenemos que traducir nuestro procedimiento al lenguaje de programación en cuestión, es decir C++.<br>
Notemos que podemos estar tomando el número a sumar como un parámetro de la función que realizará la magia, y además, cada que estemos agregando un número tenemos que considerar el número final, por lo que también lo pasaremos como un parámetro. Lo anterior se vería como:

<textarea class="cpp">
#include &lt;iostream&gt;
using namespace std;

int suma(int actual, int final){

}

int main(){
	int n;
	cin >> n;

	int resultado = suma(1, n);

	cout << resultado;

	return 0;
}</textarea>

Nota que hacemos la llamada a `suma` desde `main`, pasando como parámetros el $$ 1 $$ que es el primer número a sumar, y también el número final, es decir $$ n $$.

## Generando la llamada recursiva

Para hacer la llamada recursiva, tomemos en cuenta que la función `suma` desde donde sea que sea citada, va a devolver un entero, por lo que podemos usar ese valor que está regresando a nuestro favor. También recordemos que el número que estamos agregando al total, es una unidad menor al siguiente, por lo que la próxima vez que llamemos a la función, (ya dentro de la recursión), debemos de sumarle $$ 1 $$ al número que recién se sumó. El número final debe mantenerse igual, pues el valor final es siempre el mismo.

<textarea class="cpp">
#include &lt;iostream&gt;
using namespace std;

int suma(int actual, int final){
	int siguiente;
	siguiente = actual + 1;
	
	suma(siguiente, final);
}

int main(){
	int n;
	cin >> n;

	int resultado = suma(1, n);

	cout << resultado;

	return 0;
}</textarea>

Nota que el programa anterior tiene un gran error, pues la función `suma` regresa un entero que no se está solicitando en ningún momento en la línea 8. Es aquí donde debemos ver qué hay que hacer o más bien, cómo aprovechar ese valor que se genera ahí.

Si tuviéramos $$ n = 2 $$ entonces sólo tendríamos que tomar nuestro $$ 1 $$, sumarle $$ 2 $$ y devolvemos el resultado. Ahora, si lo pensamos un poco más, cualquier suma de esta serie, se compone de sus sumas anteriores, es decir, si tenemos $$ 1 + 2 + 3 + 4 + 5 = 15 $$, podemos decir que es lo mismo que $$ (1 + 2 + 3 + 4) + 5 = 15 $$, es decir, la suma hasta $$ 5 $$ es igual a la suma hasta $$ 4 $$ más $$ 5 $$, a su vez, la suma hasta $$ 4 $$ es igual a la suma hasta $$ 3 $$ más el $$ 4 $$.

Por lo anterior, podemos ver, que el método que nos está generando el resultado de todas las respuestas, está en la línea 8. Siendo ahí donde generamos el resultado, es el valor que debemos regresar, sumado, claro, al número actual sumado, pues juntos irán generando la serie.

<textarea class="cpp">
#include &lt;iostream&gt;
using namespace std;

int suma(int actual, int final){
	int siguiente;
	siguiente = actual + 1;

	return actual + suma(siguiente, final);
}

int main(){
	int n;
	cin >> n;

	int resultado = suma(1, n);

	cout << resultado;

	return 0;
}</textarea>

Sin embargo, sucede una cosa, la primera vez que la ejecución toca la línea 8, y trata de regresar el resultado, va a tener que ejecutar otra vez la función `suma`. Y lo seguirá haciendo hasta el fin de los tiempos. Es aquí donde tenemos que crear la mágica *condición de salida*.

## Condición de salida

Ya lo habíamos dicho cuando sintetizamos la información, sabemos que terminamos cuando el próximo número a sumar sea $$ n $$, por lo tanto, mientras ese número actual, no sea $$ n $$, podemos seguir con la recursión, y si el número a sumar ya es igual al final, lo que nos faltaría por sumar, sería precisamente ese número final, por lo que sería el valor a devolver.

<textarea class="cpp">
#include &lt;iostream&gt;
using namespace std;

int suma(int actual, int final){
	int siguiente;
	siguiente = actual + 1;

	if (actual != final){
		return actual + suma(siguiente, final);
	} else {
		return final;
	}
}

int main(){
	int n;
	cin >> n;

	int resultado = suma(1, n);

	cout << resultado;

	return 0;
}</textarea>

De esta manera, en el momento en que `actual` sea igual a `final` no se hará otra llamada recursiva, sino que sólo se devolvería el valor final, que es el que faltaría por sumar. La pila de *llamadas* y de *valores devueltos* con una entrada de `5`, sería así:

<textarea class="output">
Llamadas:				| Valor de la función	| Valor total devuelto
4 + suma(5, 5)			| 5						| 9
3 + suma(4, 5)			| 9						| 12
2 + suma(3, 5)			| 12					| 14
1 + suma(2, 5)			| 14					| 15
suma(1, 5)				| 15					| 15</textarea>

Es decir, cuando en la línea 2 (de este cuadro) se hizo `4 + suma(5, 5)` el valor que terminó regresando la función `suma` en esa llamada, fue $$ 5 $$ que sumado al $$ 4 $$ daba el total de $$ 9 $$. Al final, la función llamada desde `main` regresó el $$ 15 $$ <br>
Analiza esa tabla anterior para que te quede muy claro qué fue lo que pasó.

## Recuento de los hechos

Lo que hicimos fue ir pasando una sucesión de números, como parámetros de la función recursiva, cada vez que se hacía una nueva llamada, se pasaba el parámetro aumentado en $$ 1 $$, para de esta manera cubrir el siguiente número de la sucesión. La función devolvía la suma de dos números, excepto por la última llamada recursiva, que sólo devolvería un número, el número final de la sucesión, de esta manera, al regresar en la recursión, ese número final se sumaría con su anterior, generando un nuevo resultado, que a su vez se sumaría con el número anterior, y así hasta llegar a la primera llamada recursiva, que sería la que se hizo desde `main`.

Por lo anterior, podría verse como que la suma se realizó desde el final y hasta el inicio, pues el primer número en ser agregado realmente al resultado fue el valor final, sumado con su anterior, y luego su anterior y así sucesivamente.

## Otros ejemplos prácticos y cortos

A continuación se agregan más ejemplos con los que puedas agudizar aún más tu sentido recursivo. Estos ejemplos no se explican tan a fondo como el anterior, sin embargo, lo esencial se explica en conjunto con los comentarios. Prueba a correrlos en tu IDE favorito hasta que entiendas completamente la naturaleza recursiva.

### Imprimir el abecedario al revés

Podemos imprimir el abecedario, apoyándonos el el código ASCII. Para imprimirlo al revés, podemos usar recursión, aprovechando la pila de llamadas, el hecho de que el primer elemento en entrar es el último en salir.

<textarea class="cpp">
#include &lt;iostream&gt;
using namespace std;

void Letras(char letra){			// Función recursiva
	if (letra <= 'z'){				// Todas las letras del código ASCII que estén entre el inicio y 'z' inclusive
		Letras(letra+1);			// Procedemos a formar en la pila de llamadas la siguiente letra
		// Con 'letra+1' avanzamos al siguiente caracter en el código ASCII
		cout << letra << " ";		// Se deja pendiente mostrar hasta que ya no se realicen más llamadas
		// La letra se muestra en el sentido inverso en el que ingresaron a la pila, por eso
		// comienza con la última letra, (la última en formarse) y termina con la primera en ingresar ('a')
	}
	return;		// Cundo ya no se cumpla la recursión, sólo regresamos para vaciar la pila de llamadas
}

int main(){
	char inicio = 'a';		// Letra inicial
	
	Letras(inicio);			// La primer letra en ingresar a la pila de llamadas es la 'a'
	
	return 0;
}</textarea>

<span>Prueba a utilizar la misma recursión pero mostrando el abecedario en el orden normal</span>.

### Máximo común divisor 

El máximo común divisor de dos números, es el número más grande que divide a ambos de forma entera. Para este ejemplo recursivo, se utiliza el ***algoritmo de Euclides***.

<textarea class="cpp">
#include &lt;iostream&gt;
using namespace std;

int mcd(int a, int b){			// Como parámetros los número actuales por procesar
	if (b == 0){				// El que será el residuo de la división en la llamada recursiva
		return a;				// En el caso de división exacta, se regresa el otro número
	} else {
		return mcd(b, a%b);		// Se aprovecha el hecho de que el MCD de dos números también divide 
								// al resto de obtenido de dividir al mayor entre el menor de los dos números
	}
}

int main(){
	int a, b;
	cin >> a >> b;		// Los dós números a obtener el mcd
	
	cout << mcd(max(a, b), min(a, b));		// El primer parámetro deberá ser el mayor de los dos por eso max( , )
											// E segundo parámetro deberá ser el menor de los dos por eso min( , )
	
	return 0;
}</textarea>

Usando el mismo principio, podemos obtener el máximo común divisor de tres números:

<textarea class="cpp">
#include &lt;iostream&gt;
using namespace std;

int mcd(int a, int b){			// Como parámetros los número actuales por procesar
	if (b == 0){				// El que será el residuo de la división en la llamada recursiva
		return a;				// En el caso de división exacta, se regresa el otro número
	} else {
		return mcd(b, a%b);		// Se aprovecha el hecho de que el MCD de dos números también divide 
								// al resto de obtenido de dividir al mayor entre el menor de los dos números
	}
}

int main(){
	int a, b, c;
	cin >> a >> b >> c;				// Los números a obtener el mcd
	
	cout << mcd( a, mcd(b, c) );	// Se considera que a > b > c
	// Primero se obtiene el mcd de los últimos dos
	// Al final se obtiene el mcd de el primero y el mcd anterior
	
	return 0;
}</textarea>

### Fibonacci

El clásico problema de Fibonacci desarrollado con recursión. Ya en la sección de [Problema resueltos]({{ site.baseurl }}/Problemas/Resueltos/C++/ "Ir a la sección"){: target="_blank"} se resolvía con iteración. Seguramente te resultará interesante comparar ambos procedimientos. De manera breve, describimos la serie de Fibonacci como:

> En la serie de Fibonacci un elemento es la suma de sus dos elementos anteriores 

Como ejemplo la serie empezaría como $$ 1, 1, 2, 3, 5, 8, 13 ... $$

<textarea class="cpp">
#include &lt;iostream&gt;
using namespace std;

int fibonacci(int a, int b, int n){ // Función recursiva, a y b son los elementos actuales, n es la cantidad por crear
	if (n){		// Equivalente a (n != 0)
		int c = a + b;		// Creamos el nuevo resultado en base a los dos actuales
		//cout << a << " + " << b << " = " << c << endl;	// Salida con las sumas desarrolladas
		cout << c << " ";	// Mostramos ese resultado
		return b + fibonacci(b, c, n-1);	// La nueva suma será resultado del segundo elemento más el resultado actual
	} else {
		return 1;	// Cuando terminemos con la cantidad de elementos, regresamos 1 
					// pues sería la cantidad a regresar por sólo el primer elemento de la serie
	}
}

int main(){
	int n;
	cin >> n;	// Cantidad de elementos de la serie a mostrar
	
	cout << fibonacci(1, 0, n-1);	// En esta llamada se devuelve el n-ésimo elemento de la serie
	// Se comienza con 1, 0 para poder tener como iniciales el 1 1
	// Se ingresan n-1 porque el último elemento lo muestra este último cout
	
	return 0;
}</textarea>

<span>Prueba a cambiar el valor del primer argumento en la llamada de la línea *20*, también prueba a ver las sumas desarrolladas con la salida de la línea *7* </span>.

## Conclusión

En la mayoría de las funciones recursivas de C++, las dos partes que juegan los papeles más importantes son el valor que devuelve la función y los parámetros con los que trabaja. Es el trabajo en conjunto, de estas dos partes las que hacen la magia.

Sin nunca dejar de lado, ni restarle importancia a la condición de quiebre de la recursión, pues de esto dependerá el resultado final, y también muchas veces, de que el programa no se cicle. Para esto también hay que estar cambiando los parámetros de la función, o la condición de quiebre, o ambas, y asegurarnos de que en algún momento la recursión terminará.