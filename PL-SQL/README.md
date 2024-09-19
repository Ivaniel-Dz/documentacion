# CheatSheet de PL/SQl

## Bloques
```sql
DECLARE
--- seccion declarativa
BEGIN
-- Seccion ejecutable

EXCEPTION
-- manejo de errores y situaciones

END; -- fin del proceso
```

## Variables
```sql
DECLARE 
identificador integer := 50;
nombre varchar2(25):= 'Jose Feliciano'; // se reduce a la cantidad de datos intriducidos
apodo char(10):= 'joselo'; //no se reduce
sueldo number(5):=30000;
comision decimal(4,2):=50.20;
fecha_actual date :=(sysdate);
fecha date:=to_date('2020/07/09','yyyy/mm/dd');
saludo varchar2(50) default 'Buenos dias a todos';
mensaje constant varchar2(50):= 'No se puede modificar el contenido';

BEGIN 
dbms_output.put_line('El valor de la variable es: ' || identificador); //dbms_... es un paquete que nos muestra la salida por consola
dbms_output.put_line('El nombre del usuario es: ' || nombre);
dbms_output.put_line('El apodo del usuario es: ' || apodo);
dbms_output.put_line('El sueldo del usuario es: ' || sueldo);
dbms_output.put_line('La comision a cobrar del usaurio es de :' || comision);
dbms_output.put_line('La fecha actual es: ' || fecha_actual);
dbms_output.put_line('La fecha de contratación es : ' || fecha);
dbms_output.put_line(saludo);
dbms_output.put_line(mensaje);
END; 
```

## Condicionales

### IF/ELSE/ELSIF
```sql
DECLARE
--- seccion declarativa
BEGIN
	if(condicion) then
	--mensaje
	elsif (condicion) then
	--mensaje
	else
	--mensaje
	end if;
END;
```

### CASE
```sql
CREATE OR REPLACE FUNCTION f_dia_semana(numero int)
return varchar2
IS
dia varchar2(25);
BEGIN
dia:='';
case numero
	when 1 then dia:='lunes';
	when 2 then dia:='martes';
	when 3 then dia:='miercoles';
	when 4 then dia:='jueves';
	when 5 then dia:='viernes';
	else dia:='No es numero coorecto';
end case;
return dia;
END;
```
```sql
select f_dia_semana(1) as 'Dia de la sememan' from dual;
```

### Bucles
```sql
DECLARE
--- seccion declarativa

BEGIN
	loop
	dbms_output.put_line(valor);
	valor:=valor+10;
	exit when valor > 50; --finaliza cuanto sea > 50
	end loop;
	--Mensaje de salida
	dbms_output.put_line('valor final: ' || valor);

END; -- fin del proceso
```

### WHILE LOOP:
```sql
while condicion loop
 ---secuencia de instrucciones;
end loop;
```

### FOR:
```sql
for contador in valorI..valorF loop
--secuencia de instruciones;
end loop;
```
```sql
for contador in reverse valorF..valorI loop
--secuencia de instruciones;
end loop;
```

### LOOP anidados:
```sql
loop 
 ---secuencia de instrucciones;
	loop
	 ---secuencia de instrucciones;
	end loop;
 ---secuencia de instrucciones;
end loop;
```

## FUNCIONES STRINGs
```sql
UPPER(); --convierte a minuscula
LOWER();--convierte a mayuscula
INITCAP();---convierte mayuscula la primera letras
SUBSTR(variable,posicionInicial,PosicionFinal); --busca posicion caracteres partir de lugar indicado
INSTR(variable,'posicionInicial'); //indica la posicion de un caracter indicado en segundo parametro
RTRIM(saludo2, '#');--corta caracteres del lado derecho
LTRIM(saludo2, '#');--corta caracteres del lado izquierdo
TRIM('#' from saludo2);--corta caracteres de ambos lados
```

