---
layout: G-Article
title: Búsqueda en amplitud BFS
author: rivel_co
tags: [Búsqueda, Algoritmo, Grafos]
Hide_Tags: true
olimpiada: [OMI]
subject: [C++]
published: false
---

## Principio de la búsqueda

En programación, una búsqueda de cualquier tipo no es muy diferente a una real, sin embargo, existen muchas formas de buscar cosas, y cada método es el más efectivo en cada tipo de situación. Sin importar el método, siempre estamos buscando ***responder a una pregunta***.

Una analogía útil en la búsqueda en amplitud, es considerar un estante con determinada cantidad de cajones, en cada cajón hay otros cajones más pequeños, y en cada uno otros más pequeños, y así con diferentes grados de ***profundidad***. Nosotros estamos buscando un determinado objeto que está dentro de algún cajón. La búsqueda en profundidad nos dice que primero abriríamos todos los cajones del primer nivel, es decir todos los que están inmediatamente a nuestro alcance, luego abrir uno del segundo nivel de cada cajón ya abierto, es decir, iríamos probando de uno por uno, avanzando lentamente en la profundidad de los cajones. No abriríamos todos los de un cajón y luego todos los de otro y luego todos los del siguiente, sino que iríamos avanzando uniforme y gradualmente en los niveles de todos los cajones.

> En una búsqueda en amplitud, revisamos todos los elementos de un mismo nivel de profundidad al mismo tiempo, comenzando por el primer nivel inmediato.

Si lo vemos como un plano cartesiano, y estamos buscando un sitio en ese plano, sería como revisar un paso adelante (posición uno), volver al inicio, buscar un paso hacia atrás (posición dos) y volver, dar uno a la izquierda (posición tres) y volver y luego dar uno a la derecha (posición cuatro) y volver. Ahí ya habríamos revisado todos los ***estados inmediatos*** al estado actual. Para la segunda parte habría que revisar todos los estados inmediatos a todos los estados ya revisados, es decir, habría que ponernos en la posición uno, y de ahí dar un paso en cada dirección, luego ir a la posición dos y dar un paso en cada dirección y así sucesivamente hasta encontrar lo que buscamos. Está de más mencionar que no es necesario buscar dos veces en un mismo punto, si no estuvo en el primer momento, no estará al segundo (normalmente).

> La búsqueda en amplitud es un procedimiento recursivo, pues revisamos todos los estados inmediatos de cada estado y así hasta cubrir todos los estados que existen.

Es importante resaltar que el hecho de que un proceso tenga un principio recursivo, su implementación no forzosamente necesita el uso de recursión como tal; recuerda que la recursión es principalmente una forma de operar.

El método tan específico de la búsqueda en amplitud cobra sentido cuando nos damos cuenta de que minimiza el trabajo que hay que realizar para culminar con la búsqueda. Es decir, la especialidad de la ***búsqueda en amplitud es minimizar*** el proceso de buscar, por lo tanto, se utiliza cuando hay que responder preguntas del tipo <span>¿Cuál es la menor cantidad de pasos necesaria para... ?</span>. Esto tiene sentido si analizamos con más calma el funcionamiento de esta técnica.

Por ejemplo, en nuestra analogía de buscar en los cajones dentro de otros cajones, una pregunta sobre minimizar sería *¿cuál es la menor cantidad de cajones que hay que abrir para encontrar el objeto?* En el funcionamiento de nuestro algoritmo, primero revisamos los estados inmediatos a nuestro estado inicial, es decir, aquellas posiciones que sólo nos costarían $$1$$ operación. Si no lo encontramos ahí, pasamos a revisar los estados inmediatos a los anteriores revisados, es decir, todos los estados que nos costarían $$2$$ operaciones. Así revisamos aumentando la posible cantidad de pasos que se necesita, asegurando que al encontrarlo, sepamos cuál es la mínima cantidad necesaria para resolver nuestra búsqueda.

### Estructura de la búsqueda

Como ya hemos mencionado, lo primero es comenzar por nuestro estado inicial, el cual se genera a partir de las coordenadas iniciales, hasta ese punto hemos recorrido una distancia de $$0$$ pues aún no hacemos nada. Ese estado debe ingresar a la cola de procesamiento, y mientras tengamos un estado que procesar haremos los siguiente:

- Sacaremos el siguiente elemento a ser procesado (el del frente de la cola).
- Revisaremos si en esa posición está lo que buscamos, de ser así devolvemos la distancia que hemos recorrido hasta ese momento y terminamos, sino continuamos.
- Marcamos la posición actual como visitada en nuestra matriz encargada de ello, pues es justo ese dato el que estamos procesando, ya no hay que pasar de nuevo por ahí.
- Ahora pasamos a evaluar si los cuatro posibles lados adyacentes (estados inmediatos al estado actual) son válidos.
- Para eso determinamos una nueva posible posición, por ejemplo, arriba de la actual.
- Si esa nueva posición está dentro de nuestro mapa, no ha sido visitada, y es una casilla en la que sí podemos circular, entonces creamos un estado con esas nuevas coordenadas válidas y con la distancia nueva para llegar ahí, que sería una unidad más que la distancia actual recorrida.
- Una vez creado y configurado el nuevo estado, lo metemos en la cola de procesamiento. Hacemos lo mismo con todos los estados inmediatos.
- Dejamos que nuestra iteración encuentre la solución. 
- Si se terminaron los estados que se podían revisar en todo el mapa, y nunca regresamos una distancia, entonces regresamos un $$-1$$ como señal de que no se puede salir del laberinto.