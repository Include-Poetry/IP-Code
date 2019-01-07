---
layout: G-Article
title: Contando con parámetros
author: rivel_co
tags: [Recursión, Variables, Parámetros]
Hide_Tags: false
olimpiada: [OMIPS]
subject: [Karel pascal]
---

Es posible que Karel aprenda a contar y memorice ese número para utilizarlo posteriormente. Esta cantidad que Karel cuenta la recuerda como a una [variable]({{ site.url }}/Karel/Recursion/Parametros/ "Idea de variable &vert; #iP Code"). Es importante que sepas que para este artículo ya debes manejar [recursión sencilla]({{ site.baseurl }}/Karel/Recursion/Simple/ "Recursión simple en Karel &vert; #iP Code") y algo de [recursión con parámetros]({{ site.baseurl }}/Karel/Recursion/Parametros/ "Recursión con parámetros en Karel &vert; #iP Code"), pues en sí se mostrarán aquí algunos usos de esos parámetros.

{: #ListaContenido}
- Contando con recursión sencilla
- Vengan los parámetros
- Un método adicional
- Reto adicional

## Contando con recursión sencilla

Imagina que Karel se encuentra ubicado en un mundo sin paredes en el `1, 1` ([coordenadas del mapa]({{ site.baseurl }}/Karel/Principio/Mundo/ "Mundo de Karel &vert; #iP Code"), esquina inferior izquierda) y orientado al norte. Frente a él (`1, 2`) se encuentra un montón con una cantidad $$x$$ de zumbadores. El problema requiere que Karel tome esa cantidad $$x$$ de zumbadores y los ponga una locación adelante (`1, 3`), pero claro, para que el problema sea interesante Karel tiene una cantidad infinita de zumbadores en la mochila. Resolveremos este problema primero con recursión simple y luego utilizando parámetros.

Lo primero que tenemos que haces es idealizar el algoritmo. Comenzamos por darnos cuenta que vamos a quitar la misma cantidad de zumbadores que la que vamos a poner, es decir, si quitamos 6 zumbadores de `1, 2` vamos a poner 6 zumbadores en `1, 3`. Además sabemos que no podemos quitar zumbadores si ya los hemos tomado todos. Entonces con estas dos ideas en mente procedemos a formular la función recursiva.

Lo primero es la **condición recursiva**, vamos a quitar zumbadores *si hay zumbadores para quitar*. Por cada zumbador que tomemos vamos a marcar un *paso en la recursión*. Entonces, si estamos junto a un zumbador lo tomamos y hacemos la **llamada recursiva** para que recordemos esa acción en la *pila de llamadas*. Cuando hayamos terminado de quitar todos los zumbadores vamos a dar un paso adelante (ya sin hacer otra llamada recursiva) y vamos a "*soltar la recursión*", es decir, terminamos la función y permitimos que por cada vez que tomamos uno, dejemos uno.

<div class="karelBlock">
<textarea class="karelp">
iniciar-programa
    define-nueva-instruccion recoge como inicio
        si junto-a-zumbador entonces inicio
            coge-zumbador;
            recoge;
            deja-zumbador;
        fin sino inicio
            avanza;
        fin;
    fin;
    inicia-ejecucion
        avanza;
        recoge;
        apagate;
    termina-ejecucion
finalizar-programa</textarea>
<textarea class="karelj">
class program{
    define recoge(){
        if (nextToABeeper){
            pickbeeper();
            recoge();
            putbeeper();
        } else {
            move();
        }
    }
    program(){
        move();
        recoge();
        turnoff();
    }
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Con la línea 12 nos ubicamos en el montón de zumbadores, luego en la 13 llamamos a la función recursiva. Lo primero que hacemos es verificar que estamos sobre un zumbador, es decir, verificar que se pueden quitar más zumbadores, esta es la *condición de la recursión* y lo hacemos en la línea 3. Si esto se cumple entramos a la línea 4 donde tomamos un zumbador (sólo uno) y volvemos a llamar a la recursión en la 5. Otra vez comprobamos que hayan zumbadores para quitar y seguimos quitando. Nota en la pila de llamadas que cada vez que quitamos un zumbador dejamos pendiente dejar uno (línea 6).

Cuando ya no se cumple la condición de la recursión es porque ya hemos quitado todos los zumbadores del lugar, lo que hacemos entonces es ir a la línea 8 donde nos ubicamos en la posición donde hay que dejar la misma cantidad. Ya que estamos ahí dejamos que la función termine y entonces se *vacíe* la pila de llamadas (lo que me refería con *soltar la recursión*) y entonces por cada vez que llamamos a `recoge` estaremos dejando un zumbador. Nota aquí que cada que quitamos un zumbador llamamos a `recoge` y que cada que llamamos a `recoge` dejaremos un zumbador, entonces **cada vez que quitamos un zumbador vamos a dejar uno**. Listo, problema resuelto.

## Vengan los parámetros

Resulta que el problema anterior ya te resulta demasiado sencillo, entonces aumentamos la dificultad. El problema se mantiene igual excepto que ahora queremos dejar la cantidad $$x$$ de zumbadores que había al principio no sólo en la casilla de arriba, sino también en el origen `1, 1` y en la casilla inmediatamente al este (`2, 1`).

Si lo piensas un poco puedes notar que este problema lo podemos resolver con recursión sencilla, pero necesitamos una función especial para cada nueva ubicación de zumbadores. Es decir, debemos contar y dejar siempre que queramos dejarlos en un lugar diferente. Pero si Karel recordara la cantidad de zumbadores a dejar entonces bastaría con contar una vez y solamente ubicarnos en cada nueva posición y dejar la cantidad necesaria de zumbadores.

Para resolver el problema vamos a proceder prácticamente igual que con la recursión sencilla pero cada vez que tomemos un zumbador vamos a **incrementar** el valor del parámetro `x` (que **inicialmente deberá ser** $$0$$), para cuando la recursión termine tendremos un parámetro que es igual a la cantidad de zumbadores que había.

<div class="karelBlock">
<textarea class="karelp">
iniciar-programa
    define-nueva-instruccion recoge(x) como inicio
        si junto-a-zumbador entonces inicio
            coge-zumbador;
            recoge(sucede(x));
        fin;
    fin;
    inicia-ejecucion
        avanza;
        recoge(0);
        apagate;
    termina-ejecucion
finalizar-programa</textarea>
<textarea class="karelj">
class program{
    define recoge(x){
        if (nextToABeeper){
            pickbeeper();
            recoge(succ(x));
        }
    }
    program(){
        move();
        recoge(0);
        turnoff();
    }
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

El código anterior está incompleto, pero realiza la recursión y utilizando `sucede | succ` incrementa el valor de la variable  `x` (línea 5). Lo único que falta es recorrer los lugares donde hay que dejar los zumbadores y dejar una cantidad $$x$$ en cada uno, esto último lo haremos con una simple función `repetir x veces | iterate (x)`. Recuerda que para este punto la recursión ya no es necesaria, solamente debemos modificar un `sino | else` para el `si | if` de la línea 3. Nota que llamamos a `recoge()` desde la función principal dándole $$x$$ el valor inicial de $$0$$ (línea 11).

<div class="karelBlock">
<textarea class="karelp">
iniciar-programa
    define-nueva-instruccion recoge(x) como inicio
        si junto-a-zumbador entonces inicio
            coge-zumbador;
            recoge(sucede(x));
        fin sino inicio
            avanza;
            repetir x veces deja-zumbador;

            mientras no-orientado-al-sur hacer gira-izquierda;
            mientras frente-libre hacer avanza;
            repetir x veces deja-zumbador;

            mientras no-orientado-al-este hacer gira-izquierda;
            avanza;
            repetir x veces deja-zumbador;
        fin;
    fin;
    inicia-ejecucion
        avanza;
        recoge(0);
        apagate;
    termina-ejecucion
finalizar-programa</textarea>
<textarea class="karelj">
class program{
    define recoge(x){
        if (nextToABeeper){
            pickbeeper();
            recoge(succ(x));
        } else {
            move();
            iterate (x) putbeeper();

            while (notFacingSouth) turnleft();
            while (frontIsClear) move();
            iterate (x) putbeeper();

            while (notFacingEast) turnleft();
            move();
            iterate (x) putbeeper();
        }
    }
    program(){
        move();
        recoge(0);
        turnoff();
    }
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

En la línea 7 nos ubicamos en la primer nueva ubicación, dejamos los $$x$$ zumbadores con la línea 8 luego en la línea 10 y 11 nos ubicamos en el `1, 1` y dejamos $$x$$ zumbadores. Al final nos ubicamos en `2, 1` con las líneas 13 y 14 y dejamos los últimos $$x$$ zumbadores. Listo, problema resuelto.

## Un método adicional

También podemos pasar el valor de un parámetro de una función a otra. En realidad esto ya lo hemos hecho al momento de que desde la función principal llamamos por primera vez a `recoge()`, ese primer valor fue $$0$$. Ahora vamos a pasar el parámetro $$x$$ a una tercer función llamada `deja()`;

<div class="karelBlock">
<textarea class="karelp">
iniciar-programa
    define-nueva-instruccion deja(z) como inicio
        avanza;
        repetir z veces deja-zumbador;

        mientras no-orientado-al-sur hacer gira-izquierda;
        mientras frente-libre hacer avanza;
        repetir z veces deja-zumbador;

        mientras no-orientado-al-este hacer gira-izquierda;
        avanza;
        repetir z veces deja-zumbador;
    fin;
    define-nueva-instruccion recoge(x) como inicio
        si junto-a-zumbador entonces inicio
            coge-zumbador;
            recoge(sucede(x));
        fin sino inicio
            deja(x);
        fin;
    fin;
    inicia-ejecucion
        avanza;
        recoge(0);
        apagate;
    termina-ejecucion
finalizar-programa</textarea>
<textarea class="karelj">
class program{
    define deja(z){
        move();
        iterate (z) putbeeper();

        while (notFacingSouth) turnleft();
        while (frontIsClear) move();
        iterate (z) putbeeper();

        while (notFacingEast) turnleft();
        move();
        iterate (z) putbeeper();
    }
    define recoge(x){
        if (nextToABeeper){
            pickbeeper();
            recoge(succ(x));
        } else {
            deja(x);
        }
    }
    program(){
        move();
        recoge(0);
        turnoff();
    }
}</textarea>
<span class="karelLabel KLPascal karelLabelSelected" labFor="karelp">Pascal</span><span class="karelLabel KLJava" labFor="karelj">Java</span>
</div>

Hay que remarcar que `deja()` ni siquiera es una función recursiva, solamente es una función que recibió un parámetro y que hizo algo con él. Además, `deja()` está usando un parámetro que se llama `z` y no `x` como `recoge()` pero también se puedo haber llamado `x` sin problemas.

## Reto adicional

Arriba mencioné que podíamos resolver el último problema utilizando recursión simple, sin embargo habría que contar varias veces los zumbadores. En realidad se puede resolver el problema con recursión sencilla y contando sólo una vez <span>¿se te ocurre como?</span> Pero no basta con resolver el problema con recursión sencilla, también hay que tomar en cuenta el algoritmo que tarde menos y ahí sí resulta ser que utilizando parámetros resolvemos el problema más rápidamente y de una *forma más elegante*. Otros retos adicionales son *dejar el doble de los zumbadores recolectados* tanto con recursión sencilla como con parámetros.