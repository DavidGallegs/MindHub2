# JOINS

## INNER JOIN

En los `INNER JOIN` une filas de dos o más tablas mostrando únicamente
los registros que cumplen la condición de relación entre ellas.  
No es necesario que los nombres de los campos coincidan,
pero los valores sí deben coincidir para que la fila aparezca en el resultado.  
Se pueden encadenar múltiples `INNER JOIN` para unir varias tablas.

~~~sql
-- Empleados con departamento (Muestra todos los empleados menos Lucía que no tiene departamento)
SELECT e.nombre as "Nombre Empleado", d.cod_dpto as "Departamento" 
FROM empleado AS e
INNER JOIN departamento AS d ON d.cod_dpto = e.cod_dpto;

-- Empleados con departamento y el departamento con empresa
SELECT e.nombre AS empleado, d.nombre AS departamento, em.nombre AS empresa
FROM empleado e
INNER JOIN departamento d ON e.cod_dpto = d.cod_dpto
INNER JOIN empresa em ON d.cod_empresa = em.cod_empresa;

~~~

## LEFT JOIN

LEFT JOIN devuelve todos los registros de la tabla izquierda (Tabla1),
junto con los registros coincidentes de la tabla derecha (Tabla2).  
Si no existe coincidencia en la tabla derecha, las columnas correspondientes se rellenan con NULL.  

~~~sql
-- Todos los empleados incluyendo los que no tienen departamento (Aparece Lucia)
SELECT e.nombre as "Nombre Empleado", d.cod_dpto as "Departamento" 
FROM empleado AS e
LEFT JOIN departamento AS d ON d.cod_dpto = e.cod_dpto;
~~~

## RIGHT JOIN

Las `RIGHT JOIN` devuelve todos los registros de la tabla derecha (Tabla2),
junto con los registros coincidentes de la tabla izquierda (Tabla1).  
Si no existe coincidencia en la tabla izquierda, las columnas correspondientes se rellenan con NULL.  

~~~sql
-- Todos los departamentos y los que no tienen empleados asignados
SELECT e.nombre as "Nombre Empleado", d.cod_dpto as "Departamento" 
FROM empleado AS e
RIGHT JOIN departamento AS d ON d.cod_dpto = e.cod_dpto;
~~~

## CROSS JOIN

Las `CROSS JOIN` es un tipo de JOIN que devuelve el producto cartesiano
de dos tablas, es decir, combina **cada fila de la primera tabla**
con **cada fila de la segunda tabla**.
No requiere condición de relación (no usa ON).

~~~sql
-- Cross entre empleado y proyecto
SELECT p.nombre AS "Nombre Proyecto", e.nombre AS "Nombre Empleado" 
FROM empleado AS e
CROSS JOIN proyecto AS p;
~~~

## FULL OUTER JOIN

En las `FULL OUTER JOIN` obtenemos los registros de A, B y su intersección.

~~~sql
-- Muestra el nombre de los profesores y el curso al que imparten. SI no tienen curso, sale NULL
SELECT p.nompro AS profesor, c.numcur AS curso
FROM profesores p
FULL OUTER JOIN cursos c ON p.numpro = c.numpro;
~~~

## SELF JOIN

Un `SELF JOIN` es un JOIN donde una tabla se une consigo misma.
Se utiliza para comparar filas dentro de la misma tabla.

~~~sql
-- Empareja cada empleado con el elmpleado cuyo codigo coincide con su jefe_id (INNER: Muestra empleados con jefes)
SELECT e.nombre AS cod_empleado, j.nombre AS jefe 
FROM empleado AS e
INNER JOIN empleado AS j ON e.jefe_id = j.cod_empleado

-- LEFT JOIN: Muestra empleados con o sin jefes.
SELECT e.nombre AS cod_empleado, j.nombre AS jefe 
FROM empleado AS e
LEFT JOIN empleado AS j ON e.jefe_id = j.cod_empleado

-- RIGHT JOIN: Muestran todos los jefes, aunque no tengan nadie a su cargo, por eso NULL empleado y crea falsos jefes.
SELECT e.nombre AS cod_empleado, j.nombre AS jefe 
FROM empleado AS e
RIGHT JOIN empleado AS j ON e.jefe_id = j.cod_empleado
~~~
