# UNIDAD N

## BIBLIOTECA: AUTH ASTRO

`npx astro add node` -> Le da a Astro el motor de servidor (SSR) necesario para manejar sesiones.

`npx astro add auth-astro` -> Instala la librería principal y la inyecta en el astro.config.mjs.

`npm install @auth/core` -> Descarga los tipos explícitos para que TypeScript y VS Code te ayuden con el autocompletado y no te marquen errores en rojo en tu auth.config.ts.
Instalamos tambien la extension en VS llamada `version lens`

### 1. BASE DE DATOS

Creamos una base de datos con los capos id, correo y password

~~~sql
CREATE TABLE usuarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    correo VARCHAR(255) NOT NULL UNIQUE,
    password_hash VARCHAR(255) NOT NULL
);
~~~

### 2. CREACIÓN DEL JOIN Y LOGIN

Se crea un diseño de un login y join en `pages`
La lógica del formulario de join es un formulario con un fetch que guarda un usuario y contraseña en la base de datos en caso de no existir.

### 3. CONFIGURACIÓN .ENV

Creamos un archivo `.env` en nuestra carpeta de `frontend`
Podemos usar un generador para crear la cadena de `AUTH_SECRET`

~~~env
AUTH_SECRET="Bk2p5A/m+d9cO...="
AUTH_TRUST_HOST=true
~~~

### 4. CONFIGURACIÓN DEL AUTH

Con el diseño creado y ya con cuentas en la BD, vamos configurar el auth.

Se crea un archivo `auth.config.ts` (Con ts) en la carpeta raiz

1. Las improtaciones de la biblioteca y el tipado de los campos al ser ts

    `Credentials`: Auth-Astro soporta decenas de formas de entrar (Google, GitHub, Facebook...). Al importar Credentials, le estamos diciendo: "No vamos a usar redes sociales, vamos a usar el método clásico de correo y contraseña propios".

    `LaravelUser`: Es una interfaz de TypeScript. Sirve como un "contrato" o molde. Le dice a tu editor de código exactamente qué forma tienen los datos que Laravel te va a devolver.

    ~~~ts
    import Credentials from '@auth/core/providers/credentials';
    import { defineConfig } from 'auth-astro';

    interface LaravelUser {
    id: string;
    name: string;
    email: string;
    token: string;
    }
    ~~~

2. Creación de la función de configuración

    ~~~ts
    export default defineConfig({})
    ~~~

