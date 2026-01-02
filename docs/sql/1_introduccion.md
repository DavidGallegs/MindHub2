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

Los operadores que tenemos son:  

- Operadores de comparación: `=`, `<`, `>`, `<=`, `>=`, `<>`

| USO DE NOT | EXPLICACIÓN |
| ------------ | ------------ |
| `WHERE NOT (nombre = 'Juan');` | Registros que no tengan el nombre Juan |
| `WHERE nombre NOT LIKE 'P%';` | Registros cuyo nombre no empiece por P |
| `WHERE nombre NOT IN ('Juan', 'Pedro');` | Registros que no tengan el nombre Juan ni Pedro |
| `WHERE edad NOT BETWEEN 18 AND 65;` | Registros que no estén entre 18 y 65 años |

- Comprobación por patrones: Uso del `LIKE` junto con `%` y/o `_`
    `WHERE nombre LIKE 'P%';`  
- Buscar en varios valores: Uso del `IN` y `NOT IN`  
    `WHERE cod_dpto IN ("D003","D004");`  
- Valores nulos: Usando `IS NOT NULL` o `IS NULL`
    `WHERE nombre IS NOT NULL;`
- Rango de valores: Tenemos `BETWEEN` junto con `AND` Se puede usar con valores numéricos y fechas.  
    `WHERE salario BETWEEN 1800 AND 2200`

- Operadores lógicos: `AND`, `OR`, `NOT`
  
~~~sql
SELECT * FROM empleado
WHERE cod_dpto IN ("D003","D005") 
AND (salario BETWEEN 1800 AND 2200)
AND nombre NOT LIKE "L%"
ORDER BY nombre ASC;
~~~

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
