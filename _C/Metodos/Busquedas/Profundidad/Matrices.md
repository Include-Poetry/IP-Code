---
layout: G-Article
title: Búsqueda en profundidad DFS en matrices
author: rivel_co
tags: [Búsqueda, Recursión, Algoritmo]
Hide_Tags: true
olimpiada: [OMI]
subject: [C++]
---

Como recordarás, en la búsqueda en amplitud en matrices, encontramos el camino más corto desde un estado hasta otro pasando sólo por estados válidos en el recorrido, sin embargo, ese camino mínimo no es el único que hay. Para encontrar ***todas las formas posibles*** de resolver una búsqueda, es necesaria una ***búsqueda en profundidad*** o ***DFS*** por sus siglas en inglés *Depth First Search*.

{: #ListaContenido}
- Principio de la búsqueda
- Preparando las herramientas
- Implementación recursiva
- Conclusión

## Principio de la búsqueda

En el problema para salir de un laberinto, pudimos encontrar el camino más corto necesario para salir del laberinto, utilizando una [búsqueda en amplitud]({{ site.baseurl }}/C++/Metodos/Busquedas/Amplitud/Matrices/ "Algoritmo BFS"){: target="_blank"}. Si quisiéramos conocer todas las formas posibles de salir del laberinto, es decir, todos los diferentes caminos que podemos tomar en la resolución de un problema, podemos usar una búsqueda en profundidad. La búsqueda en profundidad se apoya en la ***recursión*** principalmente y en la capacidad de ***regresar*** en esa recursión y necesitaremos regresar en la recursión si queremos corregir el camino que ya hemos tomado.

> Por la naturaleza de la búsqueda en profundidad, el tiempo de ejecución necesario para dar todas las posibles formas de resolver un problema, suele ser mucho más alto que una búsqueda en amplitud.

La forma en la que la DFS funciona es muy sencilla, si retomamos nuestra analogía de los cajones que dentro tienen más cajones y más cajones en cada cajón, podemos realizar una búsqueda en profundidad abriendo el primer cajón del estante inicial, luego el primero del estante dentro del nuevo cajón y luego el primero de ese y así sucesivamente. En algún momento abriremos un cajón que ya no tendrá cajones dentro, es decir ya no podremos seguir yendo más profundo. En ese momento, salimos de ese cajón y abrimos el siguiente, es decir, dado que hemos estado abriendo el primer cajón de cada nivel, el primero de todos los estados inmediatos, una vez que ya no podamos abrir ese primer estado, podremos abrir el segundo y continuar. Es decir, podemos dar un paso atrás y continuar con el segundo estado inmediato. Ese paso atrás, es precisamente ***volver en la recursión***.

### Problema general

Esta es una variante del problema "***Saliendo del laberinto***". Para esta variante, se expresa en una matriz de caracteres, una especie de mapa, donde determinados caracteres representan los sitios por los que no podemos *avanzar* (comúnmente referidos como *paredes*) y otros caracteres representan los caminos por los que sí podemos avanzar. Además, se indica dónde están los puntos o ***coordenadas*** de inicio y de fin. La respuesta al problema, es mencionar a cantidad total de formas que existen para salir del laberinto, en otras palabras, decir cuántos caminos diferentes se pueden tomar para salir.

## Preparando las herramientas

El primer paso es darnos una idea sobre cómo vamos a interpretar la entrada, una entrada clásica para este tipo de problemas es algo como sigue:

<textarea class="output">
10 8
#..#.....#
#.I.####..
#.........
..#..#.#.#
.##..#.F.#
..#......#
..###...#.
..#....##.</textarea>

Como seguramente puedes intuir, los primeros dos enteros expresan la cantidad de columnas y de filas respectivamente. Los caracteres `#` son "paredes" o puntos a los que no podemos acceder, menos atravesar. Los `.` son sitios por donde podemos pasar y los caracteres `I` y `F` marcan los puntos de inicio y fin respectivamente.

Con lo anterior, podemos anticiparnos a decir que las dimensiones del mapa son variables enteras, mientras que el mapa en sí, es una ***matriz de caracteres***. Recordemos que algo crucial es interpretar el mapa como un plano cartesiano, esto nos simplifica la vida bastante. Ahora, recordemos que una búsqueda siempre se compone de estados y con lo que trabajamos en la búsqueda es precisamente con esos estados, entonces es también muy importante definir una forma sencilla de manejar cada característica de cada estado. Es muy muy importante recordar que utilizaremos la recursión para poder regresar en nuestros posibles caminos, por lo que iremos recordando cada estado anterior gracias a los ***parámetros de la recursión***.

Además de nuestra matriz de caracteres, necesitaremos otra matriz de iguales medidas que nos diga las posiciones de las que venimos, para no regresar a ellas. Esto evitará que pasemos más de una vez por el mismo lugar y principalmente que nos quedemos en un ciclo interminable de dar un paso adelante y un paso hacia atrás. Cada que terminemos de analizar todos los posibles estados de una determinada posición, podemos quitar esa marca de casilla visitada, para que esa casilla pueda ser utilizada al trazar nuevos caminos.

## Implementación recursiva

Según lo anteriormente dicho, sólo nos falta realizar la búsqueda. Hasta ahora tenemos nuestra solución del siguiente modo:

<textarea class="editor">
#include &lt;iostream&gt;
#define MAX 1000
using namespace std;

char mapa[MAX][MAX];            // Mapa
bool visi[MAX][MAX];            // Posiciones temporalmente visitadas
int filas, columnas;            // Dimensiones del mapa
int formas;                     // Número de formas posibles

int main(){
    int iniciox,    // Inicio en x
        inicioy;    // Inicio en y

    cin >> columnas >> filas;

    /* ------- Leemos el tablero ---------*/
    for (int i=0; i<filas; i++){
        for (int j=0; j<columnas; j++){
            cin >> mapa[j][i];
            if (mapa[j][i] == 'I'){     // 'I' como indicador de inicio
                iniciox = j;    // Coordenada de inicio en x
                inicioy = i;    // Coordenada de inicio en y
            }
        }
    }

    // Aquí realizamos la búsqueda en profundidad

    cout << "Formas de salir: "<< formas << '\n';   // Mostramos el número total de formas
    
    return 0;
}</textarea>

### Estructura de la búsqueda

La forma en la que la búsqueda funcionará debe estar perfectamente regulada, para evitar cualquier ciclo infinito en la recursión. El principio a seguir es el siguiente:

- La función de búsqueda no regresa ningún valor, sino que durante la recursión irá modificando el valor final de la solución sin revertirlo jamás.
- Se considerará un estado como válido si no cumple ninguna de las condiciones que lo marcarían como inválido (<span>lógicamente</span>).
- Cada que un estado sea considerado válido, marcaremos la posición de ese estado como visitada, para no volver a pasar por esa posición en el camino actual.
- Cuando terminemos de explorar todos los caminos que se pueden generar a partir de una casilla, podemos marcar esa casilla como no visitada, para que pueda ser utilizada por nuevos caminos.
- La generación de cada nuevo camino será generada en llamadas recursivas individuales y seriadas, de esa forma por cada dirección que tomemos, dejaremos pendiente en la recursión el resto de las direcciones.
- Cuando lleguemos a la casilla de fin, podemos aumentar nuestro contador de formas posibles y regresar en la recursión, pues no es necesario explorar estados a partir del estado meta o final.

<textarea class="editor">
void DFS(int x, int y){
    /* ----------- Creación de los posibles estados ----------- */
    DFS(x+1, y);                // Probamos avanzando hacia la derecha
    DFS(x, y+1);                // Probamos avanzando hacia abajo
    DFS(x-1, y);                // Probamos avanzando hacia la izquierda
    DFS(x, y-1);                // Probamos avanzando hacia arriba    

    /* De esta forma, cada que generamos una nueva posición, dejamos en espera continuar 
       con las otras tres posibles posiciones. */
    return;
}</textarea>

<textarea class="editor">
void DFS(int x, int y){
    /* ------------ Determinación de un estado válido ------------ */
    // Si nos salimos de los límites o si es una casilla no válida o es la casilla de la que venimos
    if (x < 0 || y < 0 || x >= columnas || y >= filas || mapa[x][y] == '#' || visi[x][y]){
        return;                 // No continuamos buscando en esta casilla y regresamos
    }

    // Si hemos llegado hasta este punto es porque el estado actual dado por x,y es válido

    DFS(x+1, y);                // Probamos avanzando hacia la derecha
    DFS(x, y+1);                // Probamos avanzando hacia abajo
    DFS(x-1, y);                // Probamos avanzando hacia la izquierda
    DFS(x, y-1);                // Probamos avanzando hacia arriba    
    return;
}</textarea>

<textarea class="editor">
void DFS(int x, int y){
    // Si nos salimos de los límites o si es una casilla no válida o es la casilla de la que venimos
    if (x < 0 || y < 0 || x >= columnas || y >= filas || mapa[x][y] == '#' || visi[x][y]){
        return;                 // No continuamos buscando en esta casilla y regresamos
    }
    
    visi[x][y] = true;          // Marcamos como temporalmente visitada la casilla actual
    
    DFS(x+1, y);                // Probamos avanzando hacia la derecha
    DFS(x, y+1);                // Probamos avanzando hacia abajo
    DFS(x-1, y);                // Probamos avanzando hacia la izquierda
    DFS(x, y-1);                // Probamos avanzando hacia arriba
    
    // Cuando hemos terminado de revisar todo una casilla en todas direcciones
    visi[x][y] = false;         // quitamos su marca temporal de visitado
    
    return;
}</textarea>

<textarea class="editor">
/* -------------------------- función completa de búsqueda -------------------------- */
void DFS(int x, int y){
    // Si nos salimos de los límites o si es una casilla no válida o es la casilla de la que venimos
    if (x < 0 || y < 0 || x >= columnas || y >= filas || mapa[x][y] == '#' || visi[x][y]){
        return;                 // No continuamos buscando en esta casilla y regresamos
    }
    
    if (mapa[x][y] == 'F'){     // Si hemos llegado a la casilla de fin
        formas++;               // Aumentamos la cantidad de formas posibles 
        return;                 // y regresamos
    }
    
    visi[x][y] = true;          // Marcamos como temporalmente visitada la casilla actual
    
    DFS(x+1, y);                // Probamos avanzando hacia la derecha
    DFS(x, y+1);                // Probamos avanzando hacia abajo
    DFS(x-1, y);                // Probamos avanzando hacia la izquierda
    DFS(x, y-1);                // Probamos avanzando hacia arriba
    
    // Cuando hemos terminado de revisar todo una casilla en todas direcciones
    visi[x][y] = false;         // quitamos su marca temporal de visitado
    
    return;
}</textarea>

Así, al final tendremos un código completo como sigue:

<textarea class="editor">
#include &lt;iostream&gt;
#define MAX 1000
using namespace std;

char mapa[MAX][MAX];            // Mapa
bool visi[MAX][MAX];            // Posiciones temporalmente visitadas
int filas, columnas;            // Dimensiones del mapa
int formas;                     // Número de formas posibles

void DFS(int x, int y){
    // Si nos salimos de los límites o si es una casilla no válida o es la casilla de la que venimos
    if (x < 0 || y < 0 || x >= columnas || y >= filas || mapa[x][y] == '#' || visi[x][y]){
        return;                 // No continuamos buscando en esta casilla y regresamos
    }
    
    if (mapa[x][y] == 'F'){     // Si hemos llegado a la casilla de fin
        formas++;               // Aumentamos la cantidad de formas posibles 
        return;                 // y regresamos
    }
    
    visi[x][y] = true;          // Marcamos como temporalmente visitada la casilla actual
    
    DFS(x+1, y);                // Probamos avanzando hacia la derecha
    DFS(x, y+1);                // Probamos avanzando hacia abajo
    DFS(x-1, y);                // Probamos avanzando hacia la izquierda
    DFS(x, y-1);                // Probamos avanzando hacia arriba
    
    // Cuando hemos terminado de revisar todo una casilla en todas direcciones
    visi[x][y] = false;         // quitamos su marca temporal de visitado
    
    return;
}

int main(){
    int iniciox,    // Inicio en x
        inicioy;    // Inicio en y

    cin >> columnas >> filas;

    /* ------- Leemos el tablero ---------*/
    for (int i=0; i<filas; i++){
        for (int j=0; j<columnas; j++){
            cin >> mapa[j][i];
            if (mapa[j][i] == 'I'){     // 'I' como indicador de inicio
                iniciox = j;    // Coordenada de inicio en x
                inicioy = i;    // Coordenada de inicio en y
            }
        }
    }

    DFS(iniciox, inicioy);      // Realizamos la búsqueda en profundidad

    cout << "Formas de salir: "<< formas << '\n';   // Mostramos el número total de formas
    
    return 0;
}</textarea>

Es importante notar la importancia de almacenar la solución en una variable externa a la recursión, de no ser así, eventualmente el valor de esa variable volverá a su valor inicial, que no es lo que buscamos. También es importante la forma en la que recordamos los estados anteriores para no volverlos a incluir en una misma solución, en otras palabras, la forma en la que recordamos las posiciones anteriores para no volver a pasar por ahí en un mismo camino.

## Conclusión

Es muy importante tener bien en claro la forma en la que dejar estados pendientes en la recursión nos permite explorar todos los posibles estados. Seguramente has pensado que el código anterior es más corto que el de la búsqueda en amplitud y que también podemos usarlo para ver caminos más cortos o más largos, incluso el promedio de los caminos, sin embargo, el tiempo de ejecución es muchísimo más grande en una búsqueda en profundidad. Por ejemplo, puedes probar en ambas búsquedas una entrada como:

<textarea class="output">
7 7
I......
.......
.......
.......
.......
.......
......F</textarea>

Y decir el camino más corto. La búsqueda en amplitud resolverá el problema en menos de un segundo, sin embargo la búsqueda en profundidad necesitará al rededor de $$ 15 $$ minutos para responder, esto porque buscará todos los posibles caminos y no sólo el menor, es decir explorará los $$575780564$$ diferentes caminos que puedes recorrer para llegar de un punto a otro. Puedes realizar el experimento en tu computadora y ver cuánto tarda uno y otro y ver por cuenta propia el porqué se realiza la BFS para los caminos cortos. Es posible disminuir el tiempo de ejecución de esta búsqueda en este ejemplo de camino más corto realizando ***podas***, por ejemplo no es necesario seguir explorando un camino si en algún momento requiere más pasos que la solución actual. Aún con una poda como esta, el tiempo de ejecución es mucho más elevado.

<div class="Nav">
    <a href="{{ site.baseurl }}/C++/Metodos/Busquedas/Amplitud/Matrices/">Tema anterior</a>
</div>