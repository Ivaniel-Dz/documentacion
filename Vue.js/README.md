# Vue.js 3

<p align="center">
<img src="https://mochikit.com/wp-content/uploads/2019/01/vue-js-logo.png" width="400"/>
</p>

## Creación del proyecto
#### Opción 1: desde vue
```bash
npm create vue@lasted
```
#### Opción 2: desde vite
```bash
npm create vite@lasted
```
#### Instala y gestiona de dependencia en el proyecto
```bash
npm install
```
#### Inicia un servidor de desarrollo local
```bash
npm run dev
```

## Estructura de vue
![alt text](img/image.png)
- Dentro del ``` <template> </template> ```, contendrá etiquetas, elementos html, eventos, funciones y etc..
- En el contenido se puede asignar una variable declarada o una función del script.
- Dentro del contenido con ```{{ variable o funciones }}``` asi se imprime una variable o se ejecuta una función.
- **setup** en el script se usa para no declarar las exportaciones o importaciones para usar métodos o funciones en el script (Implementación del vue3).
- **scope**, nos permite que todo los estilos declarados dentro de un etiqueta style afecte solo donde este ubicado la etiqueta, no afectara a los demás template.

## Directivas
![alt text](img/image-1.png)
- Las directivas se utilizaran para realizar eventos o algún tipo de acción, sin necesita de usar métodos como getByElement y querySelector y entre otros .
- Las directivas se declaran dentro de las etiquetas y algunos pueden ir acompañado con un atributo.
- Dentro de los atributos puede contener como value una ejecución de una variable o una función ```v-bind:atributo="variable o función" ```. 
- Las directivas tiene sus abreviaciones solo con poner ```:``` no es necesario poner ```v-bind``` o ```@ es v-on```.

### v-bind
![alt text](img/image-2.png)
- En Vue nos permite declarar estilos de css en js y luego asignar ese variable a una etiqueta a traves de la directiva v-bind, usando el atribudo ```class```.
- La directiva ```v-bind``` se utiliza para asociar dinámicamente atributos HTML a expresiones de datos en Vue.js.

### v-on
![alt text](img/image-3.png)
- La directiva ```v-on``` se utiliza para adjuntar escuchadores de eventos a elementos HTML para que reaccionen a eventos del DOM.
- ```@click``` es utilizado como un atributo dentro de la directiva ```v-on```, para realizar una acción y llama como value a una función donde ejecuta la lógica.

### v-show
![alt text](img/image-9.png)
- Oculta los elemento aplicando ```display: none;```.
- Su valor por defecto es true, ya que su valor es tipo bolean.
- A diferencia de v-if, v-show siempre renderiza el elemento en el DOM y solo lo controla con CSS.

## Variables reactivas (ref)
![alt text](img/image-4.png)
- Una variable reactivas es una variable que está vinculada a la vista y se actualiza automáticamente cuando cambia su valor.
    - ejemplo de ref: 
    ```js
        import { ref } from 'vue';

        const contador = ref(0);
        console.log(contador.value); // 0
        contador.value++; // Incrementa el valor de contador y actualiza la vista automáticamente
    ```
    - ejemplo de reactive:
    ```js
        import { reactive } from 'vue';

        const estado = reactive({
            mensaje: 'Hola',
            contador: 0
        });

        console.log(estado.mensaje); // 'Hola'
        estado.mensaje = 'Hola Mundo'; // Actualiza el mensaje y actualiza la   vista automáticamente
    ```
- Para usar variables reactivas se importa.
- Los variables que serán reactivas su valor se declara dentro de la palabra reservada ```ref(valor)```.
- Donde se use la variable reactiva dentro del script, llevara ```.value```.
- Excepto dentro del template no sera necesario que lleve ```.value```.


### Cuando usar ref y reactive
- **Variables ref:**
    - Ideal para valores primitivos simples o para acceder directamente al valor.
    - Mejor opción cuando necesitas reactividad solo en un nivel superficial y no necesitas iterar sobre propiedades.
    - Acceso al valor directo a través de ref.value.
    - Más adecuado para manejar valores simples como números, cadenas o booleanos.
