# Spring Boot
<p align="center"><a href="https://docs.spring.io/spring-boot/documentation.html" target="_blank"><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Spring_Framework_Logo_2018.svg/368px-Spring_Framework_Logo_2018.svg.png" width="400" alt="spring Logo"></a></p>

## Spring Framework
Spring Framework es un marco de trabajo para el desarrollo de aplicaciones Java empresariales. Proporciona infraestructura y herramientas para facilitar la creación de aplicaciones robustas, escalables y mantenibles, permitiendo la inversión de control (IoC), inyección de dependencias (DI) y soporte para programación orientada a aspectos (AOP).

## Spring Platform
Spring Platform es un conjunto de proyectos y herramientas basadas en Spring Framework, que incluyen Spring Boot, Spring Data, Spring Security, Spring Cloud, entre otros. Facilita la integración de tecnologías y simplifica el desarrollo de aplicaciones Java empresariales.

## Spring Boot
Spring Boot es una extensión de Spring Framework que simplifica la configuración y el desarrollo de aplicaciones mediante convenciones predefinidas y configuraciones automáticas (auto-configuration). Permite crear aplicaciones listas para producción con una configuración mínima.

## Tipos de Arquitectura
Spring Boot permite desarrollar aplicaciones bajo diferentes tipos de arquitecturas, entre ellas:
- **Monolítica**: Toda la lógica de negocio y acceso a datos se ejecuta en una sola aplicación.
- **Microservicios**: Divide la aplicación en servicios independientes que se comunican entre sí.
- **Reactiva**: Basada en eventos y asincronismo para mejorar el rendimiento.

## Spring MVC
 MVC es un patrón de diseño que contiene tres componentes principales:
 - **Modelo (Model)**:Gestiona los datos de la aplicación y la lógica de negocio.
 - **Vista (View)**:Encargada de presentar los datos al usuario.
 - **Controlador (Controller)**:Procesa las solicitudes del usuario, interactúa con el modelo y selecciona la vista adecuada para renderizar.
 * El objetivo de MVC es facilitar el mantenimiento, la escalabilidad y la reutilización del código.

### Arquitectura de Spring MVC
 - DispatcherServlet
 - Controladores
 - Modelo
 - Vista
 - View Resolve
 - Handler Mapping

 ### Flujo de trabajo en Spring MVC
 - El cliente envía una solicitud
 - DispatcherServlet recibe la solicitud
 - El controlador procesa la solicitud
 - El controlador selecciona una vista
 - El View Resolver localiza la vista
 - Se genera una respuesta

## Service 
Un **Service** en Spring Boot es una capa de la aplicación que contiene la lógica de negocio. Se anota con `@Service` y se utiliza para desacoplar la lógica de la capa de controladores.

## Repositorio
Un **Repositorio** en Spring Boot es una interfaz que facilita el acceso a la base de datos. Se anota con `@Repository` y generalmente extiende `JpaRepository` o `CrudRepository` para simplificar las operaciones CRUD.

## Clase DTO
Un **DTO (Data Transfer Object)** es una clase utilizada para transferir datos entre diferentes capas de la aplicación sin exponer la estructura interna de las entidades.

## JPA
JPA (Java Persistence API) es una especificación de Java que facilita la gestión de bases de datos relacionales mediante objetos Java. Spring Boot usa Hibernate como implementación de JPA.

## Directivas de Thymeleaf
Thymeleaf es un motor de plantillas para Spring Boot. A continuación, se muestra una tabla con algunas de sus directivas principales:

| **Directiva** | **Descripción** |
|--------------|----------------|
| `th:text` | Muestra texto en la plantilla |
| `th:if` | Evalúa una condición y muestra el contenido si es verdadera |
| `th:each` | Itera sobre una lista de elementos |
| `th:href` | Enlaza atributos href dinámicamente |
| `th:src` | Define rutas de imágenes dinámicamente |
| `th:class` | Asigna clases CSS dinámicamente |
| `th:style` | Define estilos CSS en línea |

## Inyección de Dependencias?
Es un patrón de diseño que permite desacoplar los componentes de una aplicación, facilitando la gestión de dependencias a través de contenedores de inversión de control como Spring.

## Patrones de Diseño
Los patrones de diseño son soluciones reutilizables a problemas comunes en el desarrollo de software. Algunos patrones usados en Spring Boot son:
- **Singleton**: Garantiza una sola instancia de una clase (`@Component`, `@Service`).
- **Factory Method**: Permite la creación de objetos sin especificar la clase exacta.
- **DAO (Data Access Object)**: Facilita la interacción con la base de datos (`@Repository`).
- **MVC (Modelo-Vista-Controlador)**: Organiza la aplicación en capas.

## Interruptores: Autenticación y Autorización
- **Autenticación**: Verifica la identidad de un usuario antes de permitir el acceso al sistema.
- **Autorización**: Determina los permisos y acciones que un usuario autenticado puede realizar.
Spring Security maneja estos conceptos con roles y permisos dentro de una aplicación Spring Boot.


