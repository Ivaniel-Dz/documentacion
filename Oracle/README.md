# Oracle Database
> Datos importantes:
> 1. Crear los usuarios en MAYUSCULA = DEMO, USER etc..
> 2. las TABLESPACE se crean dentro del contenedor (ORCLPDB).
> 3. los usuarios se crea dentro del contenedor (ORCLPDB).
> 4. los permisos a usuarios se dan en el contenedor (ORCLPDB).

## Configuracion de DB 19c
```bash
Nombre de BD de Conexion: orclpdb
nombre de BD Global: orcl
password: ivaniel

user admin: sys, system
password: ivaniel


Instancia: ORCL

Usuario Principal:
user: ivaniel
pass: 2024
```

## Crear usuario principal
```bash
CONN / AS SYSDBA
alter session set "_ORACLE_SCRIPT"=true;
CREATE USER ivaniel IDENTIFIED BY 12345;
GRANT DBA TO ivaniel; #le asigna el rol de administrador
```

## Entrar a SQLPlus
```bash
sqlplus / as sysdba
```

## Ver contenedores
```bash
show pdbs;
```

## Entrar a un contenedor
```bash
ALTER SESSION SET CONTAINER=ORCLPDB;
```

## Entrar a un usuario de un contenedor
```bash
CONN user/pass@contenedor;
```

## Dar permiso a un contenedor
```bash
sqlplus / as sysdba
select name, open_mode from v$pdbs;
ALTER SESSION SET CONTAINER=ORCLPDB;
ALTER PLUGGABLE DATABASE OPEN;
```

## Ver usuarios creados
```bash
set line 200;
select * from all_users;
select * from dba_users where username like 'LA%';
```

## Ver TABLESPACE
```bash
SELECT * FROM dba_tablespaces;
SELECT * FROM user_tablespaces;
```

## Ver sesiones conectados:
```bash
select username Usuario_Oracle, count(username) Numero_Sesiones from v$session group by username order by Numero_Sesiones desc;
```

## Comando basicos de SQL:

### CREACIÓN:
- Crea Base de Datos:
```bash
CREATE DATABASE name;
```

- Crea Tablas de una BBDD:
```bash
CREATE TABLE name;
```

### SELECCIONAR
- Selecciona la BBDD a Utilizar:
```bash
USE nameBBDD;
```


### MOSTRAR o VER
- Muestra contenido de la tabla con información completa:
```bash
DESC nameTable;
```

- Ver contenido de la tabla:
```bash
DESCRIBE LAB4_USER.CLIENTES;
```

### AGREGAR CONTENIDO
- Agregar contenido a la tabla:
```bash
ALTER TABLE LAB4_USER.CLIENTES ADD ID_PROV NUMBER(2) NOT NULL;
```

- Agregar llave primaria a una tabla:
```bash
ALTER TABLE nameTable ADD PRIMARY KEY (id);
```

- Agregar llave forenea en una table:
```bash
ALTER TABLE nameTable ADD CONSTRAINT FK_nameID FOREIGN KEY (id_ref) REFERENCES tabla_ref(id);
```

- Agregar Valor unicos:
```bash
ALTER TABLE nameTabla ADD CONSTRAINT u_name UNIQUE (name);
```

- Agregar un nuevo atribudo a una tabla:
```bash
ALTER TABLE nameTable ADD newAtribudo varchar(20);
```

- Agregar Referencia a Tabla
```bash
alter table PARCIAL_USER.CLIENTE add constraint FK_ID_SUCURSAL foreign key ("ID_SUCURSAL")references PARCIAL_USER.SUCURSAL ("ID_SUCURSAL");
```

### MODIFICAR
- Modificar Nombre de una atribudo:
```bash
ALTER TABLE nameTabla CHANGE nameActual newName VARCHAR(20);
```

- Modificar el tipo de datos de un atribudo:
```bash
ALTER TABLE nameTabla MODIFY name varchar(20);
```

- Modificar nombre de FK
```bash
alter table "PARCIAL2_USER"."DIRECCION" RENAME CONSTRAINT "SYS_C008435" TO "FK_DIST_DIR"
```

