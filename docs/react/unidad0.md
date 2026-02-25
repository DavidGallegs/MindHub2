# UNIDAD 0

## REQUSITOS E INSTALACIÓN

- Tener instalado `node.js` y en VisualStudio activar la opción de `format on save` en configuración
- Instalar en VS las extensiones: `VS Code ES7+ React/Redux/React-Native/JS snippets` y `ESLint`

- Instalación de React:
  - `npm create vite@latest`
  - Indicar nombre del proyecto
  - Seleccionamos el FrameWork: React
  - Seleccionamos vairante: TypeSrcript
  - Escribimos `cd app_name`, `npm i`
  
- Para ver nuestra app en navegador usamos `npm run dev`

## ESTRUCTURA DEL PROYECTO

- Carpeta **node_modules** → Contiene las dependencias del proyecto.
- Carpeta **public** → Imagenes, vídeos o documentos que el usuario puede descargar.
- Carpeta **src** → Capreta donde se desarrolla el código.
- Archivos **.gitignore**, **eslint.config.js** → archivos de configuración y git.
- Archivo **Index.html** → Contiene el `div` root que es donde se encuentra toda la aplicación.
- Archivo **package.json** → Contiene otras dependencias del proyecto.
- Archivos de confguración de TypeScript.
- Archivo de configuración de Vite.

## ARCHIVO MAIN.TSX (El Conector)

Es el **punto de entrada** de la aplicación. Su única misión es conectar el código de React con el mundo real (el navegador).

- **¿Qué hace?:** Busca el `<div id="root"></div>` en tu `index.html` y le "inyecta" toda la aplicación de React.
- **¿Cuándo se toca?:** * Para importar archivos de **estilos globales** (`index.css`).

## ARCHIVO APP.TSX (El Contenedor Maestro)

Es el **componente raíz** (Root Component). Es el primer componente de React que se renderiza y el "padre" de todos los demás.

- **¿Qué hace?:** Sirve como la estructura principal de tu web. Aquí es donde decides qué componentes se muestran
- Sirve para importar y organizar componentes y gestionar estados o rutas de navegación.
