# Angular

<p align="center"><a href="https://angular.dev/installation" target="_blank"><img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*UCVxApa10mkQNnNqvNqSaQ.png" width="400" alt="spring Logo"></a></p>

> Angular es un framework para aplicaciones web desarrollado en TypeScript, de código abierto, mantenido por Google, que se utiliza para crear y mantener aplicaciones web de una sola página.

## Comandos de Angular CLI
### **Comandos de generación**
```bash
ng new my-app                # Crear un nuevo proyecto de Angular
ng generate component home    # Crear un nuevo componente
ng g c components/home        # Crear un nuevo componente (abreviado)
ng generate component carpeta/comments --inline-template --inline-style # Crea un nuevo componente pero las plantillas y estilos estarán el mismo archivo typescript
ng generate service api       # Crear un nuevo servicio
ng g s services/data --skip-tests  # Crear un servicio sin archivos de prueba
ng generate module admin      # Crear un nuevo módulo
ng g m core --routing         # Crear un módulo con enrutamiento
ng generate directive highlight  # Crear una directiva personalizada
ng generate pipe currencyFormat  # Crear un pipe personalizado
ng generate interface user    # Crear una interfaz
ng generate class models/user # Crear una clase
ng generate enum userRoles    # Crear un enum
```

### **Comandos de ejecución**
```bash
ng serve                     # Iniciar el servidor de desarrollo
ng serve --open              # Iniciar el servidor y abrir en el navegador
ng build                     # Compilar el proyecto para producción
ng build --prod              # Compilar el proyecto en modo producción
ng test                      # Ejecutar pruebas
ng lint                      # Revisar errores de linting
ng e2e                       # Ejecutar pruebas end-to-end
```

### **Comandos de configuración**
```bash
npm install -g @angular/cli  # Instalación de cli de angular (-g instalación global)
ng add @angular/material     # Instalar Angular Material
ng add @ngrx/store          # Agregar NgRx al proyecto
ng update                    # Actualizar Angular y dependencias
ng config                    # Ver o modificar la configuración
ng version                   # Mostrar la versión de Angular CLI
```

## Arquitectura y patrones de diseño:
- **Modularidad**: La aplicación se organiza en módulos que agrupan funcionalidades relacionadas. Esto permite que cada módulo sea desarrollado, probado y mantenido de forma independiente.
- **Componentes**: Son las unidades básicas de la interfaz. Cada componente tiene su propia lógica y vista.
- **Servicios e inyección de dependencias**: Los servicios permiten centralizar la lógica de negocio o el manejo de datos, y Angular se encarga de inyectarlos en los componentes que los necesiten.
- **Routing**: Angular utiliza un sistema de enrutamiento para gestionar la navegación entre vistas o componentes.
- **RxJS**: Se usa para manejar la programación reactiva, facilitando la gestión de flujos de datos asíncronos.

## Componentes en Angular
Los componentes son bloques fundamentales en Angular. Representan una parte de la interfaz de usuario y tienen una estructura compuesta por HTML, CSS y TypeScript.

### Propiedades de los Componentes
- **selector**: Define el nombre con el cual el componente es referenciado en las plantillas.
- **standalone**: Indica si el componente requiere un NgModule o si puede funcionar de manera independiente.
- **imports**: Lista de dependencias del componente.
- **template**: Define el HTML del componente.
- **styleUrls**: Array con las rutas de los archivos CSS asociados.

### Estructura de los Componentes
- Exportar componentes:
![preview](./img/exportacion.png)

- Configuración entre componentes:
![preview](./img/config-components.png)

## Interfaces en Angular
Las interfaces en TypeScript definen la estructura de un objeto, asegurando un tipo de dato específico en Angular.

### Ejemplo:
```typescript
export interface HousingLocation {
    id: number;
    name: string;
    city: string;
    state: string;
    photo: string;
    availableUnits: number;
    wifi: boolean;
    laundry: boolean;
}
```


## Servicios en Angular
Los servicios en Angular permiten la comunicación entre componentes y la gestión de lógica de negocio, como la manipulación de datos o la realización de peticiones HTTP.


## Dependency Injection
Es un patrón de diseño utilizado en Angular para inyectar dependencias en los componentes o servicios de la aplicación, promoviendo modularidad y reutilización del código.


