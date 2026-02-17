# UNIDAD 2

## VISUALIZAR MARKDOWN BÁSICO (MK)

Creamos en `src/pages` una carpeta para el markdown.
Astro permite cargar el markdown directamente en la web
Podemos ver ese contenido escribiendo la ruta en el navegador.

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
