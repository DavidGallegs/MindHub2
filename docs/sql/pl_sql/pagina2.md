# PL SQL

Podemos usar SELECT para recibir valores.
Aplicamos el SELECT ... INTO  

~~~sql
-- Ejemplo 1
DECLARE
    v1 VARCHAR2(100);
BEGIN
    SELECT sal INTO v1 FROM emp WHERE ename LIKE 'KING';
    dbms_output.put_line(v1);
EXCEPTION
    WHEN NO_DATA_FOUND THEN dbms_output.put_line('No hay KING');
    WHEN TOO_MANY_ROWS THEN dbms_output.put_line('Más de un KING');
END;

-- Ejemplo 2
-- %TYPE conservamos el tipo de la variable
DECLARE
    v1 NUMBER(5); 
    v2 emp.ename%TYPE; 
BEGIN
    v1 := &NumeroEmpleado;
    SELECT ename INTO v2 FROM emp WHERE empno = v1;
    dbms_output.put_line('Num:'||v1||' Nombre: '||v2);
END;

-- Ejemplo 3:
DECLARE
    v1 dept.dname%TYPE; 
    v2 dept.loc%TYPE; 
BEGIN
    v1 := 'SALES';
    SELECT loc INTO v2 FROM dept WHERE dname = v1;
    dbms_output.put_line('El departamento '||v1||' está en '||v2); 
END;

~~~

También podemos hacer INSERT o UPDATES

~~~sql
-- Ejemplo 1
DECLARE
    v1 emp.empno%TYPE;
    v2 emp.ename%TYPE;
    v3 emp.job%TYPE;
BEGIN
    v1 := 9999;
    v2 := 'PEREZ';
    v3 := 'ANALISTA';
    INSERT INTO emp(empno, ename, job, deptno) VALUES(v1,v2,v3,10);
    dbms_output.put_line(v1||' '||v2||' '||v3); 
END;

-- Ejemplo 2
DECLARE
    v3 emp.job%TYPE;
BEGIN
    v3 := 'ANALISTA';
    UPDATE emp
    SET sal = NVL(sal,0) + 20000
    WHERE job = v3;
    dbms_output.put_line(v3); 
END;

-- Ejemplo 3
DECLARE
    v_empno emp.empno%TYPE;
BEGIN
    v_empno := &EmpleadoABorrar;
    DELETE FROM emp WHERE empno = v_empno;
    dbms_output.put_line('Empleado '||v_empno||' borrado.');
END;

~~~

Luego tenemos los `CURSORES EXPLICITOS`  

~~~sql
DECLARE
    CURSOR c_productos IS SELECT codproduct FROM productos WHERE codproduct > 7;
    v_cod productos.codproduct%TYPE;
BEGIN
    OPEN c_productos;
    LOOP
        FETCH c_productos INTO v_cod;
        EXIT WHEN c_productos%NOTFOUND;
        DELETE FROM productos WHERE codproduct = v_cod;
    END LOOP;
    CLOSE c_productos;
END;

~~~

Vuelve el SYSDATE

~~~sql
DECLARE
    v_fecha DATE;
BEGIN
    v_fecha := SYSDATE;
    dbms_output.put_line('Fecha y hora actual: ' || TO_CHAR(v_fecha,'DD/MM/YYYY HH24:MI:SS'));
END;

~~~
