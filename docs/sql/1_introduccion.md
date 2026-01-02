# SQL CONSULTAS

## SELECT

La sentencia `SELECT` sirve para seleccionar columnas.  
Para seleccionar todos las columnas de una tabla usamos `*`  
`SELECT * FROM empleados;`

Las columnas pueden tener `etiquetas` que se usa colocando una plabra entre comillas.  
`SELECT nompro "Nombre Profesor", salpro Salario from profesores;`

Podemos crear frases usando `|''|` por ejemplo:  
`SELECT nompro || 'TIENE LA ESPECIALIDAD EN ' || esppro ESPECIALIDAD from profesores;`

Para evitar repetir registros usamos `DISTINCT`  
`SELECT COUNT(DISTINCT nombre) FROM empleados;`

## WHERE

La sentencia `WHERE` sirve para clasificar o buscar registros específicos.  
**Recuerda:** En SQl Oracle usamos `''` para valores de texto VARCHAR2 o CHAR.  

### OPERADORES

- Operadores de comparación: `=`, `<`, `>`, `<=`, `>=`, `<>`

- Comprobación por patrones: Uso del `LIKE` junto con caractéres `%` y/o `_`
    `WHERE nombre LIKE 'P%';`  

- Buscar en varios valores: Uso del `IN` y `NOT IN`  
    `WHERE cod_dpto IN ('D003','D004');`  

- Valores nulos: Usando `IS NOT NULL` o `IS NULL`
    `WHERE nombre IS NOT NULL;`

- Rango de valores: Tenemos `BETWEEN` junto con `AND` Se puede usar con valores numéricos y fechas.  
    `WHERE salario BETWEEN 1800 AND 2200`

- Operadores lógicos: `AND`, `OR`, `NOT`

| USO DE NOT | EXPLICACIÓN |
| ------------ | ------------ |
| `WHERE NOT (nombre = 'Juan');` | Registros que no tengan el nombre Juan |
| `WHERE nombre NOT LIKE 'P%';` | Registros cuyo nombre no empiece por P |
| `WHERE nombre NOT IN ('Juan', 'Pedro');` | Registros que no tengan el nombre Juan ni Pedro |
| `WHERE edad NOT BETWEEN 18 AND 65;` | Registros que no estén entre 18 y 65 años |

~~~sql
SELECT * FROM empleado
WHERE cod_dpto IN ("D003","D005") 
AND (salario BETWEEN 1800 AND 2200)
AND nombre NOT LIKE "L%"
ORDER BY nombre ASC;
~~~

### FUNCIONES A NIVEL DE FILA (CAMPOS)

| FUNCIÓN DE CARACTARES | DESCRIPCIÓN |
| -------- | ---------- |
| `LOWER(CAMPO)` | Convierte a minúsculas todos los caracteres |
| `UPPER(CAMPO)` | Convierte a mayúsculas todos los caracteres |
| `INITCAP(CAMPO)` | Convierte a mayúscula la primera letra |

| MANIPULACIÓN DE CARACTARES | DESCRIPCIÓN |
| -------- | ---------- |
| `CONCAT(CAMPO\|Expresión, CAMPO\|Expresión)` | Concatena 2 valores, ya sean campos o cadenas |
| `SUBSTR(CAMPO,Inicio,Longitud)` | Exrae subcadenas (Inicio no es 0) |
| `LENGTH(CAMPO)` | Devuelve la longitud de la cadena |
| `INSTR(CAMPO,'caracter')` | Devuelve la posición del caractre que se busca |
| `LPAD(CAMPO,longitud,'caracter')` | Coloca a la izquieda un caracter hasta rellenar. Funciona si longitud > Length(campo) |
| `RPAD(CAMPO,longitud,'caracter')` | Coloca a la derecha un caracter hasta rellenar. Funciona si longitud > Length(campo) |
| `REPLACE(CAMPO,'caracter','remplazo')` | Remplaza subcadeas por otras subcadenas |
| `TRANSLATE(CAMPO,'caracter','remplazo')` | Remplaza caracteres por otros caracteres y puede borrar |
| `TRIM(CAMPO), LTRIM(CAMPO,''), RTRIM(CAMPO,'')` | Elimina espacios en blanco o caracteres |

### FUNCIONES MATEMÁTICAS

