---
layout: G-Article
title: Class
---

Así como las [estructuras]({{ site.baseurl }}/C++/Estructuras/Struct/ "Volver allá"){: target="_blank"}, las *clases* contienen datos miembro, como variables, pero de forma adicional, nos permiten definir ***funciones***, también como miembro.

{: #ListaContenido}
- Definiciones y concepto
- Declaración
- Usabilidad
- Constructores
- Sobrecarga de constructores

## Definiciones y concepto

Crear una nueva clase, es como crear un nuevo ***tipo de objeto***, tendrá sus características y funciones en base a lo que declaremos como elementos miembro de esa clase.

Su declaración y uso es de hecho muy similar a las de `struct`, pero aquí disponemos de otra herramienta que son ***especificadores de acceso***, estos especificadores determinan quién y cómo puede acceder a los elementos miembro. Hay tres tipos diferentes:

- Elementos privados (`private`): son sólo accesibles sólo por otros miembros de la misma clase. Por defecto, los elementos miembro de una clase son privados.
- Elementos protegidos (`protected`): Son accesibles por otros miembros de la misma clase pero también por miembros de clases derivadas.
- Elementos públicos (`public`): Son accesibles de cualquier parte de donde sea visible el objeto.

## Declaración

De manera similar a `struct`, la declaración de una clase es como sigue:

<textarea class="output">
class nombre_de_clase{
    especificador_de_acceso_1:
        miembros;
    especificador_de_acceso_2:
        miembros;
    ....
};</textarea>

De igual forma, podemos declarar objetos justo entre la llave de cierre y el punto y coma `;`.

Un ejemplo de declaración de una clase es:

<textarea class="editor">
class Pastel{
    int precio;
    string sabor;
  public:
    void inicializar(int,string);
    int precio_por_rebanadas(int);
} GrandDuc;</textarea>

Como puedes ver, nuestra clase se llama `Pastel`, que es como el nuevo tipo de variable que acabamos de crear, luego tenemos cuatro elementos miembro, dos variables privadas que son `precio` y `sabor`, y la declaración de dos funciones públicas que son `inicializar` y `precio_por_rebanadas`. Nota que aquí sólo hemos puesto la declaración, más no las hemos definido. Además, hemos creado un objeto llamado `GrandDuc`.

Como ha sido declarado, podemos acceder normalmente a las funciones públicas, justo como lo haríamos en una estructura (`struct`), tan solo insertando un punto. Por ejemplo podemos hacer algo como:

<textarea class="editor">
GrandDuc.inicializar(12,"chocolate");
cout << GrandDuc.precio_por_rebanadas(3);</textarea>

Nota que hemos accedido a las funciones así de simple porque las hemos declarado ***públicas***, no sucede lo mismo con las variables `precio` y `sabor` pues son privadas por defecto. Ahora sí, podemos pasar a definir nuestras funciones miembro.

Hay varias formas de definir las funciones miembro, puede ser de forma externa a la declaración de la clase, pero marcando que la función que se declara es perteneciente a la clase que queremos, esto lo hacemos escribiendo antes del nombre de la función, el nombre de la clase a la que pertenece, luego dos dos puntos y ahora sí, el nombre de la función, por ejemplo:

<textarea class="output">
int Nombre_de_clase::Nombre_funcion_miembro(int x){
    ...
}</textarea>

En el caso de nuestro ejemplo de la clase `Pastel` sería:

<textarea class="editor">
#include &lt;iostream&gt;
using namespace std;

class Pastel{
    int precio;     // Precio por rebanada
    string sabor;   // Sabor de rebanada
  public:
    void inicializar(int,string);
    int precio_por_rebanadas(int);
} GrandDuc;

void Pastel::inicializar(int x, string y){ // Inicializa el objeto
    precio = x;     
    sabor = y;      
    return;
}

int Pastel::precio_por_rebanadas(int x){ // Devuelve el precio de x rebanadas
    return precio*x;
}

int main(){
    GrandDuc.inicializar(12,"chocolate");
    cout << GrandDuc.precio_por_rebanadas(3);   
    
    return 0;
}</textarea>

Nota que en la función `inicializar` hemos dador por hecho que la función tiene acceso a las variables `precio` y `sabor`, esto es porque la función es parte de la clase también, por eso ambas partes, pública y privada se conocen. Si ejecutas el código anterior, obtendrás como salida `36`, cosa que concuerda que decidimos `inicializar` el precio por rebanada del `Pastel` llamado `GrandDuc` a `12`, al solicitar el `precio_por_rebanadas` correspondiente a `3`, hemos recibido que sería un precio de `36`.

Además, es importante notar el uso del ***operador de alcance*** (*scope operator*) `::`, que es quien dice que una cosa pertenece a otra, en este caso, indica que las funciones `inicializar` y `precio_por_rebanadas` pertenecen a la clase `Pastel`.

También puedes definir las funciones miembro dentro de la misma definición de la clase, sería como sigue:

<textarea class="editor">
#include &lt;iostream&gt;
using namespace std;

class Pastel{
    int precio;
    string sabor;
  public:
    void inicializar(int x, string y){
        precio = x;
        sabor = y;
        return;
    }
    int precio_por_rebanadas(int x){
        return precio*x;
    }
} GrandDuc;

int main(){
    GrandDuc.inicializar(12,"chocolate");
    cout << GrandDuc.precio_por_rebanadas(3);   
    
    return 0;
}</textarea>

Ambos métodos son válidos.

## Usabilidad

El principal atributo de las clases, es el hecho de que podemos declarar varios objetos de la misma clase y mantendrán sus propiedades individualmente, por ejemplo:

<textarea class="editor">
#include &lt;iostream&gt;
using namespace std;

class Pastel{
    int precio;
    string sabor;
  public:
    void inicializar(int x, string y){
        precio = x;
        sabor = y;
        return;
    }
    int precio_por_rebanadas(int x){
        return precio*x;
    }
};

int main(){
    Pastel GrandDuc, Mediterraneo;
    
    GrandDuc.inicializar(12,"chocolate");
    Mediterraneo.inicializar(15, "cafe");
    
    cout << GrandDuc.precio_por_rebanadas(2) << " ";
    cout << Mediterraneo.precio_por_rebanadas(2);   
    
    return 0;
}</textarea>

Esto nos produce una salida `24 30`. Nota que por la misma cantidad de rebanadas, no pagaríamos lo mismo, dado que hemos definido diferentes precios para cada pastel.

## Constructores

Como hemos visto, hemos llamado a la función `precio_por_rebanadas` sólo después de haber llamado primero a `inicializar`, pues es sólo hasta ese momento que hemos definido las características de ese pastel, de no haber definido las características como el precio, habríamos recibido un valor *no definido* (<s><span>qué raro</span></s>) de precio por rebanadas, como con cualquier variable no inicializada. Las clases, soportan un elemento llamado ***constructor***, que nos permite hacer ese trabajo de inicialización, y lo mejor es que lo hace al momento en el que declaramos nuestra variable.

Podemos crear un constructor de clase de manera interna en la definición de clase, o externa como con las demás funciones miembro. En ambos casos creamos una nueva función que no regresa ningún tipo de dato, de hecho ni siquiera hay que poner un tipo de dato `void`. Para la ***definición externa*** ponemos el nombre de la clase, los dobles dos puntos y luego de nuevo el nombre de la clase, para la ***definición interna*** basta con crear una función con el nombre de la clase, en ambos casos los parámetros que recibe la función, serán las variables privadas que hemos declarado y que queremos *inicializar*. En base a nuestro ejemplo, añadiendo un constructor podemos deshacernos de la función `inicializar`, pues de eso se encargará nuestro *constructor*. La forma de utilizarlo es como sigue:

<textarea class="editor">
#include &lt;iostream&gt;
using namespace std;

class Pastel{
    int precio;
    string sabor;
  public:
    int precio_por_rebanadas(int x){
        return precio*x;
    }
    Pastel(int a, string b){
        precio = a;
        sabor = b;
    }
};

int main(){
    Pastel GrandDuc(12, "chocolate");
    Pastel Mediterraneo(15, "cafe");
    
    cout << GrandDuc.precio_por_rebanadas(2) << " ";
    cout << Mediterraneo.precio_por_rebanadas(2);   
    
    return 0;
}</textarea>

Como podrás notar, hemos declarado e inicializado al mismo tiempo nuestros pasteles, esto lo hace todo más práctico, fácil y rápido <span>¡genial!</span>

## Sobrecarga de constructores

Otra cosa genial sobre las clases, es que podemos crear un constructor *default*, que inicialice de forma predeterminada el objeto, y además, otro constructor para hacer una inicialización específica, por ejemplo:

<textarea class="editor">
#include &lt;iostream&gt;
using namespace std;

class Pastel{
    int precio;
    string sabor;
  public:
    int precio_por_rebanadas(int x){
        return precio*x;
    }
    Pastel(int a, string b){
        precio = a;
        sabor = b;
    }
    Pastel(){
        precio = 10;
        sabor = "vainilla";
    }
};

int main(){
    Pastel GrandDuc(12, "chocolate");
    Pastel Mediterraneo(15, "cafe");
    Pastel Croccante;
    
    cout << GrandDuc.precio_por_rebanadas(2) << " ";
    cout << Mediterraneo.precio_por_rebanadas(2) << " ";    
    cout << Croccante.precio_por_rebanadas(2);
    
    return 0;
}</textarea>

Como puedes notar, podría parecer que no hemos inicializado el pastel `Croccante`, y de hecho, no lo hemos hecho nosotros, sino el constructor por defecto que hemos agregado (*línea 15*), el cual sabe que si el constructor no recibe ningún parámetro (si no es citado), él debe actual, dando por hecho que el precio será `10` y que su sabor será `vainilla`. Este constructor hará esto para cualquier objeto de la clase `Pastel` a la cual no hayamos *construido* de forma explícita en su declaración. Nota que no es necesario poner paréntesis vacíos en la declaración de `Croccante`, ponerlos nos marcaría un error de compilación. El programa anterior nos daría como salida `24 30 20`.

<div class="Nav">
    <a href="{{ site.baseurl }}/C++/Estructuras/Struct/">Tema anterior</a> | <a href="{{ site.baseurl }}/C++/Estructuras/Pila/">Tema siguiente</a>
</div>