## Property Binding e Interpolación
- **Property Binding**: Asigna valores de propiedades de una clase a atributos de un elemento en el DOM.
  ```html
  <img [src]="imageUrl">
  ```
- **Interpolación**: Permite incrustar expresiones de TypeScript en la plantilla HTML.
  ```html
  <h1>{{ title }}</h1>
  ```



## **Estados (`state`)**  
🔹 En Angular, el **estado** se refiere a los datos que determinan la presentación de la interfaz de usuario en un componente.  
🔹 Se pueden gestionar los estados de varias maneras:

### **1. Estados locales en un componente (Usando propiedades de la clase)**
```typescript
export class ExampleComponent {
  isActive: boolean = true; // Estado booleano
  count: number = 0; // Estado numérico
}
```

### **2. Usando `@Input()` y `@Output()` para comunicación entre componentes**
Se explicará más adelante.

### **3. Uso de `BehaviorSubject` y Servicios para manejar estados globales**
```typescript
import { BehaviorSubject } from 'rxjs';

export class StateService {
  private state = new BehaviorSubject<boolean>(true);
  currentState = this.state.asObservable();

  changeState(value: boolean) {
    this.state.next(value);
  }
}
```
- Esto permite compartir el estado entre varios componentes.


## **Pasar parámetros entre componentes `Input` y `Output`**  

### **1️. De padre a hijo (usando `@Input`)**
Se usa `@Input()` para enviar datos desde un componente padre a su hijo.

#### **Componente Padre (`app-parent.component.ts`)**
```typescript
@Component({
  selector: 'app-parent',
  template: `<app-child [message]="parentMessage"></app-child>`
})
export class ParentComponent {
  parentMessage = 'Hola desde el Padre!';
}
```

#### **Componente Hijo (`app-child.component.ts`)**
```typescript
@Component({
  selector: 'app-child',
  template: `<p>{{ message }}</p>`
})
export class ChildComponent {
  @Input() message: string = '';
}
```


### **2️.De hijo a padre (usando `@Output` y `EventEmitter`)**
Se usa `@Output()` para enviar datos desde un hijo hacia su componente padre.

#### **Componente Hijo (`app-child.component.ts`)**
```typescript
import { Component, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `<button (click)="sendMessage()">Enviar al Padre</button>`
})
export class ChildComponent {
  @Output() messageEvent = new EventEmitter<string>();

  sendMessage() {
    this.messageEvent.emit('Mensaje desde el hijo!');
  }
}
```

#### **Componente Padre (`app-parent.component.ts`)**
```typescript
@Component({
  selector: 'app-parent',
  template: `<app-child (messageEvent)="receiveMessage($event)"></app-child>
             <p>Mensaje recibido: {{ message }}</p>`
})
export class ParentComponent {
  message: string = '';

  receiveMessage(event: string) {
    this.message = event;
  }
}
```

## CommonModule
El módulo `CommonModule` proporciona directivas como `ngIf`, `ngFor` y otras utilidades necesarias para el desarrollo de aplicaciones en Angular.

## **Directivas**
### **Diferencia entre directivas ng vs @**
### ngFor, ngIF y etc: 
>Esta es la forma tradicional de manejar condicionales en Angular.

✅ **Ventajas:**
- Compatible con todas las versiones de Angular.
- Se integra bien con otras directivas estructurales como *ngFor.
- Más familiar para desarrolladores de Angular con experiencia.

⚠️ **Desventajas:**
- Puede generar código HTML más extenso con múltiples elementos <ng-template>.
- Menos legible en estructuras de control complejas.

### @for, @if y etc
>La nueva sintaxis es más parecida a las estructuras de control de TypeScript y mejora la legibilidad del código.

✅ **Ventajas:**
- Mayor claridad y legibilidad.
- Código más limpio y fácil de mantener.
- Soporte nativo en Angular 17+ sin necesidad de directivas estructurales.

⚠️ **Desventajas:**
- Requiere Angular 17 o superior.
- No es compatible con versiones anteriores de Angular.

