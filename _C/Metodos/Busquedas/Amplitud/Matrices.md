---
layout: G-Article
title: Búsqueda en amplitud BFS en matrices
date: 2020-01-04 12:00:00
author: rivel_co
tags: [Búsqueda, Algoritmo, Cola]
hide_tags: true
olimpiada: [OMI]
subject: [C++]
prevTopic: "Búsqueda binaria, /C++/Metodos/Busquedas/Binaria/"
nextTopic: "Búsquedas en profundidad, /C++/Metodos/Busquedas/Profundidad/Matrices/"
---

Un caso particular de una búsqueda, es la que se realiza en una matriz a manera de plano cartesiano y en donde buscamos la solución más inmediata a un problema. Este tipo de problemas son típicos y su método de abordaje es en particular útil para comprender otros tipos de búsqueda. Para ellos utilizamos las llamadas ***Búsquedas en amplitud o anchura*** o ***BFS*** por sus siglas en inglés *Breadth First Search*.

{: #ListaContenido}
- Principio de la búsqueda
- Preparando las herramientas
- Implementación iterativa
- Conclusión

## Principio de la búsqueda

En programación, una búsqueda de cualquier tipo no es muy diferente a una real, sin embargo, existen muchas formas de buscar cosas y cada método es el más efectivo en cada tipo de situación. Sin importar el método, siempre estamos buscando ***responder a una pregunta***.

Una analogía útil en la búsqueda en amplitud, es considerar un estante con determinada cantidad de cajones, en cada cajón hay otros cajones más pequeños, y en cada uno otros más pequeños, y así con diferentes grados de *profundidad*. Nosotros estamos buscando un determinado objeto que está dentro de algún cajón. La búsqueda en amplitud nos dice que primero abriríamos todos los cajones del primer nivel, es decir todos los que están inmediatamente a nuestro alcance, luego abrir uno del segundo nivel de cada cajón ya abierto, es decir, iríamos probando de uno por uno, avanzando lentamente en la profundidad de los cajones. No abriríamos todos los de un cajón y luego todos los de otro y luego todos los del siguiente, sino que iríamos avanzando uniforme y gradualmente en los niveles de todos los cajones.

> En una búsqueda en amplitud, revisamos todos los elementos de un mismo nivel de profundidad al mismo tiempo, comenzando por el primer nivel inmediato.

Si lo vemos como un plano cartesiano, y estamos buscando un sitio en ese plano, sería como revisar un paso adelante (posición uno), volver al inicio, buscar un paso hacia atrás (posición dos) y volver, dar uno a la izquierda (posición tres) y volver y luego dar uno a la derecha (posición cuatro) y volver. Ahí ya habríamos revisado todos los ***estados inmediatos*** al estado actual. Para la segunda parte habría que revisar todos los estados inmediatos a todos los estados ya revisados, es decir, habría que ponernos en la posición uno, y de ahí dar un paso en cada dirección, luego ir a la posición dos y dar un paso en cada dirección y así sucesivamente hasta encontrar lo que buscamos. Está de más mencionar que no es necesario buscar dos veces en un mismo punto, si no estuvo en el primer momento, no estará al segundo (normalmente).

> La búsqueda en amplitud es un procedimiento recursivo, pues revisamos todos los estados inmediatos de cada estado y así hasta cubrir todos los estados que existen.

Es importante resaltar que el hecho de que un proceso tenga un principio recursivo, su implementación no forzosamente necesita el uso de recursión como tal; recuerda que la recursión es principalmente una forma de operar.

El método tan específico de la búsqueda en amplitud cobra sentido cuando nos damos cuenta de que minimiza el trabajo que hay que realizar para culminar con la búsqueda. Es decir, la especialidad de la ***búsqueda en amplitud es minimizar*** el proceso de buscar, por lo tanto, se utiliza cuando hay que responder preguntas del tipo <span>¿Cuál es la menor cantidad de pasos necesaria para... ?</span>. Esto tiene sentido si analizamos con más calma el funcionamiento de esta técnica.

Por ejemplo, en nuestra analogía de buscar en los cajones dentro de otros cajones, una pregunta sobre minimizar sería *¿cuál es la menor cantidad de cajones que hay que abrir para encontrar el objeto?* En el funcionamiento de nuestro algoritmo, primero revisamos los estados inmediatos a nuestro estado inicial, es decir, aquellas posiciones que sólo nos costarían $$1$$ operación. Si no lo encontramos ahí, pasamos a revisar los estados inmediatos a los anteriores revisados, es decir, todos los estados que nos costarían $$2$$ operaciones. Así revisamos aumentando la posible cantidad de pasos que se necesita, asegurando que al encontrarlo, sepamos cuál es la mínima cantidad necesaria para resolver nuestra búsqueda.

### Problema general

Un <span>problema genial</span> que es además un clásico muy útil en el aprendizaje de la solución de búsquedas a modo de plano cartesiano, es el problema típicamente llamado "***Saliendo del laberinto***". Para este problema, se expresa en una matriz de caracteres, una especie de mapa, donde determinados caracteres representan los sitios por los que no podemos *avanzar* (comúnmente referidos como *paredes*), y otros caracteres representan los caminos por los que sí podemos avanzar. Además, se indica dónde están los puntos o ***coordenadas*** de inicio y de fin. La respuesta al problema, es decir la cantidad de pasos mínima necesaria para salir del laberinto, si no es posible salir, se indica con un valor control, típicamente $$-1$$. En la mayoría de los problemas, podemos alcanzar sólo las posiciones inmediatas arriba, abajo, a la izquierda y a la derecha, pero como es de esperar, hay muchas variaciones.

> Es muy importante recordar que en una búsqueda afecta demasiado la forma en la que ***guardamos*** e ***indexamos*** los datos.

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

Con lo anterior, podemos anticiparnos a decir que las dimensiones del mapa son variables enteras, mientras que el mapa en sí, es una ***matriz de caracteres***. <span>Genial, ahora que sabemos cómo guardar e interpretar la entrada, podemos pasar a la codificación de la solución.</span> Recordemos que algo crucial es interpretar el mapa como un plano cartesiano, esto nos simplifica la vida bastante. Ahora, recordemos, como siempre, que una búsqueda siempre se compone de estados, y con lo que trabajamos en la búsqueda es precisamente con esos estados, entonces es también muy importante definir una forma sencilla de manejar cada característica de cada estado.

Para las ***características de un estado*** en un problema de este tipo, vamos a considerar obviamente, el punto en el que estamos, es decir, la ***posición*** del mapa que estamos revisando para así poder conocer los estados próximos, que corresponden a las posiciones contiguas. Entonces por cada estado, habrá que recordar la coordenada en $$x$$ y la coordenada en $$y$$ (recuerda que lo estamos visualizando como un plano cartesiano). La otra característica muy importante, es la cantidad de operaciones que hemos realizado hasta ese estado, es decir, la ***distancia*** que hemos recorrido para llegar a esa posición. Para esas tres características, resulta muy útil crear una estructura o clase que las contenga. Para este ejemplo utilizaremos clases.

<textarea class="cpp">
class estado{
  public:
    int x;  // Coordenada en x
    int y;  // Coordenada en y
    int d;  // Distancia recorrida
    estado(int ix, int iy, int id){     // Constructor
        x = ix, y = iy, d = id;
    }
};</textarea>

Ahora hay que considerar la forma en la que vamos a ir procesando cada estado. Como recordarás, hay que seguir un orden bien definido, conforme avanzamos en cada estado posible. Primero analizamos los estados inmediatos a la posición actualmente revisada, el orden en el que analizamos esos estados de igual número de operaciones, es en realidad irrelevante (al menos en este caso). Sin embargo, sabemos que después de estos, van los que requieren una operación más, luego los que requieren otra más y así sucesivamente. Es como ir ***formando*** cada dato. <span>Seguro que ahora ya tienes una idea de la manera a procesar.</span> Dado que iremos formando cada dato e iremos procesando en el orden en el que alcanzaos cada uno, lo más recomendable es utilizar una estructura *FIFO*, como la [cola]({{ site.baseurl }}/C++/Estructuras/Contenedores/Cola/ "Implementación de cola"){: target="_blank"}.

Entonces, iremos avanzando a los estados inmediatos o contiguos al nuestro y los iremos metiendo en una cola, de la que iremos tomando los nuevos datos a procesar. Por cada dato a procesar, revisaremos si en esa posición se encuentra lo que buscamos, de no ser así, metemos a la cola los estados inmediatos a ese estado que sean válidos en nuestro problema, y continuamos tomando nuevos estados de la cola y metiendo otros conforme los vamos alcanzando. Recordemos que según la descripción del problema, sólo podemos movernos hacia arriba, abajo, izquierda y derecha, si estamos en el punto `[x][y]`, los anteriores movimientos equivaldrían a `[x][y+1]`, `[x][y-1]`, `[x-1][y]` y `[x+1][y]` respectivamente. Entonces ya sabemos cómo vamos a interpretar la entrada, también acabamos de definir la forma en la que procesaremos cada estado de la búsqueda, falta la otra parte esencial; la forma en la que determinamos si un estado debe ser procesado o no, es decir, las ***podas***.

Como se menciona en el razonamiento del problema, está de más revisar una misma posición más de una vez, si ahí no estaba lo que buscábamos al inicio, no estará si revisamos de nuevo (al menos no en la mayoría de los problemas). Por lo tanto, será bueno recordar qué posiciones ya hemos revisado, para no revisarlas de nuevo. Además, sabemos de antemano, que no podremos revisar posiciones externas al mapa, es decir, que caigan fuera de los límites de nuestra matriz-plano-cartesiano. Tampoco sería buena idea procesar las paredes o los puntos por los que no podemos circular, pues no tiene sentido por definición del problema. En base a todo esto, sabremos que usaremos estructuras como:

<textarea class="cpp">
char mapa[MAX][MAX];            // Mapa
bool visitado[MAX][MAX];        // Mapa de visitados
queue&lt;estado&gt; cola;             // Cola con los estados a revisar
int movx[4] = {1, -1, 0, 0};    // Posibles movimientos en x
int movy[4] = {0, 0, 1, -1};    // Posibles movimientos en y</textarea>

Como puedes ver, hemos definido la matriz que será el mapa (`mapa`) por defecto con las dimensiones máximas de filas y columnas, además otra matriz de las mismas dimensiones (`visitado`) que nos ayudará a saber si hemos estado o no en esa posición antes, ésta es una matriz de booleanos, pues sólo hay que saber si ya se procesó o no esa locación. También está la cola de estados (`cola`), que será donde almacenaremos los estados a procesar. Al final se agregan dos arreglos de cuatro locaciones, con valores ya asignados (`movx` y `movy`), estos arreglos nos ayudarán a alternar en las posibles direcciones en las que podemos desplazarnos.

## Implementación iterativa

<textarea class="cpp">
#include &lt;iostream&gt;
#include &lt;queue&gt;
#define MAX 1000
using namespace std;

char mapa[MAX][MAX];            // Mapa
bool visitado[MAX][MAX];        // Mapa de visitados
int movx[4] = {1, -1, 0, 0};    // Posibles movimientos en x
int movy[4] = {0, 0, 1, -1};    // Posibles movimientos en y

class estado{
  public:
    int x;  // Coordenada en x
    int y;  // Coordenada en y
    int d;  // Distancia recorrida
    estado(int ix, int iy, int id){     // Constructor
        x = ix, y = iy, d = id;
    }
};

queue&lt;estado&gt; cola;             // Cola con los estados a revisar

int main(){
    int iniciox,    // Inicio en x
        inicioy,    // Inicio en y
        filas,      // Filas en el mapa
        columnas;   // Columnas en el mapa

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

    int pasos = BFS(filas, columnas, iniciox, inicioy);

    if (pasos == -1){
        cout << "Error 404: Destino not found\n";
    } else {
        cout << "Minima cantidad de pasos: "<< pasos << '\n';
    }
    
    return 0;
}</textarea>

Nota que hemos definido con mayor detalle la forma en la que se registra la entrada, las variables que estamos usando en este ejemplo y la forma en la que identificamos y registramos el punto de inicio. Hemos citado a una función llamada `BFS` que recibe como parámetros el tamaño de nuestro mapa y las coordenadas iniciales o de partida. Además, damos por hecho de que nuestra función `BFS` regresa $$-1$$ si no ha encontrado una solución al problema, cualquier otra cosa distinta a ese $$-1$$ será la cantidad mínima de pasos necesarios para salir del laberinto. Ahora sí podemos pasar a definir la función de búsqueda `BFS`.

### Estructura de la búsqueda

Como ya hemos mencionado, lo primero es comenzar por nuestro estado inicial, el cual se genera a partir de las coordenadas iniciales, hasta ese punto hemos recorrido una distancia de $$0$$ pues aún no hacemos nada. Ese estado debe ingresar a la cola de procesamiento y mientras tengamos un estado que procesar haremos los siguiente:

- Sacaremos el siguiente elemento a ser procesado (el del frente de la cola).
- Revisaremos si en esa posición está lo que buscamos, de ser así devolvemos la distancia que hemos recorrido hasta ese momento y terminamos, sino continuamos.
- Marcamos la posición actual como visitada en nuestra matriz encargada de ello, pues es justo ese dato el que estamos procesando, ya no hay que pasar de nuevo por ahí.
- Ahora pasamos a evaluar si los cuatro posibles lados adyacentes (estados inmediatos al estado actual) son válidos.
- Para eso determinamos una nueva posible posición, por ejemplo, arriba de la actual.
- Si esa nueva posición está dentro de nuestro mapa, no ha sido visitada, y es una casilla en la que sí podemos circular, entonces creamos un estado con esas nuevas coordenadas válidas y con la distancia nueva para llegar ahí, que sería una unidad más que la distancia actual recorrida.
- Una vez creado y configurado el nuevo estado, lo metemos en la cola de procesamiento. Hacemos lo mismo con todos los estados inmediatos.
- Dejamos que nuestra iteración encuentre la solución. 
- Si se terminaron los estados que se podían revisar en todo el mapa, y nunca regresamos una distancia, entonces regresamos un $$-1$$ como señal de que no se puede salir del laberinto.

La función que realiza lo anterior puede ser:

<textarea class="cpp">
int BFS(int h, int l, int x, int y){
    estado inicial(x, y, 0);    // Estado inicial con coordenadas iniciales y 0 pasos dados

    cola.push(inicial);         // El estado inicial es el primero en procesar

    while(!cola.empty()){       // Mientras existan estados por revisar
        estado actual = cola.front();       // Sacamos el estado a procesar
        cola.pop();                         // Sacamos ese estado de la cola
        if (mapa[actual.x][actual.y] == 'F'){   // Con 'F' como caracter que marca la salida
            return actual.d;        // Regresamos el número de pasos dados
        }

        visitado[actual.x][actual.y] = true;    // Marcamos como visitada la casilla actual
        for (int i=0; i<4; i++){                // Probamos por validar los posibles cuatro movimientos
            int nuevox = actual.x + movx[i];    // Modificamos con posibles cambios en x
            int nuevoy = actual.y + movy[i];    // Modificamos con posibles cambios en y

            if (nuevox >= 0 && nuevox < l && nuevoy >= 0 && nuevoy < h){    // Revisamos que esté en los límites
                if (!visitado[nuevox][nuevoy] && mapa[nuevox][nuevoy] != '#'){  // Revisamos que no esté visitado y que no sea pared
                    estado nuevo(nuevox, nuevoy, actual.d + 1);     // Creamos el nuevo estado válido con un paso más
                    cola.push(nuevo);
                }   
            }
        }
    }
    return -1; // Si no encontró una forma de llegar al objetivo, regresamos un número control conocido
}</textarea>

Nota la forma tan genial en que generamos los cuatro posibles nuevos estados inmediatos, apoyándonos en nuestros pequeños arreglos de movimientos en ambas dimensiones.

El código completo de esta solución es:

<textarea class="cpp">
#include &lt;iostream&gt;
#include &lt;queue&gt;
#define MAX 1000
using namespace std;

char mapa[MAX][MAX];            // Mapa
bool visitado[MAX][MAX];        // Mapa de visitados
int movx[4] = {1, -1, 0, 0};    // Posibles movimientos en x
int movy[4] = {0, 0, 1, -1};    // Posibles movimientos en y

class estado{
  public:
    int x;  // Coordenada en x
    int y;  // Coordenada en y
    int d;  // Distancia recorrida
    estado(int ix, int iy, int id){     // Constructor
        x = ix, y = iy, d = id;
    }
};

queue&lt;estado&gt; cola;             // Cola con los estados a revisar

int BFS(int h, int l, int x, int y){
    estado inicial(x, y, 0);    // Estado inicial con coordenadas iniciales y 0 pasos dados

    cola.push(inicial);         // El estado inicial es el primero en procesar

    while(!cola.empty()){       // Mientras existan estados por revisar
        estado actual = cola.front();       // Sacamos el estado a procesar
        cola.pop();                         // Sacamos ese estado de la cola
        if (mapa[actual.x][actual.y] == 'F'){   // Con 'F' como caracter que marca la salida
            return actual.d;        // Regresamos el número de pasos dados
        }

        visitado[actual.x][actual.y] = true;    // Marcamos como visitada la casilla actual
        for (int i=0; i<4; i++){                // Probamos por validar los posibles cuatro movimientos
            int nuevox = actual.x + movx[i];    // Modificamos con posibles cambios en x
            int nuevoy = actual.y + movy[i];    // Modificamos con posibles cambios en y

            if (nuevox >= 0 && nuevox < l && nuevoy >= 0 && nuevoy < h){    // Revisamos que esté en los límites
                if (!visitado[nuevox][nuevoy] && mapa[nuevox][nuevoy] != '#'){  // Revisamos que no esté visitado y que no sea pared
                    estado nuevo(nuevox, nuevoy, actual.d + 1);     // Creamos el nuevo estado válido con un paso más
                    cola.push(nuevo);
                }   
            }
        }
    }
    return -1; // Si no encontró una forma de llegar al objetivo, regresamos un número control conocido
}

int main(){
    int iniciox,    // Inicio en x
        inicioy,    // Inicio en y
        filas,      // Filas en el mapa
        columnas;   // Columnas en el mapa

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

    int pasos = BFS(filas, columnas, iniciox, inicioy);

    if (pasos == -1){
        cout << "Error 404: Destino not found\n";
    } else {
        cout << "Minima cantidad de pasos: "<< pasos << '\n';
    }
    
    return 0;
}</textarea>

Si probamos la entrada planteada al principio del tema obtendremos como salida `Minima cantidad de pasos: 8` que es nada más y nada menos que la respuesta esperada. Cualquier otra forma de llegar al destino requiere de al menos `8` pasos. Si probamos con una entrada que no tenga solución, notaremos que el código arriba regresa el error de no encontrado. Para que tengas más en claro la forma en la que nuestra búsqueda procesa los estados, puedes ver cómo asignó una cantidad de pasos a cada casilla. Nuestro programa habrá visto el mapa así:

<textarea class="output">
0  2  1  0  13 12 11 10 9  0
0  1  I  1  0  0  0  0  8  9
0  2  1  2  3  4  5  6  7  8
4  3  0  3  4  0  6  0  8  0
5  0  0  4  5  0  7  F  9  0
6  7  0  5  6  7  8  9  10 0
7  8  0  0  0  8  9  10 0  0
8  9  0  11 10 9  10 0  0  0</textarea>

Los espacios donde hay un 0 son los lugares que no podemos alcanzar, ya sea porque hay una pared o porque están encerrados por ellas. Si aún no te resulta muy claro, puedes probar sin poner paredes, y de la misma forma verás cuántos pasos se requieren para ir de la casilla con `I` hasta cualquier otro punto. El siguiente mapa de pasos se generó en base a una entrada idéntica a la de ejemplo pero sin paredes. 

<textarea class="output">
3  2  1  2  3  4  5  6  7  8
2  1  I  1  2  3  4  5  6  7
3  2  1  2  3  4  5  6  7  8
4  3  2  3  4  5  6  7  8  9
5  4  3  4  5  6  7  F  9  10
6  5  4  5  6  7  8  9  10 11
7  6  5  6  7  8  9  10 11 12
8  7  6  7  8  9  10 11 12 13</textarea>

Así es como nuestra búsqueda va relacionando las distancias de todos los estados en base a las direcciones en que podemos avanzar. <span>Genial ¿no es así?</span>

## Conclusión

La búsqueda en amplitud o BFS cumple con el principio de cualquier otro tipo de búsqueda, debemos de considerar distintos ***estados*** existentes, las formas en las que se ***relacionan*** los diferentes estados, y cómo evaluar cuando un estado es válido y cuando no lo es, es decir las ***podas*** que podemos realizar. Además la BFS nos devuelve el mínimo de las distintas soluciones a una búsqueda, gracias al orden en el que se deja pendiente la evaluación de cada estado. Es importante no perder de vista lo que se está buscando y terminar nuestra función en ese momento para no perder más tiempo.

> La BFS es la búsqueda veloz y nos sirve para encontrar la solución más inmediata a un problema.