## ARRAYS
```sql
-- Inicia desde 1, y es unidimensionales.
set serveroutput on;
DECLARE
type a_paises is varray(5) of varchar2(20);
nombre a_paises;
---total integer;

BEGIN
nombre:=a_paises('Argentina','Brasil','Peru','Mexico','Colombia');
total:=nombre.count; --cuenta la cantidad de datos en una matriz
  for f in 1..5 loop
   dbms_output.put_line('Nombre:' || nombre(f));
  end loop;
END; -- fin del proceso
```

## Procedimientos almacenados
```sql
DECLARE OR REPLACE PROCEDURE saludo
AS
BEGIN
dbms_output.put_line('Hola mundo');
END saludo;

BEGIN saludo END; --Ejecuta el proceso
excute saludo; --Opcion2 para ejecutar proceso
```

### ejemplo 2:
```sql
 DECLARE OR REPLACE PROCEDURE precio_articulos
  AS
  BEGIN
   UPDATE articulos SET precio=precio+(precio*0.1);
 END;

SELECT * FROM articulos;
EXECUTE precio_articulos;
```
 
```sql
SELECT *FROM user_objects WHERE object_type='PROCEDURE'; -- Muestra los procedimientos creados
SELECT * FROM user_procedures WHERE object_name like '%saludo%'; -- Muestra los procedimientos creados
DROP procedure saludo; -- Eliminar procedimientos.
```

### PROCEDIMIENTOS ALMACENADOS CON PARÁMETROS
```sql
  --procedimiento que aumenta sueldo a empleados
 CREATE OR REPLACE PROCEDURE aumentasueldo(anio in number, porcentaje in number)
AS
 BEGIN
 UPDATE empleados SET sueldo=sueldo+(sueldo*porcentaje/100)
 WHERE (extract(year from current_date)-extract(year from fechaingreso))>anio;
 END aumentasueldo;
 ```

 ```sql
 --ejecucion
 execute aumentasueldo(10,20);
 ```

 ```sql
 --procedimiento que ingresa empleados
 CREATE OR REPLACE PROCEDURE ingresoemple(docu in char, nom in varchar2, ape in varchar2)
AS
 BEGIN
   INSERT INTO empleados VALUES(docu, nom, ape, null, null);
   END ingresoemple;
```

```sql
    --ejecucion
EXECUTE ingresoemple('25656589','Emilio', 'Perez');
```

### PROCEDIMIENTOS ALMACENADOS VARIABLES
```sql
CREATE OR REPLACE PROCEDURE autorlibro(atitulo in varchar2)
 AS
   v_autor varchar2(20);
 BEGIN
  SELECT autor INTO v_autor FROM libros WHERE titulo=atitulo;
  INSERT INTO tabla1
   SELECT titulo,precio
   FROM libros
   WHERE autor=v_autor;
 END autorlibro;
 ```

 ```sql
 EXECUTE autorlibro('El quijote');
```

## FUNCIONES
```sql
create or replace function f_costo(valor number)
return varchar
is
costo varchar(20);
begin
	costo:='';
	if valor<=500 then
	costo:='economico';
	else costo:='costoso';
	end if;
	return costo;
end;
```
```sql
select titulo, autor, precio, f_costo(precio) from libros;
```

### ejemplo 2:
```sql
create or replace function f_trimestre(fecha date)
   return varchar2
 is
  mes varchar2(20);
  trimestre number;
 begin
   mes:=extract(month from fecha);
   trimestre:=4;
   case mes
     when 1 then trimestre:=1;
     when 2 then trimestre:=1;
     when 3 then trimestre:=1;
     when 4 then trimestre:=2;
     when 5 then trimestre:=2;
     when 6 then trimestre:=2;
     when 7 then trimestre:=3;
     when 8 then trimestre:=3;
     when 9 then trimestre:=3;
     else trimestre:=4;
   end case;
   return trimestre;
 end;
 ```
 ```sql
select f_trimestre(to_date('07/07/2021','dd/mm/yyyy')) as TRIMESTRE from dual;
```

## TRIGGERS
``` sql
CREATE OR REPLACE TRIGGER tr_ingresoLibros
BEFORE INSERT
ON tabla_libros
BEGIN
	insert into tabla_control values(user, sysdate);
END tr_ingresoLibros;
```

