---
layout: G-Article
title: Operaciones con bits
author: rivel_co
tags: [Máscara de bits, Algoritmo, Variables]
Hide_Tags: true
olimpiada: [OMI]
subject: [C++]
---

Podemos aprovechar las características binarias de las variables que declaramos en C++, cada variable es almacenada en la computadora en su forma binaria, no decimal. Si cada valor es almacenado en esta forma entonces podemos aprovechar diversas propiedades que hacen todo mucho más sencillo.

{: #ListaContenido}
- Números binarios
- Operaciones bit a bit
- Operaciones más comunes
- Trucos útiles con bits
- Conclusión

## Números binarios

Como ya se decía, cada valor que almacenamos en cada variable es registrada en la computadora en su forma binaria. Si nosotros hacemos una asignación como `int x=5;` entonces estaríamos pensando en $$ x = 5_{10} $$, pero la computadora estaría guardando algo como $$ x = 101_2 $$. Para entender cómo funciona esto tenemos que entender cómo funciona el sistema binario.

>Nota que estamos marcando la diferencia entre una representación en binario o decimal utilizando un subíndice a la derecha de cada número, un subíndice $$x_2$$ nos dice que el número es binario, un subíndice $$x_{10}$$ nos dice que es decimal.

El sistema que nosotros como humanos más utilizamos es el sistema decimal, contamos utilizando hasta $$10$$ dígitos, que son en orden ascendente $$0, 1, 2, 3, 4, 5, 6, 7, 8, 9$$. Cuando queremos expresar un número mayor a todos estos dígitos entonces tenemos que utilizar un dígito más al mismo tiempo que "reseteamos" el dígito actual, es decir, cuando estamos contando desde el $$0$$ y llegamos a $$9$$ y queremos continuar, es necesario aumentar en uno el dígito de la izquierda (que al inicio es $$0$$) y volver a convertir el dígito actual (el $$9$$) en un $$0$$ y luego continuamos.

En binario o base dos, es más o menos lo mismo. Como su nombre lo dice, el sistema únicamente tiene $$2$$ dígitos disponibles, $$0, 1$$. En programación lo más conveniente es recordar ese valor de $$0$$ y $$1$$ como un *bit* apagado o encendido respectivamente. Cada bit o dígito del número binario representa la potencia de $$2$$ según la posición en la que esté. Lo podemos ver en el siguiente esquema:

<textarea class="plain-text">potencia | 5 | 4 | 3 | 2 | 1 | 0 |  
dígitos  | 0 | 0 | 0 | 1 | 0 | 1 | == 101 binario == 5 decimal</textarea>

El $$1$$ que está debajo del $$2$$ representa que al número decimal equivalente se le está sumando un $$2^2$$. Luego también hay un $$1$$ debajo del $$0$$ de la fila de las potencias, esto nos dice que al equivalente decimal se le está agregando un $$2^0$$, por lo tanto al final tendríamos que $$101_2 = 2^2 + 2^0 = 5_{10}$$. Para representar el $$13_{10}$$ en binario tendríamos que escribir $$1101_2$$.

> Recuerda muy bien lo que decía más arriba sobre considerar un $$1$$ como un *bit* encendido y un $$0$$ como uno apagado.

Si entonces utilizamos cada bit de un número para representar la ausencia o presencia de una potencia de $$2$$ o para indicar si un *bit* está encendido o apagado, podemos representar *a lo más* $$32$$ **bits** diferentes en un entero de $$32$$ bits, claro. Podemos representar hasta $$64$$ si utilizamos una variable de ese tamaño.

Es importante también familiarizarse con algunos términos. Consideramos como primer bit, al bit menos significativo (*LSB* por sus siglas en inglés) o bit en la posición $$0$$ al bit que corresponde a la potencia $$0$$ del $$2$$, es decir, cuando únicamente este bit está encendido en una variable, el valor de esa variable es $$1$$. El bit más significativo (*MSB* por sus siglas en inglés) o el último bit, será el bit que está encendido y que corresponde a la potencia más grande del $$2$$ en esa variable.

## Operaciones bit a bit

Para poder manipular una variable en su forma binaria necesitaremos usar operadores especiales que siguen una lógica particular. Primero revisaremos cómo modificar una variable en su formato binario y luego veremos de qué nos sirve hacer este tipo de operaciones.

### Operador AND

Este operador se escribe en C++ como `&`. Cuando realizamos una operación `c = a & b` lo que estaremos haciendo es mantener en `c` los bits que están encendidos **tanto en `a` como en `b`**. El siguiente código produce como salida un `1`.

<textarea class="cpp">int a = 5, b = 3, c;
c = a & b;
cout << c;
/*   a = 101
     b = 011
    ---------
     c = 001    */</textarea>

### Operador OR

Este operador se escribe en C++ como `|`. Cuando realizamos una operación `c = a | b` lo que sucede es que se mantienen en `c` los bits que estén encendidos **en `a` o en `b`**. El siguiente ejemplo daría una salida igual a `7`.

<textarea class="cpp">int a = 5, b = 3, c;
c = a | b;
cout << c;
/*   a = 101
     b = 011
    ---------
     c = 111    */</textarea>

### Operador XOR

Este operador se representa como `^` y también es llamado *OR exclusivo*. Funciona evaluando también dos valores, si aplicamos algo como `c = a ^ b` entonces conservará en `c` todos los bits que estén **encendidos en uno y sólo uno** de los valores (`a` o `b`). Es decir, si un bit está encendido en `a` pero no en `b` entonces ese bit se enciende en `c`. Si un bit está encendido tanto en `a` como en `b` entonces no se enciende en `c`. Si un bit no está encendido ni en `a` ni en `b` entonces tampoco se enciende en `c`. El siguiente ejemplo da como resultado `6`.

<textarea class="cpp">int a = 5, b = 3, c;
c = a ^ b;
cout << c;
/*   a = 101
     b = 011
    ---------
     c = 110    */</textarea>

### Operador NOT

Este operador se representa en C++ como `~`. Lo que realiza es muy sencillo, invierte el estado de los bits. Todos los bits que estén encendidos los apaga y todos los que estén apagados los enciende. Si tenemos una variable de $$4$$ bits en la que está almacenado un $$5_{10} = 101_2$$ y aplicamos un `~` entonces tendremos como nuevo resultado un $$ 2_{10} = 010_2 $$. El siguiente ejemplo produce como salida un `4294967294`.

<textarea class="cpp">unsigned int a = 1;
c = ~a;
cout << c;
/*   a = 00000000000000000000000000000001
     ~ = 11111111111111111111111111111110   */</textarea>

Recuerda que en un entero no signado de $$32$$ bits se puede almacenar hasta $$2^{32}-1$$. Si apagamos un bit (el que está encendido en `a`) y encendemos todos los demás entonces obtendremos ese $$2^{32} - 2 = 4294967294$$.

### Operador de corrimiento a la izquierda

Un operador de corrimiento "desplaza" todos los bits hacia un lado una cantidad determinada de posiciones, ya sea la izquierda o la derecha. Para hacerlo hacia la izquierda se utiliza en C++ un `<<`. Por ejemplo, si tenemos un número $$010101101_2$$ después de aplicar un corrimiento a la izquierda de $$2$$ lugares tendremos algo como $$01010110100_2$$. El siguiente ejemplo tiene como salida un $$1176_{10}$$.

<textarea class="cpp">int a = 147, b = 3, c;
c = a << b;
cout << c;
/*   a =    10010011
  << 3 = 10010011000   */</textarea>

### Operador de corrimiento a la derecha

Para desplazar los bits a la derecha en C++ se utiliza `>>`. Funciona del mismo modo que el corrimiento a la izquierda, pero en este caso el valor resultante siempre decrece pues estamos quitando bits. Si tenemos el número $$010101101_2$$ y aplicamos un corrimiento de $$3$$ lugares a la derecha entonces vamos a obtener $$000010101_2$$. El siguiente código produce una salida de `18`.
<textarea class="cpp">int a = 147, b = 3, c;
c = a >> b;
cout << c;
/*   a = 10010011
  >> 3 =    10010   */</textarea>

## Operaciones más comunes

### Encender un bit en una posición

Si queremos encender un bit (hacerlo $$1$$) en alguna posición podemos aplicar un corrimiento a la izquierda de un $$1$$ seguido por una operación OR. Por ejemplo, si queremos encender el bit $$x$$ de un número $$a$$ podemos hacer algo como sigue:

<textarea class="cpp">a = a | (1 << x); // Encendemos el bit x de a</textarea>

### Apagar un bit  en una posición

Si queremos apagar un bit (hacerlo $$0$$) en alguna posición podemos aplicar un corrimiento de un $$1$$ seguido por una operación NOT y una AND. Por ejemplo, si queremos apagar el bit $$x$$ de un número $$a$$ podemos hacer:

<textarea class="cpp">a = a & ~(1 << x); // Apagamos el bit x de a</textarea>

### Invertir un bit

También podemos invertir el valor de un bit, apagarlo si está encendido y encenderlo si está apagado. Esto se logra haciendo una operación XOR al corrimiento de un $$1$$. Si queremos invertir el bit $$x$$ de un número $$a$$ lo hacemos así:

<textarea class="cpp">a = a ^ (1 << x); // Invertimos el bit x de a</textarea>

### Revisar si un bit está encendido

Podemos saber si un bit $$x$$ está encendido en una variable $$a$$ aplicando un corrimiento de un $$1$$ seguido de una operación AND. Por ejemplo:

<textarea class="cpp">if (a & (1 << x)) // Si esto se cumple entonces el bit es 1</textarea>

## Trucos útiles con bits

### Alternar letras mayúsculas y minúsculas

Se puede pasar de una letra en mayúscula almacenada en una variable tipo `char` a una letra en minúscula utilizando operaciones bit a bit. Si vemos la representación en binario de la 'A' notaremos que es $$01000001_2$$, la de 'a' es $$01100001_2$$. En el caso de la 'B' en binario es $$01000010_2$$, la 'b' es $$01100010_2$$. Si somos atentos, notaremos que todas las letras que están en mayúscula son iguales a sus partes minúsculas excepto por el bit $$5$$. Por lo tanto, si queremos pasar una letra mayúscula a minúscula o de minúscula a mayúscula podemos aplicar un XOR en el bit $$5$$ como sigue:

<textarea class="cpp">char a = 'A';
a = a ^ (1 << 5);
cout << a;</textarea>

Podemos ver que no importa si `a = 'A'` o si `a = 'a'`, al momento de aplicar XOR (`^`) en el bit $$5$$ estaremos alternando esta letra, de mayúscula a minúscula y viceversa.

### Contar cuántos bits están encendidos

Para hacer este procedimiento existe un algoritmo ya propuesto, este algoritmo es el algoritmo de Brian Kernighan. Puedes revisar toda la descripción de este algoritmo en [GeeksforGeeks](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/ "Count set bits in an integer - GeeksforGeeks"). 

<textarea class="cpp">
int contarEncendidos(int x){ 
    int cont = 0; 
    while (x){ 
        x &= (x-1); 
        count++; 
    } 
    return count; 
}</textarea>

### Revisar si un número es una potencia de 2

Si un número es una potencia de $$2$$ entonces sólo tiene un bit encendido, todos los demás estarán apagados. Siguiendo esta lógica lo único que hay que hacer es hacer una operación AND entre $$x$$ y $$x-1$$. Hay que notar que si a un número le restamos $$1$$ todos los bits apagados desde el LSB hasta el primero que esté encendido van a alternar su valor, por lo tanto, si hacemos un AND y $$x$$ es una potencia de $$2$$ entonces todos los bits se harán cero, si no es potencia de dos, algún bit se quedará encendido. Hay que tener cuidado cuando $$ x = 0 $$.

<textarea class="cpp">
bool esPotenciaDeDos(int x){ 
    return (x && !(x & x-1)); 
} </textarea>

### Revisar que en un número de 10 dígitos todos los dígitos sean diferentes

Este ejemplo es una buena introducción al uso de las máscaras de bits. Imagina que tenemos un número $$x$$ de diez dígitos y queremos saber si están presentes los diez dígitos del sistema decimal, podemos hacer el siguiente procedimiento. En una nueva variable entera vamos encendiendo los bits en la posición que cada dígito de $$x$$ indica.

Por ejemplo, digamos que $$x = 9264017358$$, lo primero que haremos será encender en un nuevo entero $$y=0$$ el bit $$8$$, por ser el dígito menos significativo de $$x$$. Una vez que lo hayamos encendido, quitamos ese dígito de $$x$$ y encendemos ahora el siguiente dígito (el $$5$$). Continuamos hasta terminar con todos los dígitos, si todos los dígitos de $$x$$ son diferentes entonces $$y = 1111111111_2$$. Como podemos ver $$ y+1 = 2^{10} = 1024$$, por lo tanto, si `y == 1023` entonces todos los dígitos de $$x$$ son diferentes.

Lo anterior entonces se puede hacer como sigue:

<textarea class="cpp">
#include &lt;iostream&gt;
using namespace std;

int main(){
    long long int x = 9264017358;
    int mask = 0;
    while (x){
        int aux = x%10;
        mask |= (1 << aux);
        aux /= 10;
    }
    if (mask == 1023) cout << "Todos los digitos son diferentes";
    else cout << "No todos los digitos son diferentes";
    return 0;
}</textarea>

## Conclusión

El uso de operadores que manipulen bit a bit una variable resulta muy útil pues ahorra no sólo tiempo de ejecución sino también memoria. Las operaciones bit a bit pueden resultar un poco confusas al inicio, pero en realidad son bastante intuitivas y pueden ayudarnos a resolver problemas complejos cumpliendo en tiempo y memoria.

<div class="Nav">
    <a href="{{ site.baseurl }}/C++/Estructuras/Arreglos/Multidimensionales/" title="Arreglos multidimensionales &vert; #iP Code">Tema anterior</a> | <a href="{{ site.baseurl }}/C++/Estructuras/Creacion-de-tipos/Struct/" title="Struct &vert; #iP Code">Tema siguiente</a>
</div>