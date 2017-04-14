---
layout: G-Article
title: Punteros
---

¿Alguna vez has notado que si declaras una variable dentro de una función ésta no es accesible por otra función distinta a la de declaración? Ésta es una situación común que no debe presentar un mayor problema para el programador, pues afortunadamente existen elementos sencillos que nos permiten realizar este tipo de operaciones, esos elementos son los *punteros*.

{: #ListaContenido}
- Necesidad de los punteros
- Operador de dirección de memoria
- Operador de desreferencia
- Declaración de un puntero
- Resolución del problema inicial
- Punteros a punteros

## Necesidad de los punteros

Como se decía cuando se introdujeron los [tipos de variables]({{site.baseurl}}/C++/Introduccion/Variables/ "Volver allá"){: target="_blank"}, cuando declaramos una variable, el compilador ubica un espacio de memoria libre en donde podamos almacenar los valores de nuestra variable. Para poder recordar esa variable, la computadora debe recordar en qué espacio la guardó, ese espacio tiene una determinada dirección, llamada *dirección de memoria*, ese es el dato que la computadora recuerda, la dirección de memoria asociada con un nombre de una variable, cada que hacemos una modificación en esa variable, se realiza ese cambio en la dirección de memoria correspondiente a esa variable.

Nosotros casi no notamos la presencia de las direcciones, sin embargo son elementales. Cuando declaramos una variable en una función, sólo esa función conoce la dirección de memoria de esa variable, por lo que al querer citarla desde otra parte, esa variable resulta desconocida, por ejemplo el siguiente caso:

<textarea class="editor">
#include &lt;iostream&gt;
using namespace std;

void secundaria(void){
    cout << temp;
    return;
}

int main(){
    int temp = 10;
    
    secundaria();
    
    return 0;
}</textarea>

Al intentar compilar el código anterior recibirás un mensaje de error del compilador indicando que la variable `temp`no ha sido declarada en ese ámbito o contexto. Y en efecto, la función `secundaria` no conoce la variable `temp`. Claro, en base a nuestros conocimientos sobre [funciones]({{ site.baseurl }}/C++/Introduccion/Funciones/ "Volver allá"){: target="_blank"}, podemos intentar algo como:

<textarea class="editor">
#include &lt;iostream&gt;
using namespace std;

void secundaria(int x){
    cout << x;
    return;
}

int main(){
    int temp = 10;
    
    secundaria(temp);
    
    return 0;
}</textarea>

Y así imprimimos el valor de la variable `temp`, sin embargo, lo que hemos hecho aquí, es copiar el valor de `temp` a una nueva variable llamada `x` que sí conoce `secundaria`, pero esta función aún no conoce la variable `temp`. El problema se vuelve más evidente al querer hacer una reasignación a una variable desde una función distinta a la que fue creada, por ejemplo:

<textarea class="editor">
#include &lt;iostream&gt;
using namespace std;

void secundaria(int x){
    x = 5;
    return;
}

int main(){
    int temp = 10;
    secundaria(temp);
    cout << temp;
    
    return 0;
}</textarea>

El código anterior seguirá mostrando como salida el valor de `10`, pues no ha sido modificado, en la función `secundaria` se modificó el valor de la variable `x` que tenía el mismo valor de `temp`, mas no era `temp` en sí.

## Operador de dirección de memoria

Como se mencionaba antes, las variables tienen asociada una dirección de memoria única, esa dirección podemos verla nosotros utilizando el operador de dirección de memoria `&`. Si ya tenemos declarada una variable, podemos ver su dirección de memoria así:

<textarea class="editor">
#include &lt;iostream&gt;
using namespace std;

int main(){
    int x = 10;
    
    cout << &x;
    
    return 0;
}</textarea>

En la salida encontrarás un valor como `0x22fe9c`, no obtendrás exactamente ese valor, pues la variable que declares se ubicará en una dirección distinta en tu computadora, pero siempre comienzan con `0x`. Este valor no lo podemos modificar, pero podemos aprovechar su existencia para poder manipular variables de maneras distintas y útiles, como el caso del problema que se planteó al inicio.

## Operador de desreferencia

Como hemos visto, obtenemos la dirección de memoria de una variable utilizando el operador `&`, pero en el ejemplo anterior sólo lo hemos mostrado, lo útil es cuando hay una variable que pueda almacenar esa dirección de memoria, entonces es cuando utilizamos el operador de desreferencia `*`. Al utilizar este operador, podemos declarar una variable que almacene una determinada dirección de memoria, esta variable sería entonces un ***apuntador***.

Entonces, el operador de desreferencia `*` indica que la variable de la que se habla no manejará enteros ni caracteres ni ninguna otra cosa que no sea una dirección de memoria. De forma esquemática, podemos decir que:

- Una variable almacena un entero o un caracter o un valor booleano etc.
- Una dirección de memoria es el lugar en donde se aloja el valor de esa variable.
- El puntero almacena la dirección de memoria de otra variable como su propio valor.
- Un puntero también tiene su propia dirección de memoria en donde almacena su valor, que en su caso es otra dirección de memoria.

Por lo que sí, podemos decir que el el caso de un puntero, hay una dirección de memoria almacenado en una determinada dirección de memoria, mientras que en una variable que no sea apuntadora, hay almacenada un valor como un entero, en una determinada dirección de memoria.

> Al operador de desreferencia también se le suele llamar operador de indirección.

## Declaración de un puntero

Para declarar un puntero, tenemos que especificar el tipo de dato al que apuntará, además, debemos de usar el operador de desreferencia y luego declarar el nombre del puntero.

<textarea class="editor">
int *puntero;</textarea>

En el ejemplo anterior hemos declarado un puntero de enteros que se llama `puntero`. Recordemos que sólo almacenará direcciones de memoria, y sólo de variables tipo `int` en este ejemplo, en base a esto podemos hacer algo como:

<textarea class="editor">
#include &lt;iostream&gt;
using namespace std;

int main(){
    int x = 10;
    int *p;
    p = &x;
    
    cout << p;
    
    return 0;
}</textarea>

El ejecutar el código anterior obtendremos la dirección de memoria de la variable `x`. Nota que no habríamos podido compilar siquiera si no hubiéramos puesto el operador de desreferencia `*`.

Para mostrar la cosa a la que apunta `p`, debemos utilizar el operador de desreferencia:

<textarea class="editor">
#include &lt;iostream&gt;
using namespace std;

int main(){
    int x = 10;
    int *p;
    p = &x;
    
    cout << *p;
    
    return 0;
}</textarea>

La salida del código anterior es `10`, pues es la cosa a la que el apuntador apunta, en base a la dirección de memoria que almacena.

En base a lo anterior podemos modificar una variable utilizando el apuntador asociado:

<textarea class="editor">
#include &lt;iostream&gt;
using namespace std;

int main(){
    int x = 10;
    int *p;
    p = &x;
    
    *p = 5;
    
    cout << x;
    
    return 0;
}</textarea>

La salida del programa anterior es `5` pues hemos modificado la cosa a la que apunta `p`, no la dirección de memoria que almacena `p`.

> Para referirnos al valor (dirección de memoria) que almacena un puntero, no utilizamos el operador de desreferencia.

> Para referirnos al valor de la cosa a la que apunta el puntero, utilizamos el operador de desreferencia.

Y por supuesto, podemos seguir modificando nuestra variable *apuntada* como normalmente, y puedes estar seguro de que `*p` se irá *actualizando* siempre.

<textarea class="editor">
#include &lt;iostream&gt;
using namespace std;

int main(){
    int x = 10;
    int *p;
    
    p = &x;
    cout << *p << " ";
    
    *p = 5;
    cout << x << " ";
    
    x = 20;
    cout << *p;
    
    return 0;
}</textarea>

El código anterior dará como salida `10 5 20`.

## Resolución al problema inicial

Como seguramente ya te puedes imaginar, el problema inicial se resuelve fácilmente con punteros y de hecho, de dos formas distintas:

<textarea class="editor">
#include &lt;iostream&gt;
using namespace std;

void secundaria(int *x){
    *x = 20;
}

int main(){
    int temp = 10;
    
    secundaria(&temp);
    
    cout << temp;
    
    return 0;
}</textarea>

O también:

<textarea class="editor">
#include &lt;iostream&gt;
using namespace std;

void secundaria(int &x){
    x = 20;
}

int main(){
    int temp = 10;
    
    secundaria(temp);
    
    cout << temp;
    
    return 0;
}</textarea>

Donde el parámetro de la función `secundaria` ha sido declarado como una ***referencia*** de una variable previamente declarada. También es un movimiento válido.

## Punteros a punteros

Si podemos hacer punteros a cualquier tipo de variable, entonces también podemos hacer punteros a otros punteros. La forma de hacerlo es muy sencilla:

<textarea class="editor">
#include &lt;iostream&gt;
using namespace std;

int main(){
    int x = 1;
    int *p = &x;
    int **pp = &p;
    
    cout << &x << " "
         << p << " "
         << &p << " "
         << pp << " "
         << &pp;
    
    return 0;
}</textarea>

El código anterior mostrará algo como `0x22fe9c 0x22fe9c 0x22fe98 0x22fe98 0x22fe94`, es decir, dos direcciones de memoria iguales, seguidas de otras dos direcciones de memoria iguales y al final, una diferente a todas. Analiza el código anterior hasta que tengas bien claro el porqué de la salida.

> En punteros que apuntan a punteros, se pone un asterisco por cada *nivel*. Por lo que un apuntador a un apuntador será `int **p` y un apuntador a ese apuntador será `int ***p`

<div class="Nav">
    <a href="{{ site.baseurl }}/C++/Introduccion/Operadores/">Tema anterior</a> | <a href="{{ site.baseurl }}/C++/Introduccion/Sentencias/">Tema siguiente</a>
</div>