```sql
SELECT * FROM tabla_control;

insert into tabla_libros values(100,'uno','Richar back','planet',25);

select * from user_triggers where trigger_name='tr_ingresoLibros'; ---Informacion del sistema
```

### TRIGGER: FOR EACH ROW (se ejecuta por cada fila)
```sql
CREATE OR REPLACE TRIGGER tr_ingresoEmpleados
BEFORE INSERT
ON empleados
for each row -- x cada fila
BEGIN
	insert into tabla_control values(user, sysdate);
END tr_ingresoEmpleados;

drop trigger tr_ingresoEmpleados; --borra triggers 
```

### TRIGGER: BEFORE DELETE
```sql
CREATE OR REPLACE TRIGGER tr_borradoAlumnos
BEFORE DELETE
ON alumnos
for each row -- x cada fila
BEGIN
	insert into tabla_control values(user, sysdate);
END tr_borradoAlumnos;
```

### TRIGGER: BEFORE UPDATE
```sql
CREATE OR REPLACE TRIGGER tr_actualizaEmpleado
BEFORE UPDATE
ON empleados
for each row -- x cada fila
BEGIN
	insert into tabla_control values(user, sysdate);
END tr_actualizaEmpleado;
```

### TRIGGERS MULTIPLES EVENTOS
```sql
create or replace trigger tr_control_empleados
 before insert or update or delete
 on empleados
 for each row
begin
 if inserting then
   insert into control_empleados values (user, sysdate,'ingreso');
  end if;
  if deleting then
   insert into control_empleados values (user, sysdate,'borrado');
 end if; 
 if updating then
  insert into control_empleados values (user, sysdate,'actualización');
 end if;
end tr_control_empleados; 
```

### TRIGGERS :NEW :OLD
```sql
CREATE OR REPLACE TRIGGER tr_ingresoLibros
BEFORE INSERT
ON tabla_libros
for each row
BEGIN
if(:new.precio <= 30) then
	insert into tabla_oferta values(:new.codigo,:new.precio,user, sysdate);
end if
END tr_ingresoLibros;
```

### Ejemplo 2:
```sql
CREATE OR REPLACE TRIGGER tr_actualizaLibro
BEFORE UPDATE OF precio
ON tabla_libros
for each row
BEGIN
if(:old.precio<=30) and (:new.precio => 30) then
	delete from tabla_oferta where where codigo=:old.codigo;
end if;
if(:old.precio>30) and (:new.precio <= 30) then
	insert into tabla_oferta values(:new.codigo,:new.precio,user, sysdate);
end if
END tr_actualizaLibro;
```

### TRIGGERS, WHEN
```sql
CREATE OR REPLACE TRIGGER tr_aumentaSueldo
BEFORE UPDATE OF sueldo
ON empleados
for each row when(new.sueldo>old.sueldo)
BEGIN
	insert into tabla_control values(user, sysdate, :old.documento,:new.sueldo);
END tr_ingresoEmpleados;
```

### TRIGGERS, IF
```sql
CREATE OR REPLACE TRIGGER tr_actualizar_datos
BEFORE INSERT
ON empleados
FOR EACH ROW
BEGIN
	:new.apellido :=upper(:new.apellido);
	if :new.sueldo is null then
	:new.sueldo :=0;
	end if;
END;
```

### TRIGGERS, ENABLE,DISABLE
```sql
SELECT TRIGGER_NAME, TRIGGERING_EVENT, TABLE_NAME, STATUS FROM USER_TRIGGERS WHERE TABLE_NAME='Empleados';

ALTER TRIGGER tr_aumentaSueldo DISABLE; --Desactivar triggers
ALTER TRIGGER tr_aumentaSueldo ENABLE; --Activar triggers
```

