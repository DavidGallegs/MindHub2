# FUNCIONES SQL

## MIN() y MAX()

La función `MIN()` devuelve el valor más pequeño de una columna.  
Y la función `MAX()` devuelve el valor más grande de una columna.

~~~sql
SELECT MIN(salario) AS Menor_Salario FROM empleado;

SELECT MAX(salario) AS Mayor_Salario FROM empleado;
~~~

### COUNT(), AVG(), SUM()

Función `COUNT()` devuelve el número de registros que coinciden con la condición.  
La función `AVG()` devuelve el promedio de una columna numérica.  
Y la función `SUM()` devuelve la suma de una columna numérica.  

~~~sql
SELECT COUNT(salario) FROM empleado
WHERE salario > 2200;

SELECT AVG(salario) AS media_D002 FROM empleado
WHERE cod_dpto = "D002";

SELECT SUM(salario) AS total_D001 FROM empleado
WHERE cod_dpto = "D001";
~~~
