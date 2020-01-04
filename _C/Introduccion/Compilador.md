---
layout: G-Article
title: Compilador de C++
author: rivel_co
tags: [Introducción]
Hide_Tags: true
olimpiada: [OMI]
subject: [C++]
---

Cuando queremos escribir un programa, lo hacemos en un determinado *lenguaje de programación*. A este escrito que hay que hacer le llamamos *código fuente* o simplemente *código*. Éste no es ejecutado por la computadora tal cual ha sido escrito, sino que debe de ser *traducido* a su lenguaje, *el lenguaje máquina*. Una de las maneras de hacer esta traducción es **compilando** el código y esto lo hace un **compilador**. Cada lenguaje de programación necesita un compilador particular.

{: #ListaContenido}
- Compilación de un programa
- Compiladores e IDE
- Dev-C++
- Code::Blocks
- Uso de ambos IDE
- Recomendaciones

## Compilación de un programa

Cuando escribimos un programa en C/C++, lo que hacemos es crear un archivo con extensión `.c` para C y `.cpp` para C++. Dentro de ese archivo va escrito nuestro código. Una vez que ya lo tenemos hay que compilarlo para poder ver su ejecución, <span>es como traerlo a la vida.</span>

Cuando compilamos un código fuente, el compilador crea un archivo que podemos ejecutar, este archivo tiene la extensión `.exe` como la mayoría de los programas de Windows. Si quieres volver a ver la ejecución de tu programa sólo tienes que volver a abrir el archivo `.exe`. Sin embargo, tienes que volver a compilar cada que hagas cambios en tu código, para que esos nuevos cambios vuelvan a ser *traducidos* y puedan ser ejecutados.

> Una vez creado el ejecutable, éste se hace independiente del código fuente que lo generó.

## Compiladores e IDE

Lo primero que necesitamos para empezar a programar en C/C++ es un compilador que soporte estos lenguajes. Existen muchos y hay de muchos tipos. Como queremos empezar en el mundo de la programación necesitaremos además de un compilador, *un Entorno de Desarrollo Integrado* (**IDE por sus siglas en inglés**) que nos haga más sencillo escribir, ejecutar y depurar nuestros programas.

Estos entornos vienen por lo general integrados con un compilador dentro de la misma aplicación. De esta manera con instalar un sólo programa tendremos ambos. Un *IDE* incluye típicamente un *editor de código fuente*, *herramientas de construcción automáticas* y un *depurador*. De esta manera podemos escribir, probar y corregir nuestro código fácilmente.

## Dev-C++

Dev-C++ es un *IDE* para desarrollar programas escritos en C/C++, su compilador es el *MinGW* y es solamente compatible con *Windows*. Puedes conseguirlo directamente en nuestra sección de [recursos]({{ site.baseurl }}/Recursos/Descargables/){: target="_blank"}.

(<span>El proceso de instalación que se describirá está especialmente enfocado en la versión 5.10 pero es muy similar a versiones anteriores</span>).
<br>
Una vez descargado el instalador lo ejecutamos (puede ser necesario dar permisos de administrador), se comenzarán a cargar los archivos necesarios para la instalación, a continuación podrás seleccionar uno de los lenguajes disponibles, para después pasar al acuerdo de licencia. Una vez que lo aceptes te preguntará qué tipo de instalación deseas hacer, es recomendable la instalación completa (full). Después seleccionarás el sitio donde se instalará (preferentemente deja la ubicación predeterminada), y listo, haces click en **instalar**. Al finalizar se te ofrecerá la opción de ejecutar el programa. No hay problema si así lo escoges.

Ya dentro aparecerá una gran pantalla gris. Para empezar a escribir un programa hay que ir a la pestaña *Archivo* y de ahí a *Nuevo* y a continuación *Archivo fuente*. También puedes crear un nuevo *proyecto* pero para los programas que estaremos haciendo es más sencillo, práctico y por lo tanto más recomendable escoger *Archivo fuente*. También puedes utilizar el *shortcut* `ctrl + n` o el ícono de la barra.

<span>De esta manera ya estamos listos para empezar a **escribir** nuestros programas.</span>

## Code::Blocks

Code::Blocks es un *IDE* para el desarrollo de programas escritos en C/C++. Cabe señalar que es *multiplataforma*, por lo que si lo necesitas, puedes instalarlo también en un equipo con *sistema operativo* distinto de Windows. También puedes encontrarlo en nuestra sección de [recursos]({{ site.baseurl }}/Recursos/Descargables/){: target="_blank"}.

(<span>El procedimiento aquí señalado se centrará en la versión *16.01 MinGW* aunque para versiones anteriores es muy similar</span>).
<br>
Una vez descargado el instalador, podemos ejecutarlo (puede ser necesario dar permisos de administrador). Se dará la bienvenida a la instalación y después el acuerdo de licencia, a continuación el tipo de instalación (también es recomendada la instalación *full*), y el lugar donde se instalará. Está bien si todo lo dejamos así y procedemos con la instalación. Al finalizar nos preguntará si queremos iniciar con el programa. El programa se ejecutará pero la ventana de instalación permanecerá ahí, sólo hay que dar un *next*, luego un *finish* y listo.

Una vez que el programa se ha abierto, se mostrará el panel de bienvenida del entorno. Para empezar a escribir un código fuente podemos ir a la pestaña *File*, luego en *New* y a continuación (<span>y más recomendable</span>) *Empty file* (shortcut `ctrl + shift + n`). Se abrirá una página limpia, lista para escribir. Es muy recomendable que antes de empezar a escribir, **guardes** el archivo nuevo. Dirigiéndonos a la pestaña *File* y a continuación *Save file*. Ahí busca un lugar donde guardar el archivo y asegurate de escribir al final del nombre que le des, la extensión `.cpp`.

<span>Estamos listos para empezar a **escribir** nuestros programas.</span>

## Uso de ambos IDE

Principalmente estaremos utilizando las mismas funciones cada que desarrollemos nuestros programas. Estas funciones son:

**Compilar**: Con esta opción compilamos nuestro programa, de haber errores se mostrarán en la parte inferior de la pantalla. Al compilar el archivo fuente se guardará automáticamente.
<br>
**Ejecutar**: Aquí ejecutamos el programa previamente compilado.
<br>
**Compilar y ejecutar**: Hacemos las dos funciones anteriores con un sólo click.
<br>
**Guardar**: Con esta opción escogemos un nombre y una ubicación con el que guardaremos nuestro código fuente. Recuerda que cada que compilamos el código se guarda automáticamente.
<br>
**Abrir**: Aquí podremos abrir un archivo con formato `.c` o `.cpp`. No un archivo ejecutable.
<br>
**Reconstruir**: En ocasiones el compilador tiene problemas para procesar nuestro código. Cuando estos problemas son ajenos a nuestro código (por lo general se marca el error `Id returned 1 exit status` o similar), podemos usar esta opción para volver a intentarlo tras reconstruir el proceso.

Como no hay como estar bien familiarizado con nuestro entorno de trabajo, es muy útil aprenderse los atajos del teclado o *shortcuts*.

En **Dev-C++**: <br>
*Compilar*: `F9` <br>
*Ejecutar*: `F10` <br>
*Compilar y ejecutar*: `F11` <br>
*Reconstruir*: `F12`

En **Code::Blocks**: <br>
*Compilar* (build): `ctrl + F9` <br>
*Ejecutar* (run): `ctrl + F10` <br>
*Compilar y ejecutar* (Build and run): `F9` <br>
*Reconstruir* (rebuild): `ctrl + F11`

**En ambos**: <br>
*Guardar*: `ctrl + s` <br>
*Abrir*: `ctrl + o`

## Recomendaciones

Como todos sabemos *la práctica y la organización hacen al maestro*, por lo que es sumamente recomendable que mantengas tus códigos **bien organizados**, por categorías en carpetas o algún otro método que te ayude a encontrarlos fácilmente.

Tras estar trabajando un buen rato en el IDE puede que tu vista se canse, por lo que es recomendable utilizar un *tema* del entorno más amigable. Por lo general los temas con fondos oscuros y texto en alto contraste son más llevaderos (<s>y más <i>cool</i></s>). Para cambiar el tema en Dev-C++ ve a *Herramientas > Opciones del editor > Sintaxis*, en la parte inferior de la ventana hay una lista de temas predefinidos, también puedes crearlos tú. 

Hacer esto en Code::Blocks nos tomará un poco más de tiempo. Lo primero es asegurarte de que *Code::Blocks* esté cerrado. Ahora, descarga el archivo `colour_themes.conf`, puedes hacerlo justo de [aquí]({{ site.iP-Sources }}/Descargables/colour_themes.conf) o copialo de la página de sus creadores [acá](http://wiki.codeblocks.org/index.php?title=Syntax_highlighting_custom_colour_themes){: target="_blank"}. El archivo contiene ajustes de colores para los códigos de C/C++.

Ahora abre la carpeta donde se instaló Code::Clocks, típicamente para usuarios de Windows está en *C > Program Files > CodeBlocks* o una ruta muy similar según la versión de Windows que tengas. Ahí ejecuta el archivo `cb_share_config.exe`. Abrirá una pequeña ventana, dividida en dos partes, haz click en el cuadrado con tres puntos que está en la mitad derecha (*Destination configuration file*), abrirá una ventana típicamente con la dirección *C > Users > TuUsuario > AppData > Roaming > CodeBlocks* en donde inmediatamente encontrarás un archivo llamado `default.conf`, selecciona ese archivo. Ahora, haz click en el cuadro con puntos de la parte izquierda (*Source configuration file*), ahí navega hasta encontrar el archivo que descargaste. Abajo se cargará una lista de archivos, son los temas, te sugiero seleccionarlos todos, luego haz click en el botón *Transfer >>*, confirma la acción y luego haz click en *save* y confirma también. Ya puedes cerrar esa ventana y abrir *Code::Blocks*.

Dentro de Code::Blokcs dirígete a *Settings > Editor > Syntax highlighting*, en la parte de arriba en la sección *Colour theme* encontrarás los temas que instalaste. Escoge el que más te agrade y guarda los cambios.

> No es necesario que instales los dos IDE aunque tampoco hay problema si instalas ambos

> Nota que en ningún momento se ha hablado de lo que se escribirá como código fuente, solamente el cómo instalar, configurar y personalizar los IDE, así como algunas de sus funciones más básicas

<div class="Nav">
    <a id="navLeft" href="{{ site.baseurl }}/C++/Introduccion/" title="Introducción a C++ &vert; #iP Code">
        Tema anterior
        <span>Introducción a C++</span>
    </a>
    <a id="navRight" href="{{ site.baseurl }}/C++/Introduccion/Librerias/" title="Librerías en C++ &vert; #iP Code">
        Tema siguiente
        <span>Librerías en C++</span>
    </a>
</div>