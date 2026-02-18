# UNIDAD 4

## CONSTRUIR PLANTILLAS

- Ubicación: Las plantillas se crean en `src/layouts`.
  Su función es contener la estructura común (HTML base), componentes globales y recibir variables.
- Gestión de Estilos:
  Para que un estilo del Layout afecte al contenido inyectado en el slot, se debe usar `<style is:global>`.
  Jerarquía de renderizado: Página → Layout → Componente.
- El elemento `<slot/>`: Permite inyectar contenido a la página dentro de la estructura común del Layout.
- Paso de Datos: Al igual que los componentes, las plantillas reciben variables mediante `Astro.props`.

**Platilla:**

~~~astro
---
import '../styles/global.css'
const {tituloPage, texto} = Astro.props;
---
<html lang="en">
    <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width" />
        <meta name="generator" content={Astro.generator} />
        <title>{tituloPage}</title>
    </head>
    <body>
        <h1>Esta página es {tituloPage}</h1>
        <p>{texto} Es el autor</p>
        <slot/>
    </body>
</html>
~~~

**Página:**

~~~astro
---
import BaseLayout from '../layouts/Base.astro'
const nombre = "David Gallegos"
---


<BaseLayout tituloPage="Home" texto={nombre}>
    Mi nombres es {nombre}
</BaseLayout>
~~~

## PLATILLAS Y MARKDOWN (MD)

### 1. ESTRCUTURA MD

En Astro, al trabajar con archivos `.md`, dividimos la página en dos capas claramente diferenciadas:

- **La Capa de Datos (YAML):** Es el bloque superior entre los guiones `---`. Contiene **metadatos** (títulos, fechas, variables personalizadas). Astro procesa esto como un objeto de JavaScript.
- **La Capa de Contenido (Markdown):** Todo lo que va debajo de los segundos guiones `---`. Es texto plano que el motor de Astro traduce automáticamente a etiquetas HTML.

#### TABLA DE CONVERSIÓN MD A ASTRO

| Símbolo Markdown | Etiqueta HTML | Uso Principal |
| :--- | :--- | :--- |
| `# Título` | `<h1>` | Título principal (solo uno por página). |
| `## Subtítulo` | `<h2>` | Secciones principales de tus apuntes. |
| `### Subtítulo` | `<h3>` | Sub-apartados dentro de una sección. |
| `Texto normal` | `<p>` | Párrafos de texto (se crean automáticamente). |
| `* elemento` o `- elemento` | `<li>` | Elementos de una lista desordenada (`<ul>`). |
| `1. elemento` | `<li>` | Elementos de una lista numerada (`<ol>`). |
| `**negrita**` | `<strong>` | Resaltar texto con importancia. |
| `*cursiva*` | `<em>` | Énfasis en el texto. |
| `> cita` | `<blockquote>` | Bloques de texto resaltados o citas. |
| `` `código` `` | `<code>` | Código en línea o términos técnicos. |
| ` ```js ... ``` ` | `<pre><code>` | Bloques de código con resaltado de sintaxis. |
| `[Texto](URL)` | `<a>` | Enlaces o hipervínculos. |
| `![Alt](Ruta)` | `<img>` | Inserción de imágenes. |

### 2. FRONTMATTER

Para que la plantilla pueda "leer" lo que escribimos en el YAML del Markdown, utilizamos la propiedad **`Astro.props`**.

- Astro inyecta automáticamente los datos del YAML dentro de un objeto llamado `frontmatter`.
- **Uso en la plantilla:** `{frontmatter.nombre_variable}`.

### 3. EL RENDERIZADO

El contenido del cuerpo del Markdown no necesita ser llamado por una variable. Astro lo inyecta automáticamente en el lugar donde coloques la etiqueta `<slot />` dentro de tu archivo de plantilla.

### 4. ESTILIZACIÓN

Usamos **`<style is:global>`** que afecta a todo el contenido de `<slot />`.

#### EJEMPLO

> **Ruta:** `src/pages/archivo.md`

~~~markdown
---
layout: ../../layouts/documents.astro
title: "Unidad 4: Layouts"
autor: "David Gallegos"
---

## SUBTITULO 1
Contenido...
~~~

> **Ruta:** `src/layouts/plantilla.astro`

~~~astro
---
const { frontmatter } = Astro.props;
---
<html>
    <head>
        <title>{frontmatter.title}</title>
        <style is:global>
            h2 { color: #4da6ff; text-align: center; }
            p { font-size: 1.2rem; text-align: center; }
        </style>
    </head>
    <body>
        <h1>{frontmatter.title}</h1>
        <p>Escrito por: {frontmatter.autor}</p>
        <slot /> 
    </body>
</html>
~~~