### ELIMINAR
- Eliminar Usuarios
```bash
alter session set "_ORACLE_SCRIPT"=true;
drop user "demo" CASCADE;
```

- Eliminar Tabla
```bash
DROP TABLE name;
```

- Elimina datos de un tabla
```bash
TRUNCATE TABLE name;
```

- Eliminar Columna de una tabla
```bash
alter table NOMBRETABLA;
drop column NOMBRECAMPO;
```

- Eliminar Tablespace
```bash
drop tablespace "nombre";
```

- Eliminar llave primaria de una tabla:
```bash
ALTER TABLE nameTable DROP PRIMARY KEY;
```

- Eliminar Llave foranea:
```bash
ALTER TABLE nameTable DROP FOREIGN KEY FK_ID;
```

- ELiminar Valor Unico de una Tabla:
```bash
ALTER TABLE nameTabla DROP INDEX u_name;
```

## COMANDOS DE BASICOS CRUD
- Muestra contenido de la tabla:
```bash
SELECT * FROM nameTabla;
```

- Insertar Datos:
```bash
INSERT INTO nameTable (atribudo1, atribudo2, etc) VALUES ();
```

- Modificar Datos:
```bash
UPDATE nameTable SET nameAtribudo = "UpdateDato" WHERE ID = ?;
```

- Actulizar Registro de Tabla
```bash
update cliente set nombre = 'MINSA', cedula = '4-569-1011' WHERE id_cliente = 101;
```

- Borrar datos:
```bash
DELETE FROM nameTable WHERE atribudo = "dato";
```

- Borrar Registro de Tablas
```bash
DELETE FROM cliente WHERE fecha_compra < '02/04/2021';
```

- Vacia una Tabla:
```bash
DELETE FROM nameTable;
```

- Guarda los cambios
```bash
COMMIT;
```

## Ejemplo de creación de una Base de dato

1. Se crea un tablespace para guardar los usuarios

opción 1: Tablespace normal
```bash
CREATE TABLESPACE "PROJECT_TMP" LOGGING DATAFILE 'D:\App\Oracle\Database19c\oradata\ORCL\orclpdb\Laravel\PROJECT_TMP.DBF' SIZE 512M EXTENT MANAGEMENT LOCAL SEGMENT SPACE MANAGEMENT AUTO;
```

Opción 2: Tablespace Temporal
```bash
CREATE TEMPORARY TABLESPACE "PROJECT_TMP" TEMPFILE 'D:\App\Oracle\Database19c\oradata\ORCL\orclpdb\Laravel\PROJECT_TMP.DBF' SIZE 512M AUTOEXTEND ON;
```

> Si ya existe TABLESPACE se puede usarlo para no crear uno nuevo

2. Se altera la sección para agregar cambios
```bash
alter session set "_ORACLE_SCRIPT"=true;
```

3. Crear el usuario:
```bash
CREATE USER "LIBRERIA" PROFILE "DEFAULT" IDENTIFIED BY "LB2024" DEFAULT TABLESPACE "PROJECT_TMP" TEMPORARY TABLESPACE "TEMP" ACCOUNT UNLOCK;
```

