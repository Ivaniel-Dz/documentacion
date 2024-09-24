## C#

## Mostrar mensaje por pantalla
```cs
Console.WriteLine("Hola mi primer codigo"+"\n"+"C Shart");
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
```cs
```
### Sobrecargas
```cs
```
### Encapsulación
```cs
```
### Propiedades
```cs
```
### Polimorfismo
```cs
```
### Constructores
```cs
```
### Clases abstractas e interfaces
```cs
```


## Tipos Avanzados
### Enumeraciones (enum)
### Estructuras (struct)
### Delegados y eventos
### Expresiones lambda

## Manejo de Excepciones
### Try, catch, finally
### Throw y creación de excepciones personalizadas

## Colecciones y Genéricos
### Arrays
### Listas y Diccionarios
### Pilas (Stack) y colas (Queue)
### Genéricos (List<T>, Dictionary<T, T>)

## LINQ (Language-Integrated Query)
### Sintaxis básica de LINQ
### Consultas de selección, filtrado y agrupación
### Uso de métodos como `Select()`, `Where()`, `GroupBy()`

## Manejo de Archivos
### Lectura y escritura en archivos
### Streams (FileStream, StreamReader, StreamWriter)

## Conceptos Avanzados
### Tareas asíncronas (async/await)
### Expresiones regulares
### Serialización de objetos