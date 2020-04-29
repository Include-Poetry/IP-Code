---
layout: G-Article
title: Divisibilidad
date: 2020-04-09 15:30:00
author: rivel_co
tags: [MCM, MCD, GCD, LCM, Matemáticas]
hide_tags: true
olimpiada: [OMI]
subject: [C++]
---

Otra propiedad de los números que es estudiada por la *teoría de números* es la divisibilidad. Decimos que $$a$$ divide a $$b$$ (representado como $$a \mid b$$) si $$b = a*k$$ para algún entero $$k$$. Por esto también podemos decir que $$a$$ es un divisor de $$b$$ si $$a \mid b$$ o que $$a$$ es un múltiplo de $$b$$ si $$b \mid a$$. De forma sencilla decimos que $$a \mid b$$ si la operación $$\frac{b}{a}$$ no genera ningún residuo. El divisor natural más pequeño de todo número no nulo es $$1$$.

{: #ListaContenido}
- Mayor Común Divisor
- Mínimo Común Múltiplo

## Mayor Común Divisor

El Mayor Común Divisor (**MCD** o **GCD** por sus siglas en inglés *Gratest Common Divisor*) es el divisor más grande que comparten un par de enteros. Es decir, el mayor común divisor $$d$$ de dos números $$a, b$$ es el entero positivo más grande donde $$d \mid a$$ y $$d \mid b$$. Si consideramos a `gcd()` como una función que recibe dos enteros y devuelve el MCD de esos números, entonces `gcd(3, 6) == 3`, también `gcd(15, 20) == 5`. Es importante saber además, que si `gcd(x, y) == 1` entonces decimos que `x` y `y` son *primos entre sí*.

Esta es una función muy frecuentemente utilizada en competencias de programación competitiva, nos ayuda a simplificar razones, por ejemplo, si queremos simplificar la fracción $$\frac{12}{20}$$ podemos dividir tanto el denominador como el numerador entre `gcd(12, 20)`. Siendo así:

<p>
$$\frac{12}{20} = \frac{12/4}{20/4} = \frac{3}{5}$$
</p>

### Calculando el MCD (GCD)

El mejor algoritmo para encontrar el MCD de dos números es el algoritmo de Euclides, el cual se apoya en la técnica de *divide y vencerás*. El algoritmo hace uso de dos observaciones importantes:

> **1.** Si $$b \mid a$$ entonces $$gcd(a, b) = b$$

> **2.** Si $$a=bt + r$$ donde $$t$$ y $$r$$ sean enteros, entonces $$gcd(a, b) = gcd(b, r)$$

La primer observación es cierta porque si $$b$$ divide a $$a$$ entonces el divisor más grnade de $$b$$ será el más grande que los dos tengan en común, porque además **cualquier divisor** de $$b$$ dividiría a $$a$$ también. Siendo así, el divisor más grande de $$b$$ es $$b$$ mismo.

La segunda observación es cierta porque cualquier divisor común de $$a$$ y de $$b$$ debe serlo también de $$r$$, pues de no ser así, al sumarse $$r$$ a $$bt$$ (donde $$bt \mid a$$ y claro $$b \mid bt$$) el resultado no podría ser un múltiplo de $$a$$. De hecho es parte de la definición del MCD que $$mcd(a, b)$$ sea igual a $$mcd(bt + r, b)$$. 

### Implementación del algoritmo de Euclides

El algoritmo para calcular el Mayor Común Divisor de un par de números es recursivo. La recursión recae en sustituir repetidamente **el argumento más grande** de la función, por el residuo de la división de ese mismo número entre el más pequeño, esto justamente por lo que se dice arriba, si $$b<a$$ y además $$b$$ no divide a $$a$$, podemos expresar $$a=bt+r$$ en donde si dividimos $$a/b$$ entonces tendremos como residuo $$r$$ (que es más chico que $$b$$). Si continuamos haciendo esto eventualmente ese residuo será $$0$$ y entonces el $$b$$ con el que se estaba buscando pasaría a ser el MCD de la pareja original de números. 

Revisemos el algoritmo con un ejemplo en donde la función `gcd()` recibe dos números y reduelve el mayor común divisor de ellos. Para que sea más gráfico pondremos en el primer argumento al valor más grande de la pareja de números evaluada en ese momento. En el ejemplo buscamos el MCD de $$84524$$ y $$1232$$.

<p>
$$
\begin{align}
gcd(84524, 1232) & = gcd(84524 \bmod 1232, 1232)\\
                 & = gcd(748, 1232)\\
gcd(1232, 748)   & = gcd(1232 \bmod 748, 748)\\
                 & = gcd(484, 748)\\
gcd(748, 484)    & = gcd(748 \bmod 484, 484)\\
                 & = gcd(264, 484)\\
gcd(484, 264)    & = gcd(484 \bmod 264, 264)\\
                 & = gcd(220, 264)\\
gcd(264, 220)    & = gcd(264 \bmod 220, 220)\\
                 & = gcd(44, 220)\\
gcd(220, 44)     & = gcd(220 \bmod 44, 44)\\
                 & = gcd(0, 44)\\
gcd(84524, 1232) & = 44\\
\end{align}
$$
</p>

### Obtener el MCD de más de dos números

Podemos obtener el MCD de más de dos números si agrupamos las consultas a la función, es decir, si queremos saber algo como `gcd(a, b, c)` entonces es lo mismo que `gcd(gcd(a,b), c)`. No importa la cantidad de números que se pongan en la consulta, este procedimiento dará siempre el resultado correcto.

### Implementación en C++

El anterior algoritmo recursivo se puede implementar de forma sencilla en C/C++.

<textarea class="cpp">
int gcd(int a, int b) { // Se reciben dos enteros 'a' y 'b'
    if (b == 0){    // Cuando se llega al caso trivial:
        return a;   // el otro valor será el MCD
    } else {                // Si aún no se encuentra el caso trivial
        return gcd(b, a%b); // se repite el intercambio del valor más grande por el residuo
    }
}</textarea>

Nota que para este algoritmo es indistinto si el primer argumento es más grande que el segundo o viceversa. Esto funciona así porque con `gcd(b, a%b)` siempre se asegura que se pasa primero el término más grande como primer argumento, pues cuando $$b > a$$ entonces $$a \bmod b = a$$ y por lo tanto, $$b > a \bmod b$$. Por otro lado, cuando $$a > b$$ entonces $$a \bmod b < b$$ y por lo tanto, la función trabajaría igual que en otro caso.

El código anterior se puede simplificar utilizando un condicional ternario hasta hacerlo en una sola línea como sigue:

<textarea class="cpp">
int gcd(int a, int b) { return b == 0 ? a : gcd(b, a % b); }</textarea>

Aunque también podemos utilizar la función `__gcd(int a, int b)` de la librería `algorithm`, se ha visto que la función no se comparta de manera adecuada cuando maneja $$0$$ en alguno de los argumentos. Además, en la ejecución es más rápido el método que aquí se presenta, por esto recomendaría memorizar y utilizar la función `gcd()` como se ha puesto en una línea para su uso en competencias de programación.

## Mínimo Común Múltiplo

Abreviado como MCM o LCM (por sus siglas en inglés *Least o Lowest Common Multiple*), el Mínimo Común Múltiplo es el múltiplo más chico que comparten dos números naturales. En otras palabras el MCM $$m$$ de $$a$$ y $$b$$ es el entero más chico que cumple que $$a \mid m$$ y $$b \mid m$$. Su cálculo y uso está muy relacionado con el MCD, pues de hecho se puede calcular uno en base al otro.

Se ha demostrado que el $$lcm(a, b) = a * b / gcd(a,b)$$, entonces podemos calcular el MCM en función del MCD. Aquí es importante considerar el orden en el que se realizan las operaciones al momento de implementarlo en nuestro código, pues si se realiza el cálculo con enteros muy grandes y realizamos primero `a * b` entonces podríamos tener un *overflow*. La operación es más segura si se realiza de esta forma:

<textarea class="cpp">
int lcm(int a, int b) {     // La función recibe dos enteros
    int c = b / gcd(a, b);  // Se calcula primero la división 
    return a * c;           // Ahora se calcula el producto
}</textarea>

Si realizamos primero la división de $$b$$ entre $$gcd(a, b)$$ entonces estaremos trabajando con un resultado menor o igual a $$b$$, de esta forma evitamos tener un desbordamiento en la mayoría de los casos. De cualquier forma, es importante siempre considerar los límites de nuestras variables para poder manejarlas adecuadamente. El código anterior se puede simplificar también a una sola línea:

<textarea class="cpp">
int lcm(int a, int b) { return a * (b / gcd(a, b)); }</textarea>

Nota la importancia de los paréntesis para marcar un orden en las operaciones. Ese orden puede hacer toda la diferencia cuando se trabaja con enteros de *32 bits* o con entradas muy grandes.

El mínimo común múltiplo es muy útil cuando se quieren calcular puntos en los que coinciden dos ecuaciones o razones diferentes, por ejemplo cuando se desea saber cada cuándo coinciden dos eventos que se realizan con una periodicidad diferente.

Por último, es importante saber que tanto el **mínimo común múltiplo** como el **mayor común divisor** se calculan con una complejidad $$O(\log_{10} n)$$.
