# WEB ASTRO

## UNIDAD 1

### CREACIÓN ESTRUCTURA

1. Creamos proyecto: `npm create astro@latest`
2. Iniciamos el servidor: `npm run dev`

### PRIMERA CREACIÓN

Todo el proceso de creaeción es en `src`

1. `src/pages/index.astro` → Index de la web
2. Dentro de este archivo usamos `page_html` para crear la estructura inicial de html.

~~~html
    <html lang="en">
        <head>
            <meta charset="utf-8" />
            <meta name="viewport" content="width=device-width" />
            <meta name="generator" content={Astro.generator} />
            <title>Astro</title>
        </head>
        <body>
            <h1>Astro Web Prueba</h1>
        </body>
    </html>
~~~

### DESPLEGAR SITIO WEB

1. Crear cuenta en Netlify (Mi caso con github)
2. Creamos un poryecto y vinculamos con el repositorio
3. Se generará una URL final: <https://deluxe-torte-3949b3.netlify.app/>
4. Para las actualizaciones sincronizamos con GitHub
5. En unos minutos se actualiza Netlify

## UNIDAD 2

### CREAR PÁGINAS

1. En `src/pages` creamos una página siempre con extensión `.astro`
2. Siempre empeazr una página con `page...` para iniciar el html
3. Las rutas en astro son `/nombre` y el index es `/`

### IMPLEMENTACIÓN DE MARKDOWN

Para markdown creamos en `src/pages` una carpeta para el markdown
Podemos cargar directamente el md en una web

~~~~md
---
title: 'Mi primera publicación en el blog'
pubDate: 2022-07-01
description: 'Este es la primera publicación de mi nuevo blog Astro.'
author: 'Alumno de Astro'
image:
    url: 'https://docs.astro.build/assets/rose.webp'
    alt: 'El logotipo de Astro sobre un fondo oscuro con un brillo rosado.'
tags: ["astro", "bloguear", "aprender en público"]
---
# Mi primera publicación en el blog

Publicado el: 2022-07-01

¡Bienvenido a mi _nuevo blog_ sobre el aprendizaje de Astro! Aquí, voy a compartir mi viaje de aprendizaje a medida que construyo un nuevo sitio web.

## Lo que he conseguido

1. **Instalación de Astro**: En primer lugar, he creado un nuevo proyecto Astro y configurar mis cuentas en línea.

2. **Creación de páginas**: Luego aprendí cómo hacer páginas creando nuevos archivos `.astro` y colocándolos en la carpeta `src/pages/`.

3. **Creación de publicaciones**: ¡Esta es mi primera publicación! ¡Ahora tengo páginas de Astro y publicaciónes en Markdown!

## Próximos pasos

Terminaré el tutorial de Astro, y luego seguiré añadiendo más publicaciones. Mira este espacio para más por venir.
~~~~

Lo que esta al inicio es **Frontmatter** y se usará en el futuro

### AÑADIR CONTENIDO DINÁMICO

En astro podemos añadir html dinámico en la de `---`
En este caso vamos a usar una **variable**.
Es decir usamos JavaScript para añadir dinamismo.

~~~astro
<!-- Ejemplo 1:  -->
<html lang="es">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width" />
    <title>Astro</title>
    <title>{pageTitle}</title>
  </head>
  <body>
    <a href="/">Inicio</a>
    <a href="/about/">Sobre mi</a>
    <a href="/blog/">Blog</a>
    <h1>Sobre mi</h1>
    <h1>{pageTitle}</h1>
    <h2>... ¡y mi nuevo sitio Astro!</h2>

    <p>Estoy trabajando en el tutorial introductorio de Astro. Esta es la segunda página de mi sitio web, ¡y es la primera que he construido yo mismo!</p>
  </body>
</html>

~~~

~~~astro
<!-- En este ejmplo podemos ver otros uso de JS en HTML -->
---
const pageTitle = "Sobre mi";

const identity = {
firstName: "Sarah",
country: "Canada",
occupation: "Escritor técnico",
hobbies: ["fotografia", "observación de aves", "peñarol"],
};

const skills = ["HTML", "CSS", "JavaScript", "React", "Astro", "Redacción de documentos"];
---

<html lang="en">
    <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width" />
        <meta name="generator" content={Astro.generator} />
        <title>About Page</title>
    </head>
    <body>
        <a href="/">Inicio</a>
        <a href="acerca">Acerca De</a>
        <a href="blog">Blog</a>

        <h1>{pageTitle}</h1>
        <p>He aquí algunos datos sobre mí:</p>

        <ul>
            <li>Me llamo {identity.firstName}.</li>
            <li>Vivo en {identity.country} y trabajo como {identity.occupation}.</li>
            {identity.hobbies.length >= 2 &&
                <li>Dos de mis aficiones son: {identity.hobbies[0]} y {identity.hobbies[1]}</li>
            }
        </ul>

        <p>Mis habilidades son:</p>
        <ul>
            {skills.map((skill) => <li>{skill}</li>)}
        </ul>

        
    </body>
</html>
~~~

### RENDERIZACIÓN CONDICIONAL DE ELEMENTOS
