---

# 📘 **Documentación de Ionic CLI + Capacitor**

---

## 🔧 **Instalación Inicial**

```bash
npm install -g @ionic/cli
```

---

## 🆕 **Crear un nuevo proyecto**

```bash
ionic start myApp blank --type=angular
```

* `blank` → plantilla vacía
* `tabs`, `sidemenu` → otras plantillas disponibles
* `--type=angular` → también acepta `react`, `vue`, etc.

---

## ▶️ **Ejecutar el proyecto en el navegador**

```bash
ionic serve
```

* Abre el navegador con recarga automática.

---

## ⚙️ **Generar archivos (Pages, Components, Services)**

```bash
ionic generate page nombre
ionic generate component nombre
ionic generate service nombre
ionic generate module nombre
ionic generate directive nombre
ionic generate guard nombre
```

Alias: `g` en lugar de `generate`.

---

## 🧱 **Build del proyecto (para producción o Capacitor)**

```bash
ionic build
ionic build --prod
```

---

## 📱 **Agregar plataforma móvil (usando Capacitor)**

```bash
ionic capacitor add android
ionic capacitor add ios
```

---

## 🔁 **Sincronizar cambios con plataforma nativa**

```bash
ionic capacitor sync
```

* Equivalente a:

  ```bash
  ionic build
  npx cap copy
  npx cap sync
  ```

---

## 📂 **Abrir proyecto nativo en Android Studio o Xcode**

```bash
ionic capacitor open android
ionic capacitor open ios
```

---

## 🔄 **Actualizar Capacitor**

```bash
npx cap update
```

---

## 🧪 **Ejecutar app en dispositivo físico o emulador**

1. Conectar dispositivo Android por USB y habilitar depuración
2. Luego:

```bash
ionic capacitor run android -l --external
```

* `-l` → live reload (requiere red local)
* `--external` → accesible desde dispositivos en la red

---

## 🏗️ **Compilar APK o AAB (para Play Store)**

1. Abre Android Studio con:

   ```bash
   ionic capacitor open android
   ```
2. En Android Studio:

   * `Build > Build Bundle(s) / APK(s)`
   * Elige APK o AAB según lo necesario

---

## 🌐 **Cambiar puerto del servidor**

```bash
ionic serve --port=4300
```

---

## 🌍 **Documentación de configuración (ionic.config.json)**

Este archivo puede contener:

```json
{
  "name": "myApp",
  "type": "angular",
  "integrations": {
    "capacitor": {}
  }
}
```

---

## 🔄 **Migrar de Cordova a Capacitor**

```bash
ionic integrations enable capacitor
ionic capacitor init
```

---

## 📚 **Otras utilidades**

* **Ver información del entorno**

  ```bash
  ionic info
  ```

* **Actualizar Ionic CLI**

  ```bash
  npm install -g @ionic/cli
  ```

* **Mostrar ayuda**

  ```bash
  ionic --help
  ```

---

## ✅ **Consejos**

* Usa `npx cap copy` cada vez que modifiques archivos web y quieras probar en Android/iOS.
* Usa `ionic build --prod` para producción.
* Capacitor recomienda mantener Android/iOS como plataformas “desacopladas”; trabaja en ellas **desde Android Studio o Xcode**, no modifiques sus carpetas manualmente.

---
En un proyecto con **Ionic + Angular**, la configuración para autenticación **OAuth2 y JWT** es **muy similar** a Angular tradicional, pero con algunas consideraciones adicionales debido al entorno híbrido/móvil. Aquí te detallo las diferencias clave y cómo implementarlo correctamente:

---

## 🔐 **Similitudes con Angular tradicional**
1. **Uso de `HttpClient`** para llamadas a la API.  
2. **Interceptores** para agregar el token JWT a las solicitudes.  
3. **Guards** para proteger rutas (`canActivate`).  
4. **Servicios** para manejar login/logout.  
5. **Librerías compatibles** como:
   - `@auth0/angular-jwt` (para decodificar JWT).
   - `angular-oauth2-oidc` (para OAuth2/OpenID).

---

