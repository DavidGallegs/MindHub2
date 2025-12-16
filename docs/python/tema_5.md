# TEMA 5

Mejorar apuntes de ficheros y los de SQL porque están incompletos

## ACCESO A FICHEROS

### FICHEROS DE TEXTO

#### LEER FICHERO TXT

~~~txt
Hola mundo
Python es fácil
Examen aprobado
~~~

~~~python
import os
from os import strerror

# Crear la ruta del archivo en la misma carpeta que el script
ruta_carpeta = os.path.dirname(__file__)
ruta_archivo = os.path.join(ruta_carpeta, "ejemplo.txt")

# Lee un fichero de texto
try:
    with open(ruta_archivo, "r", encoding="utf-8") as fichero_txt:
        contenido = fichero_txt.read()
        print(contenido)

except IOError as e:
    print("Error durante la operación de archivos:", strerror(e.errno))
except Exception as e:
    print("Ocurrió un error inesperado:", e)
~~~

#### CREAR FICHERO TXT

~~~python
import os
from os import strerror

ruta_carpeta = os.path.dirname(__file__)
ruta_archivo = os.path.join(ruta_carpeta, "ejemplo.txt")

# Crea un fichero de texto
try:
    with open(ruta_archivo, "w", encoding="utf-8") as fichero_txt:
        fichero_txt.write("Hola mundo\n")
        fichero_txt.write("Segunda línea")

    print(f"Archivo '{ruta_archivo}' creado correctamente.")

except IOError as e:
    print("Error durante la operación de archivos:", strerror(e.errno))
except Exception as e:
    print("Ocurrió un error inesperado:", e)
~~~

### FICHEROS BINARIOS

#### LEER FICHERO BINARIO

~~~bin
Bytes en el archivo:
10 20 30 40
~~~

~~~python
import os
from os import strerror

ruta_carpeta = os.path.dirname(__file__)
ruta_archivo = os.path.join(ruta_carpeta, "datos.bin")

# Lee un fichero binario
try:
    with open(ruta_archivo, "rb") as fichero_bin:
        datos = fichero_bin.read()
        print(datos)

except IOError as e:
    print("Error durante la operación de archivos:", strerror(e.errno))
except Exception as e:
    print("Ocurrió un error inesperado:", e)
~~~

#### CREAR FICHERO BINARIO

~~~python
import os
from os import strerror

ruta_carpeta = os.path.dirname(__file__)
ruta_archivo = os.path.join(ruta_carpeta, "datos.bin")

datos = bytes([10, 20, 30, 40])

# Crea un fichero binario
try:
    with open(ruta_archivo, "wb") as fichero_bin:
        fichero_bin.write(datos)

    print(f"Archivo '{ruta_archivo}' creado correctamente.")

except IOError as e:
    print("Error durante la operación de archivos:", strerror(e.errno))
except Exception as e:
    print("Ocurrió un error inesperado:", e)
~~~

### FICHEROS CSV

Apuntes de ejercicios

### FICHEROS JSON

Apuntes de ejercicios

## DOCKER

1. Instalar docker desktop para windows
    1. Descargar instalador Docker Desktop for Windows x86_64
    2. Durante la instalación elegir opción: Utilizar WSL 2  
    3. Tras la instalación pulsa 'Close & restart'
    4. WSL -> usar "wsl --update", sino esta actualizado  
    5. Confirmamos con `docker --version`

2. Desplegar MySQL y PHPMyAdmin en un docker
    1. Creamos una carpeta mysql en Documentos.
    2. Creamos dentro un archivo llamado docker-compose.yml y pegamos ese código.
    3. Ver la ruta de nuestro docker: `docker info | findstr "Docker Root Dir"`
    4. En terminal nos metemos a la carpeta mysql y desplegamos un contenedor usando `docker compose up -d`
    5. Comprobación con `docker compose ls` y `docker compose ps`
    6. Comprobación con `docker port mysql` y `dcoker port phpma`

3. Flujo de trabajo
   1. Con `docker compose up -d` inicamos el entorno.
   2. Y al terminar con `docker compose stop` paramos el docker

4. Destruir docker
   1. Destruir contenedor y mantener archivos > `docker compose down`
   2. Destir contenedor y volumenes > `docker compose down -v`

5. Conexion a mysql usando sqlplus desde el contenedor
   1. Inciamos sesión en el contenedor > `docker exec -it mysql bash`
   2. Nos metemos en mysql con `mysql -u root -p`

6. Conexión a mysql usando phpMyAdmin
   1. Escribimos en el navegador `http://localhost: 8080`
   2. Y escribimos la contraseña.

7. Conexión a mysql usando un cliente gráfico
   1. Me meto en la carpeta de mysql de Documentos.
   2. Y creo una conexión con la extensiónd de mysql.

## MYSQL

Para funcionar sin problemas instalamos este paquete > `py -m pip install mysql-connector-python`  
Tengo los ejemplos del pdf y los ejemplos

----
CONEXIÓN  

~~~python
import mysql.connector
from mysql.connector import Error
try:
    conexion = mysql.connector.connect(
    host="localhost",
    user="series",
    password="series",
    database="series",
    )

    print(conexion)
    conexion.close()
except Error as e:
    print(f" Error con MySQL: {e}")
~~~

CREAR TABLA  

~~~python
import mysql.connector
from mysql.connector import Error
try:
    conexion = mysql.connector.connect(
        host="localhost",
        user="series",
        password="series",
        database="series",
    )
    cursor = conexion.cursor()
    cursor.execute("CREATE TABLE series (id INT AUTO_INCREMENT PRIMARY KEY, titulo 
    VARCHAR(255) NOT NULL, genero VARCHAR(100));")
    cursor.close()
    conexion.close()
except Error as e:
    print(f" Error con MySQL: {e}")
~~~

INSERTAR UNA FILA  

~~~python

~~~

INSERTAR VARIAS FILAS  

~~~python

~~~

CONSULTAS

~~~python

~~~

~~~python

~~~

~~~python

~~~

ACTUALIZACIONES

~~~python

~~~

BORRAR REGISTROS

~~~python

~~~

BORRAR TABLAS  

~~~python

~~~

GESTIONAR EXEPCIONES

~~~python

~~~

GESTIONAR TRANSACCIONES (COMMIT Y ROLLBACK)

~~~python

~~~