### **Directivas Clásicas**  
| **Directiva**     | **Descripción** |
|-------------------|----------------|
| `*ngIf`          | Renderiza un elemento solo si la condición es verdadera. |
| `*ngIf...else`   | Permite definir un bloque alternativo cuando la condición es falsa. |
| `*ngFor`         | Itera sobre una lista y genera un elemento por cada ítem. |
| `*ngSwitch`      | Permite evaluar una variable y mostrar el bloque correspondiente. |
| `*ngSwitchCase`  | Define un caso dentro de un `*ngSwitch`. |
| `*ngSwitchDefault` | Define un caso por defecto dentro de un `*ngSwitch`. |
| `*ngTemplateOutlet` | Permite renderizar un `ng-template` dinámicamente. |
| `ngClass`        | Aplica clases dinámicamente en función de una expresión. |
| `ngStyle`        | Aplica estilos CSS dinámicamente. |
| `ngModel`        | Permite la vinculación bidireccional de datos en formularios. |
| `ngModelGroup`   | Agrupa varios `ngModel` en un formulario reactivo. |
| `ngContainer`    | Contenedor estructural que no genera un elemento real en el DOM. |
| `ngTemplate`     | Plantilla reutilizable en Angular. |
| `ngContent`      | Permite la proyección de contenido dentro de un componente. |
| `ngPlural`       | Permite definir reglas para pluralización de contenido basado en valores numéricos. |
| `ngPluralCase`   | Define casos específicos de pluralización. |

---

### **Nueva Sintaxis de Directivas (Angular 17+)**  

| **Directiva** | **Descripción** |
|--------------|----------------|
| `@if`       | Alternativa a `*ngIf`. Renderiza un elemento solo si la condición es verdadera. |
| `@else`     | Alternativa a `*ngIf...else`. Define un bloque alternativo cuando la condición es falsa. |
| `@for`      | Alternativa a `*ngFor`. Itera sobre una lista de elementos. |
| `@switch`   | Alternativa a `*ngSwitch`. Evalúa una variable y muestra el bloque correspondiente. |
| `@case`     | Alternativa a `*ngSwitchCase`. Define un caso dentro de un `@switch`. |
| `@default`  | Alternativa a `*ngSwitchDefault`. Define un caso por defecto dentro de un `@switch`. |

---

**¿Cuál es mejor?**  
🔹 **Si usas Angular 17+**, la nueva sintaxis `@if`, `@for`, y `@switch` es más limpia y legible.  
🔹 **Si trabajas con versiones anteriores**, las directivas clásicas siguen siendo la mejor opción.

### Ejemplo con @if y @else:
```typescript
<section>
  @if (isLoggedIn) {
    <h1>Bienvenido {{ username }}</h1>
    <img (click)="greet()" src="https://github.com/ivaniel-dz.png" alt="photo" />
    <button (click)="isLoggedIn = false">Cerrar sesión</button>
  } @else {
    <h2>Inicia sesión</h2>
    <button (click)="isLoggedIn = true">Iniciar sesión</button>
  }

  <app-games (addFavoriteEvent)="getFavorite($event)" username="{{ username }}"></app-games>

  @if (favGame !== '') {
    <p>Tu juego favorito es {{ favGame }}</p>
  }
</section>
```
### Ejemplo con *ngIf y *ngIf:
```typescript
<section>
  <ng-container *ngIf="isLoggedIn; else loginTemplate">
    <h1>Bienvenido {{ username }}</h1>
    <img (click)="greet()" src="https://github.com/ivaniel-dz.png" alt="photo" />
    <button (click)="isLoggedIn = false">Cerrar sesión</button>
  </ng-container>

  <ng-template #loginTemplate>
    <h2>Inicia sesión</h2>
    <button (click)="isLoggedIn = true">Iniciar sesión</button>
  </ng-template>

  <app-games (addFavoriteEvent)="getFavorite($event)" username="{{ username }}"></app-games>

  <p *ngIf="favGame !== ''">Tu juego favorito es {{ favGame }}</p>
</section>
```

## **Decoradores**  
Los **decoradores** en Angular son funciones que se utilizan para modificar clases, propiedades, métodos o parámetros.  

