---
layout: G-Article
title: Contadores
date: 2020-01-04 12:00:00
author: rivel_co
tags: [Variables, Técnicas]
olimpiada: [OMI]
subject: [C++]
---

En la solución de muchos problemas de programación es muy común tener que llevar la cuenta de cuántas veces pasa un determinado suceso o se cumple una determinada condición, a las variables que utilizamos para llevar esa cuenta les llamamos *contadores*.

{: #ListaContenido}
- Concepto
- Declaración

## Concepto

Planteamos el siguiente problema, encontrar todos los divisores de un número $$x$$. Si hacemos ese procedimiento a mano, mentalmente iremos comprobando la divisibilidad de $$x$$ respecto a otros números y cada que encontremos un divisor lo *contaremos*. Si queremos realizar un programa que cuente los divisores podemos hacer algo como sigue:

<textarea class="cpp">for (int i=1; i<=x; i++){
    if (x%i == 0) // Si i divide a x ...
        // Contamos un nuevo divisor encontrado
}</textarea>

En la línea 3 podremos llevar a cabo el proceso de contar los divisores, lo único que necesitamos es declarar y manejar un contador, una variable cuyo valor represente la cantidad de divisores que tiene un número.

## Declaración

El punto clave de un contador es el momento y valor con el que se **inicializa** y el momento y valor con el que se **actualiza**. En nuestro ejemplo anterior podemos declarar el contador *antes* de comenzar con nuestro ciclo `for`, el valor inicial de ese contador será $$0$$ pues en ese momento llevamos $$0$$ divisores encontrados. Cada que se encuentre un divisor lo que tenemos que hacer es actualizar el valor del contador, en este caso (*y casi siempre*) lo incrementaremos en uno. Al final el valor de ese contador será igual al número de divisores que tiene $$x$$.

<textarea class="cpp">int cont = 0;
for (int i=1; i<=x; i++){
    if (x%i == 0)
        cont++;
}
cout << cont;</textarea>

De esta forma partimos con `cont = 0` pues no hemos encontrado ningún divisor en ese momento, cada que se cumple `x%i == 0` quiere decir que $$i$$ es un divisor de $$x$$ y por lo tanto en la línea 4 aumentamos en $$1$$ el valor de nuestro contador. Cuando terminamos de revisar todos los números de $$1$$ a $$x$$ entonces mostramos el valor de `cont`.

> Es importante saber que este método **no** es un buen método para encontrar divisores, pero es útil para entender de forma sencilla el concepto.

Consideremos otro ejemplo, recibimos una $$N$$ cantidad de enteros que representan la edad de $$N$$ personas, queremos saber cuántas de esas personas son mayores de edad ($$18$$) pero menores de $$60$$ años. Este problema lo podemos resolver fácilmente como sigue:

<textarea class="cpp">int N, aux, cont = 0;
for (int i=0; i<N; i++){
    cin >> aux;
    if (aux > 17 && aux < 60) cont++;
}
cout << cont;</textarea>

Existe otra forma de considerar a un contador, pero lo importante es tener claro que su función es *contar*. Si nos planteamos el problema de cuántas veces cabe $$x$$ en $$y$$, podemos resolverlo de varias formas. Una forma de utilizar el contador como ya se ha mostrado sería:

<textarea class="cpp">int x, y, cont = 0;
cin >> x >> y;
while(y > 0){
    y -= x;
    cont++;
}
cout << cont;</textarea>

Nota que la implementación anterior podría resultar *ridícula* inclusive. La forma más adecuada de responder el problema sería:

<textarea class="cpp">int x, y, cont;
cin >> x >> y;
cont = y/x;
cout << cont;</textarea>

Como es evidente, ni siquiera sería necesario inicializar la variable `cont`, puede que ni siquiera sea necesario llamarla así o en dado caso ni siquiera es necesario declararla. De cualquier forma, está expresando la misma función en ambos casos, dice cuántas veces algo se cumplió y es es justamente el principio de un contador.

### Cita esta página

{% include citeThis.html titulo=page.title fecha=page.date link=page.url %}