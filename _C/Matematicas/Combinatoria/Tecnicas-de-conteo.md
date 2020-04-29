---
layout: G-Article
title: Técnicas de conteo
date: 2020-01-15 12:00:00
author: rivel_co
tags: [Matemáticas, Conteo]
hide_tags: true
olimpiada: [OMI]
subject: [C++]
---

En matemáticas discretas, la combinatoria se encarga de estudiar las estructuras discretas **contables**, esto es, la **ciencia de contar**. En programación podemos hacer conteos con muchos algoritmos, pero cuando los límites de un problema son muy grandes, es mejor usar **técnicas de conteo** que nos permitan simplificar el problema a unas pocas líneas, en un programa elegante como eficiente. Existe diferentes técnicas de conteo de las que se desprenden muchas otras, aquí se hablará de forma breve sobre técnicas bastante conocidas e importantes.

{: #ListaContenido}
- Regla de la suma
- Regla de la multiplicación
- Permutaciones
- Combinaciones
- Todos los subconjuntos
- Cadenas

## Regla de la suma

Consideremos dos conjuntos, uno con $$\mid A\mid$$ elementos y otro con $$\mid B\mid $$ elementos, si tenemos que obtener un elemento de estos conjuntos, podemos escoger de entre $$\mid A\mid  + \mid B\mid $$ elementos en total. Un ejemplo muy práctico son las placas de un auto, puede tener letras y números. Tenemos $$26$$ opciones en el abecedario y $$10$$ opciones con los números. En total podemos escoger de entre $$26 + 10 = 36$$ elementos. La notación para esta regla de la suma es:

<p>
    $$ \mid A \cup B\mid  = \mid A\mid  + \mid B\mid  $$
</p>

Esta regla deriva de una más general que incluye los principios de *inclusión* y *exclusión*. Esta regla general aplica cuando los conjuntos con los que tratamos se pueden solapar, es decir, comparten elementos. Entonces se escribe como sigue:

<p>
    $$ \mid A \cup B\mid  = \mid A\mid  + \mid B\mid  - \mid A \cap B\mid $$
</p>

Esto nos dice que podemos tener en total $$\mid A\mid  \cup \mid B\mid $$ opciones, combinando las primeros $$\mid A\mid $$ elementos y los otros $$\mid B\mid$$ elementos y excluyendo los que son iguales o que comparten ambas con $$-\mid A \cap B\mid $$. Es muy importante siempre en toda técnica de conteo evitar contar varias veces la misma cosa, por eso hay que considerar el principio de inclusión y exclusión. Esta regla aplica para cualquier cantidad de conjuntos.

## Regla de la multiplicación

Si podemos tomar un elemento de cada uno de dos conjuntos, el primero con $$\mid A\mid $$ elementos y el segundo con $$\mid B\mid $$ elementos, entonces podemos formar un total de $$\mid A\mid  * \mid B\mid $$ combinaciones. Por ejemplo, si queremos comer galletas con café y tenemos $$6$$ tipos de galletas y $$3$$ tipos de café, podemos hacer un hasta $$6 * 3 = 18$$ combinaciones en total. La notación aquí es:

<p>
    $$ \mid A \times B\mid  = \mid A\mid  * \mid B\mid  $$
</p>

## Permutaciones

Una permutación es una forma de ordenar $$n$$ objetos en donde cada objeto aparece solamente una vez. Podemos decir que hay $$n! = \prod_{i=1}^n i$$ permutaciones diferentes para una $$n$$ dada. Por ejemplo, si tenemos tres elementos `A`, `B` y `C` podemos ordenarlos de $$3! = 1 * 2 * 3 = 6$$ formas diferentes, `ABC`, `BCA`, `CAB`, `ACB`, `BAC` y `CBA`. Nota que como se utiliza el factorial de $$n$$ el resultado crece muy rápido.

> El factorial de $$n$$ se define como $$n! = \prod_{i=1}^n i$$, por lo que si queremos obtener el factorial de cinco ($$5!$$) tenemos que multiplicar los números desde $$1$$ hasta $$5$$. Entonces $$5! = 1 * 2 * 3 * 4 * 5$$.

Decimos que hemos *permutado* algo cuando proponemos una permutación diferente de los elementos presentados, es decir, cuando ordenamos los elementos de una forma distinta a la inicial. Por ejemplo, la cadena `roma` puede ser una permutación de `amor`. Siguiendo este ejemplo, la cadena tendría un total de $$4!$$ posibles permutaciones.

### K-ésima permutación

También podemos decir que hacemos la $$k$$-ésima permutación de $$n$$ cuando tenemos un conjunto de $$n$$ elementos disponibles y permutamos únicamente $$k$$ elementos, donde $$0 \le k \le n$$. Por ejemplo, si tenemos un conjunto con los elementos $$\{a, b, c, d\}$$ y hacemos la permutación segunda de ese conjunto, podemos formar 12 pares diferentes: $$ab$$, $$ac$$, $$ad$$, $$ba$$, $$bc$$, $$bd$$, $$ca$$, $$cb$$, $$cd$$, $$da$$, $$db$$ y $$dc$$. Podemos calcular la $$k$$-ésima permutación de $$n$$ con la formula:

<p>
    $${}^nP_{k} = n * (n-1) * (n-2) ... (n-k+1) = \frac{n!}{(n-k)!} $$
</p>

Nota que cuando $$k=0$$ tenemos como resultado $$1$$ para cualquier $$n$$. Mientras que cuando $$k=n$$ la respuesta es $$n$$. Por definición, $$0! = 1$$.

## Combinaciones

Cuando hablamos de combinaciones es común utilizar la regla de la multiplicación que describimos más arriba, sin embargo es más interesante hablar de la $$k$$-ésima combinación. Este caso se refiere a cuántos subconjuntos de tamaño $$k$$ se pueden formar de un conjunto de $$n$$ elementos. Si retomamos el conjunto $$\{a, b, c, d\}$$ y aplicamos combinaciones de $$2$$ entonces formaríamos los subconjuntos $$\{a, b\}$$, $$\{a, c\}$$, $$\{a, d\}$$, $$\{b, c\}$$, $$\{b, d\}$$ y $$\{c, d\}$$, muchas menos que la permutación segunda. Podemos calcular la combinación $$k$$-ésima utilizando la formula:

<p>
    $${}^nC_{k} = \binom nk = \frac{n!}{k!(n-k)!} $$
</p>

Nota que aquí estamos hablando de **subconjuntos**, no de un orden en particular; es por esto que aquí el orden parece no importar, porque solamente se considera que determinado elemento esté dentro del subconjunto, no su orden.

## Todos los subconjuntos

También podemos calcular el total de subconjuntos diferentes que se pueden hacer a partir de un conjunto con $$n$$ elementos. Esto se calcula con la formula:

<p>
    $$ 2^n $$
</p>

Si queremos obtener todos los subconjuntos de un conjunto de $$3$$ elementos $$\{a, b, c\}$$ tendríamos $$\{a\}$$, $$\{b\}$$, $$\{c\}$$, $$\{a, b\}$$, $$\{a, c\}$$, $$\{b, c\}$$, $$\{a, b, c\}$$ y el conjunto vacío que también entra en los $$2^3 = 8$$ subconjuntos diferentes.

## Cadenas

Entiéndase en este caso una cadena como una sucesión de $$n$$ elementos escogidos de entre $$m$$ posibles en donde puede haber repetidos. Por ejemplo, de un conjunto con los elementos $$\{a, b, c\}$$ podemos tener diferentes las siguientes *cadenas* de tamaño $$3$$: `aaa`, `aab`, `aac`, `aba`, `abb`, `abc`, `aca`, `acb`, `acc`, `baa`, `bab`, `bac`, `bba`, `bbb`, `bbc`, `bca`, `bcb`, `bcc`, `caa`, `cab`, `cac`, `cba`, `cbb`, `cbc`, `cca`, `ccb`, `ccc`. La formula para calcular estas $$27$$ cadenas diferente es:

<p>
    $$ m^n $$
</p>
