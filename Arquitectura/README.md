# Microservicios

## 🚀 **Mejores Frameworks para Microservicios**  

#### **🔵 Node.js**  
✅ **NestJS**  
   - Basado en TypeScript y usa patrones de diseño sólidos.  
   - Integración con GraphQL, WebSockets y RabbitMQ.  
   - Compatible con Express o Fastify (más rendimiento).  
   - Ideal si tu frontend es Angular (misma estructura modular).  

✅ **Express.js** (con arquitectura modular)  
   - Ligero y flexible, aunque necesita más configuración.  
   - Requiere organizar bien middlewares y controladores.  

#### **🔴 Java**  
✅ **Spring Boot con Spring Cloud**  
   - Potente, escalable y con integración nativa a Kubernetes.  
   - Herramientas como **Eureka**, **Feign**, **Zuul** para servicios distribuidos.  
   - Ideal para **sistemas empresariales**.  

#### **🟡 Python**  
✅ **FastAPI**  
   - Rápido y eficiente con soporte para OpenAPI y AsyncIO.  
   - Ideal para **APIs REST y microservicios ligeros**.  
   - Más rápido que Flask y mejor tipado que Django.  

✅ **Flask** (con extensiones como Flask-RESTful)  
   - Más simple, pero necesita librerías adicionales para escalar.  

#### **🟢 Go (Golang)**  
✅ **Go Micro**  
   - Ligero, rápido y diseñado para microservicios desde el inicio.  
   - Buen soporte para gRPC y Kubernetes.  
   - Ideal para **arquitecturas cloud-native**.  

✅ **Gin**  
   - Framework web minimalista con excelente rendimiento.  
   - Útil si necesitas microservicios simples y rápidos.  

#### **🟣 .NET (C#)**  
✅ **ASP.NET Core con Microservices Architecture**  
   - Integración con Docker y Kubernetes.  
   - Ideal para **empresas que usan Microsoft Azure**.  

### **🔥 ¿Cuál elegir?**  
✅ **Si usas JavaScript/TypeScript → NestJS** (es modular y escalable).  
✅ **Si necesitas alto rendimiento → Go Micro**.  
✅ **Si trabajas con Python → FastAPI**.  
✅ **Si desarrollas en Java → Spring Boot**.  
✅ **Si usas .NET → ASP.NET Core**.  


## Estructura de un sistema basado en **microservicios**
La estructura de un sistema basado en **microservicios** puede organizarse de dos formas principales, dependiendo del nivel de independencia y escalabilidad que necesites:  

---

### **1️⃣ Opción 1: Proyectos Separados (Recomendado en producción)**
Cada microservicio es un **proyecto independiente**, con su propio repositorio, base de datos y despliegue.  

📌 **Ventajas:**  
✅ Independencia total (cada microservicio puede escalar de forma individual).  
✅ Se pueden usar diferentes tecnologías por servicio (ejemplo: un servicio en **Node.js** y otro en **Java**).  
✅ Fácil mantenimiento y despliegue en entornos como **Docker + Kubernetes**.  

📂 **Ejemplo de estructura (múltiples repositorios):**  
```
/microservices
  ├── user-service (NestJS)
  │   ├── src/
  │   ├── package.json
  │   ├── Dockerfile
  │   └── README.md
  │
  ├── order-service (Spring Boot)
  │   ├── src/
  │   ├── pom.xml
  │   ├── Dockerfile
  │   └── README.md
  │
  ├── payment-service (FastAPI)
  │   ├── src/
  │   ├── requirements.txt
  │   ├── Dockerfile
  │   └── README.md
  │
  ├── api-gateway (NestJS o Kong API Gateway)
  │   ├── src/
  │   ├── package.json
  │   ├── Dockerfile
  │   └── README.md
```
💡 Cada servicio tiene su **propia base de datos** y se comunican vía **REST o gRPC**.

---

### **2️⃣ Opción 2: Proyecto Monorepo (Para equipos pequeños o desarrollo inicial)**
Todos los microservicios están en **un solo repositorio**, pero organizados en **carpetas separadas** dentro del mismo proyecto.  

📌 **Ventajas:**  
✅ Más fácil de manejar en equipos pequeños.  
✅ Se pueden compartir configuraciones y dependencias.  
✅ Menos sobrecarga inicial en la administración del código.  

📂 **Ejemplo de estructura (monorepo con Nx o TurboRepo):**  
```
/backend-microservices
  ├── services/
  │   ├── user-service/
  │   │   ├── src/
  │   │   ├── package.json
  │   │   └── README.md
  │   │
  │   ├── order-service/
  │   │   ├── src/
  │   │   ├── package.json
  │   │   └── README.md
  │   │
  │   ├── payment-service/
  │   │   ├── src/
  │   │   ├── package.json
  │   │   └── README.md
  │
  ├── api-gateway/
  │   ├── src/
  │   ├── package.json
  │   └── README.md
  │
  ├── package.json
  ├── nx.json (si usas Nx)
  ├── Dockerfile
  └── README.md
```
💡 Aquí, puedes usar **Nx (para JavaScript/TypeScript)** o **Lerna** para administrar dependencias compartidas.

