# SQL MANIPULACIÓN

## INSERT INTO

Los `INSERT` pueden tener o no todos lo campos.  
Pudedes indicar el `NULL` o que se rellene automáticamente si no pons el campo.  
Con `&` podemos insertar nosotros el campo (Indicando los VARCHAR2 con `''`)  
Y para las fechas podemos usar `TO_DATE()` en vez de `''`  

~~~sql
-- INSERT COMPLETO 
INSERT INTO profesores (numpro,nompro,fnapro,jefpro,finpro,salpro,compro,esppro) 
VALUES (112,'ANGEL TOLEDO','14/05/1990',101,SYSDATE,1230,NULL,'WEB');


-- INSERT FALTA INCMOMPLETO
INSERT INTO profesores (numpro,nompro,fnapro,finpro,salpro,esppro) 
VALUES (114,'LAURA RAMIREZ','14/05/1992',SYSDATE,1530,'WEB');

-- INSERT AGREGANDO VALORES POR EL USUARIO
INSERT INTO profesores(numpro,nompro,fnapro,finpro,salpro,esppro)
VALUES (&numpro,'&nompro','&fnapro','&finpro',&salpro,'&esppro');

-- Ejemplo de INSERT
INSERT INTO profesores(numpro,nompro,fnapro,finpro,salpro,esppro)
VALUES (116,'LAURA GIMENEZ',TO_DATE('14/12/1992','DD/MM/YY'),SYSDATE,2000,'WEB');

-- INSERT + WHERE (En casos de copiar registros de una tabla a otra con alguna condición)
INSERT INTO com_no_nula
SELECT * FROM profesores
WHERE compro IS NOT NULL;
~~~

## UPDATE

Podemos modificar una o varias columnas usando `UPDATE`, `SET` y `WHERE`

~~~sql
UPDATE empleado
SET salario = 2000
WHERE dni = '48949040N';
~~~

~~~sql
UPDATE empleado
SET salario = 2000, cod_dpto = 'D002'
WHERE nombre = 'Sara';
~~~

~~~sql
-- Con subconsultas
-- Modificar el salario y la comisión del profesor con número 110 con valores que tiene el profesor 109
UPDATE profesores
SET (salpro,compro) = (SELECT salpro, compro FROM profesores WHERE numpro=109)
WHERE numpro = 110;
~~~

## DELETE

Para eliminar registros usamos el `DELETE FROM` y el `WHERE` para las condiciones  

~~~sql
DELETE FROM empleado
WHERE dni IN ('11111111A','22222222B','33333333C');

DELETE FROM empleado
WHERE dni = '98030259J';
~~~

Podemos tener `DELETE CON SUBCONSULTAS`

~~~sql
--Con subconsultas
-- Borrar de la tabla profesores , aquellos cuyo salario sea igual al del profesor 108
DELETE FROM profesores
WHERE salpro = (SELECT salpro FROM profesores WHERE numpro = 108);
~~~

### TRANSACCIONES

1. Una transacción comienza al ejecutar un `UPDATE`, `DELETE` o `INSERT`  
2. Podemos hacer un `SAVEPOINT NOMBRE`
3. Ejecutar otras acciones.  
4. Volver al punto de guardado con `ROLLBACK TO (NOMBRE SAVEPOINT)`
5. Usar `ROLLBACK` para deshacer todo hasta el último `COMMIT`.
6. Hacer un `COMMIT` para confirmar los cambios y desde ahí es una nueva transacción.

- Las sentencias DDL hacen un `COMMIT` automático (CREATE, DROP...)
