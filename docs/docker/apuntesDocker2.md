# DOCKER II

## CONFIGURACIÓN DE UN DOCKER

Una vez creada la infraestructura tenemos que instalar los frameworks y sus dependencias.
Asi como poder ver el front en tiempo real, la base de datos y usar comando como `npm run dev`.

1. Nos metemos en la carpeta de frontend del docker
`docker compose -f docker-compose-dev.yml exec frontend sh`
2. Instalamos el primer framework que es astro.
`npm create astro@latest .`
3. Luego ñadimos la extensión de astro con
`npx astro add react`
4. En caso de error usamos el comando `npm install`y luego el paso 3 otra vez.
5. Con todo instalado para poder "ver" nos vamos al archivo `package.json` y editamos la línea:
`"dev": "astro dev --host",`
6. Para mejor funcioanmiento desactivamos la telemetria
`npx astro telemetry disable`

## COMANDOS FRONTEND

~~~cmd
docker compose -f docker-compose-dev.yml up -d

docker compose -f docker-compose-dev.yml exec frontend sh

npm run dev

docker compose -f docker-compose-dev.yml down
~~~
