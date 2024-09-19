# CheatSheet de SQL

## Instrucción SELECT
1. Seleccionar toda la tabla:
```sql
SELECT * FROM movies;
```

2. selecciona una entidad especifica de una tabla:
```sql
SELECT title FROM movies;
```

3. Selecciona una o mas entidades de una tabla:
```sql
SELECT title, year FROM movies;
```

4. Selecciona una fila especifica por un atributo:
```sql
SELECT * FROM movies where id = 6;
```

5. Selecciona una valor entre otro (debe saber el valor de value1 y value2):
```sql
SELECT column_name FROM table_name WHERE column_name BETWEEN value1 AND value2;
```
```sql
SELECT title FROM movies WHERE year BETWEEN 2000 and 2008;
```

6. No selecciona los valores que esten entre los valores determinados:
```sql
SELECT column_name FROM table_name WHERE column_name NOT BETWEEN value1 AND value2;
```

7. Selecciona los valores con una condición especifica usando OPERADORES:
```sql
SELECT title,year FROM movies where id < 6;
```

8. Selecciona una valor especifico por operador LIKE no distingue mayúscula y minúscula:
```sql
SELECT title FROM movies where title like("%Toy Story%");
```

9. No seleccionar un valor especifico por el operador NOT LIKE
```sql
SELECT title from movies where director not like("%John Lasseter%");
```

10. selección datos en forma ascendente sin duplicados:
```sql
SELECT DISTINCT column_name FROM table_name ORDER BY column_name ASC ;
```

11. selección de datos usando LIMIT para escoger una cantidad de datos y ordenar.
```sql
/* Enumere las últimas cuatro películas de Pixar estrenadas (ordenadas de más reciente a menos) */
SELECT title FROM movies ORDER BY year DESC LIMIT 4;
```

12. Enumere las próximas cinco películas de Pixar ordenadas alfabéticamente.
```sql
SELECT title FROM movies ORDER BY title LIMIT 5 OFFSET 5;
```

## Instrucción INNER JOIN
1. Mostrar datos de una de dos tablas relacionadas
```sql
SELECT title, Domestic_sales, International_sales FROM Movies INNER JOIN Boxoffice ON Movies.id =  Boxoffice.Movie_id;
```

2. Uso del JOIN para trabajar en tablas relacionadas:
```sql
SELECT column, another_column FROM mytable INNER/LEFT/RIGHT/FULL JOIN another_table ON mytable.id = another_table.matching_id;
```

3. Seleccionar campos vacios (Null)
```sql
SELECT * FROM employees WHERE Building IS NULL;
```

4. Encuentre los nombres de los edificios que no tienen empleados.
```sql
SELECT DISTINCT * FROM Buildings LEFT JOIN Employees ON Building_name = Building WHERE Building IS NULL;
```

5. Enumere todas las películas y sus ventas combinadas en millones de dólares
```sql
SELECT title, (domestic_sales + international_sales) / 1000000 AS gross_sales_millions
FROM movies
  JOIN boxoffice
    ON movies.id = boxoffice.movie_id;
```

## Consultas con agregados
### Funciones:

- ``COUNT(*)``, ``COUNT(column)`` Una función común que se utiliza para contar el número de filas del grupo si no se especifica ningún nombre de columna. De lo contrario, cuente el número de filas del grupo con valores no NULL en la columna especificada.

- ``MIN(column)``	Encuentra el valor numérico más pequeño en la columna especificada para todas las filas del grupo.

- ``MAX(column)``	Encuentra el valor numérico más grande en la columna especificada para todas las filas del grupo.

- ``AVG(column)``	Encuentra el valor numérico promedio en la columna especificada para todas las filas del grupo.

- ``SUM(column)``	Encuentra la suma de todos los valores numéricos en la columna especificada para las filas del grupo

1. uso de GROUP BY:
```sql
SELECT role, AVG(years_employed) as Average_years_employed FROM employees GROUP BY role;
```

2. ejemplo de condición sin GROUP BY con WHERE: Encuentra la cantidad de artistas en el estudio.
```sql
SELECT role, COUNT(role) AS cantidad FROM employees WHERE role = 'Artist';
```

3. Ejemplo 2 de GROUP BY:
```sql
/*Encuentre la cantidad de empleados de cada rol en el estudio.*/
SELECT ROLE, COUNT(role) AS cantidad FROM employees group by role;
```

3. Condición Grupal con HAVING:
```sql
SELECT role, SUM(Years_employed) as años FROM employees GROUP BY role HAVING role = 'Engineer';
```