4. Permisos del usuario
```bash
GRANT "CONNECT" TO "LIBRERIA";
GRANT "RESOURCE" TO "LIBRERIA";

GRANT ALTER ANY INDEX TO "LIBRERIA";
GRANT ALTER ANY SEQUENCE TO "LIBRERIA";
GRANT ALTER ANY TABLE TO "LIBRERIA";
GRANT ALTER ANY TRIGGER TO "LIBRERIA";
GRANT CREATE ANY INDEX TO "LIBRERIA";
GRANT CREATE ANY SEQUENCE TO "LIBRERIA";
GRANT CREATE ANY SYNONYM TO "LIBRERIA";
GRANT CREATE ANY TABLE TO "LIBRERIA";
GRANT CREATE ANY TRIGGER TO "LIBRERIA";
GRANT CREATE ANY VIEW TO "LIBRERIA";
GRANT CREATE PROCEDURE TO "LIBRERIA";
GRANT CREATE PUBLIC SYNONYM TO "LIBRERIA";
GRANT CREATE TRIGGER TO "LIBRERIA";
GRANT CREATE VIEW TO "LIBRERIA";
GRANT DELETE ANY TABLE TO "LIBRERIA";
GRANT DROP ANY INDEX TO "LIBRERIA";
GRANT DROP ANY SEQUENCE TO "LIBRERIA";
GRANT DROP ANY TABLE TO "LIBRERIA";
GRANT DROP ANY TRIGGER TO "LIBRERIA";
GRANT DROP ANY VIEW TO "LIBRERIA";
GRANT INSERT ANY TABLE TO "LIBRERIA";
GRANT QUERY REWRITE TO "LIBRERIA";
GRANT SELECT ANY TABLE TO "LIBRERIA";
GRANT UNLIMITED TABLESPACE TO "LIBRERIA";
```

## Conexión de Oracle con PHP
```php
<?php
$username = 'tu_usuario';
$password = 'tu_contraseña';
$host = 'localhost/XE'; // XE es el SID predeterminado de Oracle Express

// Conexión
$conn = oci_connect($username, $password, $host);

if (!$conn) {
    $e = oci_error();
    echo "Conexión fallida: " . htmlentities($e['message'], ENT_QUOTES);
} else {
    echo "Conexión exitosa";
}

// Cerrar conexión
oci_close($conn);
?>

```

## Conexión de Oracle con JS (Node.js)
```js
const oracledb = require('oracledb');

async function run() {
  let connection;
  try {
    connection = await oracledb.getConnection({
      user: 'tu_usuario',
      password: 'tu_contraseña',
      connectString: 'localhost/XE' // XE es el SID predeterminado
    });
    console.log('Conexión exitosa');
  } catch (err) {
    console.error(err);
  } finally {
    if (connection) {
      try {
        await connection.close();
      } catch (err) {
        console.error(err);
      }
    }
  }
}

run();
```

## Conexión de Oracle con Java Sprint Boot

- Dependencia:

```xml
<dependency>
   <groupId>com.oracle.database.jdbc</groupId>
    <artifactId>ojdbc11</artifactId>
    <scope>runtime</scope>
</dependency>
```

- Configuración:
```properties
# Configuración de la base de datos (Oracle)
spring.datasource.url=jdbc:oracle:thin:@localhost:1521:ORCLCDB
spring.datasource.username=TU_USUARIO
spring.datasource.password=TU_CONTRASENA
spring.datasource.driver-class-name=oracle.jdbc.OracleDriver

# Configuración de JPA y Hibernate
spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto=update
spring.jpa.database-platform=org.hibernate.dialect.Oracle12cDialect
```

configuración en version yml
```yml
spring:
  datasource:
    url: jdbc:oracle:thin:@localhost:1521:ORCLCDB
    username: TU_USUARIO
    password: TU_CONTRASENA
    driver-class-name: oracle.jdbc.OracleDriver
  jpa:
    show-sql: true
    hibernate:
      ddl-auto: update
    database-platform: org.hibernate.dialect.Oracle12cDialect
```

Entidad y DAO:
Los modelos y DAOs son los mismos que en la sección de MySQL, excepto que la configuración del dialecto de Hibernate cambia a ```Oracle12cDialect```.

### Consideraciones:
- **``Seguridad:``** Nunca conectes directamente desde el frontend a una base de datos. El acceso a las bases de datos debe estar detrás de una API o servidor.
- **``CORS:``** Asegúrate de que el servidor donde está tu API permita las solicitudes desde tu aplicación frontend.
- Esta estructura mantiene la conexión con las bases de datos en el servidor y sólo devuelve los resultados al frontend de manera segura.
- Para Oracle, Spring Framework utiliza ``Hibernate`` o ``JDBC`` para interactuar con la base de datos. La configuración se realiza principalmente en el archivo ``applicationContext.xml``, donde defines el ``DataSource``, ``SessionFactory`` y ``TransactionManager``.