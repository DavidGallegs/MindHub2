# UNIDAD 3

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