## Orden de ejecución de una consulta Query
```sql

SELECT DISTINCT column, AGG_FUNC(column_or_expression), …
FROM mytable
    JOIN another_table
      ON mytable.column = another_table.column
    WHERE constraint_expression
    GROUP BY column
    HAVING constraint_expression
    ORDER BY column ASC/DESC
    LIMIT count OFFSET COUNT;
```

## Instrucción INSERT
1. Ejemplo:
```sql
INSERT INTO boxoffice (movie_id, rating, sales_in_millions) 
		VALUES (1, 9.9, 283742034 / 1000000);
```

## Instrucción UPDATE
```sql
UPDATE movies SET director = "John Lasseter" WHERE id = 2;
```
```sql
UPDATE Movies SET Title = 'Toy Story 3', Director = 'Lee Unkrich' WHERE id = 11;
```

## Instrucción DELETE
- Elimina datos especificos con WHERE
```sql
DELETE FROM Movies wHERE year < 2005;
```

- Vacía una tabla completa:
```sql
DELETE FROM nameTable;
```

## Instrucción CREATE TABLE  
```sql
CREATE TABLE movies (
    id INTEGER PRIMARY KEY,
    title TEXT,
    director TEXT,
    year INTEGER, 
    length_minutes INTEGER,
    Download_count COUNT
);
```

## Instrucción ALTER TABLE
1. Agregar columna nueva
```sql
ALTER TABLE Movies ADD Aspect_ratio FLOAT;
```

2. Agregar columna nueva con una valor determinado:
```sql
ALTER TABLE Movies ADD Language TEXT DEFAULT 'English';
```

3. Eliminar una columna:
```sql
ALTER TABLE mytable DROP column_to_be_deleted;
```

4. Cambiar nombre a la tabla:
```sql
ALTER TABLE mytable RENAME TO new_table_name;
```

## Instrucción DROP
```sql
DROP TABLE IF EXISTS mytable; / DROP TABLE mytable;
```
```sql
DROP column NOMBRECAMPO;
```

## Sentencia VIEW
1. Creación de una Vista ``CREATE VIEW``
```sql
CREATE VIEW vwPersonaPais AS
SELECT Persona.id, persona.nombre, pais.nombre AS pais FROM persona LEFT JOIN pais ON pias.id = persona.idPais;
```

2. Modificar la Vista ``ALTER VIEW``
```sql
ALTER vwPersonaPais AS
SELECT Persona.id, persona.nombre, pais.nombre AS paises FROM persona LEFT JOIN pais ON pias.id = persona.idPais;
```

3. Mostrar vista (SELECT)
```sql
SELECT * FROM vwPersonaPais;
```

## Sentencia TRIGGER
1. Estructura de TRIGGER
```sql
CREATE [OR REPLACE] TRIGGER trigger_name 
 {BEFORE | AFTER | INSTEAD OF } 
 {INSERT [OR] | UPDATE [OR] | DELETE} 
 [OF col_name] 
 ON table_name 
 [REFERENCING OLD AS o NEW AS n] 
 [FOR EACH ROW] 
 WHEN (condition)  
 BEGIN 
   --- sql statements  
 END;
```

## Instrucción INNER JOIN MULTIPLE
```sql
SELECT *
    FROM tabla1
        INNER JOIN tabla2 
            ON tabla1.columna_comun = tabla2.columna_comun
        INNER JOIN tabla3 
            ON tabla2.otra_columna_comun = tabla3.otra_columna_comun;
```


- EJEMPLO:
```sql
SELECT PROYECTOS.ID_PROYECTO, PROYECTOS.PROYECTO, PROYECTOS.FECHA, PROYECTOS.CONTACTO, PROYECTOS.CORREO, PROYECTOS.LUGAR, SEDE.SEDE, FACULTAD.FACULTAD
FROM PROYECTOS
  JOIN FACULTAD
    ON PROYECTOS.ID_FACULTAD = FACULTAD.ID_FACULTAD
  JOIN SEDE 
    ON FACULTAD.ID_SEDE = SEDE.ID_SEDE;
```

## Conexión de MySQL con PHP
```php
<?php
$servername = "localhost";
$username = "tu_usuario";
$password = "tu_contraseña";
$dbname = "nombre_base_datos";

// Crear conexión
$conn = new mysqli($servername, $username, $password, $dbname);

// Verificar conexión
if ($conn->connect_error) {
    die("Conexión fallida: " . $conn->connect_error);
}
echo "Conexión exitosa";

// Cerrar conexión
$conn->close();
?>

```

