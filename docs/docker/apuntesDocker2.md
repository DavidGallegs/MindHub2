# DOCKER II

## CONFIGURACIÓN DE UN DOCKER FRONTEND

Una vez creada la infraestructura tenemos que instalar los frameworks y sus dependencias.
Asi como poder ver el front en tiempo real, la base de datos y usar comando como `npm run dev`.

1. Nos metemos en la contenedor de frontend
`docker compose -f docker-compose-dev.yml exec frontend sh`
2. Instalamos el primer framework que es astro.
`npm create astro@latest .`
3. Instalamos las dependencias faltantes con `npm install`
4. Luego añadimos la integración de React
`npx astro add react`

5. Para poder "ver" nos vamos al archivo `package.json` y editamos la línea poniendo:
`"dev": "astro dev --host",`
6. Para mejor funcionamiento desactivamos la telemetria en el `.yml`

~~~yml
ports:
    ...
environment:
      - ASTRO_TELEMETRY_DISABLED=1
~~~

## COMANDOS FRONTEND

~~~cmd
docker compose -f docker-compose-dev.yml up -d

docker compose -f docker-compose-dev.yml exec frontend sh

npm run dev

docker compose -f docker-compose-dev.yml down
~~~

## CONFIGURACIÓN DE UN DOCKER BACKEND

1. Nos metemos en la carpeta de backend
`docker compose -f docker-compose-dev.yml exec backend bash`
2. Instalamos Laravel

~~~bash
rm -rf /var/www/html/*
cd /tmp
composer create-project laravel/laravel proyecto-temp
cp -a /tmp/proyecto-temp/. /var/www/html/
~~~

Volvemos a la carpeta de trabajo y damos permisos al servidor web:
`cd /var/www/html`
`chmod -R 777 storage bootstrap/cache`

Configurar archivo `.venv` y buscamos el apartado de `DB_CONNECTION=`
y pegamos todo este código:

~~~venv
DB_CONNECTION=mysql
DB_HOST=base_datos
DB_PORT=3306
DB_DATABASE=app_db
DB_USERNAME=root
DB_PASSWORD=root
~~~

### COMANDO BACKEND

~~~cmd
docker compose -f docker-compose-dev.yml up -d

docker compose -f docker-compose-dev.yml exec backend bash

docker compose -f docker-compose-dev.yml down
~~~

## OPTIMIZACIÓN ENTRE DOCKERS

### INSTALACIÓN DE LINUX EN WSL

En PowerShell instalaremos linux: `wsl --install -d Ubuntu`.
Tras la instalación creamos un user con una contraseña.
Con esto logramos que en linux WSL aparezca la carpeta de ubuntu.
Luego indicamos cual es el principal: `wsl --set-default Ubuntu`

En el explorador de windows en Linux > Ubuntu > home > user:
pegamos el proyecto que se va a optimizar.

Por otro lado en VS instalamos la extension de WSL para acceder.
Aparecera un simbolo `><` con el que nos podremos conectar a WSL
usando el conectar con WSL usando una distrución → Ubuntu
En WSL ejecutamos el comando up y funcionará como esperamos.

En caso de borrar el proyecto ysamos en la terminal de Ubuntu: `sudo rm -rf <carpeta>`