3. En `Credentials` se indica a auth-Astro que campos esperamos recibir.

    ~~~ts
        providers: [
            Credentials({
            name: 'Credentials',
            credentials: {
            email: { label: "Email", type: "email" },
            password: { label: "Password", type: "password" }
        },
        ...
    ~~~

4. Proteccion ante datos vacios

    ~~~ts
        async authorize(credentials) {
        if (!credentials?.email || !credentials?.password) return null;
    ~~~

5. Llamada al backend y se valida si la contraseña es correcta para ese usuario

    ~~~ts
        try {
          // LLAMADA AL BACKEND (Dentro de la red de Docker)
          const response = await fetch("http://backend:8000/api/login", {
            method: "POST",
            headers: { 
              "Content-Type": "application/json",
              "Accept": "application/json"
            },
            body: JSON.stringify({
              email: credentials.email,
              password: credentials.password,
            }),
          });

          const data = await response.json();

          // Si Laravel dice que ok, devolvemos el objeto usuario
          if (response.ok && data.user) {
            return {
              id: data.user.id,
              name: data.user.name,
              email: data.user.email,
              token: data.token, // Guardamos el token de Laravel (Sanctum/JWT)
            };
          }

          return null; // Login fallido
        } catch (error) {
          console.error("Error en la conexión con Laravel:", error);
          return null;
        }
    ~~~

6. Las callbacks (Empaquetador JWT): Los valores de nombre, id , token laravel se inyectan en JWT (JSON Web Token), una cookie de navegar muy segura.

Por otro lado tenemos las session, que al cargar una página nueva en la web, se lee la cookie encriptada, extrae los datos y los mete en el objeto session.user.

~~~ts
    callbacks: {
        async jwt({ token, user }) {
        // Si acabamos de loguear, metemos los datos del usuario en el JWT de Auth-Astro
        if (user) {
            token.userData = user;
        }
        return token;
        },
        async session({ session, token }) {
        // Pasamos los datos del JWT a la sesión que leeremos en el cliente (React)
        if (session.user) {
            session.user = token.userData as any;
        }
        return session;
        }
    }
~~~

### 5. CÓDIGO FINAL

~~~ts
import Credentials from '@auth/core/providers/credentials';
import { defineConfig } from 'auth-astro';

// 1. Definimos la interfaz del usuario que viene de Laravel para que TS no se queje
interface LaravelUser {
  id: string;
  name: string;
  email: string;
  token: string;
}

export default defineConfig({
  providers: [
    Credentials({
      name: 'Credentials',
      credentials: {
        email: { label: "Email", type: "email" },
        password: { label: "Password", type: "password" }
      },
      // 2. Esta función es el "corazón" del login
      async authorize(credentials) {
        if (!credentials?.email || !credentials?.password) return null;

        try {
          // LLAMADA AL BACKEND (Dentro de la red de Docker)
          const response = await fetch("http://backend:8000/api/login", {
            method: "POST",
            headers: { 
              "Content-Type": "application/json",
              "Accept": "application/json"
            },
            body: JSON.stringify({
              email: credentials.email,
              password: credentials.password,
            }),
          });

          const data = await response.json();

          // Si Laravel dice que ok, devolvemos el objeto usuario
          if (response.ok && data.user) {
            return {
              id: data.user.id,
              name: data.user.name,
              email: data.user.email,
              token: data.token, // Guardamos el token de Laravel (Sanctum/JWT)
            };
          }

          return null; // Login fallido
        } catch (error) {
          console.error("Error en la conexión con Laravel:", error);
          return null;
        }
      }
    })
  ],
  // 3. Los Callbacks: El puente para que los datos sobrevivan entre páginas
  callbacks: {
    async jwt({ token, user }) {
      // Si acabamos de loguear, metemos los datos del usuario en el JWT de Auth-Astro
      if (user) {
        token.userData = user;
      }
      return token;
    },
    async session({ session, token }) {
      // Pasamos los datos del JWT a la sesión que leeremos en el cliente (React)
      if (session.user) {
        session.user = token.userData as any;
      }
      return session;
    }
  }
});
~~~

### PROTECCIÓN DE RUTAS

Creamos un archivo que va actuar como protección global que controlara las rutas.
El archivo es `middleware.ts`

~~~ts
// src/middleware.ts
import { getSession } from 'auth-astro/server';
import { defineMiddleware } from 'astro:middleware';

export const onRequest = defineMiddleware(async (context, next) => {
  const session = await getSession(context.request);
  const { pathname } = context.url;

  // 1. LISTA DE RUTAS PRIVADAS (Solo para usuarios logueados)
  const privateRoutes = ['/reserva', '/perfil', '/checkout'];
  
  // Comprobamos si la URL actual EMPIEZA por alguna de las rutas privadas
  const isPrivateRoute = privateRoutes.some(route => pathname.startsWith(route));

  if (isPrivateRoute && !session) {
    // Si es privada y no hay sesión, lo echamos al login
    return context.redirect('/login');
  }

  // 2. LISTA DE RUTAS DE AUTENTICACIÓN (Solo para invitados)
  const authRoutes = ['/login', '/join'];
  
  // Comprobamos si la URL actual ES EXACTAMENTE alguna de estas
  const isAuthRoute = authRoutes.includes(pathname);

  if (isAuthRoute && session) {
    // Si ya tiene sesión e intenta ir al login/join, lo mandamos al inicio
    return context.redirect('/');
  }

  // 3. Si pasa todos los filtros, le mostramos la página normal
  return next();
});
~~~
