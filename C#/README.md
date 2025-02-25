## C# (C Sharp)
>**[Documentación](https://learn.microsoft.com/es-es/dotnet/csharp/tour-of-csharp/)**
## Mostrar mensaje por pantalla
```cs
Console.WriteLine("Hola mi primer codigo"+"\n"+"C Shart");
```
## Ingresar valor por teclado
```cs
Console.WriteLine("Ingrese el primer numero:");
x = int.Parse(Console.ReadLine());
```

## Tipos de Datos y Operadores
### Tipos de datos básicos
- int
- String
- float
- double
- bool
- boolean

```cs
// Ejemplo
int a = 2;
int b = 5;
int c = a + b;
String texto = "El resultado es: ";

Console.WriteLine(texto + c); // + concatena los variables y también sirve para sumar
```
> **Variables:** Las variables actúan como contenedores de datos que pueden cambiar durante la ejecución de un programa.

> **Constantes:** Las constantes son valores fijos que no cambian una vez definido y se utilizan para valores que no deben modificarse durante la ejecución del programa. _Ejemplo: Números de Dias de una semana, siempre sera 7._

### var
> ``var`` es una palabra clave en C# que permite declarar variables de manera implícita. El tipo de la variable se infiere del valor que se le asigna.
```cs
var numero = 10;  // El compilador infiere que 'numero' es de tipo int
var texto = "Hola";  // El compilador infiere que 'texto' es de tipo string
```
**Cuándo utilizar ``var``:**
- Cuando el tipo es obvio a partir del contexto (como en el caso de literales o expresiones sencillas).
- En consultas LINQ u otras situaciones en las que el tipo exacto es complejo o largo de escribir.

**No utilizar ``var``:**
- Cuando usar var hace que el código sea menos claro o el tipo no sea inmediatamente obvio.


### Operadores aritméticos, lógicos y relacionales
- Operadores aritméticos:
```cs
int suma = 3 + 5;
int resta = 5 - 1;
int mult = 2 * 2;
float div = 10 / 2;
float residuo = 10 % 2;

Console.WriteLine("Suma: "+ suma);
Console.WriteLine("Resta: "+ resta);
Console.WriteLine("Multiplicación: " + mult);
Console.WriteLine("Division: " + div);
Console.WriteLine("Residuo: " + residuo);
```

- Operadores de Incrementos y Decrementos
```cs
a++; // Incrementos
a--; // Decrementos
a+=2; // Incrementa en 2
a-=2; // Decrementa en 2
```

- Operadores lógicos:
    - ``&`` (AND)
    - ``&&`` (AND de cortocircuito)
    - ``|`` (OR)
    - ``||`` (AND de cortocircuito)
    - ``^`` (XOR)

- Operadores relacionales:
    - ``<`` (Menor que)
    - ``<=`` (Menor o igual que)
    - ``>`` (mayor que)
    - ``>=`` (Mayor o igual que)
    - ``==`` (Igual que)
    - ``!=`` (Distinto que)

### Métodos de string
> La clase ``string`` en C# ofrece diversos métodos para manipular y trabajar con cadenas de texto.
```cs
string frase = "Hola Mundo";

// Obtener longitud
int longitud = frase.Length;  // 10

// Convertir a mayúsculas
string mayusculas = frase.ToUpper();  // "HOLA MUNDO"

// Reemplazar texto
string reemplazo = frase.Replace("Mundo", "C#");  // "Hola C#"

// Dividir cadena
string[] palabras = frase.Split(' ');  // ["Hola", "Mundo"]

// Substring
string subcadena = frase.Substring(5, 5);  // "Mundo"
```
**Métodos comunes:**
- ``Length``: Devuelve la longitud de la cadena.
- ``ToUpper()`` y ``ToLower()``: Convierte la cadena a mayúsculas o minúsculas.
- ``Replace()``: Reemplaza una parte de la cadena con otra.
- ``Split()``: Divide la cadena en un array según un delimitador.
- ``Substring()``: Extrae una subcadena.

## Casting
> El casting en C# se refiere a convertir un tipo de dato en otro. Puede ser explícito o implícito.
- Casting implícito: Sucede automáticamente cuando no hay pérdida de datos.
```cs
int entero = 10;
double doble = entero;  // Conversión implícita de int a double
```

- Casting explícito: Se utiliza cuando puede haber pérdida de datos o la conversión no es segura.
```cs
double numero = 9.8;
int entero = (int)numero;  // Conversión explícita de double a int, pierde los decimales (entero será 9)
```

- También está el casting de referencia, donde se convierte un tipo base a un tipo derivado:
```cs
object obj = "Hola Mundo";
string str = (string)obj;  // Casting explícito
```
## Estructuras de Control
### Condicionales (if, else, else if)
```cs
int x, y;

Console.WriteLine("Ingrese el primer numero:");
x = int.Parse(Console.ReadLine()); // Ingresa por teclado el valor
Console.WriteLine("Ingrese el segundo numero:");
y = int.Parse(Console.ReadLine()); // Ingresa por teclado el valor

if (x >= y)
{
    Console.WriteLine(x + " Es mayor");
}
else
{
    Console.WriteLine(x + " Es menor");
}
```
### Switch
```cs

int dia;
Console.WriteLine("Ingrese un numero para saber el dia:");
dia = int.Parse(Console.ReadLine());

switch (dia)
{
    case 1:
        Console.WriteLine("Lunes");
        break;
    case 2:
        Console.WriteLine("Martes");
        break;
    case 3:
        Console.WriteLine("Miercoles");
        break;
    case 4:
        Console.WriteLine("Jueves");
        break;
    case 5:
        Console.WriteLine("Viernes");
        break;
    case 6:
        Console.WriteLine("Sabado");
        break;
    case 7:
        Console.WriteLine("Domingo");
        break;
    default:
        Console.WriteLine("Esta semana no existe");
        break;
}
```
### Bucles (for, while, do-while)
```cs
int num;
Console.WriteLine("Ingrese la tabla de multiplicar: ");
num = int.Parse(Console.ReadLine());

// Condicional FOR
for (int i = 1; i <= 12; i++)
{ 
    Console.WriteLine( num +"X"+ i +"="+ num*i);
}
```
```cs
// Condicional WHILE
int x = 1;
while (x <= 12)
{
    Console.WriteLine(x);
    x++;
}
```
```cs
// Condicional Do-While
int x = 1;
do
{
    Console.WriteLine(x);
    x++;
}
while (x <= 12);
```

### Operadores ternarios
```cs
int edad = 21;
Console.WriteLine(edad > 18 ? "Es mayor de edad" : "Es menor de edad");
```

## Programación Orientada a Objetos (POO)
### Clases y objetos
```cs
class Geometria
{
    static void Main()
    {
        FigurasGeometricas figuras = new FigurasGeometricas();
        double circulo = figuras.AreaCirculo(12);
        double cuadrado = figuras.AreaCuadrado(12);

        Console.WriteLine("Area del circulo es: "+ circulo);
        Console.WriteLine("Area del cuadrado es: "+ cuadrado);
    }

    class FigurasGeometricas
    {
        double pi = Math.PI;
        double lado;

        public double AreaCirculo(double radio)
        {
            double area = pi * radio * radio;
            return area;
        }

        public double AreaCuadrado(double lado)
        {
            double area = lado * lado;
            return area;
        }
    }
}
```

### Definición de métodos
> Un método es un bloque de código que contiene una serie de instrucciones. Un programa hace que se ejecuten las instrucciones al llamar al método y especificando los argumentos de método necesarios. En C#, todas las instrucciones ejecutadas se realizan en el contexto de un método.

### Métodos
```cs
class Operaciones
{
    static void Main()
    {
        Operaciones operaciones = new Operaciones();
        operaciones.Suma();
        operaciones.MostrarResta();
        operaciones.MostrarMult();
        operaciones.MostrarDiv();
    }

    // Método que no retorna un valor y sin parámetro
    public void Suma()
    {
        int suma = 2 + 3;
        Console.WriteLine("Suma: "+suma);
    }

    // Metodo que retorna un valor pero sin parámetro
    public int Resta()
    {
       int resta = 10 - 5 ;
        return resta; //Valor de retorno
    }

    public void MostrarResta()
    {   
        int resta = Resta();
        Console.WriteLine("Resta: "+resta);
    }

    //Metodo que no retorna valor pero tiene parámetro
    public void Multiplicacion(int a, int b)
    {
        Console.WriteLine("Multiplicación: "+ a * b);
    }

    public void MostrarMult()
    {
        int nun1 = 3;
        int nun2 = 5;
        Multiplicacion(nun1, nun2); //(argumento)
    }

    //Método que retorna valor y tiene parámetros
    public double Division(double a, double b)
    {
        double div = a / b;
        return div; //Valor de retorno
    }

    public  void MostrarDiv()
    {
        double num1 = 3;
        double num2 = 5;
        double div = Division(num1, num2);
        Console.WriteLine("Division: "+div);
    }
}
```

### Herencia
> Las hererencias en C# se declaran con ```:``` 
![preview](./preview/herencia.png)

### Sobrecarga
> Sobrecarga: creación de varios métodos con el mismo nombre pero con diferentes definiciones o parámetros. También se puede realizar sobrecargas a Constructores
```cs
namespace POO
{
    public class Leon : Carnivoro
    {
        // Constructor con valor por defecto
        public Leon() { //Constructor padre
            if (this.Nombre == null || !this.Nombre.Equals(""))
            {
                this.Nombre = "Leon";
            }
            Console.WriteLine("Carga de datos");
        }

        // Constructor con valor por parametro
        public Leon(string Nombre) : this() //this() permite ejecutar primero el constuctor padre
        {
            this.Nombre = Nombre;
        }

        public string ColorCabello { get; set; }

        private int velocidadDefecto = 4;
        // Metodo Correr con valor por defecto
        public void Correr () 
        {
            Console.WriteLine(velocidadDefecto+"Km/hr");
        }

        // Metodo Correr con parametro int
        public void Correr(int velocidad) {
            Console.WriteLine("Corriendo a "+velocidad+"Km/hr");
        }

        // Metodo Correr con parametro string
        public void Correr(string presa)
        {
            Console.WriteLine("Corriendo a cazar: " + presa);
        }
    }
}
```

### Sobrescitura 
> La sobrescritura es ocultar un método por otro que lo reemplaza, es decir define ese mismo método nuevamente.
```cs
namespace POO
{
    class Program
    {
        static void Main(string[] args)
        {
            Leon oLeon = new Leon("Simba");
            // Mostrar el valor sobrescrito
            Console.WriteLine(oLeon.GetNombre());
        }
    }
}
```

```cs
namespace POO
{
    public class Animal
    {
        public string Nombre { get; set; }

        // Sobrescitura
        public virtual string GetNombre() { 
            return Nombre;
        }
    }
}
```

```cs
namespace POO
{
    public class Leon : Carnivoro
    {
        // Sobrescitura
        public override string GetNombre()
        {
            return "Soy un león llamado: "+ Nombre;
        }
    }
}
```

### Encapsulación
> La encapsulacion esta implementada por modificadores de acceso y estos seran los encargados de definir el rango y la visibilidad de los miembros de la clase, veamos los disponibles:

- **public**: nos permitira exponer todos los miembros que definamos de esta manera, estos pueden ser tanto metodos (funciones) como propiedades (variables) dentro de las clases y las mismas podran ser accedidas desde afuera de la misma.

- **private**: permite denegar el acceso a las propiedades y metodos desde otros objetos o clases, y estos elementos solo pueden ser accedidos por miembros dentro de la misma clase, inclusive una instancia de la misma clase no podria acceder.

- **protected**: es mas utilizado para cuando tenemos clases heredadas, dado que trabaja como public para las clase hijas de la clase base y como private para las clases externas a la misma.

- **internal**: es el predeterminado cuando no informamos ninguno, este nos permite al igual que public exponer todos los metodos y propiedades de la clase dentro del mismo ensamblado (assembly), es decir que todas las clases podran tener acceso siempre y cuando esten dentro del mismo ensamblado.

- **protected internal**: es una mezcla entre el internal y el protected, porque ocultara a los miembros a las clases externas de esta pero si le permitira el acceso a las hijas de la clase base.

### Propiedades
> Permiten que una clase exponga una manera pública de obtener y establecer valores, a la vez que se oculta el código de implementación o verificación.

- **``get``**
- **``set``**

> Permiten **obtener** (``get``) o **establecer** (``set``) el valor de una variable desde fuera de la clase, manteniendo así el encapsulamiento y controlando el acceso a los datos internos de la clase.

```cs
namespace POO
{
    public class Leon : Carnivoro
    {
        private int velocidadDefecto = 4;
        public int Velocidad
        {   // Muestra e valor
            get { return velocidadDefecto; }
            // Modifica el valor
            set { 
                if(value < 0)
                    value = 1;
                velocidadDefecto = value; 
            }
        }
    }
}
```

### Polimorfismo
> El polimorfismo permite que las clases derivadas puedan sobrescribir los métodos de la clase base, permitiendo diferentes comportamientos para el mismo método.

>  El polimorfismo está íntimamente relacionado con la ``sobrecarga`` y la ``sobrescritura``.

**Hay dos tipos de polimorfismo:**
- Polimorfismo en tiempo de compilación (sobrecarga de métodos).
- Polimorfismo en tiempo de ejecución (sobrescritura de métodos).

> **Polimorfismo de Inclusion:** La habilidad para redefinir por completo el método de una superclase en una subclase.

- **Polimorfismo de Inclusion:**
```cs
//CLass Main
namespace Polimorfismo
{
    class Program
    {
        static void Main(string[] args)
        {
            Bar oBar = new Bar();
            Persona oMesero = new Mesero("Carlos");
            Persona oCantinero = new Cantinero("Hector");
            Persona oCliente = new Cliente("Maria");
            oBar.Entrar(oMesero);
            oBar.Entrar(oCantinero);
            oBar.Entrar(oCliente);
        }
    }
}
```
```cs
// CLass Persona
namespace Polimorfismo
{
     class Persona
    {
        public string Nombre { get; set; }

        public Persona(string Nombre) { this.Nombre = Nombre; }

        public virtual void Accion() { }
    }
}
```
```cs
// Class Bar
namespace Polimorfismo
{
    class Bar
    {
        List<Persona> listPersona = new List<Persona>();

        public void Entrar(Persona oPersona)
        {
            listPersona.Add(oPersona);
            oPersona.Accion();
        }
    }
}
```
```cs
// Class Mesero
namespace Polimorfismo
{
    class Mesero : Persona
    {
        public Mesero(string Nombre) : base(Nombre) {}

        public override void Accion()
        {
            Console.WriteLine("Atiende mesas");
        }

    }
}
```
```cs
// Class Cliente
namespace Polimorfismo
{
    internal class Cliente : Persona
    {
        public Cliente(string Nombre) : base(Nombre) { }

        public override void Accion()
        {
            Console.WriteLine("Tomar bebidas");
        }
    }
}
```
```cs
// Class Persona
namespace Polimorfismo
{
    class Cantinero : Persona
    {   
        public Cantinero(string Nombre) : base(Nombre) { }

           public override void Accion()
        {
            Console.WriteLine("Realiza bebitas");
        }

    }

}
```

Ejemplo de polimorfismo en tiempo de ejecución:
```cs
public class Animal
{
    public virtual void HacerSonido()
    {
        Console.WriteLine("Sonido de animal");
    }
}

public class Perro : Animal
{
    public override void HacerSonido()
    {
        Console.WriteLine("Ladrido");
    }
}

public class Gato : Animal
{
    public override void HacerSonido()
    {
        Console.WriteLine("Maullido");
    }
}

Animal animal = new Perro();
animal.HacerSonido();  // Salida: Ladrido

animal = new Gato();
animal.HacerSonido();  // Salida: Maullido
```
> **Explicación:** La clase Animal tiene un método HacerSonido(), y las clases Perro y Gato lo sobrescriben para dar un comportamiento específico. Aunque animal es del tipo Animal, en tiempo de ejecución se invoca el método sobrescrito de la clase derivada correspondiente.

### Constructores
```cs
namespace AbstractasInterfaces
{
class Program
    {
    static void Main(string[] args)
    {
        Persona oPesona1 = new Persona("Ivan", 28);
        Persona oPesona2 = new Persona("Luis", 29);

        Console.WriteLine(oPesona1.MostrarDatos());
        Console.WriteLine(oPesona2.MostrarDatos());
    }
    
    }
}
```
```cs
namespace AbstractasInterfaces
{
    internal class Persona
    {
        public string Nombre;
        public int Edad;

        // Constructor de la clase Persona
        public Persona(string name, int age) 
        {
            Nombre = name;
            Edad = age;
        }

        public string MostrarDatos()
        {
            return $"Mi nombre es '{Nombre}' tengo {Edad} años.";
        }
    }
}
```

### Clases abstractas e interfaces
>Una clase ``abstracta`` te permite compartir código entre clases relacionadas, mientras que una ``interfaz`` te ayuda a definir un contrato que múltiples clases pueden implementar.
```cs
namespace AbstractasInterfaces
{
    class Program
    {
        static void Main(string[] args)
        {

        }

        public abstract class Sale
        {
            public decimal _total;

            // Constructor
            public Sale(decimal total) => _total = total;
        }

        interface IInvoice
        {
            void Check();
        }

        interface ICancel
        {
            void Cancel();
        }

        interface ITax
        {
            public decimal Total { get; set; }
        }

        public class SingleSale : Sale, IInvoice, ICancel, ITax
        {
            private decimal _iva;
            public decimal Total 
            { 
                get {  return _total + _iva; }
                set => throw new NotImplementedException();
            }

            public SingleSale(decimal total) : base(total) { }

            public void Cancel()
            {
                throw new NotImplementedException();
            }

            public void Check()
            {
                throw new NotImplementedException();
            }
        }
    }
}
```

## Tipos Avanzados
### Enumeraciones (enum)
> Una enumeración es un tipo de datos que permite definir un conjunto de valores constantes.
```cs
enum DiasSemana { Lunes, Martes, Miercoles, Jueves, Viernes, Sabado, Domingo }

DiasSemana dia = DiasSemana.Lunes;
Console.WriteLine(dia);  // Salida: Lunes
```
> Explicación: Definimos una enumeración ``DiasSemana`` con valores predefinidos. Luego, asignamos un valor de la enumeración a la variable ``dia``.

### Estructuras (struct)
> Las estructuras (``struct``) son tipos de datos que permiten agrupar variables de diferentes tipos en un solo objeto. A diferencia de las clases, son tipos por valor.
```cs
struct Punto
{
    public int X;
    public int Y;

    public Punto(int x, int y)
    {
        X = x;
        Y = y;
    }
}

Punto punto = new Punto(10, 20);
Console.WriteLine($"Punto: ({punto.X}, {punto.Y})");
```
> Explicación: Aquí, ``Punto`` es una estructura que contiene dos campos ``X`` y ``Y``. Creamos una instancia de ``Punto`` con valores iniciales.

### Delegados y eventos
> Un delegado es un puntero a una función, y los eventos permiten notificar cuando sucede una acción específica.
```cs
public delegate void Notificar(string mensaje);
public class Publicador
{
    public event Notificar EventoNotificacion;

    public void EjecutarEvento()
    {
        EventoNotificacion?.Invoke("Evento activado!");
    }
}

Publicador pub = new Publicador();
pub.EventoNotificacion += msg => Console.WriteLine(msg);
pub.EjecutarEvento();  // Salida: Evento activado!
```
> Explicación: Definimos un delegado ``Notificar`` y un evento ``EventoNotificacion``. Luego, asociamos un método al evento y lo invocamos.

### Expresiones lambda
> Las expresiones lambda son funciones anónimas que se utilizan comúnmente con delegados y LINQ.
```cs
Func<int, int> cuadrado = x => x * x;
Console.WriteLine(cuadrado(5));  // Salida: 25
```
> Explicación: Usamos una expresión lambda ``x => x * x`` que toma un valor ``x`` y devuelve su cuadrado. La lambda se asigna a un delegado ``Func``.

## Manejo de Excepciones
### Try, catch, finally
> El bloque ``try-catch-finally`` permite manejar excepciones.
```cs
try
{
    int divisor = 0;
    int resultado = 10 / divisor;
}
catch (Exception ex)
{
    Console.WriteLine("No se puede dividir entre cero.");
}
finally
{
    Console.WriteLine("Bloque finally ejecutado.");
}
```
> Explicación: Intentamos dividir por cero, lo cual lanza una excepción ``Exception``, la cual es capturada en el bloque ``catch``. El bloque ``finally`` se ejecuta siempre, independientemente de si ocurrió una excepción.

### Throw y creación de excepciones personalizadas
> Podemos lanzar (``throw``) excepciones manualmente y también crear nuestras propias excepciones.
```cs
public class MiExcepcion : Exception
{
    public MiExcepcion(string mensaje) : base(mensaje) { }
}

public void LanzarExcepcion()
{
    throw new MiExcepcion("Esta es una excepción personalizada.");
}

try
{
    LanzarExcepcion();
}
catch (MiExcepcion ex)
{
    Console.WriteLine(ex.Message);  // Salida: Esta es una excepción personalizada.
}
```
> Explicación: Creamos una excepción personalizada ``MiExcepcion`` heredando de ``Exception``. Luego, lanzamos y capturamos esta excepción con ``throw``.

## Colecciones y Genéricos
### Arrays
> Un array es una colección de elementos del mismo tipo almacenados en ubicaciones de memoria contiguas.
```cs
int[] numeros = { 1, 2, 3, 4, 5 };

for (int i = 0; i < numeros.Length; i++)
{
    Console.WriteLine(numeros[i]);
}
```

### Métodos de Arrays
> Los arrays en C# tienen varios métodos útiles para manipular sus elementos.
```cs
int[] numeros = { 5, 2, 9, 1, 3 };

// Ordenar
Array.Sort(numeros);  // [1, 2, 3, 5, 9]

// Buscar un elemento
int indice = Array.IndexOf(numeros, 3);  // Indice del valor 3 es 2

// Invertir el array
Array.Reverse(numeros);  // [9, 5, 3, 2, 1]
```

**Métodos comunes:**
- **``Array.Sort()``:** Ordena los elementos de un array.
- **``Array.Reverse()``:** Invierte el orden de los elementos.
- **``Array.IndexOf()``:** Devuelve el índice de un elemento.
- **``Array.Copy()``:** Copia un rango de elementos de un array a otro.

### Operadores de Propagación
```cs
string[] paises1 = ["Panama", "Colombia"];
string[] paises2 = ["Peru", "Chile"];
string[] paises3 = ["España", "Italia"];

string[] country = [.. paises1, ..paises2, ..paises3];

foreach (var pais in country)
{
    Console.WriteLine(pais);
}
```

### Listas y Diccionarios
> Las listas (``List<T>``) y diccionarios (``Dictionary<TKey, TValue>``) son colecciones dinámicas.
```cs
List<int> lista = new List<int> { 1, 2, 3 };
lista.Add(4);
Console.WriteLine(lista[3]);  // Salida: 4

Dictionary<string, int> diccionario = new Dictionary<string, int>();
diccionario["edad"] = 25;
Console.WriteLine(diccionario["edad"]);  // Salida: 25
```
> Explicación: ``List<T>`` es una lista de elementos que permite agregar más elementos dinámicamente. ``Dictionary<TKey, TValue>`` almacena pares clave-valor.

### Pilas (Stack) y colas (Queue)
> Las pilas ``(Stack<T>)`` y colas ``(Queue<T>)`` son colecciones que siguen las estructuras LIFO (último en entrar, primero en salir) y FIFO (primero en entrar, primero en salir), respectivamente.
```cs
Stack<int> pila = new Stack<int>();
pila.Push(1);
pila.Push(2);
Console.WriteLine(pila.Pop());  // Salida: 2

Queue<int> cola = new Queue<int>();
cola.Enqueue(1);
cola.Enqueue(2);
Console.WriteLine(cola.Dequeue());  // Salida: 1
```
> Explicación: ``Stack<T>`` permite agregar y quitar elementos en orden LIFO, mientras que ``Queue<T> ``sigue el principio FIFO.

### Genéricos (List<T>, Dictionary<T, T>)
> Los genéricos permiten crear clases y métodos que operan en cualquier tipo de dato.
```cs
List<string> nombres = new List<string> { "Ana", "Luis" };
Dictionary<int, string> empleados = new Dictionary<int, string> { { 1, "Carlos" }, { 2, "Marta" } };
```
> Explicación: ``List<T>`` y ``Dictionary<T, T>`` son ejemplos de colecciones genéricas, donde ``T`` representa el tipo de dato que contendrán.

## LINQ (Language-Integrated Query)
> LINQ permite realizar consultas sobre colecciones.
### Sintaxis básica de LINQ
```cs
int[] numeros = { 1, 2, 3, 4, 5 };
var pares = from n in numeros
            where n % 2 == 0
            select n;

foreach (var numero in pares)
{
    Console.WriteLine(numero);  // Salida: 2, 4
}
```
> Explicación: Usamos LINQ para seleccionar números pares de un array.

### Consultas de selección, filtrado y agrupación
```cs
string[] frutas = { "Manzana", "Banana", "Cereza", "Mango" };

var filtro = frutas.Where(f => f.StartsWith("M")).Select(f => f);

foreach (var fruta in filtro)
{
    Console.WriteLine(fruta);  // Salida: Manzana, Mango
}
```
> Explicación: Filtramos las frutas que comienzan con la letra "M" utilizando ``Where()`` y ``Select()``.

### Uso de métodos como `Select()`, `Where()`, `GroupBy()`
```cs
var personas = new[]
{
    new { Nombre = "Juan", Edad = 20 },
    new { Nombre = "Ana", Edad = 25 },
    new { Nombre = "Luis", Edad = 20 }
};

var agrupadas = personas.GroupBy(p => p.Edad);

foreach (var grupo in agrupadas)
{
    Console.WriteLine($"Edad: {grupo.Key}");
    foreach (var persona in grupo)
    {
        Console.WriteLine($"Nombre: {persona.Nombre}");
    }
}
```
> Explicación: Agrupamos las personas por edad utilizando ``GroupBy()``.

## Manejo de Archivos
### Lectura y escritura en archivos
```cs
// Escritura
File.WriteAllText("archivo.txt", "Hola Mundo");

// Lectura
string contenido = File.ReadAllText("archivo.txt");
Console.WriteLine(contenido);  // Salida: Hola Mundo
```
> Explicación: Utilizamos F``ile.WriteAllText()`` para escribir en un archivo y ``File.ReadAllText()`` para leer su contenido.

### Streams (FileStream, StreamReader, StreamWriter)
```cs
// Escritura usando StreamWriter
using (StreamWriter sw = new StreamWriter("archivo.txt"))
{
    sw.WriteLine("Texto desde StreamWriter");
}

// Lectura usando StreamReader
using (StreamReader sr = new StreamReader("archivo.txt"))
{
    Console.WriteLine(sr.ReadToEnd());  // Salida: Texto desde StreamWriter
}
```
> Explicación: Usamos ``StreamWriter`` para escribir y ``StreamReader`` para leer archivos con streams.

## Conceptos Avanzados
### Tareas asíncronas (async/await)
```cs
public async Task<int> ObtenerDatosAsync()
{
    await Task.Delay(1000);  // Simula una operación asíncrona
    return 42;
}

async Task Main()
{
    int resultado = await ObtenerDatosAsync();
    Console.WriteLine(resultado);  // Salida: 42
}
```
> Explicación: Usamos ``async`` y ``await`` para realizar operaciones asíncronas, en este caso, simulando una espera de 1 segundo.

### Expresiones regulares
```cs
string texto = "Correo: ejemplo@mail.com";
string patron = @"\w+@\w+\.\w+";

bool esValido = Regex.IsMatch(texto, patron);
Console.WriteLine(esValido);  // Salida: True
```
> Explicación: Utilizamos expresiones regulares para verificar si un texto contiene un correo electrónico válido.

### Serialización de objetos
```cs
[Serializable]
public class Persona
{
    public string Nombre { get; set; }
    public int Edad { get; set; }
}

// Serialización
Persona persona = new Persona { Nombre = "Juan", Edad = 30 };
string json = JsonSerializer.Serialize(persona);
Console.WriteLine(json);  // Salida: {"Nombre":"Juan","Edad":30}

// Deserialización
Persona deserializada = JsonSerializer.Deserialize<Persona>(json);
Console.WriteLine(deserializada.Nombre);  // Salida: Juan
```
> Explicación: Usamos la clase ``JsonSerializer`` para serializar y deserializar objetos a/desde formato JSON.
