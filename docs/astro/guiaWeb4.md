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
