---
layout: G-Article
title: Cola
tags: [Estructuras, Cola, Arreglos, Clases, Funciones]
Hide_Tags: true
categories: [C++, OMI]
---

Otra estructura muy útil para resolver problemas es la que es del tipo *FIFO*, en este caso, ***la cola***.

{: #ListaContenido}
- Origen de su nombre
- Idea de funcionamiento
- Implementación de funcionamiento
- Implementación efectiva

## Origen de su nombre

El acrónimo *FIFO* significa *First In First Out*, que podemos traducir como *el primero en entrar es el primero en salir*. Típicamente se le llama ***cola***, que es como una *fila* de una tienda, cuando nos formamos, la primer persona que se formó es la primer persona que sale de la fila, pues es la primera en ser atendida.

## Idea de funcionamiento

La idea general de este tipo de estructura es igual a la fila de la panadería, por ejemplo, donde la gente se forma una detrás de otra y van siendo atendidos conforme han llegado.

> En una cola el primer elemento que ha ingresado es el primer elemento que será procesado.

## Implementación de funcionamiento

Podemos visualizar nuestra formación, cola o fila, como un arreglo de gente, donde cada persona o dato, tiene una ubicación determinada, el primer dato o persona en procesar es el que se ha formado o ingresado primero. En base a esto podemos ir generando nuestro código con un arreglo (no dinámico) como sigue:

<textarea class="editor">
#include &lt;iostream&gt;
using namespace std;

int cola[100];
int inicio = 0;

int main(){
    
    return 0;
}</textarea>

Donde el arreglo `cola` almacenará nuestros datos en la formación y la variable `inicio` será el índice que lleva el control de quién es el siguiente en ser atendido, es decir, como el inicio de la fila, y la variable `fin` llevará control de dónde se formará la siguiente persona. Este índice ha sido inicializado en `0`, pues la primer persona que llegué se *formará* en la primer locación del arreglo, cuando una persona se haya formado, deberemos actualizar nuestro índice, para dejar todo listo para el siguiente dato. Como podemos visualizar los datos como uno detrás del otro, pondremos el siguiente dato en la siguiente locación inmediata, por lo que por cada dato ingresado sólo hemos de desplazar el contador una unidad:

<textarea class="editor">
void push(int n){
    cola[fin] = n;
    fin++;
    return;
}</textarea>

Como puedes ver, sólo hemos actualizado el índice que maneja el final de la cola, no el de inicio, pues el inicio sigue siendo la locación `0` en este ejemplo.

> Cada que un dato entra no necesariamente significa que el primer dato haya sido procesado, por lo que el índice de inicio debe permanecer igual.

Además, nota que hemos utilizado el nombre convencional de `push` para la función que ingresa datos a nuestra estructura.

Para poder retirar un dato, lo que tenemos que hacer es actualizar nuestro indice que manera el inicio de la estructura, pues, para nuestro programa, los datos pertenecientes a la estructura son aquellos que se encuentran en las locaciones entre `inicio` y `fin`, si actualizamos nuestro `inicio`, estaremos dando por hecho que ese dato ya no pertenece a la estructura y que por lo tanto, lo podemos olvidar, además de actualizar y decir que el siguiente dato en ser procesado es el que se encuentra una unidad después. Nuestra función que elimina elementos de la cola será:

<textarea class="editor">
void pop(void){
    inicio++;
    return;
}</textarea>

Como puedes notar, sólo actualizamos el índice de `inicio` y hemos utilizado el tradicional nombre para eliminar datos `pop`.

### Otras funciones útiles

Otras funciones de nuestra pila que son muy útiles, son por ejemplo, consultar qué dato está en el inicio y en el fin de la estructura, esto lo podemos hacer así:

<textarea class="editor">
int front(void){
    return cola[inicio];
}</textarea>

Con la función anterior, estaremos devolviendo el valor del próximo elemento en salir pero sin sacarlo de la estructura. Además, hemos utilizado el clásico nombre para acceder al elemento *al frente* de la estructura `front`.

<textarea class="editor">
int back(void){
    return cola[fin-1];
}</textarea>

La función anterior devuelve el último elemento que entró, se encuentra en la locación `fin-1` puesto que en `fin` se encuentra la siguiente posición libre de la estructura. La última locación ocupada será una locación anterior, es decir `fin-1`. Además se ha utilizado el típico nombre en referencia a la última variable o la variable *de hasta atrás* de la estructura.

Para saber si la cola está vacía, podemos comparar nuestros índices de inicio y fin. Por ejemplo, en el inicio del uso de la estructura, tanto el fin como el inicio eran el mismo, pues no había ningún elemento en la estructura. Así podemos entender fácilmente que cuando el inicio apunte al mismo lugar que el fin, es que la cola está vacía, sin importar el valor que tengan.

<textarea class="editor">
bool empty(void){
    return inicio == fin;
}</textarea>

Como puedes ver, podemos obtener mucha información sobre nuestra estructura utilizando los índices del inicio y del final. <span>¿Cómo obtendrías la cantidad de elementos almacenados en la estructura?</span>

### Limitaciones de esta implementación

- Dado que el tamaño se define desde el inicio como en cualquier arreglo, la cantidad de elementos que podemos meter se ve limitada a la cantidad de elementos que pueden ser almacenados en un arreglo.
- En la implementación del ejemplo, se considera siempre que cada función funciona sólo para un elemento, en este caso sólo funciona para `cola`, de querer utilizar otro contenedor igual, tendríamos que elaborar nuevas funciones para el nuevo contenedor, sin embargo esto se puede resolver fácilmente utilizando ***clases*** o ***punteros***.

### Ventajas de esta implementación

- Es muy rápido, dado que tanto el ingreso como la eliminación de datos es de complejidad constante, sólo se realiza un incremento/decremento a una variable y una asignación típica.
- Para la mayoría de los problemas basta con la cantidad máxima permitida de variables en un arreglo.

### Ejemplo completo

El ejemplo completo con todas las funciones citadas sería:

<textarea class="editor">
#include &lt;iostream&gt;
using namespace std;

int cola[100];
int inicio = 0;
int fin = 0;

void push(int n){
    cola[fin] = n;
    fin++;
    return;
}

void pop(void){
    inicio++;
    return;
}

int front(void){
    return cola[inicio];
}

int back(void){
    return cola[fin-1];
}

bool empty(void){
    return inicio == fin;
}

int main(){
    push(20);
    push(30);
    push(40);
    push(50);
    
    cout << front() << " "
         << back() << " ";
    
    pop();
    pop();
    
    if (!empty()){
        cout << front();
    } else {
        cout << "La cola esta vacia";
    }
    
    return 0;
}</textarea>

El código anterior produce como salida `20 50 40`. Nota que el código anterior no es una implementación del todo eficiente, pues sólo aplica a una estructura, y de un sólo tipo. Una implementación más efectiva es utilizando clases o apuntadores.

## Implementación efectiva

Generar varias estructuras de este tipo, es sencillo utilizando clases.

<textarea class="editor">
#include &lt;iostream&gt;
using namespace std;

class Cola{
    int datos[100000];      // Contenedor
    int inicio;             // Índice de inicio
    int fin;                // Índice de fin
  public:
    Cola(){                 // Constructor
        inicio = fin = 0;
    }
    void push(int n){       // Insertamos un dato
        datos[fin] = n;     // Inserción de elemento n en el final de contenedor
        fin++;              // Actualización del final del contenedor
        return;
    }
    void pop(void){         // Deleción de un elemento
        inicio++;           // Actualización de índice de inicio
        return;
    }
    int front(void){        // Regresa el elemento que está al inicio de la fila
        return datos[inicio];
    }
    int back(void){         // Regresa el elemento que está al final de la fila
        return datos[fin-1];
    }
    bool empty(void){       // Devuelve true si la estructura está vacía
        return inicio == fin;
    }
};

int main(){
    Cola fila;
    Cola formacion;
    
    fila.push(20);
    fila.push(30);
    fila.push(40);
    fila.push(50);
    
    formacion.push(2);
    formacion.push(4);
    formacion.push(6);
    
    cout << fila.front() << " " << formacion.front();
    
    return 0;
}</textarea>

El código anterior produce como salida `20 2` y como puedes ver, cada fila tiene sus datos individuales.

<div class="Nav">
    <a href="{{ site.baseurl }}/C++/Estructuras/Pila/">Tema anterior</a> | <a href="{{ site.baseurl }}/C++/STL/">Tema siguiente</a>
</div>