# PL SQL

Estructura General

~~~sql
DECLARE   -- opcional: variables
    v_var NUMBER;
BEGIN     -- obligatorio
    -- código
EXCEPTION -- opcional: manejo de errores
    WHEN OTHERS THEN
        dbms_output.put_line('Error');
END;

~~~

Datos comunes son NUMBER(p,s), VARCHAR2(n), DATE, BOOLEAN  
Operadores: + - / *
Comparaciones: =,<>, >,< , <=,>=

Estrucura IF

~~~sql
IF condicion THEN
    -- código
ELSIF otra_condicion THEN
    -- código
ELSE
    -- código
END IF;


FOR i IN 1..10 LOOP
    dbms_output.put_line(i);
END LOOP;

~~~

Extra tenemos el SYSDATE, POWER(x,n), TO_CHAR, TO_NUMBER y &variabl

- Ejemplos:

~~~sql
SET SERVEROUTPUT ON;

-- Ejemplo 1
DECLARE
    v1 VARCHAR2(10) := 'antonio';
    v2 VARCHAR2(10) := 'mola';
BEGIN
    -- Mensaje según v1
    IF v1 = 'antonio' THEN
        dbms_output.put_line('Hola Antonio!');
    ELSE
        dbms_output.put_line('No eres Antonio.');
    END IF;

    -- Mensaje según v2
    IF v2 = 'mola' THEN
        dbms_output.put_line('Qué guay que mola!');
    ELSE
        dbms_output.put_line('Vaya, no mola tanto...');
    END IF;
END;


-- Ejemplo 2
DECLARE
    v1 NUMBER(5) := &numero1;
    v2 NUMBER(5) := &numero2;
BEGIN
    dbms_output.put_line(v1 + v2);
END;

-- Ejemplo 3
DECLARE
    radio NUMBER(5) := &radio;
    longitud NUMBER(10,2);
BEGIN
    longitud := 2 * 3.14 * radio;
    dbms_output.put_line('Longitud de la Circunferencia: ' || longitud);
END;

~~~
