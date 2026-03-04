# UNIDAD 6

En este caso usaremos `Preact`, el react optimizado para mayor velocidad.
`npx astro add react`

## CONSTRUIR ISLAS

Las **Islas (Astro Islands)** son la arquitectura que permite incrustar componentes interactivos (React, Preact, Vue, etc.)
dentro del HTML estático generado por Astro.

### 1. Anatomía de una Isla

Para crear interactividad necesitamos dos partes:

- **El Componente (`.jsx/tsx`):** Contiene la lógica interactiva. Recibe **props** desde Astro y utiliza *Hooks* de React (como `useState`) para manejar cambios en la pantalla (ej. cambiar un saludo al hacer clic).
- **La Invocación (`.astro`):** Importamos el componente y le pasamos los datos necesarios.

### 2. Directivas de Cliente (`client:*`)

El secreto de la velocidad de Astro es que, por defecto, **desactiva el JavaScript** de los componentes de React y los convierte en HTML muerto.
Para "despertar" el componente y que su código funcione en el navegador (proceso llamado **Hidratación**), debemos usar una directiva `client:*`.

| Directiva | ¿Cuándo carga el JavaScript? | Uso Ideal |
| :--- | :--- | :--- |
| **`client:load`** | Inmediatamente, junto con la página. | Elementos críticos que el usuario ve y toca al instante (Menú de navegación principal, Hero interactivo). |
| **`client:idle`** | Cuando la página ya cargó y el navegador tiene un "respiro". | Elementos interactivos que no son de máxima prioridad (Buscadores secundarios, pestañas de información). |
| **`client:visible`** | Solo cuando el componente entra en la pantalla (al hacer scroll). | ¡Ahorro máximo! Carruseles a mitad de página, chats de soporte en el footer o botones de "volver arriba". |
| **`client:only="react"`** | Omite el servidor. Se renderiza 100% en el navegador. | Gráficos complejos o componentes que necesitan acceder a cosas exclusivas del navegador web (como `window.localStorage`). |

Previamente existe un archivo tsx o jsx que esta en `src/components` y se importa al archivo.

~~~astro
---
// Importamos el componente de React
import Greeting from '../components/Greeting';
---
<Greeting client:load messages={["Hej", "Hallo", "Hola"]} />
~~~

## COLECCIONES

<https://docs.astro.build/es/tutorial/6-islands/4/>
