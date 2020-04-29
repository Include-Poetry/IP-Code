---
layout: G-Article
title: Búsqueda binaria o dicotómica
date: 2020-01-04 12:00:00
author: rivel_co
tags: [Búsqueda, Recursión, Iteración]
hide_tags: true
olimpiada: [OMI]
subject: [C++]
prevTopic: "Búsqueda lineal, /C++/Metodos/Busquedas/Lineales/"
nextTopic: "Búsqueda en amplitud, /C++/Metodos/Busquedas/Amplitud/Matrices/"
---

Uno de los casos más clásicos de búsquedas y que es todo un clásico justamente porque es muy eficiente y su campo de aplicación es muy muy grande es la búsqueda binaria. Sin embargo, es un poco (sólo un poco) más complejo que una búsqueda lineal. Además esta búsqueda resolverá un caso ligeramente distinto a los otros dos algoritmos vistos.

{: #ListaContenido}
- Idea de la búsqueda
- Implementación
- Eficiencia
- Conclusión

## Idea de la búsqueda

La idea del funcionamiento se basa en datos lexicográficamente ordenados. Supongamos un caso en el que los datos se ingresan de forma ***creciente***. Al tener datos ordenados de esta forma, podemos asegurar dos cosas.

> Todos los datos del conjunto se encuentran en un intervalo de tamaños conocido. Donde el primer elemento (el menor) es el ***límite inferior*** (todos los demás datos serán mayores o iguales a él) y el último elemento (el mayor) es el ***límite superior*** del intervalo (todos los demás datos serán menores o iguales a él).

En base a lo anterior, podemos saber, que si por ejemplo, nuestro límite inferior es $$2$$ y nuestro intervalo superior es $$21$$, no encontraremos en nuestro conjunto un valor que no encaje en este intervalo. Por ejemplo, el $$-3$$ no se encontrará, pues es menor que nuestro límite inferior, tampoco se encontrará el $$50$$ pues es un valor más grande que nuestro límite superior. Sin embargo, no podemos conocer a primera vista si el número $$x$$ donde $$ 2 \lt x \lt 21 $$ se encuentra en el conjunto. Pero esto no significa mayor problema, pues utilizando el mismo razonamiento anterior, podemos responder a la pregunta.

Generamos un ejemplo para el caso en el que se pregunta por el número $$x$$ donde $$ lim_{inf} \le x \le lim_{sup} $$, por ejemplo, con el conjunto de datos $$ -2, 0, 1, 3, 4, 7, 10, 25 $$ tenemos $$ lim_{inf} = -2 $$ y $$ lim_{sup} = 25 $$, además se pregunta por la existencia del número $$ x = 15 $$ en el conjunto. El número $$x$$ cae dentro de nuestro intervalo, por lo que no podemos responder inmediatamente, habrá que hacer algo más interesante.

Aplicando el mismo concepto de los intervalos, podemos comenzar con la parte ***binaria*** de la búsqueda utilizando el siguiente razonamiento:

- Dividimos nuestro conjunto en dos, utilizando los intervalos.
- La primer mitad estará comprendida por los elementos que se encuentran de la locación `[0]` a la locación `[mitad]`. Es decir, a la locación en la mitad del arreglo.
- La segunda mitad, estará comprendida por los elementos desde la locación `[mitad]` hasta la locación `[n-1]`.
- Es importante notar que ambas mitades comparten el elemento de en medio.
- A partir de cada nueva mitad, podemos definir dos nuevos intervalos, uno que va de `T[0]` hasta `T[mitad]` y otro que va de `T[mitad]` hasta `T[n-1]`. Nota que para definir los límites de los intervalos ya estamos tomando el valor en la locación y no el número de locación.
- El número $$ x $$ que estamos buscando, deberá caer en uno de los dos intervalos, pues se encuentra en alguna parte del intervalo global (inicial).
- Si por ejemplo $$ x $$ cae en el primer intervalo, es decir su valor es $$ T[0] \le x \le T[mitad] $$ es decir $$ lim_{inf} \le x \le lim_{med} $$ podemos tomar como nuevo límite superior, ese $$ lim_{med} $$, y volver a aplicar el principio anterior.
- Si $$x$$ cae en el segundo intervalo, es decir que su valor se encuentre entre $$ lim_{med} \le x \le lim_{sup} $$, entonces podemos tomar como nuevo índice inferior ese $$ lim_{med} $$ y volver a aplicar el principio anterior.
- Sabremos que hemos encontrado el valor que buscamos, cuando nuestro valor en la locación del medio, sea igual al elemento solicitado, si ya sólo estamos revisando dos elementos, y nuestro valor medio nunca fue igual al valor solicitado, podemos decir que el valor en cuestión no se encuentra en nuestro conjunto.

## Implementación

Para una forma iterativa:

<textarea class="cpp">
#include &lt;iostream&gt;
using namespace std;

int T[100];                     // Arreglo que almacenará los datos

int Binaria(int inicio, int fin, int x){
    int medio;                  // Aquí estará el índice medio
    int inf = inicio;           // El límite inferior
    int sup = fin;              // El límite superior
    
    // Mientras no estemos revisando sólo dos datos y estemos dentro del rango
    while(sup-1 != inf && x > T[inf] && x < T[sup]){
        medio = (sup+inf)/2;        // Valor medio
        
        // La siguiente línea muestra como variaron los límites en la iteración
        // cout << inf << " " << medio << " " << sup << endl;
        
        if (T[medio] == x)          // Si encontramos la coincidencia
            return medio+1;         // devolvemos la posición con su corrección y terminamos
            
        if (x < T[medio])           // Si el valor buscado es menor al punto medio
            sup = medio;            // El nuevo límite superior será la mitad
        
        if (x > T[medio])           // Si el valor buscado es mayor al punto medio
            inf = medio;            // El nuevo límite inferior será la mitad
    }
    
    return -1;                      // Si nunca se encontró nada, devolvemos -1
}

int main(){
    
    int n;                      // Cantidad de números a ingresar
    cin >> n;
    
    for (int i=0; i<n; i++){
        cin >> T[i];            // Rellenamos nuestro arreglo
    }
    
    int x;
    cin >> x;                   // Número por el que se pregunta
    
    cout << Binaria(0, n-1, x); // Búsqueda con el limite inferior, el superior y el valor buscado
    return 0;
}</textarea>

Para una forma recursiva:

<textarea class="cpp">
#include &lt;iostream&gt;
using namespace std;

int T[100]; // Arreglo que almacenará los datos

int Binaria(int inf, int sup, int x){
    int med = (sup+inf)/2;
    
    // La siguiente línea muestra como variaron los límites en la recursión
    //cout << inf << " " << med << " " << sup << endl;
    
    if (T[med] == x)                    // El valor se ha encontrado
        return med+1;                   // Regresamos su posición +1 por el desfase de índice
    
    // Ya sólo estamos checando entre dos elementos o estamos fuera del rango (caso inicial)
    if (sup-1 == inf || x < T[inf] || x > T[sup])
        return -1;                      // No lo encontramos pues lo habríamos regresado arriba
        
    if ( x < T[med] )                   // Revisamos que entre el primer rango 
        return Binaria(inf, med, x);    // seguimos con la búsqueda en la primer mitad, con el medio como superior
    
    if ( x > T[med] )                   // Revisamos que entre el segundo rango 
        return Binaria(med, sup, x);    // seguimos con la búsqueda en la segunda mitad, con el medio como inferior
}

int main(){
    int n;                      // Cantidad de números a ingresar
    cin >> n;
    
    for (int i=0; i<n; i++){
        cin >> T[i];            // Rellenamos nuestro arreglo
    }
    
    int x;                      // Número que buscamos
    cin >> x;
    
    // Se llama la búsqueda dando el valor del límite inferior, el superior y el valor buscado
    cout << Binaria(0, n-1, x); 
    
    return 0;
}</textarea>

Es importante notar que estamos utilizando como límites de cada intervalo los ***índices*** del arreglo y no los valores de cada locación, sin embargo, utilizamos los valores para comparar con el valor buscado. Esto tiene sentido, pues los índices nos dicen de ***dónde a dónde*** estamos buscando, mientras que los valores nos dicen el ***límite exacto*** de cada intervalo. Además, puedes notar que es binaria o dicotómica porque dividimos cada búsqueda en dos partes y en base a un criterio (rangos y límites) seleccionamos una mitad y seguimos buscando. En base a este concepto, no tendrás problema imaginando e implementando una *búsqueda terciaria*, por ejemplo. Considera también, en los ejemplos anteriores se espera que los datos estén en orden creciente, sin embargo, para el orden decreciente es prácticamente lo mismo, seguro que ya sabes qué partes hay que modificar.

## Eficiencia

La búsqueda binaria es sumamente eficiente, en el peor de los casos, para $$N$$ datos, el algoritmo tendrá una complejidad $$O(log N)$$ lo cual es excelente, el logaritmo es una de las mejores complejidades que podemos encontrar en algoritmos. Sin embargo, es necesario que los datos estén ordenados, o que nos sea posible ordenarlos. En el último caso, debemos considerar también la complejidad de nuestro algoritmo de ordenamiento.

## Conclusión

Identifica los mismos aspectos que se señalan en todas las búsquedas, existen distintos **estados** en la búsqueda (los intervalos que estamos revisando) y realizamos **podas** (descartamos uno de los intervalos) en base a **criterios de selección** o condiciones de validez (el valor medio comparado al valor buscado). Al final regresamos el resultado de nuestra búsqueda, ya sea que encontremos el valor o no. Considera que la búsqueda binaria se utiliza no sólo para encontrar valores en un arreglo, sino también para aproximar soluciones de una ecuación, por ejemplo.

Toma en cuenta que la búsqueda binaria es un ejemplo de algoritmo **Divide y Vencerás**, pues fragmentamos el problema en problemas más pequeños, cuya solución de cada parte nos ayuda a construir la solución final. Más adelante se aborda específicamente este tema. Lo más importante de este algoritmo es el simple y eficiente razonamiento que utiliza, ese principio es muy muy útil y por lo tanto debes tenerlo muy en cuenta al resolver un problema.

<span>¿Notas lo genial y parecidas que son las implementaciones recursivas e iterativas en estos ejemplos? Si aún no comprendes del todo la forma en la que la recursión funciona, compara estos métodos recursivos e iterativos, sus semejanzas y diferencias.</span>