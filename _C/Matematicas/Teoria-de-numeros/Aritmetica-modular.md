---
layout: G-Article
title: Aritmética modular
date: 2020-04-07 16:17:00
author: rivel_co
tags: [Matemáticas, Módulo]
hide_tags: true
olimpiada: [OMI]
subject: [C++]
---

La aritmética modular nos permite trabajar con números muy grandes y realizar sobre ellos diferentes operaciones de una forma eficiente y sencilla. Se basa en el uso y propiedades de la **operación módulo**. Entender cada propiedad resulta muy útil al resolver ciertos problemas.

{: #ListaContenido}
- Operación módulo
- Aplicación en C++
- Módulo con números decimales
- Suma
- Resta
- Multiplicación
- Exponenciales
- Divisiones
- Otras aplicaciones de la aritmética modular

## Operación módulo

La operación módulo (o simplemente *el módulo*) es una operación aritmética que **obtiene el residuo** de la división de dos números. Por ejemplo, en la división $$7 / 3$$, tenemos al $$7$$ como *dividendo* y al $$3$$ como divisor. Si realizamos esta operación obtendremos un *cociente* entero igual a $$2$$ y un **residuo** igual a $$1$$. Por lo tanto, la operación $$7$$ módulo $$3$$ es igual a $$1$$.

> Dados 2 números positivos $$a, b$$, la operación $$a$$ módulo $$b$$ devuelve el residuo de la división euclídea de $$a/b$$.

Esta operación se ha llamado de muchas formas, por ejemplo la encontrarás como $$a$$ módulo $$b$$, $$a \bmod b$$ y la más común en los entornos informáticos `a % b`. Todas estas expresiones denotan la misma operación.

Es importante notar que $$a \bmod b$$ no es igual que $$b \bmod a$$. Por ejemplo, considera que $$ a \bmod b$$ cuando $$0 < a < b$$ siempre es $$a$$, pues al ser menor $$a$$ que $$b$$ el resultado nunca puede ser entero, por otro lado $$ a \bmod b$$ cuando $$a > b$$ no puede ser $$a$$, pues de ser así entonces todavía se podría dividir ese "residuo" entre $$b$$. Pongamos algunos ejemplos.

<p>
$$\begin{align}
5 \bmod 3 & = 2\\
6 \bmod 3 & = 0\\
9 \bmod 2 & = 1\\
3 \bmod 6 & = 3\\
12 \bmod 20 & = 12\\
5 \bmod 5 & = 0\\
0 \bmod 21 & = 0\\
\end{align}$$
</p>

Es posible notar además, que $$a \bmod b = 0$$ cuando $$b$$ es un divisor de $$a$$ (es decir, cuando $$b \mid a$$). Por esto, todos los números pares módulo $$2$$ dan como resultado $$0$$. Este dato es **muy importante** pues la operación módulo nos permite saber si un número es divisor de otro. También nota como es posible calcular $$0 \bmod X$$ pero no es posible calcular $$X \bmod 0$$ pues habría que hacer una división entre $$0$$.

La operación módulo es muy útil para identificar propiedades de los números (como se decía arriba sobre los números pares), facilitando cálculos y optimizando códigos, pues es la base de la aritmética modular.

## Aplicación en C++

La operación módulo en C++ se realiza utilizando el operador `%`, por lo que si queremos obtener $$21 \bmod 8$$ lo podemos hacer con la operación `21 % 8`. Es importante saber que, como con cualquier otro operador aritmético, hay que considerar el uso de paréntesis cuando queremos obtener el módulo de varios argumentos, por ejemplo, `x + y % 2` es diferente de `(x+y) % 2`, del mismo modo `36 % a + b` es diferente de `36 % (a+b)`.

La operación módulo es muy utilizada en programación competitiva pues ayuda en la solución de muchos problemas que con otros métodos serían mucho más complicados de resolver. 

### Obtener el último dígito de un número

Si tenemos un número `x = 8324785` y queremos mostrar el último dígito, podemos aplicar el principio del módulo para saber que si dividimos ese número `x` entre $$10$$, quedaría como residuo la parte del número que es menor a $$10$$, por lo tanto `y = x % 10 = 5`. Usando el mismo razonamiento podemos obtener los últimos dos dígitos del número si aplicamos un módulo $$100$$.

### Saber el día de la semana de una fecha

Podemos saber en qué día de la semana caerá una determinada fecha si conocemos en qué día cayó en un determinado año, aplicando la operación módulo. Por ejemplo, si el año pasado el día 3 de diciembre cayó en martes, este año caerá $$365 \bmod 7 = 1$$ días después. Si el año actual es bisiesto entonces caerá $$366 \bmod 7 = 2$$ días después. A la fecha de este artículo, el 3 de diciembre del 2019 fue un martes, en el 2020 será un jueves.

Esto funciona de una manera sencilla, la semana tiene $$7$$ días (de ahí el $$7$$ en el módulo) y un año tiene $$366$$ o $$365$$ dependiendo si es bisiesto o no. Para que una fecha cayera siempre en el mismo día de la semana, sería necesario que el número de días en un año fuera múltiplo de el número de días que tiene la semana. En ese caso si el año pasado una fecha cayó en martes el siguiente año sería $$0$$ días después, es decir en martes también. Como los días de la semana no son múltiplo de los días de un año entonces siempre estará un día o dos después de la fecha anterior.

## Módulo con números decimales

En C++ no es posible realizar una operación de módulo utilizando uno o más números decimales (variables tipo `float` o `double`). Es posible, sin embargo, realizar esta operación con la función `fmod()` de la librería `cmath`. Esta función recibe dos argumentos, donde `fmod(a, b)` equivale a $$a \bmod b$$. Por ejemplo, si tenemos `x=2.4` y `y=1.2` y realizamos `z=fmod(x, y)` el valor de `z` será $$0$$. En cambio, si `y=1.1` y realizamos la misma operación, el resultado será `z==0.2` pues la parte entera del cociente $$2.4/1.1 = 2$$, el residuo en este caso sería $$0.2$$. 

Utilizar la función `fmod()` puede ser muy útil, sin embargo no es lo más recomendado pues se ha visto que esta operación es algo inestable y en procedimientos de gran precisión puede fallar. Entonces lo más recomendable es convertir, de una forma más segura esos, números decimales a números enteros. Por ejemplo, si sabemos que los datos a manejar tienen a lo más 2 dígitos en la parte decimal entonces podemos hacer algo como sigue:

<textarea class="cpp">
float a = 3.14;
float b = 2.85;
int c = a * 100;
int d = b * 100;
int modulo = (c % d)/100;</textarea>

Nota que al final estamos dividiendo entre $$100$$. Esto es para regresar el valor a su escala original, pues en la línea 3 y 4 multiplicamos por $$100$$ justamente para *pasar* los decimales a la parte entera. Si lo único que queremos saber es si $$b \mid a$$ entonces no hay necesidad de regresar la escala, lo único que nos interesa es saber si el módulo es $$0$$. Esta forma de utilizar el módulo con los números decimales es más segura que utilizar la función `fmod()`.

## Suma

Si necesitamos calcular $$(E + R) \bmod n$$ siendo $$E$$ y $$R$$ números muy grandes, es útil saber la siguiente igualdad:

<p>
$$
(E + R) \bmod n = ((E \bmod n) + (R \bmod n)) \bmod n\\
\text{Por ejemplo: }\\
\begin{align}\\
(1234 + 5678) \bmod 10 & = ((1234 \bmod 10) + (5678 \bmod 10)) \bmod 10\\
& = ((4) + (8)) \bmod 10\\
& = 12 \bmod 10\\
& = 2\\
\end{align}
$$
</p>

## Resta

La resta es prácticamente igual que la suma, pero con números negativos. De forma general tenemos la igualdad:

<p>
$$ (E - R) \bmod n = ((E \bmod n) - (R \bmod n)) \bmod n$$
</p>

En C++ podemos manejar números negativos en el módulo y se comportará de manera esperada, por esto `-4 % 2 == 0`. Aunque claro, también podemos utilizar el valor absoluto de los números con las función `abs()` de la librería `algorithm`.

## Multiplicación

El mismo principio de la suma se aplica para la multiplicación también.

<p>
$$ (E * R) \bmod n = ((E \bmod n) * (R \bmod n)) \bmod n$$
</p>

Esta operación y la anterior resultan útiles para encontrar cosas como la cantidad de *feria* (monedas menores a $1) que se tendrían si gano $203.22 y esta semana trabaje 36 horas. 

## Exponenciales

Las operaciones exponenciales siguen el principio de la multiplicación:

<p>
$$ (E^R) \bmod n = ((E \bmod n)^R \bmod n$$
</p>

En este tipo de operaciones, la aritmética modular demuestra su velocidad y su eficiencia, pues las razones exponenciales crecen más rápido que ninguna otra, de esta forma no tenemos que preocuparnos por manejar enteros tan grandes, si el problema lo permite, únicamente estaremos trabajando con módulos.

## Divisiones

Las operaciones con división son consideradas en la aritmética modular como **Congruencias** y como tal serán discutidas en otro artículo.

## Otras aplicaciones de la aritmética modular

La aritmética modular se utiliza en diferentes problemas particulares, por ejemplo ya se discutía arriba la forma de calcular el día de la semana en que caería una fecha determinada, pero es utilizada en otras situaciones también.

### Último dígito de una potencia de dos

Un problema común incluso en Olimpiadas de Matemáticas es encontrar el último dígito de una potencia de $$2$$. Esto se puede calcular manualmente pero siguiendo siempre los principios de la aritmética modular. Por ejemplo, si queremos encontrar el último dígito de $$2^{100}$$ podemos partir de un $$2^2$$ y de ahí avanzar hacia adelante subiendo al cuadrado siempre el término y obteniendo el módulo cada vez que se hace.

Si sabemos que $$2^4 = 2^2 * 2^2$$ y solamente nos interesa el último dígito de esa operación entonces podemos trabajar con el módulo. $$2^2 = 4$$, si entonces $$2^4 = 2^2 * 2^2 = 4 * 4 = 16$$ lo único que tenemos que conservar de ese resultado es el $$6$$ (último dígito del resultado). Recuerda que para obtener el último dígito de un número podemos sacar un módulo de $$10$$. Así podemos ir subiendo hasta llegar a $$2^{100}$$.

<p>
$$\begin{align}
2^2 \bmod 10 & = 4\\
2^4 \bmod 10 & = (2^2 * 2^2) \bmod 10\\
           & = ((2^2 \bmod 10)(2^2 \bmod 10)) \bmod 10\\
           & = 16 \bmod 10 = 6\\
2^8 \bmod 10 & = (6 * 6) \bmod 10\\
    & = 36 \bmod 10 = 6\\
2^{16} \bmod 10 & = (6 * 6) \bmod 10 = 6\\
2^{32} \bmod 10 & = (6 * 6) \bmod 10 = 6\\
2^{64} \bmod 10 & = (6 * 6) \bmod 10 = 6\\
2^{100} \bmod 10 & = (2^{64} * 2^{32} * 2^4) \bmod 10\\
      & = (6 * 6 * 6) \bmod 10\\
      & = 216 \bmod 10\\
      & = 6\\
\end{align}$$
</p>

De esta forma en 7 operaciones de módulo podemos calcular el último dígito de un número muy grande, como lo es $$2^{100}$$.

### Algoritmo de encriptación RSA

Este algoritmo de encriptación es el más utilizado de los algoritmos de clave pública y recae en el uso de aritmética modular. Llamemos al mensaje encriptado y establecido de forma numérica como $$m$$. Este mensaje se encripta siguiendo la fórmula $$c = m^e \bmod n$$. Ahora $$c$$ es un mensaje cifrado que únicamente se puede descifrar con la fórmula inversa $$m = c^d \bmod n$$.

Como podrás notar, es vital la relación que mantienen $$d$$ y $$e$$ y que en el algoritmo de encriptación corresponden respectivamente a la clave privada y la clave pública. De forma más precisa, $$d$$ tiene que ser el multiplicador modular inverso de $$e \bmod \varphi(n)$$ donde $$\varphi(n)$$ es la función de Euler para $$n = p * q$$ y a su vez, $$p$$ y $$q$$ son dos números primos muy grandes que se mantienen en secreto.

Como notarás, la seguridad de este tipo de encriptación recae en esos números primos que son tan grandes como difíciles y tardados de encontrar, además de la aritmética modular que permite cifrar y descifrar los mensajes.