## ⚠️ **Diferencias en Ionic (Atención a estos puntos)**
### 1. **Almacenamiento del Token**
   - **En Angular web** se usa `localStorage` o `sessionStorage`.  
   - **En Ionic** (especialmente en apps nativas con Capacitor) es más seguro usar:
     - **`@ionic/storage`** o **`@capacitor/preferences`** (almacenamiento cifrado en dispositivo).  
     - Ejemplo con `@ionic/storage`:
       ```typescript
       import { Storage } from '@ionic/storage-angular';

       constructor(private storage: Storage) {}

       async guardarToken(token: string) {
         await this.storage.set('auth_token', token);
       }
       ```

### 2. **Protección de Rutas**
   - En Ionic, la navegación suele ser por `tabs` o `ion-router-outlet`, pero los `Guards` de Angular funcionan igual.  
   - Ejemplo de guard:
     ```typescript
     @Injectable({ providedIn: 'root' })
     export class AuthGuard implements CanActivate {
       constructor(private authService: AuthService, private router: Router) {}

       canActivate(): boolean {
         if (!this.authService.isLoggedIn()) {
           this.router.navigate(['/login']);
           return false;
         }
         return true;
       }
     }
     ```

### 3. **Manejo de Deep Links (OAuth2 Redirect)**
   - En **OAuth2**, después del login, el servidor redirige a una URL (ej: `mi-app://auth-callback`).  
   - **En Ionic con Capacitor** debes configurar el `Deep Link` en:
     - **Android**: `AndroidManifest.xml` (para el intent-filter).  
     - **iOS**: `Info.plist` (para URL schemes).  
   - Usa `@ionic/angular` o `AppLauncher` de Capacitor para manejar la redirección:
     ```typescript
     import { App } from '@capacitor/app';

     App.addListener('appUrlOpen', (data) => {
       if (data.url.includes('/auth-callback')) {
         // Extrae el token de la URL y procesa el login
       }
     });
     ```

### 4. **Librerías Específicas para Mobile**
   - Para autenticación con Google/Facebook, usa:
     - **`@abacritt/angularx-social-login`** (para web).  
     - **Capacitor plugins** como `@capacitor/google-auth` o `@capacitor/facebook-login` (para apps nativas).  

---

## 🛠️ **Ejemplo de Configuración con JWT**
### Interceptor para agregar el token:
```typescript
@Injectable()
export class JwtInterceptor implements HttpInterceptor {
  constructor(private storage: Storage) {}

  intercept(request: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    return from(this.storage.get('auth_token')).pipe(
      mergeMap((token) => {
        if (token) {
          request = request.clone({
            setHeaders: { Authorization: `Bearer ${token}` },
          });
        }
        return next.handle(request);
      })
    );
  }
}
```
**Registra el interceptor en `app.module.ts`**:
```typescript
providers: [
  { provide: HTTP_INTERCEPTORS, useClass: JwtInterceptor, multi: true },
],
```

---

## 📱 **Ejemplo de Login con OAuth2 en Ionic**
```typescript
// auth.service.ts
import { OAuthService } from 'angular-oauth2-oidc';

@Injectable({ providedIn: 'root' })
export class AuthService {
  constructor(private oauthService: OAuthService) {
    this.oauthService.configure({
      clientId: 'tu-client-id',
      issuer: 'https://tu-auth-server.com',
      redirectUri: window.location.origin + '/auth-callback',
      scope: 'openid profile email',
    });
  }

  login() {
    this.oauthService.initCodeFlow();
  }

  logout() {
    this.oauthService.logOut();
  }
}
```

---

## ✅ **Conclusión**
- **La base es la misma** que en Angular (interceptores, guards, servicios).  
- **Diferencias clave**:  
  - Almacenamiento seguro del token (`@ionic/storage` o `@capacitor/preferences`).  
  - Manejo de deep links en OAuth2 (configuración nativa con Capacitor).  
  - Plugins específicos para autenticación social en móvil.  



Aquí tienes una **tabla comparativa detallada** entre **Angular tradicional** y **Angular con Ionic**, destacando las diferencias clave en componentes, configuración, navegación, y otros aspectos relevantes:

---

