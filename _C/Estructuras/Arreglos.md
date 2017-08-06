---
layout: G-Article
title: Arreglos en C++
author: rivel_co
tags: [Variables compuestas, Arreglos]
Hide_Tags: true
olimpiada: [OMI]
subject: [C++]
---

Así como una variable tipo `int` almacena números enteros, `char` caracteres, `bool` valores booleanos, etc. Se podría decir que existen variables que almacenan, nada más y nada menos que *otras variables*. Esta es una manera de concebir a los *arreglos*.

{: #ListaContenido}
- Creación de una variable
- Declaración de un arreglo
- Inicialización de un arreglo
- Manejo de un arreglo
- Arreglo de caracteres
- Máximo de un arreglo

## Creación de una variable

¿Recuerdas que antes de utilizar el valor de una variable debemos *inicializarla*? Y esto era porque cuando declaramos una variable el compilador le asigna un valor *aleatorio*. La respuesta técnicamente más correcta a esto, es el hecho de como se organiza la memoria de una computadora.

Imagina la memoria como una caja compuesta por muchos pequeños compartimentos cuadrados, organizados como en una gran cuadrícula. En estos compartimentos es donde almacenamos la información. Cuando nosotros declaramos una variable, el compilador busca un espacio de la memoria donde pueda *poner* ese valor, una vez que lo encuentra *anota* dónde lo guardó, y vincula esa dirección de la memoria a un nombre. Ese nombre es el nombre de la variable.

Ese lugar donde el compilador guardará tu variable, es un lugar donde aún hay información, datos de algún proceso ya finalizado, o archivos temporales, por lo que, ese espacio no está del todo vacío, pero sí lo podemos ocupar. Es por eso que las variables no inicializadas tienen un valor *basura*, y es hasta que nosotros inicializamos que ese valor se limpia para guardar ahora el valor que nosotros le dimos.

Cada que nosotros hacemos una referencia en nuestro código a una variable, el compilador va a ese espacio de la memoria y hace las modificaciones que nosotros señalamos. La manera que usa la computadora para seleccionar un espacio de memoria, es digamos, poco organizado, lo que provoca que en la cuadrícula (que imaginamos como la memoria) hayan espacios *huecos* en donde no hay información que se esté usando. En esos espacios huecos es en donde guarda nuestras variables, o más bien los valores de éstas. Este sistema provoca que las variables que declaramos en nuestro programa no queden *juntas*, o más bien dicho, en espacios de memoria [contiguos](http://dle.rae.es/?id=AVOhPla){:target="_blank"}

Por ahora no hay problema que las variables que declaramos no estén una junto a la otra, es decir, de todas maneras el compilador recuerda donde están y gracias a ello todo funciona bien.<br>
Sin embargo, si las variables estuvieran contiguas no tendría que recordar tantas direcciones donde están, pues podría recordar *un bloque* donde las dejó, y ya en ese bloque sería más sencillo ubicar a cada una individualmente.

Bajo este principio es como existen y usamos los arreglos. Como un *conjunto de espacios de memoria contiguos* en donde guardamos nuestros valores. Al usarlos, nos referimos a ese bloque de variables por un nombre, y a cada variable de ese bloque por un índice.

## Declaración de un arreglo

Para declarar un arreglo primero tenemos que decir de qué tipo será, puede ser de cualquiera de los tipos de variables que ya vimos. Luego el nombre que tendrá el arreglo y al final y entre corchetes la cantidad de variables que tendrá este arreglo. Por ejemplo:

<textarea class="editor">
// Declaración de un arreglo
int primero[10];
char segundo[5];
bool otro[22];</textarea>

En estos casos tendremos $$ 10 $$ variables tipo `int`, $$ 5 $$ tipo `char` y $$ 22 $$ tipo `bool`. Ahora, recuerda que el valor de cada variable dentro del arreglo es independiente al resto de los valores de ese mismo arreglo. Para acceder a cada variable individualmente tenemos que mencionar primero su *índice*.

Al manejar arreglos tenemos que tener en mente siempre que son variables ordenadas, una junto a otra en la memoria de la computadora, para tenerlas ordenadas la computadora las numera, esta numeración está [indexada](http://dle.rae.es/?id=LNTIjYS){: target="_blank"} en $$ 0 $$, es decir, está numerada iniciando por el $$ 0 $$. Por lo que el índice de la primer variable del arreglo es $$ 0 $$. Y por lo tanto, el índice de la última variable de nuestro arreglo `primero` es $$ 9 $$. ¿Por qué nueve? Recuerda que empezamos a contar por el $$ 0 $$, para cuando lleguemos al $$ 9 $$, tendremos las $$ 10 $$ variables que declaramos.

## Inicialización de un arreglo

Al igual que cualquier otra variable ya vista, los arreglos y sus locaciones necesitan inicializarse para que podamos empezar a usar sus valores, hay varias maneras:

<textarea class="editor">
// Inicialización 
#include &lt;iostream&gt;
using namespace std;

int main(){
    int arreglo[10]; // Arreglo de 10 "locaciones"
    arreglo[0] = 12;
    arreglo[3] = 5;
    arreglo[8] = 9;
    arreglo[9] = 2;
    cout << arreglo[3] << " ";
    cout << arreglo[0] << " ";
    cout << arreglo[9];
    return 0;
}</textarea>
 

La salida del código anterior es `5 12 2`. Las *locaciones* o variables del arreglo que no inicializamos, al igual que una variable no inicializada, tiene un valor *basura* que no debemos usar. Tampoco debemos usar la locación con índice del tamaño de nuestro arreglo, (en el ejemplo $$ 10 $$), o de un valor mayor, pues ese valor es *inestable* y para nada confiable. Hacer lo que llamamos "*salirse de un arreglo*" (es decir, referirse a una locación mayor o igual al número de locaciones declarado) puede causar muchos errores en el compilador, si necesitas un arreglo más grande, entonces declara uno con más locaciones. En este ejemplo se han inicializado algunas locaciones de manera manual.

También podemos inicializarlo todo de una vez, sin hacer uso de tantas asignaciones, de la siguiente manera:

<textarea class="editor">
// Inicialización de un arreglo
#include &lt;iostream&gt;
using namespace std;

int main(){
    int arreglo[5] = {5, 213, 212, 2312, 21}; 
    cout << arreglo[2] << " ";
    cout << arreglo[0] << " ";
    cout << arreglo[3];
    return 0;
}</textarea>

De esta manera, separamos con comas cada valor dentro de las llaves, estos valores se irán asignando a cada locación, en el mismo orden en el que se especifica dentro de las llaves. De esta manera el programa anterior nos daría la salida `212 5 2312`. También podemos inicializar sólo una parte del arreglo, pero en el mismo orden anterior.

<textarea class="editor">
// Inicialización de un arreglo
#include &lt;iostream&gt;
using namespace std;

int main(){
    int arreglo[5] = {5, 213, 2312}; 
    cout << arreglo[0] << " ";
    cout << arreglo[1] << " ";
    cout << arreglo[2];
    cout << "\n";
    
    char otro[10] = {'A', 'n', '!', 'p'};
    cout << otro[1] << " ";
    cout << otro[3] << " ";
    cout << otro[2];
    return 0;
}</textarea>

La salida del anterior código es `5 213 2312` en la primera línea y `n p !`

## Manejo de un arreglo

En el ejemplo anterior, nos referimos a algunas locaciones del arreglo de manera manual, es decir, nosotros pusimos una constante (un número) para referirnos a su índice. Este método, aunque funciona, es poco práctico, es mejor manejarlo de manera *dinámica*, es decir, usando variables.

Ahora imagina la siguiente situación; necesitas hacer un programa que lea del teclado una 10 números, y que después de haberlos ingresado todos, los muestre en pantalla en el mismo orden en el que fueron ingresados. De manera manual tendríamos que poner $$ 10 $$ `cin` pidiendo en cada una una locación distinta, para después poner $$ 10 $$ `cout` mostrando cada una. Sin embargo de manera dinámica esto sería mucho más sencillo:

<textarea class="editor">
// Uso de un arreglo
#include &lt;iostream&gt;
using namespace std;

int main(){
    int numeros[10], i;
    for (i=0; i < 10; i++){ // Pedimos 10 números
       cin >> numeros[i];
    }
    // Aquí ya terminamos de pedir
    for (i=0; i < 10; i++){ // Mostramos 10 números
       cout << numeros[i] << " ";
    }
    return 0;
}</textarea>

Nota como la variable `i` irá cambiando a medida que el ciclo se repite, y para cada cambio su valor hace referencia a una locación de memoria distinta. De esta manera podemos manejar el arreglo con muy pocas líneas. <span>genial ¿no crees?</span>

## Arreglo de caracteres

El término *arreglo* en realidad se desprende del término original (en inglés) *array* cuya traducción inmediata al español es *formación* u *ordenación*. Sin embargo, para nosotros la palabra *arreglo* también encaja con la descripción que ya dimos.

Tomemos entonces la definición de un arreglo como una composición de partes ordenadas. Ahora, ya vimos que cada parte es una variable. Si estas variables son enteros, tenemos entonces una composición de números enteros. ¿y si estas variables son letras o simplemente caracteres?

<textarea class="editor">
// Arreglo de caracteres
#include &lt;iostream&gt;
using namespace std;

int main(){
    char arreglo[4];
    arreglo[0] = 'H';
    arreglo[1] = 'o';
    arreglo[2] = 'l';
    arreglo[3] = 'a';
    
    for (int i=0; i < 4; i++){
        cout << arreglo[i];
    }
    
    return 0;
}</textarea>

La salida del anterior código es `Hola`. Tras este principio es como usamos *palabras* como variables. Sin embargo hay varias cosas importantes a notar, por ejemplo, en el ejemplo declaramos un arreglo de $$ 4 $$ locaciones, que es exactamente la misma cantidad de letras que tiene la palabra que definimos con ella. ¿Qué pasaría si usamos más letras que locaciones declaradas? Pues nos estaríamos saliendo del arreglo, y eso, como ya dijimos, no puede ser bueno.

¿Y qué pasaría si hubiéramos usado menos letras que locaciones? Pues tendríamos espacios sin *inicializar*, por lo que al recorrer el arreglo completo para mostrar la palabra, obtendríamos un resultado extraño. Por ejemplo:

<textarea class="editor">
// Arreglo de caracteres
#include &lt;iostream&gt;
using namespace std;

int main(){
    char arreglo[10];
    arreglo[0] = 'H';
    arreglo[1] = 'o';
    arreglo[2] = 'l';
    arreglo[3] = 'a';
    
    for (int i=0; i < 10; i++){
        cout << arreglo[i];
    }
    
    return 0;
}</textarea>

Al correr el código anterior, obtuve como salida `Hola  ê "` que muy seguramente es distinta a la que tú obtendrías. Esos valores que no aparecen o son caracteres extraños, pertenecen a los espacios sin inicializar. Teniendo este problema de la cantidad de locaciones y la cantidad de caracteres utilizados, *C++* nos da una gran ventaja.

<textarea class="editor">
// Arreglo de caracteres
#include &lt;iostream&gt;
using namespace std;

int main(){
    char palabra[10]; // Máximo 10 letras
    
    cin << palabra; 
    /* Utilizamos la entrada estándar para pedir
    nuestra palabra. No usamos índices pues no estamos
    pidiendo una sola locación, sino el arreglo entero */
    
    cout << palabra; // Mostramos el arreglo completo
    
    return 0;
}</textarea>

De esta manera no nos preocupamos si se ingresa una cantidad menor de caracteres, el compilador sabrá cuántas hemos inicializado, y además para cuando queramos mostrarlo, mostrará sólo las locaciones utilizadas. Ten en cuenta que este método de solicitar y mostrar el arreglo por su nombre y sin índices, sólo funciona con arreglos tipo `char`. El programa anterior con entrada `Prueba` mostrará como salida `Prueba`. Nota que tenemos como máximo la cantidad total de locaciones, así que una entrada como `parangaricutirimicuaro` no podrá ser almacenada en su totalidad, y por lo tanto no se podrá mostrar más allá de los primero $$ 10 $$ caracteres, que son los que se almacenaron. Una entrada así produciría la salida: `parangaric`, es decir, sólo las primeras $$ 10 $$ letras.

Recuerda que aún con el método anterior, la palabra ingresada sigue perteneciendo a un arreglo, y como tal, podemos referirnos a cada locación individualmente. También podemos inicializar un arreglo de caracteres de la siguiente manera:

<textarea class="editor">
// Inicialización de un arreglo
#include &lt;iostream&gt;
using namespace std;

int main(){
    char palabra[10] = "Prueba";
    cout << palabra[2] << " ";
    cout << palabra[0] << " ";
    cout << palabra[5] << " ";
    cout << palabra[1];
    return 0;
}</textarea>

Se mostraría la salida `u P a r`. Con todo esto en mente ¿cómo mostrarías una palabra de 8 letras al revés?

## Máximo de un arreglo

Como ya sabes, cuando declaramos un arreglo, el compilador busca en la memoria un bloque de locaciones en donde estén todas éstas juntas, si pedimos $$ 10 $$ locaciones, no le será muy difícil encontrar un espacio en donde hay $$ 10 $$ espacios disponibles y contiguos. Pero a medida que aumentamos la cantidad de locaciones solicitadas, se vuelve una tarea más complicada encontrar un bloque más grande de espacios disponibles.


Debido a esto, no podemos declarar arreglos excesivamente grandes, de hecho los compiladores suelen marcar un error de compilación cuando se trata de hacer algo así, por esto y por razones de arbitrariedad, tomaremos el número $$ 1000000 $$ (un millón) como máximo para declarar un arreglo. Si estás tratando de resolver un problema y crees que tu solución necesita de un arreglo mayor a $$ 1000000 $$ entonces es mejor que busques otra solución.


Recordemos además el hecho de que tenemos que ser considerados con la memoria, si declaramos un arreglo tipo `int` de $$ 1000000 $$ de locaciones, y cada variable `int` mide $$ 32 $$ bits, y además $$ 1000 $$ bits equivalen a un *kilobit* y a su vez, $$ 1000 $$ kilobits equivalen a un *megabit*, el arreglo mencionado nos constaría ¡$$ 32 $$ *mb* de memoria!

<div class="Nav">
    <a href="{{ site.baseurl }}/C++/Introduccion/Sentencias/">Tema anterior</a> | <a href="{{ site.baseurl }}/C++/Estructuras/Creacion-de-tipos/Struct/">Tema siguiente</a>
</div>