## Anotaciones en Spring Boot
Las anotaciones en Spring Boot son metadatos utilizados para simplificar la configuración y la implementación de funcionalidades en la aplicación. Permiten definir componentes, configurar inyecciones de dependencias, manejar peticiones HTTP, entre otras funcionalidades.

### Tabla de anotaciones en Spring Boot

| **Anotación**           | **Funcionalidad** | **Cuándo usarlo** |
|------------------------|------------------|------------------|
| `@Configuration` | Define una clase como fuente de configuración para Spring. | Cuando se necesita definir beans de manera programática. |
| `@Bean` | Declara un bean administrado por Spring dentro de una clase de configuración. | Cuando se quiere registrar manualmente un componente en el contexto de Spring. |
| `@RequestMapping` | Mapea solicitudes HTTP a métodos específicos en controladores. | Para definir rutas en controladores. |
| `@GetMapping` | Maneja solicitudes HTTP GET. | Para obtener datos desde el servidor. |
| `@PostMapping` | Maneja solicitudes HTTP POST. | Para enviar datos al servidor y crear nuevos recursos. |
| `@PutMapping` | Maneja solicitudes HTTP PUT. | Para actualizar un recurso existente. |
| `@DeleteMapping` | Maneja solicitudes HTTP DELETE. | Para eliminar un recurso existente. |
| `@ManyToMany` | Define una relación de muchos a muchos entre entidades. | Cuando dos entidades tienen una relación bidireccional de muchos a muchos. |
| `@ManyToOne` | Define una relación de muchos a uno entre entidades. | Cuando una entidad está relacionada con una sola entidad padre. |
| `@OneToMany` | Define una relación de uno a muchos entre entidades. | Cuando una entidad tiene múltiples instancias de otra entidad. |
| `@Controller` | Marca una clase como un controlador MVC. | Para manejar solicitudes web y devolver vistas (en aplicaciones con plantillas). |
| `@RestController` | Combina `@Controller` y `@ResponseBody`, devolviendo directamente datos JSON o XML. | Cuando se crean API REST en Spring Boot. |
| `@ModelAttribute` | Vincula atributos del modelo a un método de un controlador. | Para inicializar datos en formularios o vistas. |
| `@RequestParam` | Extrae parámetros de la URL de una solicitud HTTP. | Cuando se necesitan parámetros de consulta en un método de controlador. |
| `@PathVariable` | Extrae valores de la URL de una solicitud HTTP. | Para capturar valores dentro de la ruta de una API REST. |
| `@Value` | Inyecta valores desde `application.properties` o `application.yml`. | Para configurar valores desde propiedades externas. |
| `@Component` | Marca una clase como un componente gestionado por Spring. | Para definir un bean genérico en el contenedor de Spring. |
| `@Autowired` | Permite la inyección de dependencias automáticamente. | Cuando se necesita inyectar beans en otra clase. |
| `@Repository` | Marca una clase como un componente de acceso a datos. | Para clases que interactúan con bases de datos. |
| `@Service` | Marca una clase como un servicio dentro de la lógica de negocio. | Para definir servicios en la capa de negocio. |
| `@ControllerAdvice` | Maneja excepciones globales en controladores. | Para gestionar errores en toda la aplicación de manera centralizada. |
| `@Transactional` | Gestiona transacciones en operaciones de base de datos. | Cuando se necesita asegurar la atomicidad de una operación. |
| `@EnableScheduling` | Habilita la ejecución de tareas programadas. | Cuando se necesita ejecutar procesos en intervalos definidos. |
| `@Scheduled` | Define un método que se ejecuta en un horario específico. | Para tareas automatizadas dentro de la aplicación. |
| `@RestControllerAdvice` | Maneja excepciones globales en APIs REST. | Para manejar errores en controladores REST de manera global. |
| `@EnableJpaRepositories` | Habilita la funcionalidad de Spring Data JPA. | Para permitir la gestión automática de repositorios JPA. |
| `@Entity` | Define una clase como una entidad en JPA. | Para mapear una clase a una tabla de base de datos. |
| `@Table` | Especifica el nombre de la tabla en la base de datos. | Cuando se necesita definir un nombre específico para una entidad en la BD. |
| `@Column` | Define un campo de una entidad como una columna de la tabla. | Cuando se necesita personalizar el mapeo de atributos en la BD. |
| `@GeneratedValue` | Define la estrategia de generación de valores de clave primaria. | Cuando se necesita una clave primaria autoincremental. |
| `@Lob` | Define un campo como un objeto de gran tamaño (Large Object). | Para almacenar archivos grandes en la base de datos. |
| `@Cacheable` | Habilita el almacenamiento en caché de un método. | Cuando se quiere optimizar el acceso a datos frecuentemente consultados. |

