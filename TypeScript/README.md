# TypeScript
<p align="center"><a href="https://www.typescriptlang.org/docs/handbook/typescript-from-scratch.html" target="_blank"><img src="https://miro.medium.com/v2/resize:fit:828/format:webp/1*eZX21KaXanUokLYelxNURg.png" width="400" alt="spring Logo"></a></p>

>TypeScript es un lenguaje de programación que extiende JavaScript, añadiendo tipos estáticos y otras características para mejorar la productividad y la calidad del código.

## Tabla de Comparación: TypeScript vs JavaScript

| Característica          | TypeScript                          | JavaScript                        |
|-------------------------|-------------------------------------|-----------------------------------|
| **Tipado**              | Estático (se definen tipos)         | Dinámico (tipos inferidos)        |
| **Compatibilidad**      | Superconjunto de JavaScript         | Lenguaje base                     |
| **Detección de errores**| En tiempo de compilación            | En tiempo de ejecución            |
| **Herramientas**        | Autocompletado, refactorización     | Menos herramientas avanzadas      |
| **Compilación**         | Requiere compilación a JavaScript   | No requiere compilación           |
| **Uso recomendado**     | Proyectos grandes/complejos         | Proyectos pequeños/rápidos        |

---

### Ejemplo de Código con Explicación

#### JavaScript:
```javascript
function suma(a, b) {
    return a + b;
}

console.log(suma(5, 3)); // 8
console.log(suma("Hola", "Mundo")); // "HolaMundo"
```

- **Explicación**:
  - En JavaScript, no se especifican tipos para los parámetros `a` y `b`.
  - La función puede sumar números o concatenar cadenas, ya que el tipado es dinámico.
  - Esto puede llevar a errores inesperados si no se manejan correctamente los tipos.


#### TypeScript:
```typescript
function suma(a: number, b: number): number {
    return a + b;
}

console.log(suma(5, 3)); // 8
console.log(suma("Hola", "Mundo")); // Error en tiempo de compilación
```

- **Explicación**:
  - En TypeScript, se especifica que `a` y `b` deben ser de tipo `number`.
  - Si se intenta pasar un tipo incorrecto (como cadenas), el compilador arroja un error **antes de ejecutar el código**.
  - Esto mejora la seguridad y reduce errores en tiempo de ejecución.

### Diferencia Clave:
- **TypeScript** asegura que los tipos sean correctos en tiempo de compilación, evitando errores comunes.
- **JavaScript** es más flexible pero propenso a errores si no se validan los tipos manualmente.


## Anotaciones de Tipo
>Las anotaciones de tipo son una forma explícita de indicar el tipo de datos que una variable, parámetro, función o retorno debe tener. Estas anotaciones ayudan al compilador a verificar que el código cumpla con las restricciones de tipos, mejorando la seguridad y la calidad del código.

## **Inferencia de tipos**
>Es la capacidad del compilador para deducir automáticamente el tipo de una variable, parámetro o expresión sin necesidad de que el programador lo especifique explícitamente. Esto hace que el código sea más conciso y fácil de escribir, sin perder los beneficios del sistema de tipos.

## **Anotaciones para variables**:
Se especifica el tipo de una variable al declararla. Aunque no es necesario agregar el tipado porque se puede inferir los variables.
   ```typescript
   let nombre: string = "Juan";
   let edad: number = 25;
   let esEstudiante: boolean = true;
   ```

## **Anotaciones para arreglos**:
Se indica el tipo de los elementos que contendrá el arreglo.
   ```typescript
   let numeros: number[] = [1, 2, 3];
   let palabras: string[] = ["hola", "mundo"];
   let lenguajes: (string | number) [] = [] // se pueden tipar arrays
   ```

## **Anotaciones para objetos**:
Se define la estructura del objeto especificando los tipos de sus propiedades.
   ```typescript
   let persona: { nombre: string, edad: number } = {
       nombre: "Ana",
       edad: 30
   };
   ```

## **Anotaciones para funciones**:
- **Parámetros**: Se especifica el tipo de los parámetros.
- **Retorno**: Se indica el tipo de valor que la función devolverá.
- **Inferencia**: No sufre de inferencia, asi que se tiene que agregar el tipo a las funciones.
   
```typescript
// función normal
function suma(a: number, b: number): number  { ///se declara el tipo de dato que devolverá :number
    return a + b;
}
```

```typescript
//función que recibe parámetro tipo objeto
function saludar({name, age}: {name: string, age: number}) : string { //s
    declara el tipo de dato que devolvera :string
    console.log(`Hola ${name}, tiene ${age} años`)

    return name
  }
```

```typescript
// Funcion que recibe como parametro otra funcion, se declara que tipo dedatos retornara, en este caso void
const sayHiFromFunction = (fn: (name: string) => void) => {
    fn('Ivan')
}

const sayHi = (name: string) => {
    console.log(`Hola ${name}`)
}

sayHiFromFunction(sayHi)
```