### **📌 Tabla Comparativa: Angular Tradicional vs Angular con Ionic**
| **Categoría**          | **Angular Tradicional**                          | **Angular con Ionic**                          | **Notas** |
|-------------------------|-----------------------------------------------|---------------------------------------------|-----------|
| **Componentes UI**      | Componentes nativos de HTML (`<div>`, `<button>`). | Componentes Ionic (`<ion-button>`, `<ion-card>`). | Ionic añade componentes móvil-first con estilos y funcionalidades específicas (ej: gestures, modals nativos). |
| **Estilos**             | CSS estándar o preprocesadores (SCSS). | SCSS con variables CSS de Ionic (`--ion-color-primary`). | Ionic usa shadow DOM en sus componentes para evitar colisiones de estilos. |
| **Navegación**          | `RouterOutlet` de Angular. | `ion-router-outlet` + `ion-tabs` (con estado preservado). | Ionic maneja la pila de navegación como una app móvil (ej: animaciones de "back"). |
| **Routing**             | Configuración en `app-routing.module.ts`. | Similar, pero con soporte para lazy loading de páginas Ionic. | Ejemplo: `loadChildren: () => import('./page.module').then(m => m.PageModule)`. |
| **Estado de Componentes** | Se destruyen al navegar (a menos que uses `RouteReuseStrategy`). | Preserva el estado en `ion-router-outlet` (como en apps móviles). | Ideal para tabs o flujos complejos. |
| **Servicios/Inyección** | Igual en ambos. | Igual, pero con servicios específicos de Ionic (`Platform`, `LoadingController`). | |
| **Manejo de Formularios** | `ReactiveForms` o `Template-Driven`. | Igual, pero con componentes Ionic (`ion-input`, `ion-select`). | Validación y lógica idéntica. |
| **HTTP/API Calls**      | `HttpClient` de Angular. | Igual, pero con plugins de Capacitor para funcionalidades nativas (ej: `@capacitor/http`). | |
| **Autenticación**       | JWT, OAuth2 estándar. | Igual, pero con almacenamiento seguro (`@ionic/storage` o `@capacitor/preferences`). | Deep links en OAuth2 requieren configuración en Capacitor. |
| **Comunicación entre Componentes** | `@Input()`, `@Output()`, servicios. | **Igual**, pero común usar servicios para tabs/páginas. | |
| **Modales/Overlays**    | Dialogs personalizados o librerías (ej: Angular Material). | Componentes Ionic (`ion-modal`, `ion-popover`). | Integración nativa con gestos y animaciones. |
| **Almacenamiento**      | `localStorage` o `sessionStorage`. | `@ionic/storage` o `@capacitor/preferences` (seguro en móvil). | Capacitor ofrece cifrado en dispositivo. |
| **Plugins Nativos**     | No aplica. | Capacitor/Cordova para acceder a hardware (cámara, GPS). | Ejemplo: `@capacitor/camera`. |
| **Build y Despliegue**  | `ng build` (para web). | `ionic build` + `npx cap add android/ios` (para móvil). | Capacitor copia el build a un proyecto nativo. |
| **Debugging**           | Herramientas de navegador (DevTools). | DevTools + herramientas nativas (Android Studio/Xcode). | Ionic DevApp para pruebas rápidas en dispositivo. |
| **PWA**                 | Configuración manual o `@angular/pwa`. | Soporte integrado con `@ionic/pwa-elements`. | Ionic facilita la generación de PWAs. |
| **Animaciones**         | CSS o Angular Animations. | Animaciones específicas de Ionic (`ion-animation`) + integración con gestos. | Mejor rendimiento en móvil. |
| **Theming**             | CSS custom o librerías (ej: Bootstrap). | Variables CSS de Ionic (`--ion-color-*`) + modo claro/oscuro automático. | |

---

### **🔹 ¿Qué no cambia?**
1. **Core de Angular**: Inyección de dependencias, módulos, pipes, directivas, etc.  
2. **RxJS**: Manejo de observables y operadores.  
3. **Estructura de proyecto**: `src/app`, lazy loading, etc.  
4. **Testing**: Karma/Jasmine (aunque Ionic recomienda probar en dispositivos reales).  

---

### **🚀 Conclusión**  
- **Ionic extiende Angular** para móvil, pero no rompe sus patrones base.  
- **Las diferencias clave** son:  
  - **Componentes UI** (Ionic tiene su propio set).  
  - **Navegación** (más similar a apps nativas).  
  - **Plugins** para hardware (Capacitor/Cordova).  
  - **Build** multiplataforma (iOS/Android/PWA).  

Si ya sabes Angular, aprender Ionic es fácil: solo añade los componentes y herramientas móviles. ¡Es como Angular con superpoderes para apps híbridas! 📱✨

Sí, en **Ionic + Angular**, la comunicación entre componentes **padres e hijos** funciona **exactamente igual** que en Angular tradicional, ya que Ionic está construido sobre Angular. Puedes usar los mismos métodos estándar de Angular para pasar datos entre componentes. Aquí te resumo las principales técnicas:

