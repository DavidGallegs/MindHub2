# UNIDAD 5

## AUTOMATIZACIÓN DE ÍNDICES (GLOB)

Astro permite escanear carpetas para generar listas de contenido automáticamente.
Esto evita tener que actualizar los enlaces a mano cada vez que creamos un nuevo archivo `.md`.

### EXPLICACIÓN

1. **import.meta.glob()**: Función para importar múltiples archivos a la vez.
   - Ruta: `'./carpeta/*.md'` (Busca todos los archivos Markdown en esa carpeta).
   - Opciones: `{ eager: true }` es necesario para obtener los datos de inmediato en tiempo de compilación.

2. **Propiedades Automáticas**:
   Al importar archivos con glob, cada objeto resultante contiene:
   - `url`: La ruta URL generada automáticamente para ese archivo (ideal para el `href` de los enlaces).
   - `frontmatter`: Todo el contenido del YAML de ese archivo (títulos, etiquetas, etc.).

3. **Renderizado Dinámico**:
   Usamos `.map()` para transformar el array de archivos en elementos HTML (`<li>`, `<a>`).

### EJEMPLO

~~~astro
---
const allPosts = Object.values(import.meta.glob('./markdown/*.md', { eager: true }));
---
<ul>
    {allPosts.map((post:any) => <li><a href={post.url}>{post.frontmatter.title}</a></li> )}
</ul>
~~~

## CREAR PÁGINAS DINÁMICAMENTE (getStaticPaths)

Las rutas dinámicas permiten generar múltiples páginas a partir de un solo archivo `.astro`.
El nombre del archivo debe ir entre corchetes para indicar que es dinámico: `src/pages/tags/[tag].astro`.

1. **`getStaticPaths()`**: Función que retorna un array de objetos. Cada objeto debe tener una propiedad `params` que defina el valor de la ruta.
2. **Generación automática**: Astro creará una página real por cada objeto definido en el array durante el proceso de compilación.
3. **Consumo de datos**: Usamos `Astro.params` para capturar el valor de la URL y personalizar el contenido de la página.

~~~astro
---
import BaseLayout from '../../layouts/Base.astro'

export async function getStaticPaths() {
    return [
        { params: { tag: "pag1" } },
        { params: { tag: "pag2" } },
        { params: { tag: "pag3" } },
    ];
}

const {tag} = Astro.params;
---
<BaseLayout tituloPage={tag}>
    <p>Entrada etiquetadas con {tag}</p>
</BaseLayout>
~~~

## PROPS EN RUTAS DINÁMICAS

Esta técnica permite que cada página generada dinámicamente reciba información específica del sitio (como una lista de artículos) para procesarla de forma independiente.
Aprovechando que el archivo `[tag].astro` actúa como un embudo: recibe todos los posts, pero gracias al filtrado, solo deja pasar los que coinciden con el nombre del archivo (la ruta).

### Ventajas

- **Páginas de Índice:** Permite crear páginas automáticas para etiquetas, autores o categorías.
- **Eficiencia:** Solo filtramos los datos que necesitamos para esa URL específica.

### Elementos Clave

1. **`props` en `getStaticPaths`**: Es el objeto encargado de enviar datos desde la configuración de la ruta hacia el HTML del componente.
2. **`Astro.props`**: Recupera los datos enviados para que podamos trabajar con ellos.
3. **Lógica de Filtrado**: Permite que la página `/tags/astro` solo muestre los posts cuyo YAML contenga la etiqueta "astro".

~~~astro
---
import BaseLayout from '../../layouts/Base.astro'

export async function getStaticPaths() {
    const allPost = Object.values(import.meta.glob('../markdown/*.md', {eager: true})); 

    return [
        { params: { tag: "pag1" }, props: {posts: allPost}},
        { params: { tag: "pag2" }, props: {posts: allPost} },
    ];
}

const {tag} = Astro.params;
const {posts} = Astro.props;
const filteredPosts = posts.filter((post:any) => post.frontmatter.tags?.includes(tag))
---

<BaseLayout tituloPage={tag}>
    <p>Entrada etiquetadas con {tag}</p>
    <ul>
        {filteredPosts.map((post: any) => <li><a href={post.url}>{post.frontmatter.title}</a></li>)}
    </ul>
</BaseLayout>
~~~

## GENERAR PÁGINAS A PARTIR DE ETIQUETAS EXISTENTES

Se deja de escribir los nombres de las rutas a mano. El archivo `[tag].astro` se convierte en un generador automático que "lee" los archivos Markdown y crea páginas en función de las etiquetas existentes.

### Funcionamiento de: `getStaticPaths`

1. **Obtención:** Traemos todos los posts con `import.meta.glob`.
2. **Extracción y Limpieza:**
   - Usamos `.map()` para sacar los arrays de etiquetas.
   - Usamos `.flat()` para convertir una "lista de listas" en una sola lista plana.
   - Usamos `new Set()` para eliminar duplicados (si 5 posts tienen la etiqueta "astro", solo queremos una página de "astro").
3. **Mapeo de Rutas:** Devolvemos un objeto por cada etiqueta única, enviando los posts ya filtrados mediante `props`.

### 3. Funciones adicionales

Es importante entender estas tres herramientas para manipular los datos:

- **`flat()`**: Aplana arrays anidados → `[[A], [B, C]]` → `[A, B, C]`.
- **`new Set()`**: Estructura de datos que almacena valores únicos. → `[A, A, B]` → `{A, B}`.
- **`Spread operator (...)`**: Convierte el `Set` de nuevo en un `Array` para poder usar métodos como `.map()`.

~~~astro
---
import BaseLayout from '../../layouts/Base.astro'

export async function getStaticPaths() {
    const allPost = Object.values(import.meta.glob('../markdown/*.md', {eager: true}));

    const uniqueTags = [...new Set(allPost.map((post:any) => post.frontmatter.tags).flat())]

    return uniqueTags.map((tag) => {
        const filteredPosts = allPost.filter((post:any) => post.frontmatter.tags.includes(tag))
        return {
            params: {tag},
            props: {posts: filteredPosts},
        }
    })
}

const {tag} = Astro.params;
const {posts} = Astro.props;
---

<BaseLayout tituloPage={tag}>
    <p>Entrada etiquetadas con {tag}</p>
    <ul>
        {posts.map((post: any) => <li><a href={post.url}>{post.frontmatter.title}</a></li>)}
    </ul>
</BaseLayout>
~~~

## CREAR PÁGINA ÍNDICE DE ETIQUETAS

Una vez automatizado la creación de paginas para los posts podemos crear un índice,
en la misma ruta de `pages/tags/` creamos un `index.astro` donde se hará el indice.

Usando las funciones de `glob` para obtener el contenido de los archivos `.md`
y el uso de `frontmatter + Set` para filtrar los valores de las etiquetas y crear el array de objetos.

Lo invocamos en el `html`, ahí podemos usar `style` para estilizarlo o podemos meterlo en un layout o componente

~~~astro
---
import BaseLayout from '../../layouts/Base.astro'
const allPosts = Object.values(import.meta.glob('../markdown/*.md', { eager: true }));
const tags = [...new Set(allPosts.map((post: any) => post.frontmatter.tags).flat())];

---
<BaseLayout tituloPage="Índice de etiquetas">
    <div class="tags">{tags.map((tag) => (<p class="tag"><a href={`/tags/${tag}`}>{tag}</a></p>))}</div>
</BaseLayout>

~~~
