# **C# .NET**

## **1. Introducción a .NET**

### ¿Qué es .NET?
.NET es un framework de desarrollo de Microsoft que permite construir aplicaciones de distintos tipos como aplicaciones web, de escritorio, móviles y más. Es compatible con múltiples lenguajes, siendo C# el más común.

### Componentes principales de .NET:
- **.NET SDK**: Herramientas para compilar, ejecutar y gestionar aplicaciones.
- **.NET Runtime**: Motor que ejecuta las aplicaciones .NET.
- **ASP.NET Core**: Framework para construir aplicaciones web modernas y APIs.
- **Entity Framework Core (EF Core)**: Herramienta ORM para facilitar el acceso a bases de datos.

---

## **2. Configuración del Entorno**

### Instalación del SDK de .NET
1. Descargar el [SDK de .NET](https://dotnet.microsoft.com/download).
2. Instalar el SDK y luego verificar la instalación con:
   ```bash
   dotnet --version
   ```

### IDE para .NET
- **Visual Studio**: Una opción completa para desarrollo .NET.
- **Visual Studio Code**: Ligero, con soporte para .NET a través de extensiones de C#.

---

## **3. Creación de Proyectos en .NET**

### Proyecto de Consola
1. Crear un nuevo proyecto:
   ```bash
   dotnet new console -n MiAplicacion
   ```
2. Ejecutarlo:
   ```bash
   dotnet run
   ```

### Proyecto Web con ASP.NET Core
1. Crear un nuevo proyecto web:
   ```bash
   dotnet new webapp -n MiWebApp
   ```
2. Ejecutar el proyecto:
   ```bash
   dotnet run
   ```

---

## **4. Fundamentos Esenciales de .NET**

### Estructura de un Proyecto
- **`Program.cs`**: Punto de entrada de la aplicación.
- **`appsettings.json`**: Archivo de configuración.
- **Controladores**: Para manejar las solicitudes HTTP.
- **Vistas**: Archivos de presentación (HTML).

### Compilación y Publicación
- Compilar el proyecto para producción:
  ```bash
  dotnet publish -c Release
  ```

---

## **5. ASP.NET Core MVC (Modelo-Vista-Controlador)**

### ¿Qué es MVC?
- **Modelo**: Representa los datos de la aplicación.
- **Vista**: Interfaz de usuario.
- **Controlador**: Gestiona las solicitudes del usuario y coordina el modelo y la vista.

### Ejemplo de un Controlador
```cs
using Microsoft.AspNetCore.Mvc;

namespace MiWebApp.Controllers
{
    public class HomeController : Controller
    {
        public IActionResult Index()
        {
            return View();  // Renderiza la vista Index
        }
    }
}
```

### Crear una Vista
1. Crear la carpeta `Views/Home/`.
2. Dentro de ella, agregar `Index.cshtml`:
   ```html
   <h1>¡Bienvenido a mi aplicación en ASP.NET Core!</h1>
   ```

---

## **6. Acceso a Datos con Entity Framework Core**

### Instalar EF Core
1. Agregar EF Core al proyecto:
   ```bash
   dotnet add package Microsoft.EntityFrameworkCore.SqlServer
   dotnet add package Microsoft.EntityFrameworkCore.Tools
   ```

### Configuración de DbContext
```cs
using Microsoft.EntityFrameworkCore;

public class AppDbContext : DbContext
{
    public DbSet<Producto> Productos { get; set; }

    protected override void OnConfiguring(DbContextOptionsBuilder options)
        => options.UseSqlServer("cadena-de-conexion");
}

public class Producto
{
    public int Id { get; set; }
    public string Nombre { get; set; }
    public decimal Precio { get; set; }
}
```

### Migraciones y Creación de la Base de Datos
- Generar migraciones:
  ```bash
  dotnet ef migrations add InitialCreate
  ```
- Actualizar la base de datos:
  ```bash
  dotnet ef database update
  ```

---

## **7. Operaciones Asíncronas con `async` y `await`**

### Tareas Asíncronas
```cs
public async Task ProcesarDatosAsync()
{
    await Task.Delay(2000);  // Simula una operación de 2 segundos
    Console.WriteLine("Proceso completado.");
}
```

### Ejecución de múltiples tareas
```cs
public async Task EjecutarTareasAsync()
{
    Task tarea1 = Task.Run(() => Console.WriteLine("Tarea 1"));
    Task tarea2 = Task.Run(() => Console.WriteLine("Tarea 2"));
    
    await Task.WhenAll(tarea1, tarea2);  // Espera a que ambas tareas finalicen
}
```

---

## **8. Seguridad en ASP.NET Core**

### Autenticación y Autorización
- Usar **Identity** para autenticar usuarios.
- Implementar **JWT (JSON Web Tokens)** para APIs seguras.

### Middleware de Seguridad
```cs
public void Configure(IApplicationBuilder app)
{
    app.UseAuthentication();  // Middleware de autenticación
    app.UseAuthorization();   // Middleware de autorización
}
```

---

## **9. Buenas Prácticas de Diseño**

### Principios SOLID
- **S**: Single Responsibility (Responsabilidad única).
- **O**: Open/Closed (Abierto para extensión, cerrado para modificación).
- **L**: Liskov Substitution (Sustitución de Liskov).
- **I**: Interface Segregation (Segregación de interfaces).
- **D**: Dependency Inversion (Inversión de dependencias).

### Inversión de Control (IoC) y DI (Inyección de Dependencias)
- Registrar servicios en `Startup.cs`:
  ```cs
  public void ConfigureServices(IServiceCollection services)
  {
      services.AddTransient<IMiServicio, MiServicio>();
  }
  ```

---

## **10. Testing y Depuración**

### Pruebas Unitarias
- Usar `xUnit` para escribir y ejecutar pruebas unitarias:
  ```bash
  dotnet new xunit -n MiProyecto.Tests
  ```

### Depuración
- Herramientas de depuración en Visual Studio o VS Code para inspeccionar variables y seguir el flujo del código.

---

## **11. Manejo de Archivos y Streams**

### Leer y escribir archivos
```cs
using System.IO;

// Escribir archivo
File.WriteAllText("archivo.txt", "Hola Mundo");

// Leer archivo
string contenido = File.ReadAllText("archivo.txt");
Console.WriteLine(contenido);
```

### Usar Streams
```cs
using (StreamWriter writer = new StreamWriter("archivo.txt"))
{
    writer.WriteLine("Escribiendo con StreamWriter.");
}
```

---

## **12. Servicios Web y APIs RESTful**

### Creación de APIs
- Usar ASP.NET Core para crear APIs RESTful.
  ```cs
  [ApiController]
  [Route("api/[controller]")]
  public class ProductosController : ControllerBase
  {
      [HttpGet]
      public IEnumerable<Producto> Get()
      {
          return _context.Productos.ToList();
      }
  }
  ```

### Documentación con Swagger
1. Instalar el paquete Swagger:
   ```bash
   dotnet add package Swashbuckle.AspNetCore
   ```
2. Configurar Swagger en `Startup.cs`:
   ```cs
   public void ConfigureServices(IServiceCollection services)
   {
       services.AddSwaggerGen();
   }

   public void Configure(IApplicationBuilder app)
   {
       app.UseSwagger();
       app.UseSwaggerUI(c => c.SwaggerEndpoint("/swagger/v1/swagger.json", "Mi API v1"));
   }
   ```

---

## **13. Publicación y Despliegue**

### Publicación del Proyecto
- Compilar el proyecto para producción:
  ```bash
  dotnet publish -c Release -o ./publicacion
  ```

### Despliegue en Azure
- Desplegar aplicaciones ASP.NET Core en **Azure App Service** con las herramientas integradas en Visual Studio.

---

## **14. Ejemplo Completo de Creación de un Proyecto MVC en .NET**

### Paso 1: Crear un proyecto MVC
En la consola, ejecuta:
```bash
dotnet new mvc -n MiAplicacionMVC
cd MiAplicacionMVC
dotnet run
```

### Paso 2: Estructura del Proyecto
```bash
MiAplicacionMVC/
├── Controllers/
│   └── HomeController.cs
├── Models/
├── Views/
│   └── Home/
│       └── Index.cshtml
├── Program.cs
├── Startup.cs
└── MiAplicacionMVC.csproj
```

### Paso 3: Agregar un Controlador
En `Controllers/HomeController.cs`:
```cs
using Microsoft.AspNetCore.Mvc;

namespace MiAplicacionMVC.Controllers
{
    public class HomeController : Controller
    {
        public IActionResult Index()
        {
            return View();  // Renderiza la vista Index
        }
    }
}
```

### Paso 4: Crear una Vista
En `Views/Home/Index.cshtml`:
```html
<h1>¡Bienvenido a mi aplicación MVC en ASP.NET Core!</h1>
<p>Esta es la página principal.</p>
``

`

### Paso 5: Ejecutar el Proyecto
Ejecuta el proyecto:
```bash
dotnet run
```

Navega a `http://localhost:5000/Home/Index` y verás la página generada.

---

## Estructura de Carpeta de un Proyecto
```bash
- src
  - ProjectName
    - Controllers
    - Models
    - DTOs
    - Services
    - Repositories
    - Views
    - wwwroot
      - css
      - js
      - images
    - Data
    - Migrations
    - Properties
  - ProjectName.Tests
    - UnitTests
    - IntegrationTests
- .gitignore
- ProjectName.sln
- README.md
```

## 📌 Configuración de Conexión a Bases de Datos con EF Core
- MS SQL Server:
```json
{
  "ConnectionStrings": {
    "ConnectionDB": "Data Source=(local)\\SQLEXPRESS;Initial Catalog=nameBD;Integrated Security=True;Trusted_Connection=True;TrustServerCertificate=True;"
  }
}
```

- MySQL
```json
{
  "ConnectionStrings": {
    "ConnectionDB": "Server=localhost;Database=nameDB;User=root;Password=root;SslMode=Required;"
  }
}
```

- PostgreSQL:
```json
{
  "ConnectionStrings": {
    "ConnectionDB": "Host=localhost;Database=nameDB;Username=postgres;Password=postgres"
  }
}
```

- **Program.cs**
```cs
// Configuración de la base de datos (Postgres)
builder.Services.AddDbContext<AppDBContext>(options =>
{
    options.``UsePackage``(builder.Configuration.GetConnectionString("ConnectionDB"));
});
```
**UsePackage:**
- PostgreSQL = ``UseNpgsql``
- MySQL = ``UseMySql``
- SQL Server = ``UseSqlServer``

## 📦 Paquetes NuGet

### Entity Framework Core

* **Microsoft.EntityFrameworkCore** → Núcleo de EF Core, permite trabajar con modelos y LINQ.
* **Microsoft.EntityFrameworkCore.Tools** → Herramientas para generar migraciones y administrar la BD desde la consola.

### Proveedores de Base de Datos

* **Microsoft.EntityFrameworkCore.SqlServer** → Proveedor para conectar con **MS SQL Server**.
* **Pomelo.EntityFrameworkCore.MySql** → Proveedor para conectar con **MySQL/MariaDB**.
* **Npgsql.EntityFrameworkCore.PostgreSQL** → Proveedor para conectar con **PostgreSQL**.
* *(MongoDB no tiene soporte oficial de EF Core, se usa con librerías externas como MongoDB.Driver).*

### Autenticación

* **Microsoft.AspNetCore.Authentication.Cookies** → Autenticación basada en **cookies** (sesiones clásicas).
* **Microsoft.AspNetCore.Authentication.JwtBearer** → Autenticación con **JSON Web Tokens (JWT)**.
* **Google.Apis.Auth** → Autenticación con **Google OAuth2**.

---

## 🛠️ Comandos de EF Core Tools (Visual Studio / PMC)

* **Add-Migration "Nombre"** → Genera una nueva clase de migración según los cambios en el modelo.
* **Update-Database** → Aplica las migraciones a la BD (crea la BD si no existe).
* **Remove-Migration** → Elimina la última migración pendiente (no aplicada).

---

## 🛠️ Comandos .NET CLI

* **dotnet restore** → Descarga y restaura las dependencias definidas en el `.csproj`.
* **dotnet list package** → Lista los paquetes NuGet instalados en el proyecto.
* **dotnet ef migrations add Nombre** → Crea una migración desde la CLI (equivalente a `Add-Migration`).
* **dotnet ef database update** → Aplica las migraciones a la BD desde la CLI.
* **dotnet add package NombreDelPaquete** → Instala un paquete NuGet en el proyecto.
---


## 🔑 JWT (JSON Web Token) VS 🍪 Cookies

### 🚀 Diferencias prácticas

| Aspecto             | JWT                                           | Cookies                                                        |
| ------------------- | --------------------------------------------- | -------------------------------------------------------------- |
| **Dónde se guarda** | Cliente (localStorage, sessionStorage, etc.)  | Navegador (cookie automática)                                  |
| **Ideal para**      | APIs REST, SPA (Angular, React, Vue), móviles | Web apps clásicas con servidor que maneja vistas, MVC o Razor Pages |
| **Escalabilidad**   | Fácil distribuir (stateless)                  | Requiere manejar sesión compartida si hay múltiples servidores |
| **Seguridad**       | Vulnerable si se guarda mal en frontend       | Protegidas con `HttpOnly`, pero dependen de dominio            |

---

## mapeo entre DTOs ↔ Entidades
- Si usas directamente ``Models`` → no hay que mapear (ya es la entidad).
- Si usas ``DTOs`` → sí necesitas mapear (AutoMapper o SetValues).

### Comparaciones 
- **``Manual``** = control, simple, pero repetitivo.
```cs
var entity = new Library
{
    Id = dto.Id,
    Name = dto.Name,
    Address = dto.Address
};
```

- **``AutoMapper``** = recomendado para proyectos medianos/grandes.
```cs
var entity = _mapper.Map<Library>(dto);
```

- **``SetValues``** = sirve, pero no es lo más limpio fuera de EF (se usa más en repositorios que en servicios).
```cs
var entity = new Library();
_context.Entry(entity).CurrentValues.SetValues(dto);
```

### Combinación de Mapeo
```cs
// Mapeo automático con AutoMapper
var newLibrary = _mapper.Map<Library>(libraryDto);

// Sobrescribir campos que no vienen del DTO
newLibrary.UserId = userId;
newLibrary.Clave = _encryptor.Encrypt(libraryDto.Clave);
```

