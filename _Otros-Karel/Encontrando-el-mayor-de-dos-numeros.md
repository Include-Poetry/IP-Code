---
layout: G-Article
title: Encontrando el mayor de dos números
date: 2020-01-04 12:00:00
author: rivel_co
tags: [Recursión, Variables, Parámetros]
olimpiada: [OMIPS]
subject: [Karel pascal]
---

Utilizando los parámetros Karel puede encontrar al mayor de dos números, donde cada número está expresado como una cantidad de zumbadores determinada. Aquí estaremos utilizando a `sucede() | succ()`, `precede() | pred()` y `si-es-cero() | iszero()`.  

{: #ListaContenido}
- Descripción del problema
- Contando el primer montón
- Comparando con el segundo montón
- Números iguales
- Reto adicional

## Descripción del problema

Karel se encuentra ubicado en el origen (`1, 1`) orientado al norte. En `1, 2` y `2, 2` se encuentran montones de zumbadores. Karel debe decir cuál de esos dos montones es el mayor. Si el de la derecha es el mayor Karel deberá orientarse al este, si el de la izquierda es mayor Karel deberá terminar orientado al oeste. Se da por hecho que ningún montón de zumbadores es infinito y que ambos montones tienen una diferente cantidad de zumbadores.

Lo primero que tenemos que hacer es que Karel sepa cuántos zumbadores hay en un montón, para esto vamos a contarlos y guardar esa cantidad en un parámetro llamado `x`. Lo que sigue es ir al otro montón y comparar. La comparación se realizará más o menos como hicimos la [búsqueda del nueve]({{ site.bareurl }}/Otros-temas/Karel/Contando-con-parametros/ "Contando con parámetros &vert; #iP Code"). <span>Sencillo ¿no?</span>

## Contando el primer montón

Primero hay que dar un paso al frente para ubicarnos en el primer montón de zumbadores. Lo que sigue es contar *[como ya sabemos]({{ site.bareurl }}/Otros-temas/Karel/Contando-con-parametros/ "Contando con parámetros &vert; #iP Code")* mientras incrementamos el valor de un parámetro. Cuando ya hayamos terminado de contar ese montón nuestro parámetro estará listo y podremos ubicarnos en el siguiente montón y realizar la debida comparación.

<div class="karelBlock">
<textarea class="karelp">
iniciar-programa
    define-nueva-instruccion cuenta(x) como inicio
        si junto-a-zumbador entonces inicio
            coge-zumbador;
            cuenta(sucede(x));
        fin sino inicio
            repetir 3 veces gira-izquierda;
            avanza;
            gira-izquierda;
            compara(x);
        fin;
    fin;
    inicia-ejecucion
        avanza;
        cuenta(0);
        apagate;
    termina-ejecucion
finalizar-programa</textarea>
<textarea class="karelj">
class program{
    define cuenta(x){
        if (nextToABeeper){
            pickbeeper();
            cuenta(succ(x));
        } else {
            iterate (3) turnleft();
            move();
            turnleft();
            compara(x);
        }
    }
    program(){
        move();
        cuenta(0);
        turnoff();
    }
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Nuestro parámetro empieza siendo $$0$$ en la línea 15, en la línea 5 vamos incrementando el valor de nuestro parámetro utilizando `sucede()`. Una vez que terminamos de contar los zumbadores de ese montón nos pasamos al que sigue con las líneas 7, 8 y 9. Al final llamamos a la función `compara()` pasándole el parámetro que es igual a la cantidad de zumbadores en el primer montón (línea 10).

## Comparando con el segundo montón

Ya sabemos cuantos zumbadores hubo en el primer montón, lo guardamos en `x` con la función `cuenta()` y se lo pasamos a `compara()` pero ahora le llamaremos `z`. Lo que haremos ahora es restarle al parámetro `z` la cantidad de zumbadores que vamos recogiendo y utilizando comparaciones sabremos cuál de los dos montones es el mayor, la lógica de las comparaciones es como sigue.

Si el parámetro ya es $$0$$ significa que terminamos de restarle al segundo montón todos los zumbadores del primero y todavía sin acabar con el segundo, por lo tanto el segundo montón es mayor. Si el parámetro todavía no es $$0$$ pero ya no tenemos zumbadores para quitarle al segundo entonces el primero es mayor. Una vez que sabemos lo que ha pasado y lo que eso significa, sólo tenemos que orientarnos según las reglas del problema y listo.

<div class="karelBlock">
<textarea class="karelp">
define-nueva-instruccion compara(z) como inicio
    si no si-es-cero(z) entonces inicio
        si junto-a-zumbador entonces inicio
            coge-zumbador;
            compara(precede(z));
        fin sino inicio
            mientras no-orientado-al-oeste hacer gira-izquierda;
        fin;
    fin sino inicio
        mientras no-orientado-al-este hacer gira-izquierda;
    fin;
fin;</textarea>
<textarea class="karelj">
define compara(z){
    if (!iszero(z)){
        if (nextToABeeper){
            pickbeeper();
            compara(pred(z));
        } else {
            while (notFacingWest) turnleft();
        }
    } else {
        while (notFacigEast) turnleft();
    }
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

En la línea 2 estamos revisando si el parámetro **no es cero**, si **no** es cero entonces todavía no hemos quitado los zumbadores del primer montón y entramos en la línea 3. En esta línea revisamos que podamos tomar todavía zumbadores del segundo. Si sí podemos entonces lo tomamos y restamos $$1$$ al parámetro. Si ya no podemos tomar zumbadores (línea 7) significa que ya no hay más del segundo montón y nos orientamos al oriente. Si por otro lado, ya habíamos terminado de restarle al parámetro entonces el segundo montón es mayor y nos orientamos al este (línea 10).

## Números iguales

Cuando los dos números son iguales lo que hay que hacer es meter otra comparación. Puede que ya hayamos terminado de quitar los `z` zumbadores del primer montón pero que también hayamos terminado de quitar los zumbadores del segundo montón, esto significaría que los dos montones **son iguales**. Aquí habría que establecer otra forma de indicar que los dos números son iguales, orientando a Karel al sur, por ejemplo.

## Reto adicional

Imagina ahora que lo que quieres hacer es encontrar el mayor de todos los números de un mundo de medidas determinadas ¿cuál sería la mejor manera de encontrarlo? Además, ¿se te ocurre una forma de encontrar el mayor de dos números sin utilizar los parámetros? ¿cuál es el método óptimo?