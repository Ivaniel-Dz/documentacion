# Java

## Tipo de Datos Primitivos
![preview](https://whdeveloper.wordpress.com/wp-content/uploads/2019/01/tipos1.png)

## Datos de Objeto
- **String**: Para cadenas de texto.
- **Integer**, **Double**, **Boolean**: Envoltorios para tipos primitivos.
- **ArrayList**, **HashMap**: Estructuras de datos.
- Cualquier clase definida por el usuario.

### Ejemplo:
```java
import java.util.ArrayList;
import java.util.HashMap;

// Clase definida por el usuario
class Persona {
    String nombre;
    int edad;

    Persona(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }

    @Override
    public String toString() {
        return nombre + " (" + edad + " años)";
    }
}

public class Main {
    public static void main(String[] args) {
        // String: Cadena de texto
        String mensaje = "Hola, mundo!";

        // Integer: Envoltorio para int
        Integer numeroEntero = 42;

        // Double: Envoltorio para double
        Double numeroDecimal = 3.14;

        // Boolean: Envoltorio para boolean
        Boolean esVerdadero = true;

        // ArrayList: Estructura de datos dinámica
        ArrayList<String> lista = new ArrayList<>();
        lista.add("Manzana");
        lista.add("Banana");
        lista.add("Naranja");

        // HashMap: Estructura de datos clave-valor
        HashMap<String, Integer> inventario = new HashMap<>();
        inventario.put("Manzanas", 10);
        inventario.put("Bananas", 5);
        inventario.put("Naranjas", 8);

        // Clase definida por el usuario
        Persona persona = new Persona("Juan", 25);

        // Mostrar los datos
        System.out.println("Mensaje: " + mensaje);
        System.out.println("Número entero: " + numeroEntero);
        System.out.println("Número decimal: " + numeroDecimal);
        System.out.println("Es verdadero: " + esVerdadero);
        System.out.println("Lista de frutas: " + lista);
        System.out.println("Inventario: " + inventario);
        System.out.println("Persona: " + persona);
    }
}
```

## Almacenamiento de Datos
1. **Variable**: Una variable es un espacio en memoria que almacena un valor que puede cambiar durante la ejecución del programa. Se declara con un tipo de dato y un nombre, y su valor puede modificarse múltiples veces.

**¿Cuándo usar una variable?**
 - Cuando el valor necesita cambiar durante la ejecución del programa.

- Para almacenar datos temporales, como resultados de cálculos, entradas del usuario, etc.

**Valores que pueden ser variables:**
- Cualquier tipo de dato (primitivo u objeto) puede ser almacenado en una variable.

**Ejemplos:**
```java
int edad = 25; // Variable primitiva
String nombre = "Juan"; // Variable de tipo objeto
double precio = 19.99; // Variable primitiva
```

2. **Constantes:** Una constante es un valor que no puede cambiar después de su inicialización. En Java, las constantes se declaran usando la palabra clave ``final``. Por convención, los nombres de las constantes se escriben en mayúsculas.

**¿Cuándo usar una constante?**
- Cuando el valor no debe cambiar durante la ejecución del programa.

- Para definir valores fijos, como configuraciones, valores matemáticos (pi, gravedad), o cualquier dato que sea inmutable.

**Valores que pueden ser constantes:**
- Cualquier tipo de dato (primitivo u objeto) puede ser constante.

**Ejemplos:**
```java
final double PI = 3.1416; // Constante primitiva
final String MENSAJE = "Hola, mundo"; // Constante de tipo objeto
final int DIAS_SEMANA = 7; // Constante primitiva
```

## Métodos de la clase ``String``
| Método | Descripción | Ejemplo |
|---|---|---|
| `length()` | Devuelve la longitud de la cadena. | `String cadena = "Hola Mundo"; int longitud = cadena.length(); // longitud = 10` |
| `charAt(int index)` | Devuelve el carácter en la posición especificada. | `String cadena = "Hola Mundo"; char caracter = cadena.charAt(0); // caracter = 'H'` |
| `indexOf(String str)` | Devuelve la posición de la primera aparición de la subcadena especificada. | `String cadena = "Hola Mundo"; int indice = cadena.indexOf("Mundo"); // indice = 5` |
| `lastIndexOf(String str)` | Devuelve la posición de la última aparición de la subcadena especificada. | `String cadena = "Hola Mundo Mundo"; int indice = cadena.lastIndexOf("Mundo"); // indice = 11` |
| `concat(String str)` | Concatena la cadena especificada al final de la cadena actual. | `String cadena1 = "Hola"; String cadena2 = " Mundo"; String resultado = cadena1.concat(cadena2); // resultado = "Hola Mundo"` |
| `substring(int beginIndex)` | Devuelve una nueva cadena que es una subcadena de la cadena actual, comenzando desde el índice especificado. | `String cadena = "Hola Mundo"; String subcadena = cadena.substring(5); // subcadena = "Mundo"` |
| `substring(int beginIndex, int endIndex)` | Devuelve una nueva cadena que es una subcadena de la cadena actual, desde el índice `beginIndex` (inclusivo) hasta el índice `endIndex` (exclusivo). | `String cadena = "Hola Mundo"; String subcadena = cadena.substring(0, 4); // subcadena = "Hola"` |
| `replace(char oldChar, char newChar)` | Reemplaza todas las apariciones del carácter `oldChar` con el carácter `newChar`. | `String cadena = "Hola Mundo"; String nuevaCadena = cadena.replace('o', 'a'); // nuevaCadena = "Hala Munda"` |
| `toLowerCase()` | Convierte la cadena a minúsculas. | `String cadena = "Hola Mundo"; String minusculas = cadena.toLowerCase(); // minusculas = "hola mundo"` |
| `toUpperCase()` | Convierte la cadena a mayúsculas. | `String cadena = "Hola Mundo"; String mayusculas = cadena.toUpperCase(); // mayusculas = "HOLA MUNDO"` |
| `trim()` | Elimina los espacios en blanco al principio y al final de la cadena. | `String cadena = "   Hola Mundo   "; String cadenaSinEspacios = cadena.trim(); // cadenaSinEspacios = "Hola Mundo"` |
| `equals(Object obj)` | Compara la cadena con el objeto especificado. | `String cadena1 = "Hola"; String cadena2 = "Hola"; boolean sonIguales = cadena1.equals(cadena2); // sonIguales = true` |
| `equalsIgnoreCase(String str)` | Compara la cadena con otra cadena, ignorando las diferencias entre mayúsculas y minúsculas. | `String cadena1 = "Hola"; String cadena2 = "hola"; boolean sonIguales = cadena1.equalsIgnoreCase(cadena2); // sonIguales = true` |
| `compareTo(String str)` | Compara la cadena con otra cadena lexicográficamente. | `String cadena1 = "Hola"; String cadena2 = "Mundo"; int resultado = cadena1.compareTo(cadena2); // resultado < 0` |
| `contains(CharSequence s)` | Devuelve `true` si la cadena contiene la secuencia de caracteres especificada. | `String cadena = "Hola Mundo"; boolean contiene = cadena.contains("Mundo"); // contiene = true` |
| `startsWith(String prefix)` | Devuelve `true` si la cadena comienza con el prefijo especificado. | `String cadena = "Hola Mundo"; boolean comienzaCon = cadena.startsWith("Hola"); // comienzaCon = true` |
| `endsWith(String suffix)` | Devuelve `true` si la cadena termina con el sufijo especificado. | `String cadena = "Hola Mundo"; boolean terminaCon = cadena.endsWith("Mundo"); // terminaCon = true` |


## Operadores
- **Aritméticos:** ``+``, ``-``, ``*``, ``/``, ``%``.
- **Comparación:** ``==``, ``!=``, ``>``, ``<``, ``>=``, ``<=``.
- **Lógicos:** ``&&`` (AND), ``||`` (OR), ``!`` (NOT).

### Jerarquía de operaciones
![preview](https://recursos.pacoelchato.com/img/YBHU7L482hY4Ry7xUqLAmGk4iJPdx9oxVaGU9pGl.png)

## Estructuras de Control
Las estructuras de control permiten tomar decisiones y repetir bloques de código.

### Sentencia de condición
- **If-Else:**
```bash
int edad = 18;
if (edad >= 18) {
    System.out.println("Eres mayor de edad.");
} else {
    System.out.println("Eres menor de edad.");
}
```

- **Switch:**
```java
int dia = 3;
switch (dia) {
    case 1:
        System.out.println("Lunes");
        break;
    case 2:
        System.out.println("Martes");
        break;
    default:
        System.out.println("Día no válido");
}
```

### Bucles
- **for:**

```java
for (int i = 0; i < 5; i++) {
    System.out.println("Iteración: " + i);
}
```

- **while:**
```java
int i = 0;
while (i < 5) {
    System.out.println("Iteración: " + i);
    i++;
}
```

## Arreglo y Matrices

**Qué es un arreglo:**
Un arreglo es una estructura de datos que almacena una colección de elementos del mismo tipo. Tiene un tamaño fijo que se define al momento de su creación.


**Qué es una matriz:**
Una matriz es un arreglo de arreglos, es decir, una estructura de datos que almacena elementos en forma de tabla (filas y columnas). Puede tener dos o más dimensiones.

### Tabla de comparación
| Característica          | Arreglo                          | Matriz                          |
|-------------------------|----------------------------------|---------------------------------|
| **Dimensión**           | Unidimensional (una sola fila).  | Multidimensional (filas y columnas). |
| **Acceso**              | Un índice (ej: `arreglo[0]`).   | Dos índices (ej: `matriz[0][0]`). |
| **Uso común**           | Listas simples de elementos.    | Tablas o estructuras de datos más complejas. |

---

## Entrada y Salida de Datos
La entrada y salida de datos se refiere a cómo un programa interactúa con el usuario o con fuentes externas para recibir información (entrada) y mostrar resultados (salida).

### salida de Datos
La salida de datos se refiere a cómo el programa muestra información al usuario. En Java, la forma más común de hacerlo es utilizando la clase ``System.out``.`

- ``System.out.print()``: Muestra un mensaje sin saltar de línea.
- ``System.out.println()``: Muestra un mensaje y salta de línea al final.
- ``System.out.printf()``: Permite formatear la salida (similar a printf en C).

```java
System.out.print("Hola, ");
System.out.println("mundo!");
System.out.printf("desarrollador");
```

### Entrada de Datos
La entrada de datos se refiere a cómo el programa recibe información del usuario. En Java, la forma más común es utilizando la clase ``Scanner``, que permite leer datos desde la consola.

```java
// Importar la clase Scanner
import java.util.Scanner;

//Crear un objeto Scanner
Scanner scanner = new Scanner(System.in);

// Leer datos
System.out.print("Ingresa tu nombre: ");
String nombre = scanner.nextLine();
```

**Ejemplo:**

```java
import java.util.Scanner;

public class EntradaSalida {
    public static void main(String[] args) {
        // Crear un objeto Scanner
        Scanner scanner = new Scanner(System.in);

        // Leer datos
        System.out.print("Ingresa tu nombre: ");
        String nombre = scanner.nextLine();

        System.out.print("Ingresa tu edad: ");
        int edad = scanner.nextInt();

        System.out.print("Ingresa un número decimal: ");
        double decimal = scanner.nextDouble();

        // Mostrar los datos
        System.out.println("Nombre: " + nombre);
        System.out.println("Edad: " + edad);
        System.out.println("Número decimal: " + decimal);

        // Cerrar el Scanner
        scanner.close();
    }
}
```

### Tabla de Métodos de Entrada en ``Scanner``

| **Tipo de Dato** | **Método en `Scanner`**       | **Descripción**                                                                 | **Ejemplo de Uso**                          |
|------------------|------------------------------|---------------------------------------------------------------------------------|---------------------------------------------|
| `String`         | `nextLine()`                 | Lee una línea completa de texto (hasta el salto de línea).                      | `String nombre = scanner.nextLine();`       |
| `int`            | `nextInt()`                  | Lee un número entero.                                                           | `int edad = scanner.nextInt();`             |
| `double`         | `nextDouble()`               | Lee un número decimal.                                                          | `double precio = scanner.nextDouble();`     |
| `float`          | `nextFloat()`                | Lee un número decimal de precisión simple.                                      | `float altura = scanner.nextFloat();`       |
| `long`           | `nextLong()`                 | Lee un número entero largo.                                                     | `long numeroGrande = scanner.nextLong();`   |
| `short`          | `nextShort()`                | Lee un número entero corto.                                                     | `short numeroCorto = scanner.nextShort();`  |
| `byte`           | `nextByte()`                 | Lee un número entero de 8 bits (byte).                                          | `byte dato = scanner.nextByte();`           |
| `boolean`        | `nextBoolean()`              | Lee un valor booleano (`true` o `false`).                                       | `boolean esValido = scanner.nextBoolean();` |
| `char`           | No hay método directo        | Para leer un carácter, se usa `next().charAt(0)`.                               | `char letra = scanner.next().charAt(0);`    |
| `String` (palabra) | `next()`                    | Lee una sola palabra (hasta el primer espacio en blanco).                       | `String palabra = scanner.next();`          |

---

## Manejo de archivos
- ``FileWriter``: Esta clase se utiliza para escribir caracteres en un archivo. Recibe la ruta del archivo como argumento en su constructor.

- ``PrintWriter``: Esta clase proporciona métodos para escribir datos formateados en un archivo. Utiliza un objeto FileWriter para escribir los datos.

### Crear y escribir documentos
```java
public class Main {
    public static void main(String[] args) throws IOException {

        FileWriter archivo = null; // Declaración de variable FileWriter para escribir en el archivo
        PrintWriter escritor = null; // Declaración de variable PrintWriter para escribir datos formateados en el archivo

        try {
            // Crea el archivo en la ruta especificada
            archivo = new FileWriter("C:\\Users\\Ivan\\Documents\\Project-Java\\escribirArchivos\\src\\file\\texto.txt");
            // Declara que se va a agregar contenido al archivo
            escritor = new PrintWriter(archivo);

            // Agrega texto al archivo
            escritor.println("Titulo del texto"); // Escribe "Título del texto" seguido de un salto de línea
            escritor.print("Cuerpo del texto"); // Escribe "Cuerpo del texto" sin salto de línea

        } catch (Exception e) { // Captura cualquier excepción que ocurra durante la creación o escritura del archivo
            System.out.println("Error: " + e.getMessage()); // Imprime un mensaje de error con la descripción de la excepción
        } finally {
            // Cierra el archivo en el bloque finally para asegurar que se cierre incluso si ocurre una excepción
            System.out.println("Archivo de texto Creado."); // Imprime un mensaje indicando que el archivo se ha creado
            if (archivo != null) { // Verifica si el archivo se abrió correctamente antes de cerrarlo
                archivo.close(); // Cierra el archivo
            }
        }
    }
}
```

### Crear, Editar, Eliminar Archivos y Documentos
```java
import java.io.File; // Importa la clase File para trabajar con archivos y directorios

public class Main {
    public static void main(String[] args) {

        // Crea un objeto File representando el archivo "prueba.txt"
        File archivo1 = new File("C:\\Users\\Ivan\\Documents\\Project-Java\\manejoArchivos\\src\\file\\prueba.txt");

        // Imprime información sobre el archivo
        System.out.println("Existe: " + archivo1.exists()); // Verifica si el archivo existe
        System.out.println("¿Se puede leer?: " + archivo1.canRead()); // Verifica si el archivo se puede leer
        System.out.println("¿Se puede escriber?: " + archivo1.canWrite()); // Verifica si el archivo se puede escribir

        // Crear un directorio o carpeta
        File archivo2 = new File("C:\\Users\\Ivan\\Documents\\Project-Java\\manejoArchivos\\src\\file\\carpetaCreada");
        System.out.println(archivo2.mkdir()); // Intenta crear el directorio y muestra el resultado (true si se creó, false si no)

        // Crear subdirectorios o subcarpetas anidadas
        File archivo3 = new File("C:\\Users\\Ivan\\Documents\\Project-Java\\manejoArchivos\\src\\file\\carpeta1\\carpeta2\\carpeta3");
        System.out.println(archivo3.mkdirs()); // Intenta crear los directorios anidados y muestra el resultado (true si se crearon, false si no)

        // Renombrar archivo
        // Renombra "prueba.txt" a "texto.txt"
        System.out.println(archivo1.renameTo(new File("C:\\Users\\Ivan\\Documents\\Project-Java\\manejoArchivos\\src\\file\\texto.txt"))); // Intenta renombrar y muestra el resultado

        // Eliminar archivo
        System.out.println(archivo1.delete()); // Intenta eliminar "texto.txt" (si existe) y muestra el resultado
    }
}
```

## programación Orientado a Objeto (POO)
Aquí tienes una explicación corta con ejemplos súper breves:  

### **Clase**  
**Definición:** Es un modelo o plantilla para crear objetos.  
**Ejemplo:**  
```java
class Animal {
    String nombre;
}
```

---

### **Clase Abstracta**  
**Definición:** Una clase que no se puede instanciar y puede tener métodos abstractos (sin implementación).  
**Ejemplo:**  
```java
abstract class Animal {
    abstract void hacerSonido();
}
```

---

### **Métodos**  
**Definición:** Son funciones dentro de una clase que definen su comportamiento.  
**Ejemplo:**  
```java
class Animal {
    void hacerSonido() {
        System.out.println("Hace un sonido");
    }
}
```

---

### **Objetos**  
**Definición:** Instancias de una clase.  
**Ejemplo:**  
```java
Animal perro = new Animal();
```

---

### **5. Constructor**  
**Definición:** Método especial que se ejecuta al crear un objeto.  
**Ejemplo:**  
```java
class Persona {
    String nombre;
    
    Persona(String nombre) { 
        this.nombre = nombre; 
    }
}
```

---

### **Sobrecarga de Métodos**  
**Definición:** Crear varios métodos con el mismo nombre pero diferente cantidad o tipo de parámetros.  
**Ejemplo:**  
```java
class Calculadora {
    int suma(int a, int b) { return a + b; }
    double suma(double a, double b) { return a + b; }
}
```

---

### **Herencia: Superclase y Subclase**  
**Definición:** La subclase hereda atributos y métodos de la superclase.  
**Ejemplo:**  
```java
class Animal {  // Superclase
    void hacerSonido() { System.out.println("Hace un sonido"); }
}

class Perro extends Animal {  // Subclase
    void hacerSonido() { System.out.println("Guau Guau"); }
}
```

### **Interfaz**  
**Definición:** Una interfaz es una estructura que define un conjunto de métodos que una clase debe implementar, sin definir su implementación.  

**Ejemplo:**  
```java
interface Volador {
    void volar();
}

class Pajaro implements Volador {
    public void volar() {
        System.out.println("El pájaro vuela");
    }
}
```
💡 *La clase `Pajaro` implementa la interfaz `Volador`, obligándola a definir el método `volar()`.*  

---

### **Orden entre Clase, Clase Abstracta e Interfaz**  
📌 **Orden de general a específico:**  

🔹 **Interfaz** → Define solo métodos sin implementación (contrato).  
🔹 **Clase Abstracta** → Puede tener métodos abstractos y concretos.  
🔹 **Clase Concreta** → Implementa todo y se puede instanciar.  

📌 **Ejemplo con orden:**  
```java
interface Volador { 
    void volar(); 
}  

abstract class Animal {  
    abstract void hacerSonido();  
}  

class Pajaro extends Animal implements Volador {  
    public void hacerSonido() { System.out.println("Pío pío"); }  
    public void volar() { System.out.println("El pájaro vuela"); }  
}
```
💡 *Primero definimos una interfaz, luego una clase abstracta y, por último, una clase concreta que combina ambas.*  

| Característica        | Clases Abstractas | Interfaces |
|----------------------|-----------------|------------|
| **Definición**       | Son clases que pueden contener métodos abstractos (sin implementación) y métodos concretos (con implementación). | Son estructuras que solo pueden contener métodos abstractos y constantes (en algunos lenguajes modernos, pueden incluir métodos por defecto). |
| **Métodos con implementación** | Puede contener métodos con implementación. | En general, no contienen métodos con implementación (excepto en algunos lenguajes modernos como Java y C#). |
| **Herencia múltiple** | No se puede heredar de más de una clase abstracta. | Se pueden implementar múltiples interfaces en una clase. |
| **Uso principal** | Se utiliza para definir una jerarquía de clases con comportamiento común. | Se usa para definir un contrato que otras clases deben seguir. |
| **Constructores** | Puede tener constructores. | No puede tener constructores. |
| **Modificadores de acceso** | Puede tener métodos y atributos con cualquier modificador de acceso (public, protected, private). | Todos los métodos son públicos por defecto y no pueden tener otros modificadores de acceso. |
| **Atributos/Propiedades** | Puede tener atributos con estado (variables de instancia). | No puede tener atributos con estado; solo constantes (en algunos lenguajes). |
| **Extensibilidad** | Se extiende mediante herencia (`extends` en Java, `:` en C#). | Se implementa con (`implements` en Java, `:` en C#). |
| **Ejemplo de uso** | Plantilla base para clases relacionadas, como `Animal` con métodos `mover()` y `hacerSonido()`. | Definir comportamiento común sin relación directa entre clases, como `Serializable` o `Comparable`. |
  
### **Abstracción**  
**Definición:** Ocultar detalles innecesarios y mostrar solo lo esencial.  
**Ejemplo:**  
```java
abstract class Animal {
    abstract void hacerSonido();
}

class Perro extends Animal {
    void hacerSonido() {
        System.out.println("Guau Guau");
    }
}
```
💡 *Solo mostramos el método esencial `hacerSonido()`, sin detallar su implementación en `Animal`.*  

---

### **Encapsulamiento**  
**Definición:** Restringir el acceso a los datos y exponer solo lo necesario mediante métodos.  
**Ejemplo:**  
```java
class Persona {
    private String nombre;

    public void setNombre(String nombre) { this.nombre = nombre; }
    public String getNombre() { return nombre; }
}
```
💡 *La variable `nombre` está protegida y solo puede modificarse mediante `setNombre()` y `getNombre()`.*  

---

### **Polimorfismo**  
**Definición:** Un mismo método se comporta de manera diferente según el objeto.  
**Ejemplo:**  
```java
class Animal {
    void hacerSonido() { System.out.println("Sonido genérico"); }
}

class Gato extends Animal {
    void hacerSonido() { System.out.println("Miau"); }
}
```
💡 *El método `hacerSonido()` se comporta diferente en `Gato` sin cambiar su nombre.*  

## Métodos de clase Stream
Aquí tienes una tabla que resume las funciones de **Streams** en Java, incluyendo ejemplos de uso para cada una de las operaciones mencionadas:

---

### **Tabla de Funciones de Streams**

| **Función**       | **Descripción**                                                                 | **Ejemplo de Uso**                                                                 |
|--------------------|---------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|
| **`peek()`**      | Permite realizar una acción (como imprimir) sin modificar el stream.            | `stream.peek(str -> System.out.println("Contenido: " + str))`                     |
| **`filter()`**    | Filtra elementos basados en una condición.                                      | `stream.filter(str -> str.contains("a"))`                                         |
| **`dropWhile()`** | Omite elementos mientras se cumpla una condición, luego deja pasar el resto.    | `stream.dropWhile(str -> str.startsWith("A"))`                                    |
| **`takeWhile()`** | Toma elementos mientras se cumpla una condición, luego omite el resto.          | `stream.takeWhile(str -> str.startsWith("A"))`                                    |
| **`skip()`**      | Omite los primeros `n` elementos del stream.                                    | `stream.skip(3)`                                                                  |
| **`limit()`**     | Limita el stream a los primeros `n` elementos.                                  | `stream.limit(4)`                                                                 |
| **`sorted()`**    | Ordena los elementos del stream (orden natural o con un comparador).            | `stream.sorted()`                                                                 |
| **`distinct()`**  | Elimina elementos duplicados del stream.                                        | `stream.distinct()`                                                               |
| **`map()`**       | Transforma cada elemento del stream usando una función.                         | `stream.map(str -> str.toUpperCase())`                                            |
| **`flatMap()`**   | Aplana un stream de colecciones en un solo stream.                              | `stream.flatMap(list -> list.stream())`                                           |
| **`forEach()`**   | Ejecuta una acción para cada elemento del stream.                               | `stream.forEach(str -> System.out.println(str))`                                  |
| **`count()`**     | Cuenta el número de elementos en el stream.                                     | `long count = stream.count()`                                                     |
| **`collect()`**   | Convierte el stream en una colección o estructura de datos.                     | `List<String> lista = stream.collect(Collectors.toList())`                        |
| **`anyMatch()`**  | Verifica si algún elemento cumple con una condición.                            | `boolean result = stream.anyMatch(str -> str.startsWith("A"))`                    |
| **`allMatch()`**  | Verifica si todos los elementos cumplen con una condición.                      | `boolean result = stream.allMatch(str -> str.length() > 3)`                       |
| **`noneMatch()`** | Verifica si ningún elemento cumple con una condición.                           | `boolean result = stream.noneMatch(str -> str.isEmpty())`                         |
| **`findFirst()`** | Obtiene el primer elemento del stream (si existe).                              | `Optional<String> first = stream.findFirst()`                                     |
| **`findAny()`**   | Obtiene cualquier elemento del stream (útil en streams paralelos).              | `Optional<String> any = stream.findAny()`                                         |
| **`reduce()`**    | Combina los elementos del stream en un solo valor (por ejemplo, suma o cadena). | `Optional<String> result = stream.reduce((str1, str2) -> str1 + "-" + str2)`      |

---

### **Ejemplos de Uso**
```java
import java.util.Arrays;
import java.util.Comparator;

public class Main {
    public static void main(String[] args) {

        // Crea una lista inmutable de cadenas (String) que representan los continentes.
        var continentes = Arrays.asList("America", "Europa", "Asia", "Oceania", "Africa");

        // Convierte la lista en un flujo (Stream) para realizar operaciones funcionales.
        continentes.stream()
                // Ordena el flujo de cadenas por la longitud de cada cadena, de menor a mayor.
                // Comparator.comparingInt(String::length) crea un comparador que compara las longitudes de las cadenas.
                .sorted(Comparator.comparingInt(String::length))
                // Itera sobre cada cadena ordenada del flujo y la imprime en la consola.
                .forEach(System.out::println); //Iterar la lista
    }
}
```

## Manejo de Errores
``Try``, ``Catch`` y ``Finally`` son bloques de código que permiten controlar y gestionar excepciones (errores) que pueden ocurrir durante la ejecución de un programa.

- **Try**: Este bloque contiene el código que se va a ejecutar y que podría generar una excepción.

- **Catch**: Este bloque se encarga de capturar y manejar la excepción que se haya producido en el bloque try. Se especifica el tipo de excepción que se va a capturar.

- **Finally**: Este bloque contiene código que se ejecuta siempre, independientemente de si se produce una excepción o no. Se utiliza para realizar tareas de limpieza o liberación de recursos.

Los errores personalizados son excepciones definidas por el usuario para representar situaciones específicas de error en su programa. Permiten tener un control más preciso sobre el manejo de errores y proporcionar mensajes de error más descriptivos.

### Ejemplo:
```java
public class Main {
    public static void main(String[] args) {
        try {
            // Código que puede lanzar una excepción
            int resultado = dividir(10, 0);
            System.out.println("Resultado: " + resultado);
        } catch (ArithmeticException e) {
            // Manejo de la excepción ArithmeticException (división por cero)
            System.err.println("Error: División por cero");
        } catch (MiExcepcionPersonalizada e) {
            // Manejo de una excepción personalizada
            System.err.println("Error personalizado: " + e.getMessage());
        } finally {
            // Código que se ejecuta siempre
            System.out.println("Bloque finally");
        }
    }

    // Método que puede lanzar una excepción
    public static int dividir(int numerador, int denominador) {
        if (denominador == 0) {
            throw new MiExcepcionPersonalizada("No se puede dividir por cero");
        }
        return numerador / denominador;
    }
}

// Clase para crear una excepción personalizada
class MiExcepcionPersonalizada extends RuntimeException {
    public MiExcepcionPersonalizada(String mensaje) {
        super(mensaje);
    }
}
```

## Expresiones LAMBDA
Una expresión lambda es una función anónima, es decir, una función que no tiene nombre. Se utiliza para escribir código más conciso y expresivo, especialmente cuando se trabaja con interfaces funcionales (interfaces con un solo método abstracto).

### Ejemplo:
```java
// Interfaz funcional con un solo método abstracto
interface Operacion {
    int operar(int a, int b);
}

public class Main {
    public static void main(String[] args) {

        // Expresión lambda para sumar dos números
        Operacion suma = (a, b) -> { return a + b; };

        // Expresión lambda para restar dos números
        Operacion resta = (a, b) -> a - b; // Se puede omitir 'return' y las llaves si es una sola expresión

        // Usar las expresiones lambda
        int resultadoSuma = suma.operar(5, 3); // resultadoSuma = 8
        int resultadoResta = resta.operar(10, 4); // resultadoResta = 6

        System.out.println("Suma: " + resultadoSuma);
        System.out.println("Resta: " + resultadoResta);
    }
}
```

## **Collections**

| Colección | Descripción | Características | Ejemplo |
|---|---|---|---|
| **List** | Colección ordenada de elementos. | Permite duplicados. Los elementos se acceden por su índice. | `ArrayList`, `LinkedList`, `Vector` |
| **Set** | Colección de elementos únicos. | No permite duplicados. Los elementos no tienen un orden específico. | `HashSet`, `TreeSet`, `LinkedHashSet` |
| **Map** | Colección de pares clave-valor. | Cada clave es única. Los valores se acceden por su clave. | `HashMap`, `TreeMap`, `LinkedHashMap` |
| **Queue** | Colección que sigue el principio FIFO (First-In, First-Out). | Los elementos se añaden al final y se retiran del principio. | `LinkedList`, `PriorityQueue`, `ArrayDeque` |

### Ejemplos de uso

- **List<>**

```java
List<String> nombres = new ArrayList<>();
nombres.add("Juan");
nombres.add("María");
nombres.add("Juan"); // Se permite duplicado
System.out.println(nombres); // Imprime: [Juan, María, Juan]
```

- **Set<>**

```java
Set<String> nombres = new HashSet<>();
nombres.add("Juan");
nombres.add("María");
nombres.add("Juan"); // No se añade, ya existe
System.out.println(nombres); // Imprime: [María, Juan] (el orden puede variar)
```

- **Map<>**

```java
Map<String, Integer> edades = new HashMap<>();
edades.put("Juan", 30);
edades.put("María", 25);
System.out.println(edades.get("Juan")); // Imprime: 30
```

- **Queue<>**

```java
Queue<String> tareas = new LinkedList<>();
tareas.offer("Tarea 1");
tareas.offer("Tarea 2");
System.out.println(tareas.poll()); // Imprime: Tarea 1 (se retira)
```

### **Métodos de Collections**    
Son estructuras que permiten almacenar, manipular y gestionar grupos de objetos de manera flexible y eficiente. Se encuentran dentro del paquete `java.util` e incluyen listas, conjuntos y mapas.  

| **Método**            | **Descripción** |
|----------------------|----------------|
| `add(E e)` | Agrega un elemento a la colección. |
| `remove(Object o)` | Elimina un elemento de la colección. |
| `size()` | Devuelve el número de elementos en la colección. |
| `contains(Object o)` | Verifica si la colección contiene un elemento específico. |
| `isEmpty()` | Retorna `true` si la colección está vacía. |
| `clear()` | Elimina todos los elementos de la colección. |
| `iterator()` | Retorna un iterador para recorrer la colección. |

---

- **Ejemplo:**
```java
import java.util.ArrayList;
import java.util.List;

public class EjemploCollections {
    public static void main(String[] args) {
        // Crear una lista de tipo String
        List<String> nombres = new ArrayList<>();

        // Agregar elementos a la lista
        nombres.add("Juan");
        nombres.add("María");
        nombres.add("Pedro");

        // Imprimir la lista
        System.out.println("Lista de nombres: " + nombres);

        // Obtener el tamaño de la lista
        int tamaño = nombres.size();
        System.out.println("Tamaño de la lista: " + tamaño);

        // Acceder a un elemento de la lista
        String primerNombre = nombres.get(0);
        System.out.println("Primer nombre: " + primerNombre);

        // Eliminar un elemento de la lista
        nombres.remove(1);
        System.out.println("Lista después de eliminar un elemento: " + nombres);

        // Verificar si la lista contiene un elemento
        boolean contiene = nombres.contains("Juan");
        System.out.println("¿La lista contiene a Juan? " + contiene);
    }
}
```

### Consideraciones adicionales

*   La elección de la colección adecuada depende de los requisitos específicos de cada caso.
*   Es importante conocer las características de cada colección para optimizar el rendimiento del programa.
*   Java ofrece muchas otras colecciones especializadas para diferentes situaciones.


## **Iterador**  
Es una interfaz en Java utilizada para recorrer elementos de una colección de manera segura sin necesidad de acceder directamente a su estructura interna.  

| **Método**            | **Descripción** |
|----------------------|----------------|
| `hasNext()` | Retorna `true` si hay más elementos en la colección. |
| `next()` | Devuelve el siguiente elemento en la iteración. |
| `remove()` | Elimina el último elemento retornado por `next()`. |

💡 *El iterador es útil para recorrer listas, conjuntos y otras estructuras sin causar errores de modificación concurrente.*  

### Ejemplo
```java
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

public class EjemploIterador {
    public static void main(String[] args) {
        // Crear una lista de tipo Integer
        List<Integer> numeros = new ArrayList<>();

        // Agregar elementos a la lista
        numeros.add(1);
        numeros.add(2);
        numeros.add(3);

        // Obtener un iterador para la lista
        Iterator<Integer> iterador = numeros.iterator();

        // Recorrer la lista con el iterador
        while (iterador.hasNext()) {
            int numero = iterador.next();
            System.out.println("Número: " + numero);
        }

        // Otra forma de recorrer la lista con un bucle for-each
        for (int numero : numeros) {
            System.out.println("Número (for-each): " + numero);
        }
    }
}
```

## **Hilos y Concurrencia**  
Un **hilo (thread)** es una unidad de ejecución dentro de un programa. La **concurrencia** permite ejecutar múltiples hilos al mismo tiempo para realizar tareas en paralelo.  

**Ejemplo de Hilo en Java:**  
```java
class MiHilo extends Thread {
    public void run() {
        System.out.println("Hilo en ejecución...");
    }
}

public class Main {
    public static void main(String[] args) {
        MiHilo hilo = new MiHilo();
        hilo.start();  // Inicia el hilo
    }
}
```
💡 *`start()` ejecuta el método `run()` en un hilo separado.*  

---

## **`synchronized` en Java**  
La palabra clave **`synchronized`** evita problemas de acceso simultáneo a un recurso compartido en entornos con múltiples hilos.  

**Ejemplo de `synchronized`:**  
```java
class Contador {
    private int cuenta = 0;

    public synchronized void incrementar() {
        cuenta++;
    }
}
```
💡 *`synchronized` evita que dos hilos modifiquen `cuenta` al mismo tiempo, previniendo condiciones de carrera.*  
