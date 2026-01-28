# ASTRO

## CONCEPTOS

- Astro usa una **arquitectura de islas**. Se basa en componentes UI
que se catalogan con islas interactivas (HTML+JS+CSS) y islas estáticas (HTML+CSS)
![imgaen](images/astro_islas.png)

## INSTALAR Y CONFIGURAR ASTRO

- Requisitos: Visual Studio, Node JS (v18-v20) y Terminal
- Astro escuchará todos los cambios en la carpeta `src/`
- En Visual Studio instalar la extensión de Astro

1. `npm create astro@latest`
   ![imagen](images/astro_instalacion.png)
2. `npm run dev` → Inicia servidor de desarrollo
3. `npm run dev` → Crea una carpeta `dis/` con la web
4. `npm run preview` → Muestra la versión final de la web

## ESTRUCTURA DE PROYECTO

- `src/*` → El código fuente de tu proyecto (componentes, páginas, estilos, imágenes, etc.)
- `public/*` → Archivos sin código que no serán procesados (fuentes, íconos, etc, txt, pdf, csv...)
- `package.json` → El manifiesto de tu proyecto
- `astro.config.mjs` → El archivo de configuración de Astro.
- `tsconfig.json` → El archivo de configuración de TypeScript.

En `src` tenemos:
`src/pages` → Paginas de la web.
`src/component` → Componentes de framewroks (Vue o React) y componentes astro.
`src/layouts` → Contiene las plantillas que definene la estructura del UI en una o varias páginas.
`src/styles` → Guarda archivos CSS y/o Sass
