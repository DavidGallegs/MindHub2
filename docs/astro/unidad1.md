# UNIDAD 1

## PÁGINAS ASTRO

Las páginas se encuentran en: `src/pages`.
Dentro de un archivo `.astro` escribimos `page_html` para crear la estructura inicial de html.

~~~html
    <html lang="en">
        <head>
            <meta charset="utf-8" />
            <meta name="viewport" content="width=device-width" />
            <meta name="generator" content={Astro.generator} />
            <title></title>
        </head>
        <body>

        </body>
    </html>
~~~

## ESTILIZAR (CSS)

Para estelizar elementos o una  página completa creamos un archivo `.css` en la carpeta `src/styles/`.
Y luego en la página o componente `.astro` importamos los estilos.
El `import` siempre tiene que estar al inicio.

~~~astro
---
import '../styles/global.css'
---

<html lang="en">
    ...
</html>
~~~

## CONTENIDO DINÁMICO (JS)

### VARIABLES

Para crear html dinámico usamos JavaScript entre los `---`.
Y luego lo llamamos usando `{}`
Se puede usar variables, funciones, objetos, arrays, condiciones...

~~~astro
---
const tituloWeb = "Index web";
---

<html lang="en">
    <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width" />
        <meta name="generator" content={Astro.generator} />
        <title>{tituloWeb}</title>
    </head>
</html>
~~~

### CONDICIONALES

Al código podemos añadir operadordes de `if` para renderizar o no elementos

~~~astro
---
const happy = true;
const finished = false;
const goal = 3;
---

<html lang="en">
    <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width" />
        <meta name="generator" content={Astro.generator} />
        <title>About Page</title>
    </head>
    <body>
        <p>Renderizar</p>
        {happy && <p>¡Estoy feliz de aprender Astro!</p>}
        {finished && <p>¡He terminado este tutorial!</p>}
        {goal === 3 ? <p>Mi objetivo son 3 días.</p> : <p>Mi objetivo no son 3 días.</p>}
    </body>
</html>
~~~

### ARRAYS

En el caso de arrays, para mostrarlos usamos `map()`

~~~astro
---
const mascotas = ["perro", "gato", "loro"]
---

<html lang="en">
    <body>
        <ul>
            {mascotas.map((mascota) => <li>{mascota}</li>)}
        </ul>
    </body>
</html>
~~~

## COMPONENTES

Los componentes se crean en la carpeta de `src/components` y se llaman con `import`.
Estos son archivos `.astro` que se importan en la página con un nombre que comienza por mayúscula
y con su propio CSS y JavaScript.

Los componentes en astro se pueden anidadar, es decir, puede haber un compoennte padre
que contega otros componentes (Componente hijos).

~~~astro
---
import Componente from '../components/Componente.astro';
---
<html lang="en">
    <body>
        <Componente/>
    </body>
</html>
~~~

## PASO DE VARIABLES ENTRE COMPONENTES

Los componentes hijos pueden recibir variables del componente padre

**Componente Hijo:**

~~~astro
---
const { platform, username } = Astro.props;
---
<!-- social.astro -->
<a href={`https://www.${platform}.com/${username}`}>{platform}</a>
~~~

**Componente Padre:**

~~~astro
---
import Social from './social.astro';
---
<!-- footer.astro -->
<footer>
    <Social platform="twitter" username="astrodotbuild" />
    <Social platform="github" username="withastro" />
    <Social platform="youtube" username="astrodotbuild" />
</footer>
~~~

## SCRIPTS CON ASTRO

En el propio archivo astro podemos insertar javaScript con la etiqueta `<script>`
Otra forma es con una importación de un archivo js desde la carpeta `src/js/`
Tenemos en cuenta que no usaremos por lo usual JavaScript , sino islas y frameworks como React,
pero es bueno saber que si se puede usar para DOM básico por el momento.

~~~astro
<body>
    <h1>Prueba de Script</h1>
    <button id="miBoton">Haz click</button>

    <script src="../js/index.js"></script>
</body>
~~~

~~~js
    const boton = document.querySelector('#miBoton');

    boton?.addEventListener('click', () => {
        alert("¡Hola desde un archivo JS externo!");
    });
~~~
