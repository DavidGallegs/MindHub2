# CREACIÓN DE TABLAS

## CREAR TABLA

~~~sql
CREATE TABLE empleados (
    idempleado NUMBER(5),
    nombre VARCHAR2(50),
    sexo CHAR(1),
    salario NUMBER(10,2),
    fechanac DATE
);
~~~

## ALTERAR TABLA

~~~sql
-- Añadir un campo "departamento"
ALTER TABLE empleados ADD (departamento VARCHAR2(30));

-- Modificar longitud del campo "nombre"
ALTER TABLE empleados MODIFY (nombre VARCHAR2(100)); 
~~~

## CAMBIAR NOMBRE

~~~sql
-- Renombrar tabla
RENAME empleados  TO trabajadores;
ALTER TABLE empleados RENAME TO trabajadores;


~~~

## TRUNCAR

~~~sql
-- Borrar todos los registros sin eliminar la estructura
TRUNCATE TABLE trabajadores;
~~~

## BORRAR TABLA

~~~sql
-- Eliminar la tabla completamente
DROP TABLE trabajadores;
~~~

## RESTRICCIONES DE TABLA

### RESTRICCIONES PK,CK,UK Y FK

~~~sql
ALTER TABLE empleados ADD (
CONSTRAINT empleados_idempleado_pk PRIMARY KEY (idempleado),
CONSTRAINT empleados_salario_ck CHECK (salario >= 0),
CONSTRAINT empleados_nombre_uk UNIQUE (nombre),
CONSTRAINT empleados_departamento_fk FOREIGN KEY (departamento) REFERENCES departamentos(departamento));
~~~

### NOT NULL

~~~sql
ALTER TABLE empleados MODIFY (sexo NOT NULL);
~~~

### DISABLE, ENABLE Y DROP CONSTRAINT

~~~sql
ALTER TABLE empleados DISABLE CONSTRAINT empleados_salario_ck;
ALTER TABLE empleados ENABLE CONSTRAINT empleados_salario_ck;
ALTER TABLE empleados DROP CONSTRAINT empleados_salario_ck;
~~~
