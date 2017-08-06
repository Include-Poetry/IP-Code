---
layout: G-Article
title: Búsquedas lineales
author: rivel_co
tags: [Recursión, Búsquedas, Arreglos, Algoritmo]
Hide_Tags: true
olimpiada: [OMI]
subject: [C++]
---

Muy a menudo, resolviendo problemas, te ves en la situación de buscar un determinado valor en un conjunto de datos. Existen diferentes formas de hacer esto.

{: #ListaContenido}
- Problema general
- Barridos
- Locación valor
- Búsqueda binaria o dicotómica

## Problema general

Imagina que en determinado problema genial, tu programa recibe una $$N$$ cantidad de números enteros, se asegura que todos los números ingresados caben en un entero signado de 32 bits, además no hay datos repetidos y estos no tienen orden específico. Además, recibes un número entero $$x$$, que es el número que estamos buscando. Si ese número se encuentra en el conjunto inicial, entonces mostramos la posición que el número tuvo en la entrada, sino, mostramos `-1`.

Considera que los siguientes ejemplos están desarrollados buscando solucionar este problema, sin embargo, encontrarás muchísimas variaciones a las que seguro te adaptarás fácilmente.

## Barridos

La forma más elemental, básica y seguramente intuitiva de todas las formas de búsqueda, es el barrido.

Cuando uno barre una habitación con un instrumento como la *escoba*, tenemos que recorrer cada espacio del cuarto en un orden, generalmente en ese caso particular, se hace de adelante hacia atrás, para no entorpecer el objetivo del barrido, que es dejar el área limpia. No es muy difícil entonces, darse cuenta de lo que hace referencia un algoritmo de barrido:

> Barrer un determinado conjunto de datos, es *recorrer* o *revisar* cada dato individualmente hasta lograr el objetivo del barrido mismo.

Un ejemplo que también funciona, es imaginar que tenemos una colección de cajas con pasteles adentro, en alguna de las cajas está tu pastel favorito, para encontrarlo a través de barridos, deberás *revisar* todas las cajas individualmente hasta que encuentres el que estás buscando, es decir, deberás *barrer* toda la colección. <span>Seguramente puede ser de gran utilidad en el entendimiento de la idea, revisar el asunto con [Karel]({{site.baseurl}}/Topicos-adicionales/Karel/Barridos-con-Karel/ "Barridos con Karel"){: target="_blank"}</span>.

### Implementación

En nuestro problema general, utilizando C++, podemos hacer un barrido convencional en búsqueda de nuestro elemento, de la siguiente manera:

Para una forma iterativa:

<textarea class="editor">
#include &lt;iostream&gt;
using namespace std;

int T[100];             // Arreglo que almacenará los datos
int x;                  // Número por el que se pregunta

int Barrido(int n){             // Función de barrido
    for (int i=0; i<n; i++){    // Recorremos todas las locaciones de nuestro arreglo
        if (T[i] == x){         // En cuanto se encuentre el valor
            return i+1;         // se regresa la ubicación en la que entró
        }
    }
    return -1;      // Si nunca se encontró el valor, el ciclo terminará y se regresará -1
}

int main(){
    
    int n;                      // Cantidad de números a ingresar
    cin >> n;
    
    for (int i=0; i<n; i++){
        cin >> T[i];            // Rellenamos nuestro arreglo
    }
    
    cin >> x;                   // Número por el que se pregunta
    
    cout << Barrido(n);         // Mostramos el resultado de nuestra búsqueda
    return 0;
}</textarea>

Para una forma recursiva: 

<textarea class="editor">
#include &lt;iostream&gt;
using namespace std;

int T[100];             // Arreglo que almacenará los datos
int x;                  // Número por el que se pregunta

int Barrido(int i, int n){      // Función de barrido
    if (i < n){
        if (T[i] == x){         // En cuanto se encuentre el valor
            return i+1;         // se regresa la ubicación en la que entró
        } else {
            return Barrido(i+1, n);     // Si no se enontró, seguimos buscando, ahora con la siguiente locación
        }
    }

    return -1;      // Se llegará a esta linea si nunca se llegó a la 10, es decir, si no se encontró
}

int main(){
    
    int n;                      // Cantidad de números a ingresar
    cin >> n;
    
    for (int i=0; i<n; i++){
        cin >> T[i];            // Rellenamos nuestro arreglo
    }
    
    cin >> x;                   // Número que buscamos
    
    cout << Barrido(0, n);      // Mostramos el resultado de nuestra búsqueda
    
    return 0;
}</textarea>

Como puedes notar, la cosa es recorrer todas las locaciones del arreglo, es decir, barrer todo el conjunto de datos que se ingresó, cada revisión se realiza comparando cada valor individual con el número buscado `x`. En cuanto se encuentre, se regresa la locación actual *más uno*, para arreglar el desfase de la locación `0`. Si el ciclo termina y nunca se llegó al `return i+1;` entonces la función procederá con el `return -1;` del final, lo cual es congruente, pues sólo se llega a esa línea en caso de que no se encontrara el valor.

### Eficiencia

Para analizar la eficiencia de este algoritmo, hay que imaginar un caso extremo. Por ejemplo, imagina una entrada de un millón de datos, en donde no se encuentra el número $$x$$ que se busca, tu programa tardaría *demasiado* (en contexto con la velocidad de una computadora, claro) en responder a la pregunta, pues tendría que revisar un millón de elementos primero. En este caso, podemos decir que este algoritmo es de complejidad $$ O(N) $$ para $$ N $$ datos. Esta eficiencia podría parecer "buena" para el ojo inexperto, sin embargo, imagina que además se realizan no sólo una, sino $$M$$ preguntas, el barrido sería de complejidad $$O(NM)$$, para valores grandes, esto resulta verdaderamente lento. 

## Locación valor

Esta forma de búsqueda es ***excepcionalmente eficiente***, sin embargo, su campo de aplicación es relativamente limitado. El principio en el que funciona, es, como su nombre lo dice, relacionar una locación con un valor.

Imagina de nuevo el caso de las cajas de pastel y que cada sabor de pastel tiene por nombre un número único, como los datos de nuestro problema ejemplo. Además, cuentas con un gran estante en donde cada cajón tiene un número asociado igual a los posibles sabores de tus pasteles, y además están ordenados de forma ascendente. Sería sencillo que cada vez que guardas un pastel, lo pusieras en el cajón asociado a su sabor, así cuando se te pregunte por la existencia de un sabor de pastel, sólo tengas que darle un vistazo a ese número de cajón y sabrías si hay en existencia.

Ahora sólo tienes que cambiar en la descripción anterior, los *pasteles* por ***datos*** y los *cajones* por ***locaciones***. Es decir, estaremos guardando en un arreglo, en la locación igual al número que entró, la posición en la que ese dato entró. Cuando se pregunte por un elemento, sólo hay que ver esa locación y si en efecto hay un número de orden, entonces podremos regresarlo.

### Implementación

<textarea class="editor">
#include &lt;iostream&gt;
using namespace std;

int T[100];                 // Arreglo que almacenará los datos

int main(){
    int n;                  // Cantidad de datos a ingresar
    cin >> n;
    
    int temp;   // Variable que almacenará de forma temporal cada nuevo valor
    for (int i=0; i<n; i++){       // Rellenamos el arreglo
        cin >> temp;        // Solicitamos el nuevo dato y lo guardamos en forma temporal
        T[temp-1] = i+1;    // Guardamos el orden en el que entró en la locación equivalente al dato
        // Considera que se "corrige" el desfase de locación con ese -1, para usar desde la locación 0
        // Se "corrige" el orden de entrada con el +1 pues el índice comenzó en 0
    }
    
    int x;
    cin >> x;           // Solicitamos el dato por el que se pregunta
    
    if (T[x-1] > 0){    // Volvemos a usar la corrección de locación
        cout << T[x-1]; // Si el valor es diferente de 0 (mayor) entonces mostramos ese valor
        // Pues el valor almacenado en [x-1] es el orden en el que entró x
    } else {
        cout << -1;     // Si el valor de la locación sigue siendo 0 (por ser el arreglo una variable pública)
                        // entonces no se encuentra en los datos ingresados
    }
    
    return 0;
}</textarea>

### Eficiencia

Como se mencionaba al inicio, el punto débil de este genial funcionamiento es su relativamente limitado campo de aplicación. Hay varios aspectos a notar en este algoritmo, pues las condiciones en las que funciona son especiales:

- Se debe asegurar de que no hay datos repetidos.
- Sólo funciona para valores positivos o para números cuyo valor absoluto no se repita.
- Sólo funciona para valores relativamente pequeños (alrededor de un millón).

Sin embargo, aunque las condiciones anteriores parecen ser muy específicas, es muy seguro que utilizarás este principio en algunos problemas que realices, y eso te simplificará la vida. 

Sobre la complejidad del algoritmo, es muy notorio que es de la mejor complejidad posible, pues es ***constante*** $$ O(1) $$. Es decir, respondemos cada pregunta de forma instantánea, pues sólo hay que revisar una locación y listo. Para $$ M $$ consultas tendrá una complejidad $$ O(M) $$.

## Búsqueda binaria o dicotómica

Llegamos entonces a uno de los casos más clásicos de búsquedas, y es todo un clásico justamente porque es muy eficiente y su campo de aplicación es muy muy grande. Sin embargo, es un poco (sólo un poco) más complejo. Además esta búsqueda resolverá un caso ligeramente distinto a los otros dos algoritmos.

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

### Implementación

Para una forma iterativa:

<textarea class="editor">
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

<textarea class="editor">
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

### Eficiencia

La búsqueda binaria es sumamente eficiente, en el peor de los casos, para $$N$$ datos, el algoritmo tendrá una complejidad $$O(log N)$$ lo cual es excelente, el logaritmo es una de las mejores complejidades que podemos encontrar en algoritmos. Sin embargo, es necesario que los datos estén ordenados, o que nos sea posible ordenarlos. En el último caso, debemos considerar también la complejidad de nuestro algoritmo de ordenamiento.

## Conclusión

Existen diferentes métodos de búsqueda de datos, cada método tiene ventajas y desventajas sobre los demás, el momento en el que utilizamos uno u otro, al igual que como con cualquier algoritmo, depende del problema que estemos tratando. Normalmente uno no se encuentra con problemas en los que tengamos que implementar un algoritmo tal cual se expresa en la literatura, sin embargo, podemos seleccionar un algoritmo específico y modificarlo para que resuelva el problema, mientras menos complejas sean las modificaciones que requiera el algoritmo, más probable es que ese es el indicado.

Nota como en cada ejemplo estamos evaluando distintos ***estados*** o condiciones de nuestra búsqueda, sólo tomamos aquellos estados que nos guíen a la solución, descartamos o ***podamos*** los estados que no encajan o que no son útiles para la respuesta, y nos desplazamos entre un estado y otro por determinadas ***condiciones de validez***. Recuerda y comprende muy bien estos conceptos de *estado*, *poda* y *condiciones de validez* pues son las bases de todas las búsquedas.

<span>¿Notas lo genial y parecidas que son las implementaciones recursivas e iterativas en estos ejemplos? Si aún no comprendes del todo la forma en la que la recursión funciona, compara estos métodos recursivos e iterativos, sus semejanzas y diferencias.</span>

<div class="Nav">
    <a href="{{ site.baseurl }}/C++/Metodos/Busquedas/">Tema anterior</a> | <a href="{{ site.baseurl }}/C++/Metodos/Busquedas/Amplitud/Matrices/">Tema siguiente</a>
</div>