- **Variables reactivas (reactive):**
    - Útiles para objetos complejos o estructuras de datos anidadas.
    - Proporcionan reactividad profunda, lo que significa que todos los niveles de propiedades del objeto son reactivos.
    - Más apropiado cuando necesitas iterar sobre propiedades de un objeto o realizar manipulaciones dinámicas en profundidad.
    - Mejor rendimiento en actualizaciones masivas de objetos complejos debido a su reactividad profunda

## Directiva de condiciones
![alt text](img/image-5.png)
- Nos permite realiza evaluación de condición en la etiqueta podemos combinar de la siguiente manera:
    - v-if y v-else
    - v-if y v-else-if
- La su estructura es: ```<etiqueta v-directiva="variable condición"> contenido </etiqueta>``` 

## Propiedad computada
![alt text](img/image-6.png)
- Para usarlo tiene que importarse al script.
- Siempre es reactiva por defecto.
- Se almacena en caché el resultado de su cálculo y solo se recalcula cuando alguna de las dependencias cambia.
- siempre retornara algo.
- Es una propiedad que se calcula dinámicamente en función de los datos reactivos existentes en tu aplicación.
- La propiedad computada es una excelente opción cuando necesitas realizar cálculos dinámicos basados en datos reactivos de manera eficiente y mantenible.
### Cuando usar la propiedad computada

1. **Transformaciones o formatos de datos**: Cuando necesitas mostrar datos en un formato específico o transformarlos de alguna manera para la presentación en la interfaz de usuario. Por ejemplo, convertir una fecha en un formato legible o aplicar algún formato numérico especial.

2. **Filtrado y ordenamiento de listas**: Cuando necesitas filtrar o ordenar una lista de datos basada en ciertos criterios. Puedes utilizar propiedades computadas para realizar estas operaciones de manera eficiente y mantener la lógica de filtrado y ordenamiento separada del marcado.

3. **Validación de datos**: Cuando necesitas validar ciertos datos o realizar cálculos condicionales basados en ellos. Por ejemplo, validar un formulario o calcular un subtotal basado en ciertos campos.

4. **Cálculos basados en múltiples datos**: Cuando necesitas realizar cálculos que dependen de múltiples datos reactivos en tu aplicación. Las propiedades computadas te permiten definir la lógica de cálculo de manera clara y concisa, sin necesidad de repetir código.

5. **Optimización de rendimiento**: Cuando necesitas optimizar el rendimiento de tu aplicación al evitar cálculos innecesarios. Las propiedades computadas almacenan en caché sus resultados y se recalculan solo cuando alguna de las dependencias cambia, lo que puede mejorar significativamente el rendimiento en aplicaciones con lógica compleja.

La propiedad computada es una excelente opción cuando necesitas realizar cálculos dinámicos basados en datos reactivos de manera eficiente y mantenible en tus aplicaciones Vue.js.

## Imágenes en Vue
![alt text](img/image-7.png)
- La carpeta /public, es recomendable guarda en esa carpeta por que no se compila la carpeta y no es necesario importar su uso en el script.
- La carpeta /assets borra los archivos que no vienen por defecto cada vez que reinicia el proyecto, Importar en el script para usar las imágenes, Compila para usar la imagen. 
- En la variable donde se guarde la dirección de la imagen no es necesario poner ```public/img/imagen.jpg```, porque VUE ya lo supone que esta hay, por eso solo se pone el nombre y extension de la img.
- La directiva ```:src="variable"``` en Vue.js se utiliza para enlazar dinámicamente el atributo src de un elemento HTML a una expresión en el modelo de datos de Vue.js. Esto permite cargar imágenes u otros recursos de forma dinámica según el estado de la aplicación.

## Cargar datos externos
![alt text](img/image-8.png)
- Se importa desde el script, se puede importar un archivo externo de otro carpeta o de la misma carpeta.
- Se importa el objeto con el que se quiere trabajar y se declara para poder usarlo dentro del código.

## Directivas mas usadas
Las directivas en Vue.js son atributos especiales que se aplican a los elementos HTML y les indican a Vue.js cómo debe comportarse el DOM.

- `v-for`:
   - La directiva `v-for` se utiliza para renderizar una lista de elementos basada en una matriz o un objeto iterable.
   - Ejemplo:
     ```html
     <ul>
       <li v-for="item in items" :key="item.id">{{ item.text }}</li>
     </ul>
     ```

