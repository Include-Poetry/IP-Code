---
layout: G-Article
title: Estructuras de datos en C++
date: 2020-01-04 12:00:00
author: rivel_co
tags: [Variables compuestas, Estructuras]
Hide_Tags: true
olimpiada: [OMI]
subject: [C++]
---

Si quisiéramos describir un pastel, por ejemplo, necesitaríamos hablar de varias de sus características, al menos abarcar las que necesitaremos para realizar una descripción general. En esta descripción podemos considerar a el pastel como un conjunto de variables, pues el valor de sus características no siempre es el mismo. Este sistema es muy útil, y de hecho, sencillo de implementar en *C++*. Aquí las conocemos como *estructuras de datos*, que son un conjunto de datos, juntos, bajo un mismo nombre.

{: #ListaContenido}
- Concepto de objeto
- Estructuras de datos usando struct

## Concepto de objeto

Volvamos al pastel, imagina que de él queremos hablar de varias cosas, el primero es su tamaño, luego su sabor, después su precio y al final su peso. Tenemos aquí $$ 4 $$ características del pastel del que vamos a hablar. Ahora, sabemos que el pastel *integra* todas estas características consigo mismo. Cuando hablamos de él, estamos incluyendo también sus características, entre las que están, entre otras, las que ya mencionamos.

Pueden haber, sin duda, muchas combinaciones distintas de esas $$ 4 $$ características, tamaños distintos, sabores distintos, precios distintos y también pesos distintos. Sin embargo, al hablar de un pastel, sea cual sea éste, vamos a tener que referirnos a esas características, porque son características de un pastel. Es decir, podemos ver al pastel como una gran variable *u objeto* que involucra a otras variables también.

<textarea class="output">
pastel{
    tamaño
    sabor
    precio
    peso
}</textarea>

De esta manera, estamos hablando de un objeto de tipo pastel, que involucra cuatro características. Podemos crear, por lo tanto, objetos de este mismo tipo si además podemos dar las características requeridas, por ejemplo:

<textarea class="output">
pastel SelvaNegra{
    tamaño: G
    sabor: chocolate
    precio: 200
    peso: 2.5
}</textarea>

Así, podemos decir, que `SelvaNegra` es un objeto del tipo *pastel*, y que además tiene $$ 4 $$ características, que es de *tamaño* grande, de *sabor* chocolate, que tiene un *precio* de $200 y además *pesa* 2.5kg. En el caso de las últimas dos características pusimos sólo la cantidad, y no la unidad de medida, pero podemos dar por convención que hablamos de pesos y de kilogramos.

## Estructuras de datos usando struct

Así como fácilmente en el ejemplo anterior, pudimos decir un tipo de objeto, sus características, y además crear un objeto de ese tipo, podemos, con la misma facilidad, hacer lo mismo en C++. Para esto usaremos el elemento `struct`. Su sintaxis es muy similar a la manejada en el ejemplo.

<textarea class="cpp">
// Sintáxis de struct
struct TipoDeObjeto{
    // Características
    int algo;
};</textarea>

Primero usamos la palabra reservada `struct`, seguido del nombre del *tipo* de objeto. Luego, y entre llaves, ponemos sus características, que estarán relacionadas con un tipo de variable, y un nombre para ésta. Al final ponemos un `;`. Siguiendo eso, si quisiéramos hacer nuestro objeto tipo *pastel* una realidad, haríamos lo siguiente:

<textarea class="cpp">
// Sintáxis de struct
struct pastel{
	char tamano;
	char sabor[20];
	int precio;
	float peso;
};</textarea>

Nota que para el tamaño estamos contemplando solamente una letra, (C, M, G). Para el sabor estamos contemplando una palabra, por ello utilizamos un arreglo. El precio lo tomamos como que siempre será un número entero, y el peso como un número que sí puede ser decimal. Un programa incluyendo lo anterior, y además declarando un objeto en sí, de éste tipo, se vería así:

<textarea class="cpp">
// Declaración con struct
#include &lt;iostream&gt;
using namespace std;

int main(){
    struct pastel{
        char tamano;
        char sabor[20];
        int precio;
        float peso;
    };
    
    pastel SelvaNegra;

    return 0;
}</textarea>

Como verás, aún no hemos dado características a `SelvaNegra`, sino que sólo hemos dicho que usaremos un objeto de tipo `pastel` y que se llamará así. Para darle las características, podemos hacer dos cosas, la primera es dar sus valores al momento que lo declaramos, poniendo los valores de cada característica *en el mismo orden* en el que están las variables declaradas dentro del tipo de objeto.

<textarea class="cpp">
// Inicialización en linea con struct
#include &lt;iostream&gt;
using namespace std;

int main(){
    struct pastel{
        char tamano;
        char sabor[20];
        int precio;
        float peso;
    };

    pastel SelvaNegra = {'G', "chocolate", 200, 2.5};

    return 0;
}</textarea>

La otra manera de hacerlo, es refiriéndonos a cada característica del objeto. Para hacerlo, usaremos el operador `.` que nos da una *instancia* de un objeto. Es lo que hemos venido manejando como las *características*. Para referirnos a cada *instancia* de un objeto, debemos poner primero el nombre del objeto (no su tipo), luego el operador `.` y después el nombre de la instancia, en otras palabras, el nombre de la variable declarada dentro del tipo de objeto. En nuestro ejemplo sería de la siguiente manera:

<textarea class="cpp">
// Inicialización individual con struct
#include &lt;iostream&gt;
using namespace std;

int main(){
    struct pastel{
        char tamano;
        char sabor[20];
        int precio;
        float peso;
    };

    pastel SelvaNegra;

    SelvaNegra.tamano = 'G';
    //SelvaNegra.sabor = "chocolate";
    SelvaNegra.precio = 200;
    SelvaNegra.peso = 2.5;

    cout << SelvaNegra.tamano << " ";
    //cout << SelvaNegra.sabor << " ";
    cout << SelvaNegra.precio << " ";
    cout << SelvaNegra.peso;

    return 0;
}</textarea>

Para este ejemplo se puso como comentario la asignación y salida de la propiedad `sabor`, esto debido a que no podemos hacer la asignación directa a un arreglo completo, como lo hicimos en el ejemplo anterior. Sin embargo, podemos referirnos a cada locación de la instancia, de esta manera:

<textarea class="cpp">
// Inicialización individual con struct
#include &lt;iostream&gt;
using namespace std;

int main(){
    struct pastel{
        char tamano;
        char sabor[20];
        int precio;
        float peso;
    };

    pastel SelvaNegra;

    SelvaNegra.tamano = 'G';
    //SelvaNegra.sabor = "chocolate";
    SelvaNegra.sabor[0] = 'c';
    SelvaNegra.sabor[1] = 'h';
    SelvaNegra.sabor[2] = 'o';
    SelvaNegra.sabor[3] = 'c';
    SelvaNegra.sabor[4] = 'o';
    SelvaNegra.sabor[5] = 'l';
    SelvaNegra.sabor[6] = 'a';
    SelvaNegra.sabor[7] = 't';
    SelvaNegra.sabor[8] = 'e';
    SelvaNegra.precio = 200;
    SelvaNegra.peso = 2.5;

    cout << SelvaNegra.tamano << " ";
    cout << SelvaNegra.sabor << " ";
    cout << SelvaNegra.precio << " ";
    cout << SelvaNegra.peso;

    return 0;
}</textarea>

Sí, es más *show* hacer algo así, además de poco práctico, sin embargo más adelante veremos maneras más sencillas de hacer una asignación como la que estábamos tratando de hacer. Con el ejemplo anterior, también pudimos ver una manera de mostrar las instancias de un objeto, usando el operador `.`. El programa anterior daría la salida `G chocolate 200 2.5`.

### Cita esta página

{% include citeThis.html titulo=page.title fecha=page.date link=page.url %}

<div class="Nav">
    <a id="navLeft" href="{{ site.baseurl }}/C++/Estructuras/Operaciones-con-bits/" title="Operaciones con bits &vert; #iP Code">
        Tema anterior
        <span>Operaciones con bits</span>
    </a>
    <a id="navRight" href="{{ site.baseurl }}/C++/Estructuras/Creacion-de-tipos/Class/" title="Class &vert; #iP Code">
        Tema siguiente
        <span>Class</span>
    </a>
</div>