| FUNCIONES MATEMÁTICAS | DESCRIPCIÓN |
| -------- | ---------- |
| `ROUND(CAMPO,N)` | Redondea a N decimales |
| `TRUNC(CAMPO,N)` | Trunca a N decimales |
| `MOD(CAMPO,N)` | Devuelve el resto de la división |
| `ABS(CAMPO)` | Devuelve el valor absoluto |
| `CEIL(CAMPO)` | Redondea hacia arriba al entero más cercano |
| `FLOOR(CAMPO)` | Redondea hacia abajo al entero más cercano |
| `POWER(CAMPO,N)` | Eleva un valor a N |
| `SIGN(CAMPO)` | Si es mayor a 0 devuelve 1, si es negativo -1 y si es 0 da 0 |
| ``SQRT(CAMPO)` | Devuelve la raiz cuadrada |

### FUNCIONES DE FECHAS

Por lo general las fechas se devuelven DD/MM/AA.  
Se pueden añadir y quitar dias con `+` y `-`  
La resta entre fechas devuelve la diferencia de días.  

| FUNCIONES DE FECHA | DESCRIPCIÓN |
| -------- | ---------- |
| `MONTHS_BETWEEN(F1,F2)` | Devuelve los meses de diferencia |
| `ADD_MONTHS(F,N)` | Añade N meses a la fecha |
| `NEXT_DAY (F,'DÍA')` | Devuelve la fecha del día marcado usando de punto de partida F |
| `LAST_DAY(F)` | Devuelve el último día de ese mes |
| `TRUNC(F,'FORMAT')` | Trunca al formato indicado |
| `ROUND(F,'FORMAT')` | Redondea al formato indicado |
| `EXTRACT('DAY \| MONTH \| YEAR'FROM CAMPO)` | Extrae un valor de la fecha |
| `TO_CHAR(F,'FORMAT')` | Convierte una fecha a una cadena de otro formato |

- Para el `TO_CHAR` tenemos los formatos de: `Y,YY,YYY,YYY, YEAR`, `MM,MON,MONTH`,`DY,DAY,SYEAR,DD,DDD`

## ORDER BY

Podemos ordenar alfabéticamente, fechas y números usamos `ORDER BY`  
Se puede ordenar de forma ascendente con `ASC` y descendente con `DESC`  
Su estructura es: `SELECT nombre FROM empleados ORDER BY nombre ASC`  
Podemos usar como valores los nombres de los campos o números que indican la posición del campo en el `SELECT`

## ALIAS

Se usa para darle a una columna o tabla un nombre temporal.  

~~~sql
-- Alias tabla y columna
SELECT salario AS dinero FROM empleado AS trabajadores;

-- Alias grupal
SELECT CONCAT(dni, ' ', nombre, ' ', apellidos) AS informacion_empleado
FROM empleado;
~~~

## GROUP BY

El `GROUP BY` se usa para agrupar filas que tienen el mismo valor
en una o varias columnas, y aplicar funciones de agregación
sobre cada grupo.

Y toda columna del SELECT que no esté dentro de una función
de agregación debe aparecer en el GROUP BY.

~~~sql
-- Ejemplo
SELECT cod_dpto, COUNT(*) AS "Empleados por departamento" FROM empleado
GROUP by cod_dpto;

-- Ejemplo con JOIN
SELECT e.cod_dpto, d.nombre AS "Nombre Departametno", COUNT(*) AS "Cantidad de empleados"  
FROM empleado AS e
INNER JOIN departamento AS d ON d.cod_dpto = e.cod_dpto
GROUP BY e.cod_dpto, d.nombre;
~~~

## HAVING

La cláusula `HAVING` se usa para filtrar grupos creados con `GROUP BY`,
usando condiciones sobre funciones de agregación.

~~~sql
SELECT e.cod_dpto, d.nombre AS "Nombre Departametno", COUNT(*) AS "Cantidad de empleados"  
FROM empleado AS e
INNER JOIN departamento AS d ON d.cod_dpto = e.cod_dpto
GROUP BY e.cod_dpto, d.nombre
HAVING COUNT(*) >= 2;
~~~

## ORDEN CORRECTO EN UNA CONSULTA

1. `SELECT`
2. `FROM`
3. `WHERE`
4. `GROUP BY`
5. `HAVING`
6. `ORDER BY`

~~~sql
SELECT d.nombre AS departamento, COUNT(e.cod_empleado) AS total_empleados
FROM empleado AS e
INNER JOIN departamento AS d
ON e.cod_dpto = d.cod_dpto
WHERE e.salario > 1200
GROUP BY d.nombre
HAVING COUNT(e.cod_empleado) >= 2
ORDER BY total_empleados DESC;
~~~

<!--https://www.w3schools.com/mysql/mysql_exists.asp -->