---

### **🔥 ¿Cuál usar?**  
✅ **Si trabajas en producción → Proyectos separados (Microservicios 100% independientes).**  
✅ **Si es un equipo pequeño o un MVP → Monorepo (más fácil de manejar).**  


## 💡 **¿Cómo consumir microservicios en un frontend Angular?**  
En **frontend**, tienes dos opciones principales según el tamaño del proyecto y la independencia requerida:  

---

## **✅ Opción 1: Un solo proyecto Angular (Recomendado para la mayoría de casos)**  
👉 Aquí, todos los módulos están en **un solo proyecto** y Angular consume los microservicios del backend según sea necesario.  

📌 **Ventajas:**  
✅ Más fácil de manejar para equipos pequeños o medianos.  
✅ Compartes el estado global con NgRx o Services.  
✅ Mejor experiencia de usuario al navegar (sin múltiples deploys).  

📂 **Ejemplo de estructura en Angular:**  
```
/frontend-angular
  ├── src/
  │   ├── app/
  │   │   ├── modules/
  │   │   │   ├── auth/  (Login, Registro)
  │   │   │   ├── orders/ (Manejo de pedidos)
  │   │   │   ├── payments/ (Pagos)
  │   │   │   ├── shared/ (Componentes reutilizables)
  │   │   ├── services/ (Consumo de APIs)
  │   │   ├── app-routing.module.ts
  │   │   ├── app.module.ts
  │   ├── environments/ (Variables según el entorno)
  │   ├── main.ts
  ├── package.json
  ├── angular.json
```
🔹 **¿Cómo consume los microservicios?**  
Cada módulo usa **services** para consumir el backend:  

```ts
// auth.service.ts (ejemplo de login)
@Injectable({ providedIn: 'root' })
export class AuthService {
  private API_URL = 'https://api.example.com/auth';
  
  constructor(private http: HttpClient) {}

  login(credentials: any): Observable<User> {
    return this.http.post<User>(`${this.API_URL}/login`, credentials);
  }
}
```

📌 **¿Cuándo usar esta opción?**  
✔️ Si el frontend es para un solo sistema (ejemplo: **panel de administración** o **app de usuario**).  
✔️ Si los módulos están relacionados y comparten estado.  
✔️ Si quieres un mejor UX sin múltiples cargas de aplicaciones.  

---

## **✅ Opción 2: Microfrontends (Para proyectos muy grandes o independientes)**  
👉 Aquí, **cada módulo de Angular es un proyecto independiente** y se integran con un **shell principal** (por ejemplo, usando **Module Federation**).  

📌 **Ventajas:**  
✅ Equipos trabajan de forma separada en cada módulo (ejemplo: un equipo en Login, otro en Payments).  
✅ Cada frontend puede desplegarse de forma independiente.  
✅ Puedes mezclar tecnologías (ejemplo: un microfrontend en React, otro en Angular).  

📂 **Ejemplo de estructura (Microfrontends con Module Federation)**  
```
/frontend-shell  (Contenedor principal)
  ├── src/
  │   ├── app/
  │   │   ├── navbar/ (Carga los microfrontends)
  │   │   ├── app-routing.module.ts
  │   │   ├── app.module.ts
  │   ├── main.ts
  ├── webpack.config.js (Module Federation)
  ├── angular.json
```
```
/frontend-login  (Microfrontend del login)
/frontend-orders  (Microfrontend de órdenes)
/frontend-payments  (Microfrontend de pagos)
```
🔹 **¿Cómo se integran los microfrontends?**  
Cada microfrontend expone un módulo para que el **shell principal** lo cargue dinámicamente.  

```js
// webpack.config.js (del shell principal)
new ModuleFederationPlugin({
  remotes: {
    login: "login@http://localhost:4201/remoteEntry.js",
    orders: "orders@http://localhost:4202/remoteEntry.js",
  }
});
```

📌 **¿Cuándo usar esta opción?**  
✔️ Si los módulos son **totalmente independientes** y los manejan **diferentes equipos**.  
✔️ Si cada módulo necesita **diferentes ciclos de vida y despliegue**.  
✔️ Si la app es muy grande y necesita **escalar horizontalmente**.  

---

## **🔥 ¿Cuál opción elegir?**  
✅ **Si trabajas en un equipo pequeño o mediano → Usa un solo Angular con módulos (Opción 1).**  
✅ **Si trabajas en una empresa grande con equipos separados → Usa Microfrontends (Opción 2).**  

🔹 **¿Quieres ayuda con la configuración de Module Federation o prefieres un ejemplo práctico?** 🚀