---

## 📤 **De Padre → Hijo** (Input Properties)
**Igual que en Angular**: Usas `@Input()` para recibir datos en el hijo.

### Ejemplo:
#### **Padre (`parent.component.ts`)**:
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  template: `
    <app-child [mensaje]="mensajePadre"></app-child>
  `,
})
export class ParentComponent {
  mensajePadre = "Hola desde el padre!";
}
```

#### **Hijo (`child.component.ts`)**:
```typescript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `<p>{{ mensaje }}</p>`,
})
export class ChildComponent {
  @Input() mensaje: string = "";
}
```

---

## 📥 **De Hijo → Padre** (Output + EventEmitter)
**Igual que en Angular**: Usas `@Output()` y `EventEmitter` para enviar datos al padre.

### Ejemplo:
#### **Hijo (`child.component.ts`)**:
```typescript
import { Component, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `
    <ion-button (click)="enviarMensaje()">Enviar al Padre</ion-button>
  `,
})
export class ChildComponent {
  @Output() mensajeEnviado = new EventEmitter<string>();

  enviarMensaje() {
    this.mensajeEnviado.emit("Hola desde el hijo!");
  }
}
```

#### **Padre (`parent.component.ts`)**:
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  template: `
    <app-child (mensajeEnviado)="recibirMensaje($event)"></app-child>
    <p>{{ mensajeDelHijo }}</p>
  `,
})
export class ParentComponent {
  mensajeDelHijo = "";

  recibirMensaje(mensaje: string) {
    this.mensajeDelHijo = mensaje;
  }
}
```

---

## 🔄 **Comunicación entre Componentes no Relacionados**
Si los componentes **no tienen relación padre-hijo**, puedes usar:
1. **Servicios con `Subject` o `BehaviorSubject`** (igual que en Angular).  
2. **Estado global** (NgRx, Akita, o servicios compartidos).  

### Ejemplo con Servicio:
#### **Servicio (`data.service.ts`)**:
```typescript
import { Injectable } from '@angular/core';
import { BehaviorSubject } from 'rxjs';

@Injectable({ providedIn: 'root' })
export class DataService {
  private mensajeSource = new BehaviorSubject<string>("Mensaje inicial");
  mensajeActual = this.mensajeSource.asObservable();

  cambiarMensaje(mensaje: string) {
    this.mensajeSource.next(mensaje);
  }
}
```

#### **Componente Emisor**:
```typescript
constructor(private dataService: DataService) {}

enviarMensaje() {
  this.dataService.cambiarMensaje("Nuevo mensaje");
}
```

#### **Componente Receptor**:
```typescript
mensaje: string = "";

constructor(private dataService: DataService) {}

ngOnInit() {
  this.dataService.mensajeActual.subscribe(mensaje => {
    this.mensaje = mensaje;
  });
}
```

---

## 🌐 **Comunicación con Tabs o Páginas en Ionic**
En Ionic, si necesitas comunicar componentes en diferentes páginas o tabs:
- **Usa servicios** (como el ejemplo anterior).  
- **Params en navegación** (si pasas datos entre páginas):

### Ejemplo con `NavController`:
#### **Enviar datos a otra página**:
```typescript
import { NavController } from '@ionic/angular';

constructor(private navCtrl: NavController) {}

irAPaginaDestino() {
  this.navCtrl.navigateForward('/destino', {
    state: { datos: { id: 1, nombre: 'Ejemplo' } }
  });
}
```

#### **Recibir datos en la página destino**:
```typescript
import { ActivatedRoute } from '@angular/router';

constructor(private route: ActivatedRoute) {}

ngOnInit() {
  const datos = this.route.snapshot.paramMap.get('state');
  console.log(datos); // { id: 1, nombre: 'Ejemplo' }
}
```

---

## ✅ **Conclusión**
- **Ionic no modifica** los mecanismos de comunicación de Angular.  
- **Padre → Hijo**: `@Input()`.  
- **Hijo → Padre**: `@Output()` + `EventEmitter`.  
- **Componentes no relacionados**: Servicios con `Subject`/`BehaviorSubject`.  
- **Entre páginas/tabs**: Parámetros de navegación o servicios.  

¡Es Angular puro, pero con componentes UI de Ionic! 🚀