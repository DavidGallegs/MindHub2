# VISTAS

## CREAR VISTAS

Primero creamos la `SELECT` y luego añadimos la vista

~~~sql
CREATE VIEW prof_web AS
SELECT * FROM profesores
WHERE esppro = 'WEB';

-- Uso de la vista
SELECT * FROM prof_web;
~~~

## ELEMENTOS A LA HORA DE CREAR VISTAS

Podemos añadir `OR REPLACE` o `WITH READ ONLY` que evita que los datos se modifiquen.

~~~sql
CREATE OR REPLACE VIEW prof_web AS
SELECT * FROM profesores
WHERE esppro = 'WEB'
WITH READ ONLY;
~~~

Podemos añadir `WITH CHECK OPTION` que se encarga de consevar los valores de los
de los campos ante `UPDATES` en la vista.  
Pudes darle un nombre a la restrcción `WITH CHECK OPTION CONSTRAINT NOMBRE_Constrain`
y esto como si fuera una constrain puede hacerla `ENABLE`, `DISABLE` o `DROP` como en las tablas  

~~~sql
-- Evita que puedan mover un profesor a otra especialidad
CREATE OR REPLACE VIEW prof_web AS
SELECT * FROM profesores
WHERE esppro = 'WEB'
WITH CHECK OPTION CONSTRAINT web_ck;

ALTER VIEW prof_web DISABLE CONSTRAINT web_ck;
ALTER VIEW prof_web ENABLE CONSTRAINT web_ck;
ALTER VIEW prof_web DROP CONSTRAINT web_ck;
~~~

Y tenemos el `FORCE` que crea una vista si la tabla no existe y se coloca depueés del `REPLACE` en caso de haber.  
Por defecto siempre esta en `NOFORCE`  

~~~sql
-- Evita que puedan mover un profesor a otra especialidad
CREATE FORCE VIEW prof_web AS
SELECT * FROM profesores
WHERE esppro = 'WEB';
~~~

## BORRAR VISTA

~~~sql
DROP VIEW prof_web;
~~~