```typescript
// funciones flechas y se declara el tipo de valor a retornar :number
const sumar = (a: number, b: number) :number => {
    return a + b
}
```

```typescript
// Funciones Anónimas si tiene inferencia de datos
const avenger = ['Spider-ma', 'Iron man', 'Hulk']

avenger.forEach(function (avenger) {
    console.log(avenger.toUpperCase());
})
```
    
## **Anotaciones para tipos personalizados**:
Se pueden crear tipos personalizados con `type` o `interface`.
   ```typescript
   type Punto = {
       x: number;
       y: number;
   };

   let punto: Punto = { x: 10, y: 20 };
   ```

## **Anotaciones para tipos genéricos**:
Se usan para crear funciones o clases que trabajen con múltiples tipos.
   ```typescript
   function identidad<T>(valor: T): T {
       return valor;
   }

   let resultado: number = identidad<number>(42);
   ```
## **Anotaciones para uniones**:
Permiten que una variable tenga más de un tipo posible.
   ```typescript
   let id: string | number;
   id = "ABC123"; // Válido
   id = 123;      // Válido
   ```

## **Anotaciones para tipos literales**:
Se restringe el valor exacto que una variable puede tomar.
   ```typescript
   let direccion: "norte" | "sur" | "este" | "oeste";
   direccion = "norte"; // Válido
   direccion = "centro"; // Error
   ```

## **Anotaciones para `any`**:
Desactiva la verificación de tipos para una variable.
   ```typescript
   let valor: any = "esto puede ser cualquier cosa";
   valor = 42; // Válido
   ```

## **Anotaciones para unknown**
Similar a any, pero más seguro, ya que requiere una verificación de tipo antes de usarse.
```typescript
let valorDesconocido: unknown = "esto podría ser cualquier cosa";
    
if (typeof valorDesconocido === "string") {
    console.log(valorDesconocido.toUpperCase()); // Válido
}
```

## **Type Aliases y PascalCase**
```typescript
type HeroId = `${string}-${string}-${string}-${string}-${string}`;
```
- **Type Alias**: Es una forma de crear un nombre para un tipo específico. Aquí, `HeroId` es un alias para un tipo de cadena con un formato específico.
- **PascalCase**: Es una convención de nomenclatura donde la primera letra de cada palabra está en mayúscula. Se usa comúnmente para tipos y clases.
- **Template Union Types**: Permite crear tipos basados en patrones de cadenas. En este caso, `HeroId` es un tipo que representa un UUID (identificador único) con el formato `xxxx-xxxx-xxxx-xxxx-xxxx`.


## **Tipos opcionales y `readonly`**
```typescript
type Hero = {
    id?: HeroId; // Opcional
    name: string;
    age: number;
    isActive?: boolean; // Opcional
};
```
- **Tipos opcionales**: Se definen con `?`. Indican que una propiedad puede estar presente o no en el objeto.
- **`readonly`**: Si se usa, la propiedad no puede ser modificada después de su creación (solo lectura).


## **Creación de un objeto `Hero`**
```typescript
let hero: Hero = {
    name: 'thor',
    age: 1500
};
```
- Aquí se crea un objeto `hero` que cumple con el tipo `Hero`. Como `id` e `isActive` son opcionales, no es necesario incluirlos.


## **Función para crear un héroe**
```typescript
function createHero(hero: Hero): Hero {
    const { name, age } = hero;
    return {
        id: crypto.randomUUID(), // Genera un UUID único
        name,
        age,
        isActive: true
    };
}
```
- **`crypto.randomUUID()`**: Es una función nativa del navegador que genera un identificador único (UUID).
- La función toma un objeto `Hero` como parámetro y devuelve un nuevo objeto `Hero` con un `id` generado automáticamente.


## **Template Union Types para colores hexadecimales**
```typescript
type HexadecimaColor = `#${string}`;
```
- Define un tipo que solo acepta cadenas que comienzan con `#`, como los colores hexadecimales (`#FFFFFF`, `#000000`, etc.).


## **Union Types**
```typescript
type HeroPowerScale = 'low' | 'medium' | 'high';
let dato: number | string;
```
- **Union Types**: Permiten que una variable pueda ser de uno de varios tipos. En este caso:
  - `HeroPowerScale` solo acepta los valores `'low'`, `'medium'` o `'high'`.
  - `dato` puede ser de tipo `number` o `string`.


## **Intersection Types**
```typescript
type HeroBasicInfo = {
    name: string;
    age: number;
};

type HeroProperties = {
    readonly id?: HeroId;
    isActive?: boolean;
    poweScale?: HeroPowerScale;
};

type Hereo = HeroBasicInfo & HeroProperties;
```
- **Intersection Types**: Combina dos o más tipos en uno solo. Aquí, `Hereo` es la combinación de `HeroBasicInfo` y `HeroProperties`.


