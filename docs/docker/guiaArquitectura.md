# GUÍA: ENTORNO DE PRUEBAS

## INSTALAR LINUX EN WSL

1. `wsl --install -d Ubuntu` → Instala Ubuntu.
    - Se define un user y una contraseña.
2. `wsl --set-default Ubuntu` → Colocamos Ubuntu como default.
3. Instalamos en VisualStudio la extension de WSL.
4. Aparece un simbolo `><` en la barra inferior con el que nos podremos conectar a WSL.
    - En la primera conexión a WSL elegimos la opción: `Conectar a WSl mediante distribución → Ubuntu`

## CREACIÓN DE LA ESTRUCTURA

~~~doc
📁 app/
├── 📃 docker-compose-dev.yml       
├── 📁 docker/                     
│   ├── 📃 php.Dockerfile         
│   └── 📃 node.Dockerfile         
├── 📁 frontend/                   
└── 📁 backend/
~~~

1. Nos conectamos desde VisualStudio a WSL Ubuntu → /home/user/. Y creamos un proyecto con esa estructura.
    - Código en la carpeta de ejemplos.
2. Usamos `docker compose -f docker-compose-dev.yml up -d --build` para crear la estructura.

## CONFIGURACIÓN DOCKER FRONTEND

1. Nos metemos dentro del docker de frontend: `docker compose -f docker-compose-dev.yml exec frontend sh`
2. Instalamos Astro: `npm create astro@latest`
   - Nombre de la carpeta del proyecto es un `.`
3. Instalamos React: `npx astro add react`
4. Salimos del contenedor FrontEnd con `exit`
5. Otorgamos permisos para editar archivos: `sudo chown -R $USER:$USER frontend/`
6. Configuramos el `package.json`:
   - Quitamos el simbolo `^` para evitar actualizaciones automáticas en `"dependences"`.
   - Añadimos la palabra `--host` a la línea: `"dev": "astro dev --host",`

7. Optimización de TypeScript (Evitar errores fantasma en WSL):
   Para que VS Code no marque errores de archivos borrados y funcione fluido en Ubuntu:
   - Vamos a **Settings** → pestaña **Remote [WSL: Ubuntu]**.
   - Buscamos `typescript watch` y pulsamos en **Edit in settings.json**.
   - Pegamos este bloque para sincronizar el editor con los eventos de Linux:

   ~~~json
   {
       "js/ts.tsserver.watchOptions": "vscode",
       "typescript.tsserver.watchOptions": {
           "watchFile": "useFsEvents",
           "watchDirectory": "useFsEvents",
           "fallbackPolling": "dynamicPriority"
       }
   }
   ~~~

   - Finalmente, refrescamos el editor: `F1` -> **Developer: Reload Window**.

### VERSIONES DE ESTA GUÍA FRONTEND

~~~json
"dependencies": {
    "@astrojs/react": "4.4.2",
    "@types/react": "19.2.14",
    "@types/react-dom": "19.2.3",
    "astro": "5.17.1",
    "react": "19.2.4",
    "react-dom": "19.2.4"
  }
~~~

### COMANDOS FRONTEND

~~~cmd
docker compose -f docker-compose-dev.yml up -d

docker compose -f docker-compose-dev.yml exec frontend sh

npm run dev

docker compose -f docker-compose-dev.yml down
~~~

## CONFIGURACIÓN DOCKER BACKEND

1. Nos metemos dentro del docker de backend: `docker compose -f docker-compose-dev.yml exec backend bash`
2. Instalamos Laravel siguiendo estos pasos

    ~~~bash
    rm -rf /var/www/html/*
    cd /tmp
    composer create-project laravel/laravel proyecto-temp
    cp -a /tmp/proyecto-temp/. /var/www/html/
    ~~~

3. Volvemos a la carpeta de trabajo y damos permisos al servidor web:

    ~~~bash
    cd /var/www/html
    chmod -R 777 storage bootstrap/cache
    ~~~

4. Salimos del contenedor con `exit`
5. Otorgamos permisos para editar archivos: `sudo chown -R $USER:$USER backend/`
6. Configuramos el fragmento de la base de datos del archivo `.env`

    ~~~env
    DB_CONNECTION=mysql
    DB_HOST=base_datos
    DB_PORT=3306
    DB_DATABASE=app_db
    DB_USERNAME=root
    DB_PASSWORD=root 

    SESSION_DRIVER=file <!-- Buscar y editar esta línea-->
    ~~~

7. En el `composer.json` eliminamos los `^` del array `"require"` para evitar actualziaciones automáticas.

### VERSIONES DE ESTA GUÍA BACKEND

~~~json
    "require": {
        "php": "8.2",
        "laravel/framework": "12.0",
        "laravel/tinker": "2.10.1"
    },
~~~

### COMANDOS BACKEND

~~~cmd
docker compose -f docker-compose-dev.yml up -d

docker compose -f docker-compose-dev.yml exec backend bash

docker compose -f docker-compose-dev.yml down
~~~

## EXTENSIONES EN WSL:UBUNTU

Al estar en el WSL:Ubuntu, tenemos que volver a instalar las extensiones de Localhost → WSL:Ubuntu.
Aunque algunas ya están activas por defecto.