### TRIGGERS, RAISE_APPLICATION_ERROR
```sql
CREATE OR REPPLACE TRIGGER tr_control_empleados
BEFORE INSERT OR UPDATE OR DELETE
ON empleados
FOR EACH ROW
	BEGIN
	if(:new.sueldo>5000)then
	raise_application_errror(-20000, 'Sueldo no puede superar los $5000.00');
	end if;
	insert into control values (user, sysdate, 'Insercion');
	if(:old.seccion='Gerencia')then
	raise_application_errror(-20000, 'No se puede eliminar puesto de gerente');
	end if;
	insert into control values (user, sysdate, 'Insercion');
	if updating('Documento')then
	raise_application_errror(-20000, 'No se puede actualizar numero de document');
	end if;
end tr_control_empleados;
```

## CURSORES
```sql 
set serveroutput on;
```

### cursores implícitos
```sql
declare
filas number(2);
begin
update empleados
set sueldo = sueldo + 500 where sueldo >= 3000;
if sql%notfound then
dbms_output.put_line('==No hay empleados disponibles===');
elsif sql%found then
filas:=sql%rowcount;
dbms_output.put_line(filas || ':empleados actualizado');
end if;
end;
```

### Cursores explícitos
```sql
set serveroutput on;

DECLARE
v_docu empleados.documento%type;
v_nom empleados.nombre%type;
v_ape empleados.apellidos%type;
v_suel empleados.sueldo%type;

CURSOR c_cursor2 IS
	SELECT documento, nombre, apellido, sueldo FROM empleados WHERE documento=222;
BEGIN
	OPEN c_cursor2;
	FETCH cursor2 INTO v_docu, v_nom, v_ape, v_suel;
	CLOSE cursor2;
dbms_output.put_line('Document:' || v_docu);
END;
```

### cursores: select y update:
```sql
DECLARE
v_empleados empleados%rowtype; --Guarda toda la tabla en una variable
BEGIN
	FOR v_empleados IN (SELECT * FROM empleados) LOOP --recorre y muestra la tabla
	dbms_output.put_line(v_empleados.nombre: || v_empleados.sueldo);
	END LOOP;
END;
```

### Ejemplo 2:
```sql
BEGIN
	UPDATE empleados SET sueldo = 1000 WHERE documento= 23;
	IF SQL%NOTFOUND THEN
	dbms_output.put_line('No exsite el registo');
	END IF
END;
```

### Cursores con parametros:
```sql
DECLARE
	v_nom productos.nombre_producto%type;
	v_pre productos.precio%type;
CURSOR c_productos (idprod productos.id_producto%type)
	IS
	SELECT nombre_producto, precio FROM productos WHERE id_producto = idprod;
BEGIN
	OPEN c_productos(1);
	LOOP
	FETCH c_productos INTO v_nom, v_pre;
	EXIT WHEN c_productos%notfound;
	dbms_output.put_line('Aritculo: '||v_nom || ',Precio: '||v_pre);
	END LOOP´;
	CLOSE c_productos;
END;
```

### ref_cursors
```sql
CREATE OR REPLACE FUNCTION f_datoempleados(v_valor1 in number,
					   v_valor2 in number)
RETURN SYS_REFCURSOR
IS
 v_ref sys_refcursor;
BEGIN
	OPEN v_ref FOR SELECT * FROM empleados
 	WHERE documento IN (v_valor, v_valor2);
	RETURN v_ref;
END;

VAR rc1 refcursor
EXEC :rc1:=f_datoempleados(2,3);
PRINT rc1;
```

## VARIABLES COMPUESTAS
```sql
declare 
reg_productos productos%rowtype;
begin
select * into reg_productos from productos where codigo = 3;
dbms_output.put_line('Caracteristicas: ');
-- se imprime por consola los datos
dbms_output.put_line('Codigo de producto: ' || reg_productos.codigo);
-----etc..
end;
```

### ejemplo 2:
```sql
DECLARE
	CURSOR cu_productos is select * from productos;
	var_productos cu_productos%rowtype;
BEGIN
	OPEN cu_productos;
	LOOP
	FETCH cu_productos into var_productos;
	EXIT WHEN cu_productos%notfound;
	dbms_output.put_line(var_productos.codigo || var_productos.nombre);
	END LOOP;
END;
```