## **Type Indexing y ReturnType**
```typescript
function createAddress() {
    return {
        planet: 'Tierra',
        city: 'Barcelona'
    };
}

type Address = ReturnType<typeof createAddress>;
```
- **Type Indexing**: Permite extraer el tipo de retorno de una función.
- **`ReturnType`**: Es una utilidad de TypeScript que obtiene el tipo de retorno de una función. Aquí, `Address` es el tipo del objeto devuelto por `createAddress`.


## **Matrices y Tuplas**
```typescript
type CellValue = 'X' | 'O' | '';
type GameBoard = [
    [CellValue, CellValue, CellValue],
    [CellValue, CellValue, CellValue],
    [CellValue, CellValue, CellValue],
];

const gameBoard: GameBoard = [
    ['X', 'X', 'X'],
    ['O', 'X', 'O'],
    ['', 'X', '']
];
```
- **Tuplas**: Son arreglos con una longitud fija y tipos específicos para cada posición.
- En este caso, `GameBoard` es una tupla que representa un tablero de 3x3 para un juego como el tres en raya. Cada celda puede ser `'X'`, `'O'` o `''` (vacía).

## **Enums**
```typescript
const enum ERROR_TYPES {
    NOT_FOUND = 'notFound',
    UNAUTHORIZED = 'unathorized',
    FORBIDDEN = 'forbidden'
}

function mostrarMensaje(tipoDeError: ERROR_TYPES) {
    if (tipoDeError === ERROR_TYPES.NOT_FOUND) {
        console.log('No se encuentra el recurso');
    } else if (tipoDeError === ERROR_TYPES.UNAUTHORIZED) {
        console.log('No tienes permiso para acceder');
    } else if (tipoDeError === ERROR_TYPES.FORBIDDEN) {
        console.log('No tienes permisos para acceder');
    }
}
```

- **Enums**: Son colecciones de valores finitos y nombrados. Aquí, `ERROR_TYPES` es un enum que define tres tipos de errores.
- **`const enum`**: Es una versión optimizada de los enums que se elimina en tiempo de compilación, reduciendo el código generado.
- **Uso**: La función `mostrarMensaje` recibe un valor del enum `ERROR_TYPES` y muestra un mensaje dependiendo del tipo de error.


## **Aserciones de tipos**
```typescript
const canvas = document.getElementById('span');

if (canvas instanceof HTMLCanvasElement) {
    const ctx = canvas.getContext('2d');
}
```

- **Aserciones de tipos**: Permiten afirmar que un valor es de un tipo específico. Aquí, se usa `instanceof` para verificar si `canvas` es una instancia de `HTMLCanvasElement`.
- **`instanceof`**: Verifica si un objeto es una instancia de una clase o constructor específico.
- **`typeof`**: Se usa para verificar el tipo de un valor primitivo (como `string`, `number`, etc.).


## **Interfaces**
```typescript
interface Producto {
    id: string;
    nombre: string;
    precio: number;
    quantity: number;
}

interface Zapato extends Producto {
    talla: number;
}

interface Carrito {
    totalPrice: number;
    productos: Producto[];
}

const carrito: Carrito = {
    totalPrice: 100,
    productos: [
        {
            id: '1',
            nombre: 'Producto 1',
            precio: 100,
            quantity: 1
        }
    ]
};
```

- **Interfaces**: Son una forma de definir la estructura de un objeto. Aquí, `Producto` define las propiedades básicas de un producto.
- **Herencia de interfaces**: La interfaz `Zapato` extiende `Producto` y añade una propiedad adicional (`talla`).
- **Uso**: La interfaz `Carrito` define la estructura de un carrito de compras, que incluye un precio total y una lista de productos.


## **Intersection de interfaces**
```typescript
// Opción 1
interface CarritoOps {
    add: (producto: Producto) => void;
    remove: (id: number) => void;
    clear: () => void;
}

// Opción 2
interface CarritoOps {
    add(producto: Producto): void;
    remove(id: number): void;
    clear(): void;
}
```

- **Intersection de interfaces**: Permite combinar múltiples interfaces en una sola. Aquí, `CarritoOps` define métodos para manipular un carrito de compras.
- **Diferencia entre opciones**: Ambas opciones son equivalentes, pero la segunda es más común para definir métodos en interfaces.


## **Interfaces vs Types**
- **Interfaces**: Son ideales para definir la forma de objetos y pueden extenderse o implementarse en clases.
- **Types**: Son más flexibles y pueden definir uniones, intersecciones, tipos primitivos, etc.
- **¿Cuándo usarlas?**:
  - Usa **interfaces** para definir la estructura de objetos o para herencia.
  - Usa **types** para uniones, intersecciones o tipos más complejos.