- `v-model`:
   - La directiva `v-model` se utiliza para crear enlaces bidireccionales entre un elemento de formulario y los datos de Vue.js.
   - Ejemplo:
     ```html
     <input v-model="mensaje" placeholder="Ingrese un mensaje">
     ```

- `v-once`:
   - La directiva `v-once` se utiliza para renderizar un elemento o componente de forma estática, sin volver a evaluarlo.
   - Útil para elementos estáticos que no cambian después de su primera renderización.
   - Ejemplo:
     ```html
     <p v-once>{{ mensajeEstatico }}</p>
     ```

- `v-text`:
   - La directiva `v-text` se utiliza para establecer el contenido de un elemento con el texto renderizado desde una expresión de datos.
   - Es similar a la interpolación de texto `{{ }}`, pero se puede usar en combinación con otros atributos.
   - Ejemplo:
     ```html
     <span v-text="mensaje"></span>
     ```

Estas son solo algunas de las directivas más comunes en Vue.js. Hay muchas otras directivas disponibles que proporcionan funcionalidades adicionales para manipular el DOM y los datos de manera eficiente.

## Ejemplo de compasar variables, object, function de un componente a otro
> En Vue 3, los props se utilizan para pasar datos de un componente padre a un componente hijo. Te mostraré un ejemplo sencillo de cómo hacerlo, incluyendo varios tipos de datos que puedes pasar como props.

### Paso 1: Crear el Componente Hijo

Primero, definamos un componente hijo llamado `ChildComponent.vue` que recibirá props de su componente padre.

**ChildComponent.vue**
```vue
<template>
  <div>
    <h3>Props en el Componente Hijo</h3>
    <p>Texto: {{ text }}</p>
    <p>Número: {{ number }}</p>
    <p>Booleano: {{ boolean }}</p>
    <p>Objeto: {{ objectProp.name }}, Edad: {{ objectProp.age }}</p>
    <p>Arreglo: {{ arrayProp.join(', ') }}</p>
    <p>Función: {{ functionProp() }}</p>
  </div>
</template>

<script setup>
// en vue 3 ya no es necesario importar define defineProps

// Definir las props que el componente hijo recibirá
const props = defineProps({
  text: String,
  number: Number,
  boolean: Boolean,
  objectProp: Object,
  arrayProp: Array,
  functionProp: Function
});
</script>
```

### Paso 2: Crear el Componente Padre

Ahora, crearemos un componente padre llamado `ParentComponent.vue` que enviará los props al componente hijo.

**ParentComponent.vue**
```vue
<template>
  <div>
    <h1>Componente Padre</h1>
    <ChildComponent 
      text="Hola, Vue!" 
      :number="123" 
      :boolean="true" 
      :object-prop="{ name: 'Juan', age: 30 }"
      :array-prop="[1, 2, 3, 4, 5]"
      :function-prop="sayHello"
    />
  </div>
</template>

<script setup>
import ChildComponent from './ChildComponent.vue';

// Definir métodos y otras lógicas aquí
function sayHello() {
  return '¡Hola desde la función!';
}
</script>

```

### Explicación

1. **Componente Hijo (`ChildComponent.vue`)**: 
   - Define una serie de props que puede recibir, cada una con un tipo de dato específico (`String`, `Number`, `Boolean`, `Object`, `Array`, `Function`).
   - En el template, se muestran estos props.

2. **Componente Padre (`ParentComponent.vue`)**:
   - Importa el `ChildComponent` y lo utiliza en el template.
   - Pasa diferentes tipos de datos como props al `ChildComponent`, incluyendo un string, número, booleano, objeto, arreglo y función.

### ¿Cómo se utiliza?

Al montar `ParentComponent.vue` en tu aplicación, verás que `ChildComponent.vue` recibe todos los props y los muestra en la pantalla. Este ejemplo cubre diferentes tipos de datos que puedes pasar como props y te proporciona una base sólida para entender cómo funcionan en Vue 3.


## Vue Router
En Vue.js, el **Router** y el **Link** son herramientas esenciales para manejar la navegación entre diferentes componentes o páginas en una aplicación de una sola página (SPA, por sus siglas en inglés).

### 1. Vue Router