| **Decorador** | **Descripción** |
|--------------|----------------|
| `@Component` | Define una clase como un componente de Angular. |
| `@Directive` | Crea una directiva personalizada. |
| `@Pipe` | Define una clase como un Pipe para transformar datos. |
| `@Injectable` | Marca una clase como un servicio inyectable. |
| `@Input` | Permite recibir valores de un componente padre a hijo. |
| `@Output` | Permite emitir eventos del hijo al padre. |
| `@HostListener` | Escucha eventos del DOM en la directiva o componente. |
| `@HostBinding` | Vincula propiedades del DOM a la directiva o componente. |
| `@ViewChild` | Obtiene una referencia a un elemento hijo en la plantilla. |
| `@ViewChildren` | Obtiene referencias a múltiples elementos hijos en la plantilla. |
| `@ContentChild` | Obtiene una referencia a un elemento anidado dentro de `<ng-content>`. |
| `@ContentChildren` | Obtiene múltiples referencias de elementos anidados en `<ng-content>`. |

---

## Routing en Angular
El sistema de rutas en Angular permite la navegación entre componentes.

### Conceptos Claves
- **router-outlet**: Punto de anclaje donde se carga dinámicamente el contenido de una ruta.
- **[routerLink]**: Directiva utilizada para la navegación interna sin recargar la página.

Ejemplo:
```html
<a [routerLink]="['/home']">Inicio</a>
```

## Operadores de TypeScript en Angular
- **`?`** (Operador de encadenamiento opcional): Previene errores al acceder a propiedades de objetos indefinidos o nulos.
  ```typescript
  user?.name
  ```
- **`??`** (Operador de coalescencia nula): Proporciona un valor por defecto cuando una variable es `null` o `undefined`.
  ```typescript
  let name = user.name ?? 'Desconocido';
  ```

## Formularios Reactivos en Angular
Los formularios reactivos en Angular permiten manejar datos de entrada de manera programática.

### Propiedades:
- **[formGroup]**: Agrupa los controles de un formulario.
- **formControlName**: Asocia un input con un control en el `FormGroup`.
- **(submit)**: Maneja el evento de envío del formulario.

Ejemplo:
```html
<form [formGroup]="myForm" (submit)="onSubmit()">
  <input type="text" formControlName="name">
</form>
```

## **Propiedades**
| Propiedad  | Descripción |
|------------|------------|
| `class` | Aplica clases CSS a un elemento. |
| `style` | Aplica estilos en línea. |
| `[innerHTML]` | Inserta contenido HTML dentro de un elemento. |
| `[value]` | Define el valor de un input. |
| `[disabled]` | Habilita o deshabilita un elemento. |
| `[hidden]` | Oculta un elemento sin removerlo del DOM. |
| `[checked]` | Define si un checkbox o radio está marcado. |
| `[readonly]` | Define si un campo de entrada es solo lectura. |
| `[selected]` | Define si un `<option>` de un `<select>` está seleccionado. |

---

## **Eventos**
| Evento  | Descripción |
|---------|------------|
| `(click)` | Detecta clics en elementos. |
| `(dblclick)` | Detecta doble clic. |
| `(mouseover)` | Detecta cuando el cursor pasa sobre un elemento. |
| `(mouseout)` | Detecta cuando el cursor sale de un elemento. |
| `(mouseenter)` | Detecta cuando el cursor entra en un elemento. |
| `(mouseleave)` | Detecta cuando el cursor deja un elemento. |
| `(keydown)` | Detecta cuando una tecla es presionada. |
| `(keyup)` | Detecta cuando una tecla es soltada. |
| `(keypress)` | Detecta cuando una tecla es presionada y sostenida. |
| `(input)` | Detecta cambios en un campo de entrada. |
| `(change)` | Detecta cambios en un `<select>` o `<input>`. |
| `(focus)` | Detecta cuando un elemento recibe el foco. |
| `(blur)` | Detecta cuando un elemento pierde el foco. |
| `(submit)` | Detecta el envío de un formulario. |
| `(scroll)` | Detecta cuando el usuario hace scroll. |
| `(load)` | Detecta cuando una imagen o recurso se ha cargado. |

---

## Peticiones HTTP en Angular
Angular permite hacer peticiones HTTP a servidores utilizando el servicio `HttpClient`.

### Ejemplo:
```typescript
import { HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';

@Injectable({ providedIn: 'root' })
export class DataService {
  constructor(private http: HttpClient) {}

  getData() {
    return this.http.get('https://api.example.com/data');
  }
}
```
