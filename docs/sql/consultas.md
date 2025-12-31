# SQL CONSULTAS

## SELECT

La sentencia `SELECT` sirve para seleccionar campos.  
Para seleccionar todos los campos de una tabla usamos `*`
    SELECT * FROM empleados;  

Para evitar repetir registros usamos `DISTINCT`  
Y para tener un contador de registros únicos en la tabla usamos `COUNT(DISTINCT)`  
    SELECT COUNT(DISTINCT nombre) FROM empleados;  

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