## Conexión de MySQL con JavaScript (Node.js)
```js
const mysql = require('mysql2');

// Crear conexión
const connection = mysql.createConnection({
  host: 'localhost',
  user: 'tu_usuario',
  password: 'tu_contraseña',
  database: 'nombre_base_datos'
});

// Conectar a la base de datos
connection.connect((err) => {
  if (err) {
    console.error('Error conectándose a la base de datos:', err.stack);
    return;
  }
  console.log('Conexión exitosa');
});

// Cerrar conexión
connection.end();
```

## Conexión de MySQL con Next.js
Conexión a MySQL en Next.js usando ``mysql2`` y ``getServerSideProps``
```js
import mysql from 'mysql2/promise';

export async function getServerSideProps() {
  const connection = await mysql.createConnection({
    host: 'localhost',
    user: 'tu_usuario',
    password: 'tu_contraseña',
    database: 'nombre_base_datos'
  });

  const [rows] = await connection.execute('SELECT * FROM tu_tabla');
  await connection.end();

  return {
    props: {
      data: rows
    }
  };
}

const Page = ({ data }) => (
  <div>
    {data.map((item) => (
      <p key={item.id}>{item.nombre}</p>
    ))}
  </div>
);

export default Page;
```

## Conexión de MySQL con Java Sprint Boot
- Dependencias en`` pom.xml``:
```java
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <scope>runtime</scope>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

- Configuración en ``application.properties``:
```java
spring.datasource.url=jdbc:mysql://localhost:3306/nombre_base_datos
spring.datasource.username=tu_usuario
spring.datasource.password=tu_contraseña
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect
```

- Repositorio y Modelo:
```java
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class Usuario {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String nombre;
    private int edad;

    // Getters y Setters
}
```

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface UsuarioRepository extends JpaRepository<Usuario, Long> {
}
```

 ## Conexión a MySQL con Spring Framework (Java)
 - Dependencias en ``pom.xml``:
 ```java
 <dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.30</version>
</dependency>

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.3.18</version>
</dependency>

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.3.18</version>
</dependency>

<dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate-core</artifactId>
    <version>5.6.9.Final</version>
</dependency>
```

- Configuración en ``applicationContext.xml``:
 ```java
 <beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans 
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- Definir DataSource -->
    <bean id="dataSource" class="org.apache.commons.dbcp2.BasicDataSource">
        <property name="driverClassName" value="com.mysql.cj.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql://localhost:3306/nombre_base_datos"/>
        <property name="username" value="tu_usuario"/>
        <property name="password" value="tu_contraseña"/>
    </bean>

    <!-- Configuración de Hibernate -->
    <bean id="sessionFactory" class="org.springframework.orm.hibernate5.LocalSessionFactoryBean">
        <property name="dataSource" ref="dataSource"/>
        <property name="packagesToScan" value="com.tuapp.modelo"/>
        <property name="hibernateProperties">
            <props>
                <prop key="hibernate.dialect">org.hibernate.dialect.MySQL8Dialect</prop>
                <prop key="hibernate.show_sql">true</prop>
                <prop key="hibernate.hbm2ddl.auto">update</prop>
            </props>
        </property>
    </bean>

    <!-- Definir el TransactionManager -->
    <bean id="transactionManager" class="org.springframework.orm.hibernate5.HibernateTransactionManager">
        <property name="sessionFactory" ref="sessionFactory"/>
    </bean>
</beans>
```

- Entidad (Modelo):
 ```java
 import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class Usuario {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String nombre;
    private int edad;

    // Getters y Setters
}
```

- DAO (Data Access Object):
 ```java
 import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Repository;
import org.springframework.transaction.annotation.Transactional;

import java.util.List;

@Repository
public class UsuarioDao {

    @Autowired
    private SessionFactory sessionFactory;

    @Transactional
    public List<Usuario> obtenerUsuarios() {
        Session session = sessionFactory.getCurrentSession();
        return session.createQuery("from Usuario", Usuario.class).list();
    }

    @Transactional
    public void guardarUsuario(Usuario usuario) {
        Session session = sessionFactory.getCurrentSession();
        session.saveOrUpdate(usuario);
    }
}
```

### Consideraciones:
- **``Seguridad:``** Nunca conectes directamente desde el frontend a una base de datos. El acceso a las bases de datos debe estar detrás de una API o servidor.
- **``CORS:``** Asegúrate de que el servidor donde está tu API permita las solicitudes desde tu aplicación frontend.
- Esta estructura mantiene la conexión con las bases de datos en el servidor y sólo devuelve los resultados al frontend de manera segura.
- Para MySQL, Spring Framework utiliza ``Hibernate`` o ``JDBC`` para interactuar con la base de datos. La configuración se realiza principalmente en el archivo ``applicationContext.xml``, donde defines el ``DataSource``, ``SessionFactory`` y ``TransactionManager``.