## **Datos primitivos**
- **Datos primitivos**: Son los tipos básicos en TypeScript, como:
  - `string`: Cadenas de texto.
  - `number`: Números (enteros o decimales).
  - `boolean`: Valores `true` o `false`.
  - `null` y `undefined`: Valores nulos o indefinidos.
  - `symbol`: Valores únicos e inmutables.

## **Tipado de Clases**
En TypeScript, las clases pueden tener propiedades y métodos con tipos definidos. Esto permite asegurar que los datos y comportamientos de la clase sean consistentes.

```typescript
class Animal {
    nombre: string;
    edad: number;

    constructor(nombre: string, edad: number) {
        this.nombre = nombre;
        this.edad = edad;
    }

    hacerSonido(): void {
        console.log("Sonido genérico");
    }
}
```

## **Propiedades: `private`, `public`, `protected`**
- **`public`**: Accesible desde cualquier lugar (por defecto).
- **`private`**: Solo accesible dentro de la clase.
- **`protected`**: Accesible dentro de la clase y sus subclases.

```typescript
class Persona {
    public nombre: string;
    private edad: number;
    protected id: string;

    constructor(nombre: string, edad: number, id: string) {
        this.nombre = nombre;
        this.edad = edad;
        this.id = id;
    }
}
```


## **Clases e Interfaces en TypeScript**
- **Clases**: Son plantillas para crear objetos con propiedades y métodos.
- **Interfaces**: Definen la forma de un objeto, pero no implementan comportamiento.

```typescript
interface SerVivo {
    respirar(): void;
}

class Humano implements SerVivo {
    respirar() {
        console.log("Respirando...");
    }
}
```


## **Extensión `.d.ts`**
Los archivos `.d.ts` son archivos de declaración de TypeScript que contienen definiciones de tipos para código JavaScript existente. Se usan para agregar tipado a librerías que no están escritas en TypeScript.

```typescript
// ejemplo.d.ts
declare module "mi-libreria" {
    export function saludar(nombre: string): void;
}
```


## **Tipos Genéricos**
Los tipos genéricos permiten crear componentes que funcionan con múltiples tipos sin perder la seguridad de tipos.

```typescript
function identidad<T>(valor: T): T {
    return valor;
}

let numero = identidad<number>(42); // T es number
let texto = identidad<string>("Hola"); // T es string
```

## **Utility Types**
Son tipos predefinidos en TypeScript que facilitan la manipulación de tipos.

- **`Partial<T>`**: Hace todas las propiedades de `T` opcionales.
- **`Readonly<T>`**: Hace todas las propiedades de `T` de solo lectura.
- **`Pick<T, K>`**: Selecciona un subconjunto de propiedades de `T`.
- **`Omit<T, K>`**: Omite un subconjunto de propiedades de `T`.

```typescript
interface Usuario {
    id: number;
    nombre: string;
    edad: number;
}

type UsuarioParcial = Partial<Usuario>; // Todas las propiedades son opcionales
type UsuarioSoloNombre = Pick<Usuario, 'nombre'>; // Solo la propiedad 'nombre'
type UsuarioSinEdad = Omit<Usuario, 'edad'>; // Omite la propiedad 'edad'
```

## Resumen de conceptos aplicados:
1. **Type Aliases**: Para crear nombres personalizados para tipos.
2. **Tipos opcionales**: Con `?` para propiedades que pueden estar ausentes.
3. **`readonly`**: Para propiedades inmutables.
4. **Template Union Types**: Para patrones de cadenas.
5. **Union Types**: Para variables que pueden ser de varios tipos.
6. **Intersection Types**: Para combinar tipos.
7. **Type Indexing y `ReturnType`**: Para inferir tipos de funciones.
8. **Tuplas**: Para arreglos con longitud y tipos fijos.
9. **Enums**: Para definir colecciones de valores finitos.
10. **Aserciones de tipos**: Para verificar o afirmar el tipo de un valor.
11. **Interfaces**: Para definir la estructura de objetos.
12. **Herencia de interfaces**: Para extender interfaces existentes.
13. **Intersection de interfaces**: Para combinar múltiples interfaces.
14. **Interfaces vs Types**: Diferencias y casos de uso.
15. **Datos primitivos**: Tipos básicos en TypeScript.
16. **Tipado de clases**: Define tipos para propiedades y métodos.
17. **Propiedades**: `public`, `private`, `protected` controlan el acceso.
18. **Clases e interfaces**: Clases implementan comportamiento, interfaces definen estructura.
19. **Extensión `.d.ts`**: Para declaraciones de tipos en código JavaScript.
20. **Tipos genéricos**: Permiten reutilizar código con múltiples tipos.
21. **Utility types**: Facilitan la manipulación de tipos.


