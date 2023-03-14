# Grids V 1.0 (index3.html)

Esta es la primera versión de prueba para darle un formato de **Grids** a la pagina de Inovación RED
Para empezar el video donde encontre la información es [YouTube] (https://youtu.be/68O6eOGAGqA “este”).

Primero debiamos definir el tamaño de cada columna y fila que vamos a tener en nuestra página
para hacer esto tenemos que ver en que espacios iría cada cosa, desde que espacio va a ocupar el header, el banner, el contendio principal
la decoracion, los widgets, etc. Este diseño lo pueden ver en la página de inicio del figma que tenemos. Puse unos 
cuadritos semitransparentes para más o menos diferenciar los espacios; nuevamente, esto es mejor explicado en el video.


## Cógido

Para empezar tenemos que asignarle clases a cada espacio que haremos, los cuales se definiran con **<div>** en el html:

```
    <div class="container">
        <nav>
            <a href="#">Inicio</a>
            <a href="#">Miembros</a>
            <a href="#">Historia</a>
            <a href="#">Proyectos</a>
            <i class="fa fa-bars"></i>
        </nav>
        <div id="Banner">Banner</div>
        <div id="SideDecor">side</div>
        <div id="Widgets">Widgets</div>
        <div id="Main"></div>
    </div>

```

En el caso de la barra de navegación para esa se utilizará el tag **<nav>** para no tener mas clases de las necesarias.
Además estos **<div>** los tendremos que poner dentro de un otro div que será el "padre" como podemos ver. 

Ahora para comenzar con el css, primero diremos que el padre muestre a los hijos en forma de Grids y especificaremos que 
ocupe toda la pantalla, además del tamaño de cada fila y columna:

```
    .container{
        display: grid;
        height: 100vh;
        grid-template-columns: 5% 80% 15%;
        grid-template-rows: 9% 40% 2fr 20%;
        grid-template-areas: 
        "nav nav nav" 
        "Banner Banner Banner"
        "SideDecor Main Widgets"
        "footer footer footer";
    }   

```

Generalmente cuando se define el tamaño de las grids en esta manera de trabajar se utilizan las unidades **fr** que equivalen
a fracciones de la pantalla, sin embargo observé que cuando utilizaba dicha unidad, entre mas contenido agregaras a ciertas partes de la pagina,
las demás se iban haciendo mas pequeñas para acomodarse; para resolverlo utilicé porcentajes en lugar de fr, al parecer no afecta en nada y 
creo que queda más limpio, pero aun no estoy tan seguro de eso así que si provoca problemas pueden corregirlo.
Cabe aclarar que para que usar porcentajes funcione, **si solo se usan porcentajes para definir el tamaño**, la suma de estos
tendrá que llegar a 100%, de otra manera no cubrirán toda la pagina o se saldrán de la misma.



El tag de **grid-template-areas** lo usaremos para definir los espacios que ocuparán cada cada parte de nuestros elementos
pero para que funcione primero tenemos que definirlos dentro del archivo de ccs asi: 

```

#Banner{
    background-color: blueviolet;
    grid-area: Banner;
}

```

Con el tag **grid-area** le asignaremos un nombre para que el padre pueda saber a quien llamar al momento de mostrar los elementos.


## Grids dentro de otras grids

Debido a la estructura que le dimos a la página en figma, creo que la forma más adecuada de implementarla sería usando otro sistema
de grids dentro de la grid de la sección **Main**; pero en este caso no tendriamos que definir globalmente que espacio ocupará cada 
espacio como en el código de arriba, sino que solo hasta que haya una sección de ruleta o que sus elementos esten centrados,
es decir que no haya una foto o texto a la misma altura, será cuando utilizaremos el tag **grid-template-areas** para decir
que esta fila solo la ocupará un solo elemento, que sera la ruleta o el contenido que deseemos. 

En este caso como la pagina comienza con una sección con texto e imagenes a la misma altura, implementé este codigo:

```
.subcontainer-Index{
    margin-left: 1.5rem;
    margin-top: 1.5rem;
    display: grid;
    grid-template-columns: 50% 50%;
    gap: 0.8em;
    font-size: 24px;
}

```
Y para acomodar si queremos primero la imagen o primero el texto, simplemente variaremos el orden en que aparecen estos elementos
en el archivo html.

```
<div class="subcontainer-Index">

            <!-- aquí aparece primero el texto y despues la imagen -->

            <p>Somos un equipo de estudiantes que reúne a aquellos liderazgos estudiantiles
                generadores de ideas, proyectos e iniciativas, que buscan impactar dentro y
                fuera de la comunidad universitaria, mediante la vinculación de distintos
                departamentos institucionales, con el objetivo de desarrollar su
                crecimiento personal y profesional.</p>
            <img src="yoshi.jpg">


            <!-- aquí aparece primero la imagen y despues el texto -->

            <img src="yoshi.jpg">
            <p>Riqueza, Esperanza y Dignidad, son las siglas del comité
                RED, las cuales fueron extraídas de la última visita del
                Papa a México, haciendo referencia al hecho de que los
                jóvenes mexicanos somos la riqueza y dignidad de
                nuestro país, que nosotros somos los que buscamos
                constantemente la paz y la dignidad de las personas.</p>
        </div>

```

## Notas extra

### Títulos

Los titulos deben ir afuera de la division de los grids de contenido, de otra manera estos se tomarán como contenido
y la estructura que podría aparecer seria: 

**Titulo            Texto
Imagen**

No se aun si haya alguna forma más eficiente de acomodarlo pero a mi parecer es mejor dejarlos fuera de los **<div>** 
solo por si acaso, algo asi: 

```
<h1 class="tittle-left">¿Quiénes somos?</h1>
        <div class="subcontainer-Index">
            ...
        </div>

```

Además considero que debemos tener 3 clases para los titulos; una por si están a la izquierda (**tittle-left**), 
una si están a la derecha (**tittle-right**) y otra si están centrados (**tittle-center**).
Esto no complica mucho más el css y siento que podemos tener un mejor control sobre como queremos que se vean los títulos.



### Variables

Creo que tambien deberiamos utilizar variables en el css para asi si necesitamos modificar algo que ocupamos en muchos lados,
solo tengamos que cambiar una sola linea de código, además que asi podemos hacer operaciones entre las variables
si necesitamos hacer cierta parte de la página responsiva. Las variables están en la primera linea del css en la parte de **:root**.
Por ahora no he definido ninguna, pero pensé que sería buena idea introducir esa idea ahora.


### Responsividad

Trate de hacer que la pagina se viera no tan amontonada si sse visualiza en un telefono, para esto en el momento que la 
pantalla llegue a los 600px de ancho, ahora solo habrá una columna en todo el cuerpo de la página y se eliminarán los espacios
de la decoración y los widgets, hablando de estos aún hay un problema, cuando se visualiza a esa resolución la página, 
los widgets no desaparecen y quedan debajo de todo y a la derecha, por lo que se crea overflow y aun no resuelvo eso.



##### Cambios realizados por Jesús el 09/03/2023