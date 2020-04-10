---
layout: G-Article
title: Números primos
date: 2020-04-08 15:30:00
author: rivel_co
tags: [Matemáticas, Algoritmo, Teoría de números]
Hide_Tags: true
olimpiada: [OMI]
subject: [C++]
---

Un número primo es un número natural mayor a $$1$$ que únicamente tiene dos divisores, $$1$$ y él mismo. Los primeros números primos son $$2, 3, 5, 7, ...$$. Es importante notar que el único número primo que es par es el $$2$$, además de ser el más chico de todos. También es importante saber que los números primos son infinitos y no son producidos por ninguna formula conocida hasta ahora.

{: #ListaContenido}
- Importancia de los números primos
- Saber si un número es primo
- Forma óptima de saber si un número es primo
- Criba de Eratostenes

## Importancia de los números primos

La importancia de los números primos se ve bien representada por el *teorema fundamental de la aritmética* que dice que cualquier entero puede representarse como el **producto único** de números primos, por ejemplo, el número $$506$$ se puede representar como . Los números primos que componen ese producto que da como resultado el número entero **son únicos**, es decir, no hay otra multiplicación de primos que genere el mismo número, claro que el orden puede cambiar pero no así los números que lo componen. 

> Al conjunto único de números primos cuyo producto da un número dado $$n$$ se le denomina **factorización en primos** de $$n$$. Por esto se dice que un número primo $$p$$ es factor de $$n$$ si ese número $$p$$ pertenece a la factorización en primos de $$n$$.

Como se decía arriba, los números primos solamente tienen dos divisores, el $$1$$ y ellos mismos, los números que no son primos se llaman *compuestos*. Sabemos que los números naturales son infinitos, pero <span>¿lo son también los números primos?</span>

Euclides demostró que los números primos son infinitos por medio de una *reducción al absurdo* bastante bonita. Se podría demostrar que los números primos son finitos si encontramos que no es posible proponer un número que no pueda ser dividido por algún número primo conocido.

Supongamos que los números primos no son infinitos, entonces podríamos ponerlos todos en una lista que llamaremos $$p$$. Con todos los números primos puestos ahí, podríamos hacer una operación como $$S = 1 + \prod_{i=1}^n p_i$$. De esta forma obtendríamos en $$S$$ el **producto** de todos los números primos, más $$1$$, pero no sólo eso, estaríamos realizando con esta operación, un resultado que no es divisible por ningún número de $$p$$.

Entonces, $$S$$ sería mayor que todos los números de la lista y debería ser un número compuesto, pues siguiendo el caso supuesto, ya no hay más números primos. Sin embargo, $$S$$, como todos los demás números, debería poder descomponerse en números primos, pero ningún número de la lista podría dividir exactamente a $$S$$ pues hay un $$+1$$ extra en esa cuenta que siempre va a sobrar cuando dividamos $$S$$ entre cualquier número de $$p$$. Por lo tanto, debería haber otro número primo, más grande que cualquiera en la lista, que pudiera dividir a $$S$$. Por esto siempre nos faltarían primos por incluir en la lista y por lo tanto, los **primos tienen que ser infinitos**.

Nota que la ecuación $$S = 1 + \prod_{i=1}^n p_i$$ la propone Euclides con toda la intención de proponer un número que no pueda ser dividido por ningún $$p_i$$. Esta ecuación pone a prueba el propuesto de que los primos sean finitos y de esta forma nos permite demostrar lo contrario.

Es muy común en problemas de programación competitiva encontrarnos problemas que involucren números primos, por alguna propiedad en el problema o porque explícitamente se menciona. La cosa con los números primos en estos problemas, es generarlos y usarlos rápidamente, de una forma eficiente, pues generalmente se necesitan muchos primos y muchas veces tienen que ser muy grandes.

## Saber si un número es primo

Para saber si un número es primo, lo que tenemos que saber es cuáles son sus divisores, si tiene más de dos entonces por definición no sería primo. Hay varias formas de saber esto.

### La forma "bruta"

Para saber si un número $$n$$ tiene otros divisores además del $$1$$ y $$n$$, podemos revisar si es divisible por alguno de los números en el rango $$[2 ... N-1]$$. Esta operación es de complejidad $$O(N)$$ que podría parecer buena, pero dado que los números primos pueden llegar a ser muy grandes y son infinitos, esta forma de cálculo resulta ser bastante ineficiente en las competencias de programación competitiva. De cualquier forma, podemos intentar lo anterior con el siguiente código:

<textarea class="cpp">
bool esPrimo(int n){
    for (int i=2; i&lt;n && esPrimo; i++){
        if (n%i == 0) return false;
    }
    return true;
}</textarea>

Nota que hicimos una pequeña "optimización" al evaluar únicamente desde $$2$$ y hasta $$n-1$$ (esto con el `i<n`), si el número es primo entonces no deberá haber ningún otro divisor en todo ese rango. También la búsqueda de los divisores termina cuando se encuentra un divisor, pues no es necesario seguir buscando más si ya se ha encontrado uno. Aún con estas modificaciones la complejidad sigue siendo $$O(n)$$, no muy buena.

## Forma óptima de saber si un número es primo

Se puede optimizar mucho más el algoritmo utilizando la raíz cuadrada del número a evaluar. Si podemos evaluar la cantidad de divisores que tiene un número $$n$$ hasta su raíz cuadrada, entonces podemos saber si el número es primo o no. Esto funciona y se puede comprobar fácilmente. Pensemos en número $$x$$ que donde $$x \mid N$$, entonces podríamos decir que $$N = x * \frac{N}{x}$$, ahora, si $$\frac{N}{x} < x$$ y nosotros vamos buscando los divisores de forma ascendente desde el $$2$$, nos tendríamos que encontrar primero a $$\frac{N}{x}$$ como divisor de $$N$$ que a $$x$$. Pero ambos, tanto $$x$$ como $$\frac{N}{x}$$ serían divisores de $$N$$, porque su producto da como resultado $$N$$. Ahora, no podría pasar que $$x, \frac{N}{x} > \sqrt N$$, pues de ser ambos mayores a la raíz, su producto sería mayor que $$N$$, al menos uno de ellos dos (o un factor primo de uno de ellos dos) debería aparecer antes de $$\sqrt N$$, es decir, ser más chico que $$\sqrt N$$.

Es por esto, que si vamos buscando de forma ascendente desde $$2$$ y no encontramos ningún divisor de $$N$$ que sea menor a $$\sqrt N$$ podemos estar seguros de que tampoco estará un divisor después de la raíz. Si hay un divisor antes de la raíz, tampoco nos interesa seguir buscando, sabremos en ese momento que $$N$$ no es un número primo. Hasta este punto, nuestro algoritmo sería de complejidad $$O(\sqrt N)$$.

Otra optimización que podemos hacer a este algoritmo y que es muy sencilla de codificar, es probar únicamente con los números impares luego de haber probado con el $$2$$. Es decir, si sabemos que el número que nos interesa saber si es primo o no, no es dividido por $$2$$ entonces tampoco lo será por cualquiera de los múltiplos de $$2$$. Hasta este punto podríamos decir que la complejidad baja a ser $$O(\sqrt{N} / 2)$$ que para fines prácticos sigue siendo $$O(\sqrt N)$$. Un algoritmo que evalúe lo anterior sería:

<textarea class="cpp">
bool primo(int n){  // Recibe un entero n
    if (n%2 == 0 && n != 2) return false;   // Se evalua si es par, excepto en el caso del 2
    for (int i=3; i&lt;sqrt(n) + 1; i+=2){ // Va desde 3 hasta la raíz cuadrada y solamente números impares
        if (n%i == 0) return false; // Si alguno divide a n entonces no es primo
    }
    return true; // Si nunca tuvo un divisor entonces es primo
}</textarea>

Podemos llevar esta idea de eliminar a los pares más allá y probar a dividir únicamente entre números primos. Esto funciona porque si un número primo $$p$$ no divide a $$N$$, entonces tampoco lo hará cualquiera de sus múltiplos. Esto reduce bastante más la complejidad del algoritmo, piensa en el caso de $$1,000,000$$, en el rango $$[1 ... \sqrt{10^6}]$$ hay $$500$$ números impares, pero solamente $$168$$ números primos. Del *teorema de los números primos* podemos decir que hay aproximadamente $$ x / \ln x$$ números primos menores o iguales a $$x$$. Por esto podemos decir que el algoritmo final tendría una complejidad de $$O(\frac{\sqrt N}{\ln{\sqrt N}})$$.

Para poder codificar lo anterior, tenemos que tener listo un conjunto de números primos con los que podamos probar la divisibilidad. El mejor método para generar muchos números primos es la *criba de Eratostenes*. 

## Criba de Eratostenes

La criba de Eratostenes utiliza el método de eliminar múltiplos de números para al final solamente dejar los que sí son primos. Parte de tomar al $$2$$ como número primo, luego *elimina* a los múltiplos de $$2$$ empezando por $$2^2$$, luego regresa al siguiente número que **no** ha sido tachado, que sería el $$3$$. De igual forma se eliminan todos los múltiplos de $$3$$ empezando por $$3^2$$. Se continúa así hasta que se ha evaluado todo el rango que hemos decidido evaluar, por ejemplo si queremos encontrar todos los primos de $$[1 ... 10^7]$$. En el siguiente código se implementa el algoritmo de la criba de Eratostenes.

<textarea class="cpp">
#define ll long long        // Para facilitar escritura
bool compuestos[10000001];  // Para eliminar números
ll primos[100000];          // Aquí guardaremos los números primos
ll total = 0;               // Lleva la cuenta total de primos
void cribaErat(ll limite){
    compuestos[0] = compuestos[1] = true;   // El 0 y el 1 no son primos
    for (ll i=2; i<=limite; i++){           // Iteramos con todos los números en el rango
        if (compuestos[i] == false){            // Si un numero sí es primo entonces:
            for (ll j = i*i; j<=limite; j+=i){  // Se borran sus múltiplos empezando por i²
                compuestos[j] = true;           // Esos números se marcan como compuestos/no primos
            }
            primos[total] = i;  // Añadimos el número actual a la lista de primos
            total++;            // Actualizamos el contador
        }
    }
}</textarea>

Nota que se hace uso de variables `long long` para poder almacenar números muy grandes. Además se aprovecha el hecho de que las variables globales comienzan con un valor de $$0$$ para declarar el arreglo `compuestos`. El "eliminar" de este código consiste en marcar como `true` los números como en el arreglo compuestos. También nota como en el ciclo de la línea 9 se empieza con el cuadrado del número actualmente evaluado y se van eliminando los múltiplos al avanzar con `j+=i`. En este código se podría evaluar el rango $$[0 ... 10^7]$$ que suele ser suficiente para la mayoría de los problemas de programación.

Con la criba de primos también podemos decir si un número más grande que el rango de la criba es primo, esto lo haríamos como se dijo antes, revisando si el número a evaluar puede ser dividido por los números de la criba. Si el número primo más grande generado por la criba es $$P$$ entonces este método descrito solamente alcanzaría para evaluar un número $$N$$ donde $$N \leq P^2$$.