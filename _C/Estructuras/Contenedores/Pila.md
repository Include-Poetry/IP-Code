---
layout: G-Article
title: Estructura pila
author: rivel_co
tags: [Estructuras, Pila, Arreglos, Clases, Funciones]
Hide_Tags: true
olimpiada: [OMI]
subject: [C++]
---

Una estructura de gran utilidad al momento de resolver problemas, ***es la pila***, que es una estructura de tipo FILO.

{: #ListaContenido}
- Origen de su nombre
- Idea de funcionamiento
- Implementación de funcionamiento
- Implementación efectiva

## Origen de su nombre

La palabra *pila* generalmente es asociada a una fuente de energía eléctrica, y nos recuerda a  la llamada *pila voltáica* de *Alessandro Volta*, en la que se ordenan monedas de cobre y zinc para así obtener electricidad.

La manera de organizar dichas monedas, es la que sugirió el nombre de este invento. Volta ***apiló*** una moneda de Zinc sobre una de Cobre y repitiendo este proceso varias veces, formó su ***pila*** de monedas. En el caso de la programación, una pila (como estructura de datos) se basa en este mismo concepto, donde lo que importa, es el orden en el que se procesan la información, como si estuvieran siendo apilados.

## Idea de funcionamiento

Como se mencionaba más arriba, la pila es una estructura de tipo *FILO* que es un acrónimo de *First In Last Out*, que significa *el primero en entrar es el último en salir*. Como cuando tenemos una pila de galletas sobre la mesa, la primer galleta que se puso es la que se encuentra hasta el fondo de la pila, a su vez, la última galleta que se ponga en la pila quedará hasta arriba.

Ese es el concepto fundamental de una pila, y procesar datos de esta manera nos ayuda a resolver de manera sencilla muchos problemas, además nos ayuda a comprender procesos recursivos correctamente.

> En una pila, el primer elemento que se ingresa a la estructura es el último elemento que se procesa. Mientras que el último elemento en ingresar es el primero en procesar.

## Implementación de funcionamiento

Para crear un contenedor que funcione como una pila y de forma no dinámica, usaremos arreglos. Con esto, se quiere dar a entender que la estructura que almacenará los datos, será un arreglo, puede ser de cualquier tipo, según sea el tipo de elemento que estaremos guardando en la pila.

Por lo tanto, primero declaramos un nuevo arreglo, para este ejemplo lo haremos de enteros `int`, además en el ejemplo almacenaremos máximo $$100$$ elementos. Para fines prácticos, declararemos nuestra pila como una variable global.

<textarea class="cpp">
#include &lt;iostream&gt;
using namespace std;

int pila[100];

int main(){
   
   return 0;
}</textarea>

Entonces, en el arreglo `pila` estaremos guardando nuestros datos. Nota que lo importante de este tipo de estructuras es la forma en la que manejamos los datos cuando entran y cuando salen. Para esto, nos estaremos apoyando en una variable que será nuestro ***índice***, esta variable irá recordando cuál es la posición en la que ingresará el nuevo elemento y también cuál es el próximo elemento en salir. A nuestro índice lo llamaremos `i` y su valor inicial será $$0$$ por comodidad. Por el mismo motivo la declararemos como una variable global también.

<textarea class="cpp">
#include &lt;iostream&gt;
using namespace std;

int pila[100];
int i = 0;

int main(){
   
   return 0;
}</textarea>

Nota que dado que la variable es global, no hay necesidad de inicializar de forma explícita en $$0$$ pero igual lo hemos hecho. 

### Ingresar datos

Ahora sí, el punto interesante es cuando empezamos a ingresar datos. Como decíamos antes, el índice `i` nos indica en donde se ingresará el siguiente elemento, hasta ahora no tenemos ningún elemento, por lo que tiene sentido que nuestro siguiente elemento (el primero) sea almacenado en la posición $$0$$ de nuestro arreglo. Por comodidad, crearemos una nueva función que ingrese el nuevo elemento en la estructura.

Una vez que el nuevo valor se ha ingresado a la estructura, hay que actualizar nuestro índice, indicando en dónde irá el siguiente elemento que pueda llegar. Entonces lo que haremos será "mover" una locación nuestro índice hacia adelante, es decir, el siguiente elemento (el segundo) se guardará en `pila[1]`. Considera que en el caso específico de este ejemplo, la función sólo necesita saber qué valor ingresará, pues gracias al índice ya sabe donde lo guardará.

<textarea class="cpp">
#include &lt;iostream&gt;
using namespace std;

int pila[100];
int i = 0;

void push(int n){
    pila[i] = n;
    i++;
    return;
}

int main(){

   return 0;
}</textarea>

> Tradicionalmente se utiliza como instancia que ingresa datos a una estructura el nombre `push`

<span>¡Genial!</span> Hasta ahora, podemos ingresar elementos sin problema a nuestro arreglo, y nuestro índice `i` irá controlando en dónde se guarda cada elemento, todo va bien. Ahora podemos pasar a la parte en donde se ***retiran*** elementos de la pila. 

### Eliminar datos

Tradicionalmente a la función o instancia que retira elementos de una estructura se le llama `pop`. Para poder quitar elementos, lo que haremos no será ni darle un nuevo valor a ese elemento, ni tratar de borrarlo, bastará con *ignorarlo* para que ya no altere nuestra estructura y podamos seguir con normalidad. Hasta el momento, nuestro programa sigue la idea de que todo entre la locación `0` y `i-1` es parte de nuestra pila. Se considera `i-1` porque en la posición `i` será en donde irá nuestro nuevo elemento, que es justo adelante del último que ingresó, por lo que al restar uno a ese índice, estaremos "regresando" a la posición del último elemento que ya es parte de nuestra pila.

Entonces, todo sobre nuestra pila está entre `0` y `i-1`, no es hasta `i`, de hecho, esa locación en adelante es *ignorada*, y lo que esté ahí eventualmente se irá sobrescribiendo con los nuevos datos, por lo tanto basta con actualizar nuestro índice hacia atrás, ignorando así el último elemento que estaba ahí, como *eliminándolo* de nuestra pila, pues será sobrescrito por el siguiente valor que se ingrese. Considera que para eliminar un dato, la función en sí no necesita saber nada (en el caso específico de este ejemplo) pues gracias al índice, y al funcionamiento de la pila, ya sabe qué elemento sigue en salir.

En base a lo anterior, nuestro código iría así:

<textarea class="cpp">
#include &lt;iostream&gt;
using namespace std;

int pila[100];
int i = 0;

void push(int n){
    pila[i] = n;
    i++;
    return;
}

void pop(void){
    i--;
    return;
}

int main(){
    
   return 0;
}</textarea>

> Nota que hasta ahora el código no hace nada en sí, pero se está preparando para el funcionamiento de la pila.

Entonces, ya podemos ingresar datos y sacarlos de nuestro arreglo también, todo marcha genial. 

### Otras funciones

Seguramente hay más cosas que necesitaremos en un problema que sólo meter y sacar elementos. Una función clásica es obtener el valor del próximo elemento en salir, es decir, del último que entró. Esto sin eliminarlo de la pila. Generalmente a esta función de la pila se le llama `top`.

<textarea class="cpp">
int top(void){
    return pila[i-1];
}</textarea>

Podemos confirmar su funcionamiento por el razonamiento que hacíamos anteriormente, sobre la posición del último elemento.

Otra función útil es saber si el contenedor está vacío, de estar vacío no podemos seguir retirando elementos. Esto lo podemos revisar fácilmente viendo el valor de nuestro índice, si ese índice vale $$0$$ entonces podemos decir que el contenedor está vacío, pues estaríamos como en las condiciones iniciales. A la función que revisa si un contenedor de este estilo está vacío o no, se le llama típicamente `empty`.

<textarea class="cpp">
bool empty(void){
    return i == 0;
}</textarea>

Nota que la función anterior devuelve `true` cuando la pila está vacía.

> ¿Puedes decir cuántos elementos tiene la estructura sólo por su índice?

### Limitaciones de esta implementación

- Dado que el tamaño se define desde el inicio como en cualquier arreglo, la cantidad de elementos que podemos meter se ve limitada a la cantidad de elementos que pueden ser almacenados en un arreglo.
- En la implementación del ejemplo, se considera siempre que cada función funciona sólo para un elemento, en este caso sólo funciona para la estructura `pila`, de querer utilizar otro contenedor igual, tendríamos que elaborar nuevas funciones para el nuevo contenedor, sin embargo esto se puede resolver fácilmente utilizando ***clases*** (para crear una clase con el tipo de estructura) o ***punteros*** (pasando cada arreglo como un argumento a cada función).

### Ventajas de esta implementación

- Es muy rápido, dado que tanto el ingreso como la eliminación de datos es de complejidad constante, sólo se realiza un incremento/decremento a una variable y una asignación típica.
- Para la mayoría de los problemas basta con la cantidad máxima permitida de variables en un arreglo.

### Ejemplo final

De manera global, podemos ver el código como sigue:

<textarea class="cpp">
#include &lt;iostream&gt;
using namespace std;

int pila[100];      // Arreglo que almacena los datos
int i = 0;          // Índice de la pila

void push(int n){   // Inserción de un elemento
    pila[i] = n;    // Se inserta elemento
    i++;            // Se actualiza el índice
    return;
}

void pop(void){     // Deleción de un elemento
    i--;            // Se actualiza el índice
    return;
}

int top(void){      // Obtención de último elemento ingresado
    return pila[i-1];  
}

bool empty(void){   // Devuelve true si la pila está vacía
    return i == 0; 
}

int main(){
    push(7);
    push(8);
    push(9);
    push(1);
    cout << top() << endl;
    
    pop();
    pop();
    cout << top() << endl;
    
    if (empty()){
        cout << "Pila vacia\n";
    } else {
        cout << "Pila no vacia\n";
    }
    
    return 0;
}</textarea>

La salida del anterior código es:

<textarea class="output">
1
8
Pila no vacia
</textarea>

> Esta implementación es poco práctica, pues sólo se ha creado con fines demostrativos.

Es importante que notes además, que deberás adaptar el concepto de muchas formas diferentes, en ocasiones se mezclan las funciones `pop` y `top` en una misma función, muchas veces no se utiliza una función para saber si el contenedor está vacío, pues sólo se compara directamente el índice con cero y cosas por el estilo.

## Implementación efectiva

Para una implementación mucho más útil, es aconsejable utilizar clases, dejando un código como sigue:

<textarea class="cpp">
#include &lt;iostream&gt;
using namespace std;

class pila{                 // Nombre de clase
    int datos[100000];      // Arreglo que almacena los datos
    int i;                  // Índice de la pila
public:
    pila(){                 // Constructor
        i = 0;
    } 
    void push(int n){       // Inserción de datos
        datos[i] = n;       // Se asigna el nuevo valor
        i++;                // Se actualiza el índice
        return;
    }
    void pop(void){         // Deleción de un dato
        i--;                // Actualización de índice
        return;
    }
    int top(){              // Devuelve el último elemento ingresado
        return datos[i-1]; 
    }
    bool empty(void){       // Devuelve verdadero si la estructura está vacía
        return i == 0;
    }
};

int main(){
    pila nueva;
    nueva.push(7);
    nueva.push(8);
    nueva.push(9);
    nueva.pop();
    cout << nueva.top() << endl;
    
    pila otra;
    otra.push(1);
    otra.push(2);
    otra.push(3);
    otra.push(4);
    otra.push(5);
    otra.push(6);
    cout << otra.top() << endl;
    
    nueva.pop();
    cout << nueva.top() << endl;
    
    return 0;
}</textarea>

El código anterior da una salida como sigue:

<textarea class="output">
8
6
7
</textarea>

Nota que de la misma forma el ejemplo anterior está limitado a la cantidad máxima de elementos que pueden ser almacenados en un arreglo, además, la clase `pila` del ejemplo sólo funciona con enteros, sin embargo esto puede ser modificado fácilmente como ya imaginarás.

<div class="Nav">
    <a href="{{ site.baseurl }}/C++/Estructuras/Creacion-de-tipos/Class/">Tema anterior</a> | <a href="{{ site.baseurl }}/C++/Estructuras/Contenedores/Cola/">Tema siguiente</a>
</div>