**Vue Router** es una biblioteca de Vue.js que se utiliza para manejar la navegación y el enrutamiento en aplicaciones de una sola página. Permite definir rutas en tu aplicación que corresponden a diferentes componentes y manejar la navegación del usuario entre ellos sin recargar la página.

**Cuándo usarlo:**
- Cuando tienes una aplicación Vue con múltiples vistas o páginas.
- Cuando necesitas una navegación más compleja que la que se puede lograr con enlaces simples.
- Cuando quieres mantener la experiencia de usuario fluida sin recargar toda la página.

**Configuración básica de Vue Router:**

Para usar Vue Router, debes instalarlo y configurarlo en tu proyecto Vue. A continuación, te muestro cómo se configura:

```bash
npm install vue-router
```

Luego, configura el router en tu archivo principal de Vue (por ejemplo, `main.js`):

```javascript
import { createApp } from 'vue';
import App from './App.vue';
import { createRouter, createWebHistory } from 'vue-router';

// Importa los componentes que se usarán como rutas
import Home from './components/Home.vue';
import About from './components/About.vue';

// Define las rutas
const routes = [
  { path: '/', component: Home },   // Ruta para el componente Home
  { path: '/about', component: About }  // Ruta para el componente About
];

// Crea el router
const router = createRouter({
  history: createWebHistory(),
  routes,
});

// Crea la aplicación Vue y usa el router
createApp(App).use(router).mount('#app');
```

### 2. RouterLink

**RouterLink** es un componente que Vue Router proporciona para crear enlaces de navegación en tu aplicación. Funciona de manera similar a una etiqueta HTML `<a>`, pero está optimizado para trabajar con Vue Router, de manera que la navegación es más eficiente y no recarga toda la página.

**Cuándo usarlo:**
- Cuando necesitas crear un enlace que navega a una ruta específica en una aplicación Vue con Vue Router.
- Cuando quieres beneficiarte de las características de optimización de Vue Router, como la carga perezosa (lazy loading) de componentes.

**Uso básico de RouterLink:**

El componente `<RouterLink>` se utiliza en el template de tus componentes Vue para crear enlaces de navegación. Aquí hay un ejemplo de cómo usarlo:

```vue
<template>
  <div>
    <h1>My Vue App</h1>
    <!-- Usar RouterLink para la navegación -->
    <nav>
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/about">About</RouterLink>
    </nav>
    
    <!-- Muestra el componente correspondiente a la ruta actual -->
    <router-view></router-view>
  </div>
</template>
```

En este ejemplo:

- `<RouterLink to="/">Home</RouterLink>` crea un enlace que lleva al componente `Home` cuando se hace clic.
- `<RouterLink to="/about">About</RouterLink>` crea un enlace que lleva al componente `About` cuando se hace clic.
- `<router-view></router-view>` es un contenedor que muestra el componente correspondiente a la ruta actual.

### Ejemplo completo

Un ejemplo completo que incluye la configuración del router y el uso de `<RouterLink>` para la navegación sería así:

#### `main.js`

```javascript
import { createApp } from 'vue';
import App from './App.vue';
import { createRouter, createWebHistory } from 'vue-router';
import Home from './components/Home.vue';
import About from './components/About.vue';

const routes = [
  { path: '/', component: Home },
  { path: '/about', component: About },
];

const router = createRouter({
  history: createWebHistory(),
  routes,
});

createApp(App).use(router).mount('#app');
```

#### `App.vue`

```vue
<template>
  <div id="app">
    <nav>
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/about">About</RouterLink>
    </nav>
    <router-view></router-view>
  </div>
</template>
```

#### `Home.vue`

```vue
<template>
  <div>
    <h2>Home Page</h2>
    <p>Welcome to the Home page!</p>
  </div>
</template>
```

#### `About.vue`

```vue
<template>
  <div>
    <h2>About Page</h2>
    <p>This is the About page!</p>
  </div>
</template>
```

### Resumen

- **Vue Router** gestiona la navegación en aplicaciones de una sola página.
- **RouterLink** crea enlaces de navegación que se integran perfectamente con Vue Router.
- Se usan juntos para crear aplicaciones Vue con múltiples vistas o componentes, proporcionando una experiencia de usuario fluida.