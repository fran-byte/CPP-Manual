# Manual Completo de C++ - CPP 42

## 📚 Índice de Contenidos

1. [Introducción](#introducción)
2. [Fundamentos de C++](#fundamentos-de-c)
3. [Variables y Tipos de Datos](#variables-y-tipos-de-datos)
4. [Operadores](#operadores)
5. [Control de Flujo](#control-de-flujo)
6. [Funciones](#funciones)
7. [Arrays y Strings](#arrays-y-strings)
8. [Punteros y Referencias](#punteros-y-referencias)
9. [Programación Orientada a Objetos](#programación-orientada-a-objetos)
10. [Gestión de Memoria](#gestión-de-memoria)
11. [STL - Standard Template Library](#stl---standard-template-library)
12. [Entrada/Salida de Archivos (I/O)](#entradasalida-de-archivos-io)
13. [Algoritmos Avanzados](#algoritmos-avanzados)
14. [Templates y Programación Genérica](#templates-y-programación-genérica)
15. [Excepciones y Manejo de Errores](#excepciones-y-manejo-de-errores)
16. [Type Casting](#type-casting)

---

## Introducción

Esta sección presenta el manual y su propósito, explicando que está diseñado para guiar a través del repositorio de los proyectos CPP de 42 que contiene 10 módulos progresivos que enseñan C++ desde lo básico hasta conceptos avanzados utilizando el estándar C++98.

Este manual está diseñado para llevarte desde cero hasta el nivel necesario para resolver todos los ejercicios del repositorio **CPP_Piscine**. El repositorio contiene 10 módulos progresivos que enseñan C++ siguiendo el estándar C++98, desde conceptos básicos hasta programación avanzada con STL.

El estándar C++98 es la primera versión estandarizada del lenguaje y aunque posteriormente han surgido versiones más modernas (C++11, C++14, C++17, C++20), entender C++98 es fundamental para comprender las bases del lenguaje y su evolución. En el contexto de 42, se utiliza este estándar para asegurar un aprendizaje sólido de los conceptos fundamentales antes de abordar características más avanzadas.

### Estructura del Repositorio

Presenta una tabla organizada de los 10 módulos del repositorio, mostrando el enfoque principal y ejercicios clave de cada uno para proporcionar una visión general del aprendizaje progresivo.

El repositorio está organizado en 10 módulos, cada uno enfocado en conceptos específicos:

| Módulo | Enfoque Principal | Ejercicios Clave |
|--------|------------------|------------------|
| Module 00 | Clases básicas | PhoneBook, Account |
| Module 01 | Memoria y referencias | Zombies, Weapons |
| Module 02 | Sobrecarga de operadores | Fixed-point arithmetic |
| Module 03 | Herencia | ClapTrap hierarchy |
| Module 04 | Polimorfismo | Animal/Brain, AMateria |
| Module 05 | Excepciones | Bureaucrat/Form |
| Module 06 | Type casting | Conversiones |
| Module 07 | Templates | Array class |
| Module 08 | STL Containers | Span, MutantStack |
| Module 09 | STL Mastery | BitcoinExchange, PmergeMe |

La progresión está cuidadosamente diseñada: comienza con conceptos básicos de programación orientada a objetos y gradualmente introduce características más avanzadas como polimorfismo, templates y contenedores STL. Cada módulo construye sobre los conocimientos adquiridos en los anteriores, creando una curva de aprendizaje suave pero desafiante.

---

## Fundamentos de C++

Esta sección cubre los conceptos básicos esenciales de programación en C++, incluyendo la estructura de programas, directivas de preprocesador y sistemas de compilación con Makefiles.

### Estructura Básica de un Programa

Explica que todo programa C++ comienza con la función `main()`, mostrando un ejemplo práctico del ejercicio PhoneBook que ilustra un bucle principal de entrada de usuario.

Todo programa en C++ comienza con la función `main()`. Esta función es el punto de entrada del programa, donde la ejecución comienza. Observa la estructura básica en el ejercicio PhoneBook:

```cpp
#include "PhoneBook.hpp"

int main(void)
{
    std::string input;
    PhoneBook PB;
    
    while (true)
    {
        std::getline(std::cin, input);
        checkCommands(input, &PB);
    }
    return (0);
}
```

En este ejemplo, podemos ver varios elementos fundamentales:
1. `#include "PhoneBook.hpp"` - Incluye la declaración de la clase PhoneBook
2. `int main(void)` - La función principal que retorna un entero (0 indica éxito)
3. Declaración de variables (`std::string input`, `PhoneBook PB`)
4. Un bucle infinito (`while (true)`) que mantiene el programa en ejecución
5. Entrada del usuario mediante `std::getline(std::cin, input)`
6. Llamada a función `checkCommands()` para procesar la entrada
7. `return (0)` - Aunque en este caso el bucle es infinito, técnicamente el return nunca se alcanza

La función `main` debe existir exactamente una vez en cada programa C++. El tipo de retorno `int` y los parámetros pueden variar ligeramente, pero esta es la forma más común.

### Directivas de Preprocesador

Describe las directivas `#include` para incluir cabeceras, diferenciando entre cabeceras estándar de la biblioteca y cabeceras personalizadas del proyecto.

Las directivas `#include` permiten incluir cabeceras. En este repositorio se usan dos tipos:

```cpp
// Cabeceras estándar
#include <iostream>
#include <string>
#include <fstream>

// Cabeceras propias
#include "PhoneBook.hpp"
```

Las directivas de preprocesador son procesadas antes de la compilación propiamente dicha. La diferencia entre `< >` y `" "` es importante:
- `< >` busca en los directorios estándar del sistema (para bibliotecas estándar)
- `" "` busca primero en el directorio actual, luego en los directorios del sistema

Cada inclusión inserta el contenido completo del archivo en ese punto del código. Esto es por qué es importante usar **guards de inclusión** (`#ifndef`, `#define`, `#endif`) en los archivos de cabecera para evitar inclusiones múltiples.

### Compilación y Makefiles

Muestra el sistema de compilación estandarizado usado en todos los módulos, con Makefiles que siguen el estándar C++98 y configuraciones de flags específicas.

Todos los módulos usan un sistema de compilación consistente con Makefiles que siguen el estándar C++98:

```makefile
CXX = c++
CXXFLAGS = -Wall -Wextra -Werror -Wshadow -std=c++98 -I inc
```

Un Makefile es un archivo que define reglas para compilar el proyecto. Los elementos clave son:
- `CXX = c++` - Define el compilador a usar
- `CXXFLAGS` - Flags del compilador:
  - `-Wall -Wextra` - Activa todas las advertencias
  - `-Werror` - Trata las advertencias como errores (muy útil para mantener código limpio)
  - `-Wshadow` - Advierte cuando una variable oculta otra del ámbito exterior
  - `-std=c++98` - Especifica el estándar C++98
  - `-I inc` - Añade el directorio `inc` a la búsqueda de cabeceras

El uso consistente de Makefiles asegura que todos los módulos se compilen de la misma manera, facilitando el desarrollo y la portabilidad.

---

## Variables y Tipos de Datos

Esta sección presenta los tipos de datos fundamentales en C++, métodos de declaración e inicialización, y el uso de constantes para valores inmutables.

### Tipos Fundamentales

Lista los tipos básicos de datos utilizados en los ejercicios del repositorio, incluyendo tipos primitivos y la clase `std::string` para manejo de cadenas.

En los ejercicios del repositorio encontrarás los siguientes tipos básicos:

```cpp
int         // Números enteros (típicamente 4 bytes, rango aprox. ±2.1 mil millones)
float       // Números decimales de precisión simple (4 bytes, 6-7 dígitos decimales)
double      // Números decimales de precisión doble (8 bytes, 15-16 dígitos decimales)
char        // Caracteres (1 byte, -128 a 127 o 0 a 255)
bool        // Valores booleanos (true/false)
std::string // Cadenas de texto (clase de la STL)
```

Los tipos primitivos tienen tamaños específicos que pueden variar entre arquitecturas, pero en sistemas modernos de 32/64 bits los tamaños son generalmente como se indican. `std::string` no es un tipo primitivo sino una clase de la Standard Template Library que maneja cadenas de caracteres de forma dinámica y segura.

### Declaración e Inicialización

Muestra ejemplos prácticos de declaración e inicialización de variables, usando el ejercicio BitcoinExchange para ilustrar tipos comunes.

Ejemplo del ejercicio BitcoinExchange:

```cpp
int dateINT;
float ammount;
std::string line;
std::map<int, float> database;
```

En C++98, es importante inicializar las variables siempre que sea posible para evitar comportamientos indefinidos. Existen varias formas de inicialización:
```cpp
int a = 5;           // Inicialización tradicional
int b(5);            // Inicialización por constructor (sintaxis de función)
int c = int(5);      // Inicialización explícita
// En C++11 y posteriores existe también inicialización uniforme con {}
```

En el ejemplo de BitcoinExchange, las variables se declaran primero y se inicializan más tarde con valores específicos. Esto es común cuando los valores se obtienen de entrada del usuario o de archivos.

### Constantes

Explica el uso de la palabra clave `const` para declarar valores inmutables, con ejemplos tomados del ejercicio Fixed.

Usa `const` para declarar valores inmutables:

```cpp
Fixed const b(10);
Fixed const c(42.42f);
```

La palabra clave `const` tiene múltiples usos en C++:
1. Variables constantes: valores que no pueden modificarse después de la inicialización
2. Parámetros constantes: indican que una función no modificará el parámetro
3. Métodos constantes: indican que el método no modifica el objeto
4. Retornos constantes: previenen la modificación del valor retornado

En el contexto de los ejercicios, `const` es crucial para:
- Garantizar la corrección del código (el compilador detecta intentos de modificación)
- Permitir optimizaciones del compilador
- Hacer explícita la intención del programador

---

## Operadores

Esta sección cubre los diferentes tipos de operadores en C++, incluyendo operadores aritméticos, de comparación y de asignación.

### Operadores Aritméticos

Muestra operadores aritméticos básicos implementados mediante sobrecarga en el ejercicio Fixed, permitiendo operaciones matemáticas con objetos.

En el ejercicio Fixed se implementan operaciones aritméticas con sobrecarga:

```cpp
Fixed a;  // Ya lo veremos más adelante pero Fixed es un tipo de objeto.
Fixed b;
Fixed result = a + b;  // Suma
result = a - b;        // Resta
result = a * b;        // Multiplicación
result = a / b;        // División
```

La sobrecarga de operadores permite definir el comportamiento de los operadores estándar (+, -, *, /, etc.) para tipos definidos por el usuario (clases). Esto hace que el código sea más intuitivo y legible. En el ejercicio Fixed, se sobrecargan estos operadores para trabajar con números de punto fijo, una representación alternativa a los números de punto flotante.

Los operadores aritméticos básicos en C++ son:
- Suma: `+`
- Resta: `-`
- Multiplicación: `*`
- División: `/`
- Módulo: `%` (solo para tipos enteros)

### Operadores de Comparación

Presenta operadores de comparación comunes utilizados en estructuras condicionales para evaluar relaciones entre valores.

```cpp
if (a == b)  // Igualdad
if (a != b)  // Desigualdad
if (a < b)   // Menor que
if (a > b)   // Mayor que
if (a <= b)  // Menor o igual que
if (a >= b)  // Mayor o igual que
```

Los operadores de comparación retornan valores booleanos (`true` o `false`) y son fundamentales para el control de flujo. También pueden ser sobrecargados para tipos personalizados. Cuando se sobrecargan operadores de comparación, es importante mantener relaciones consistentes (por ejemplo, si `a == b` es verdadero, entonces `a != b` debe ser falso).

En C++98, estos operadores se implementan típicamente como funciones miembro o funciones amigas de la clase.

### Operadores de Asignación

Explica operadores de asignación simple y compuestos que modifican el valor de variables u objetos mediante operaciones combinadas.

```cpp
a = b;        // Asignación simple
a += b;       // Suma y asignación
a -= b;       // Resta y asignación
a *= b;       // Multiplicación y asignación
a /= b;       // División y asignación
```

El operador de asignación (`=`) copia el valor del operando derecho al operando izquierdo. Los operadores compuestos (`+=`, `-=`, etc.) combinan una operación aritmética con la asignación. Estos operadores también pueden ser sobrecargados.

Es importante distinguir entre:
- **Asignación**: `a = b` (copia el valor de b a a)
- **Inicialización**: `int a = b` (crea a con el valor de b)

La sobrecarga del operador de asignación es particularmente importante cuando una clase maneja recursos dinámicos (memoria, archivos, etc.), ya que se debe implementar una "copia profunda" en lugar de una "copia superficial".

---

## Control de Flujo

Esta sección describe estructuras de control para dirigir la ejecución del programa, incluyendo condicionales y bucles.

### Condicionales if-else

Muestra estructuras condicionales utilizadas en el ejercicio PhoneBook para procesar comandos de entrada del usuario.

Ejemplo del ejercicio PhoneBook:

```cpp
if (input == "EXIT" || input == "E")
    PB->print_error("\033[0;31mExit program.\033[0m");
if (input == "ADD" || input == "A")
{
    std::cout << "\e[0;32mAdding contact...\e[0;37m" << std::endl;
    PB->add_contact();
}
```

La estructura `if` permite la ejecución condicional de código. Su forma básica es:
```cpp
if (condición) {
    // código a ejecutar si condición es verdadera
}
```

Se puede extender con `else` y `else if`:
```cpp
if (condición1) {
    // código si condición1 es verdadera
} else if (condición2) {
    // código si condición2 es verdadera
} else {
    // código si ninguna condición es verdadera
}
```

En el ejemplo del PhoneBook, se usan condiciones con operadores lógicos (`||` significa OR) para permitir múltiples formas de ingresar comandos (por ejemplo, "EXIT" o "E").

### Bucles

Subsección que presenta diferentes tipos de bucles utilizados para repetición de código, con ejemplos específicos.

#### Bucle for

Ejemplo de bucle `for` que itera un número específico de veces, utilizado para acceder a elementos de un array.

```cpp
for (int i = 0; i < limit; i++)
{
    aux = &_agenda[i % 8];
    grid_printItem(std::to_string(i % 8));
}
```

El bucle `for` tiene tres componentes principales:
1. **Inicialización**: `int i = 0` - Se ejecuta una vez al inicio
2. **Condición**: `i < limit` - Se verifica antes de cada iteración
3. **Expresión de incremento**: `i++` - Se ejecuta al final de cada iteración

En este ejemplo específico, el uso de `i % 8` sugiere que se está trabajando con una estructura circular o buffer cíclico de tamaño 8.

#### Bucle while

Muestra un bucle `while` infinito que procesa entrada del usuario hasta cumplir ciertas condiciones.

```cpp
while (true)
{
    std::getline(std::cin, input);
    if (std::cin.eof())
        print_error(ERROR_EOF);
    if (input.length() == 1 && _str_is_digit(input) && _index_in_range(input))
        break;
}
```

El bucle `while` ejecuta su cuerpo mientras la condición sea verdadera. En este caso, `while (true)` crea un bucle infinito que solo se rompe con la sentencia `break`.

Variantes del bucle while:
- `while (condición)`: Verifica condición antes de ejecutar
- `do { ... } while (condición)`: Ejecuta al menos una vez, verifica condición al final

El uso de `std::cin.eof()` detecta el fin de archivo (EOF), que ocurre cuando el usuario presiona Ctrl+D (Unix/Linux) o Ctrl+Z (Windows).

---

## Funciones

Esta sección cubre la creación y uso de funciones en C++, incluyendo declaración, definición, parámetros, retorno y sobrecarga.

### Declaración y Definición

Explica la separación entre declaración (prototipo) en archivos de cabecera y definición (implementación) en archivos de código fuente.

Las funciones en C++ tienen una declaración (prototipo) y una definición:

```cpp
// Declaración en el header
void add_contact();
void search_and_print_contact();

// Definición en el archivo .cpp
void PhoneBook::add_contact() // este enconcreto es un método de la clase PhoneBook.
{
    // Implementación
}
```

La separación entre declaración e implementación es una buena práctica de programación que:
1. **Mejora la organización**: Las interfaces están claramente separadas de las implementaciones
2. **Reduce tiempos de compilación**: Los cambios en implementaciones solo requieren recompilar el archivo .cpp correspondiente
3. **Facilita el trabajo en equipo**: Los programadores pueden trabajar con solo las declaraciones

Para funciones miembro de clase (métodos), el operador de resolución de ámbito `::` especifica a qué clase pertenece el método.

### Parámetros y Retorno

Muestra ejemplos de funciones con parámetros y valores de retorno, ilustrando cómo las funciones procesan datos.

```cpp
int parse_date(std::string& dateString, std::string file)  // paso por REFERENCIA vs paso por COPIA
{
    std::tm date = {};
    // ... procesamiento
    return (convert_date_to_int(date));
}
```

Los parámetros pueden pasarse de tres formas principales:
1. **Por valor (copia)**: `void func(Tipo valor)` - Crea una copia del argumento
2. **Por referencia**: `void func(Tipo& referencia)` - Trabaja con el objeto original
3. **Por puntero**: `void func(Tipo* puntero)` - Similar a referencia pero puede ser nullptr

En el ejemplo, `dateString` se pasa por referencia (`std::string&`) para evitar copias costosas de strings. El tipo de retorno `int` indica que la función devuelve un valor entero.

Las funciones que no devuelven valor tienen tipo de retorno `void`.

### Sobrecarga de Funciones

Presenta el concepto de sobrecarga de funciones, permitiendo múltiples funciones con el mismo nombre pero diferentes parámetros.

```cpp
void addNumber(int value);
void addArray(int array[], size_t size);
void addRange(int min, int max);
```

La sobrecarga de funciones permite definir múltiples funciones con el mismo nombre pero diferentes parámetros (en tipo, número o ambos). El compilador decide cuál llamar basándose en los argumentos proporcionados.

La sobrecarga es útil para:
- Proporcionar interfaces consistentes para operaciones similares
- Manejar diferentes tipos de datos de forma transparente
- Proporcionar valores por defecto para parámetros (aunque en C++98 esto se hace con parámetros por defecto, no con sobrecarga)

Es importante notar que el tipo de retorno **no** se considera para la sobrecarga. Dos funciones no pueden diferir solo en el tipo de retorno.

---

## Arrays y Strings

Esta sección cubre estructuras de datos básicas para almacenamiento de elementos, incluyendo arrays estáticos y cadenas de texto.

### Arrays Estáticos

Muestra la declaración e inicialización de arrays estáticos con tamaño fijo, y cómo calcular el tamaño del array.

```cpp
int const amounts[] = {42, 54, 957, 432, 1234, 0, 754, 16576};
size_t const amounts_size = sizeof(amounts) / sizeof(int);
```

Los arrays estáticos en C++ tienen las siguientes características:
- Tamaño fijo determinado en tiempo de compilación
- Los elementos se almacenan en memoria contigua
- Se accede a los elementos mediante índices (0 a tamaño-1)
- El nombre del array se convite implícitamente a un puntero al primer elemento

El cálculo `sizeof(amounts) / sizeof(int)` es una técnica común para obtener el número de elementos en un array estático. `sizeof` devuelve el tamaño en bytes, por lo que dividir por el tamaño de un elemento da el número de elementos.

### std::string

Presenta la clase `std::string` como alternativa segura y flexible a arrays de caracteres, con métodos para entrada/salida.

La clase `std::string` proporciona operaciones seguras con cadenas:

```cpp
std::string input;
std::getline(std::cin, input);

if (input == "EXIT" || input == "E")
    // procesar
```

`std::string` es parte de la Standard Template Library (STL) y ofrece numerosas ventajas sobre los arrays de caracteres estilo C:
- Gestión automática de memoria
- Capacidad de crecimiento dinámico
- Operadores sobrecargados (==, +, etc.)
- Métodos útiles (find(), substr(), length(), etc.)
- Mayor seguridad (menos propenso a desbordamientos de buffer)

En C++98, `std::getline(std::cin, input)` es la forma preferida de leer líneas completas, ya que maneja espacios correctamente (a diferencia de `std::cin >> input`).

### std::vector

Introduce `std::vector` como contenedor dinámico versátil de la STL, mostrando operaciones básicas como inserción.

Contenedor dinámico usado extensivamente en los ejercicios:

```cpp
std::vector<int> _myVector;
std::vector<int> sortedNumbers = _myVector;
std::sort(sortedNumbers.begin(), sortedNumbers.end());
```

`std::vector` es el contenedor secuencial más común de la STL. Sus características principales son:
- Tamaño dinámico (puede crecer y reducirse)
- Acceso aleatorio en tiempo constante (mediante `[ ]` o `at()`)
- Almacenamiento contiguo en memoria
- Inserción/eliminación eficiente al final, menos eficiente en otras posiciones

En el ejemplo, `sortedNumbers = _myVector` crea una copia del vector (copia profunda). `std::sort` ordena los elementos usando iteradores (`begin()` y `end()`).

---

## Punteros y Referencias

Esta sección explica mecanismos para manejar memoria y crear alias de variables, fundamentales para gestión de recursos.

### Punteros

Describe punteros como variables que almacenan direcciones de memoria, con ejemplos de uso en el ejercicio Animal/Brain.

Los punteros almacenan direcciones de memoria. En el ejercicio Animal/Brain:

```cpp
Brain* brain;  // Puntero a un objeto Brain

// En el constructor
brain = new Brain();

// En el destructor
delete brain;
```

Los punteros son variables que contienen direcciones de memoria de otras variables u objetos. Características clave:
- Declaración: `Tipo* nombre;`
- Operador de dirección: `&variable` obtiene la dirección de una variable
- Operador de desreferencia: `*puntero` accede al valor apuntado
- Pueden ser `nullptr` (C++11) o `NULL` (C++98) para indicar "no apunta a nada"

Los punteros son esenciales para:
- Gestión dinámica de memoria (`new`/`delete`)
- Paso eficiente de objetos grandes a funciones
- Implementación de estructuras de datos dinámicas
- Polimorfismo (punteros a clases base)

### Referencias

Explica referencias como alias de variables existentes, mostrando ejemplos de referencias constantes y referencias a punteros.

Las referencias son alias de otras variables:

```cpp
std::string const & getType() const;  // Referencia constante
AMateria* & getMateria(int idx);      // Referencia a puntero
```

Las referencias son similares a punteros pero con diferencias importantes:
- Deben inicializarse al declararse
- No pueden cambiar a qué variable se refieren
- No pueden ser nullptr/NULL
- No requieren operador de desreferencia explícito (*)
- Sintaxis más limpia

Tipos de referencias:
1. **Referencias simples**: `Tipo& ref = variable;`
2. **Referencias constantes**: `const Tipo& ref = variable;` (no permite modificación)
3. **Referencias a punteros**: `Tipo*& ref = puntero;` (puede modificar el puntero)

Las referencias constantes son especialmente útiles para parámetros de funciones, ya que evitan copias costosas sin permitir modificaciones accidentales.

### Gestión de Memoria

Subsección que cubre operadores para asignación y liberación de memoria dinámica, esenciales para manejo manual.

#### new y delete

Muestra el uso de `new` para crear objetos dinámicos y `delete` para liberar la memoria asignada.

```cpp
// Asignación dinámica
AMateria* materia = new Ice();

// Liberación de memoria
delete materia;
```

`new` y `delete` son operadores para gestión manual de memoria en C++:
- `new Tipo` asigna memoria para un objeto y llama a su constructor
- `delete puntero` libera la memoria y llama al destructor
- **Regla fundamental**: Cada `new` debe tener exactamente un `delete` correspondiente

Problemas comunes con `new`/`delete`:
1. **Fugas de memoria**: Olvidar llamar a `delete`
2. **Doble eliminación**: Llamar a `delete` dos veces en el mismo puntero
3. **Eliminación de arrays**: Usar `delete` en lugar de `delete[]` para arrays

En C++ moderno se prefieren punteros inteligentes (`std::unique_ptr`, `std::shared_ptr`), pero en C++98 debemos manejar la memoria manualmente con cuidado.

#### Arrays dinámicos

Presenta la creación y eliminación de arrays dinámicos usando `new[]` y `delete[]`, con ejemplo de array de enteros.

```cpp
// Crear array dinámico
int* mirror = new int[MAX_VAL];

// Liberar array dinámico
delete [] mirror;
```

Para arrays dinámicos, se usan `new[]` y `delete[]`:
- `new Tipo[tamaño]` asigna memoria para un array y llama al constructor por defecto para cada elemento
- `delete[] puntero` libera la memoria y llama al destructor para cada elemento

**Importante**: Siempre usar `delete[]` para arrays creados con `new[]`, y `delete` para objetos individuales creados con `new`. Mezclarlos causa comportamiento indefinido.

---

## Programación Orientada a Objetos

Esta sección cubre los principios fundamentales de POO en C++, incluyendo clases, objetos, herencia y polimorfismo.

### Clases y Objetos

Subsección que introduce los conceptos básicos de clases como plantillas para objetos, con ejemplos de definición.

#### Definición de Clase

Muestra la estructura básica de una clase con secciones privadas y públicas, usando PhoneBook como ejemplo.

```cpp
class PhoneBook
{
private:
    Contact _agenda[8];
    int _id;

public:
    PhoneBook();
    void add_contact();
    void search_and_print_contact();
};
```

Una clase es una plantilla para crear objetos. Contiene:
1. **Miembros datos**: Variables que almacenan el estado del objeto
2. **Miembros función (métodos)**: Funciones que definen el comportamiento
3. **Especificadores de acceso**: Controlan la visibilidad de los miembros
   - `private`: Solo accesible desde dentro de la clase (encapsulamiento)
   - `public`: Accesible desde cualquier parte
   - `protected`: Accesible desde la clase y clases derivadas (herencia)

La convención de nombres con guión bajo (`_id`) indica miembros privados, pero esto es solo una convención, no una regla del lenguaje.

#### Constructores

Presenta diferentes tipos de constructores: por defecto y de copia, con ejemplos que muestran inicialización.

```cpp
// Constructor por defecto
PhoneBook::PhoneBook() : _id(0)
{
    // inicialización
}

// Constructor de copia
Cat::Cat(const Cat& f) : Animal(f)  // Copia correctamente la parte Animal del objeto Cat (de la que hereda)
{
    brain = NULL; // Se evita que brain apunte a basura
    *this = f;  // Se usa el operador de asignación (operator=) dentro del constructor de copia
}
```

Los constructores son métodos especiales que inicializan objetos:
1. **Constructor por defecto**: No tiene parámetros (o todos tienen valores por defecto)
2. **Constructor de copia**: Crea un objeto copiando otro existente
3. **Constructor con parámetros**: Inicializa con valores específicos

La lista de inicialización (`: _id(0)`) es preferible a asignar valores en el cuerpo del constructor porque es más eficiente (inicializa directamente en lugar de asignar).

En el constructor de copia de `Cat`, se ve:
1. Llamada al constructor de copia de la clase base (`Animal(f)`)
2. Inicialización cuidadosa de punteros antes de la copia
3. Reutilización del operador de asignación (`*this = f`)

#### Destructor

Ejemplo de destructor que libera memoria dinámica, mostrando la importancia de limpieza de recursos.

```cpp
Cat::~Cat()
{
    delete brain;
}
```

El destructor es un método especial que se llama automáticamente cuando un objeto es destruido. Su propósito es liberar recursos (memoria, archivos, conexiones de red, etc.).

Características de los destructores:
- Nombre: `~NombreClase()`
- No tiene tipo de retorno ni parámetros
- Si una clase tiene recursos dinámicos, generalmente necesita un destructor
- En jerarquías de herencia, los destructores se llaman en orden inverso a los constructores (primero el destructor de la clase derivada, luego el de la base)

### Herencia

Subsección que explica el mecanismo de herencia para crear jerarquías de clases, permitiendo reutilización.

#### Herencia Simple

Muestra herencia simple con clase base virtual, usando ScavTrap como ejemplo que hereda de ClapTrap.

```cpp
class ScavTrap : public virtual ClapTrap
{
public:
    ScavTrap();
    void guardGate();
};
```

La herencia permite crear una nueva clase (derivada) basada en una existente (base). Tipos de herencia:
- `public`: Miembros públicos/protegidos de la base permanecen públicos/protegidos en la derivada
- `protected`: Miembros públicos/protegidos de la base se vuelven protegidos en la derivada
- `private`: Miembros públicos/protegidos de la base se vuelven privados en la derivada

La herencia `virtual` (como en `public virtual ClapTrap`) resuelve el problema del diamante en herencia múltiple, asegurando que solo exista una copia de la clase base en la jerarquía.

#### Herencia Múltiple y Virtual

Ejemplo de herencia múltiple con DiamondTrap que hereda de dos clases diferentes, ilustrando el problema del diamante.

```cpp
class DiamondTrap : public ScavTrap, public FragTrap
{
public:
    DiamondTrap();
    void whoAmI();
};
```

C++ permite herencia múltiple: una clase puede heredar de múltiples clases base. Esto puede causar ambigüedades si:
1. Dos clases base tienen miembros con el mismo nombre
2. Las clases base comparten una clase abuelo común (problema del diamante)

El **problema del diamante** ocurre cuando:
- Clase B y Clase C heredan de Clase A
- Clase D hereda de B y C
- D tiene dos copias de A (una a través de B, otra a través de C)

La solución es usar herencia virtual para A en B y C.

### Polimorfismo

Subsección que cubre polimorfismo como mecanismo para que objetos de diferentes clases respondan al mismo mensaje.

#### Funciones Virtuales

Presenta funciones virtuales puras para interfaces abstractas y destructores virtuales para limpieza segura.

```cpp
class Animal
{
public:
    virtual void makeSound() const = 0;  // Función virtual pura
    virtual ~Animal() {}                  // Destructor virtual
};

class Dog : public Animal
{
public:
    void makeSound() const override;     // Sobrescribir (override) = redefinir una función virtual heredada
                                        // está obligada a implementar esa función
};
```

El polimorfismo permite tratar objetos de clases derivadas como objetos de la clase base. Para que funcione:
1. **Funciones virtuales**: Marcadas con `virtual` en la clase base
2. **Funciones virtuales puras**: `= 0` hace la clase abstracta (no se pueden crear instancias)
3. **Destructores virtuales**: Necesarios cuando se eliminan objetos derivados a través de punteros base

Cuando una función es virtual, la llamada se resuelve en tiempo de ejecución según el tipo real del objeto (enlace dinámico), no según el tipo del puntero/referencia (enlace estático).

Nota: `override` es de C++11; en C++98 simplemente se redeclara la función con el mismo nombre y firma.

#### Ejemplo de Polimorfismo

Muestra polimorfismo en acción con array de punteros base que apuntan a objetos derivados.

```cpp
Animal* zoo[ZOO_SIZE];

for (int i = 0; i < ZOO_SIZE; i++)
{
    if (i < ZOO_SIZE / 2)
        zoo[i] = new Dog();
    else
        zoo[i] = new Cat();
}

for (int i = 0; i < ZOO_SIZE; i++)
    zoo[i]->makeSound();  // Llamada polimórfica, llama tanto al metodo de Dog como al de Cat
                        // Si es Dog → llama a Dog::makeSound()
                        // Si es Cat → llama a Cat::makeSound()
```

Este es un ejemplo clásico de polimorfismo:
1. Se crea un array de punteros a `Animal`
2. Cada puntero apunta a un objeto `Dog` o `Cat`
3. Al llamar a `makeSound()`, se ejecuta la versión correcta según el tipo real

**Importante**: Sin destructores virtuales, al hacer `delete zoo[i]` solo se llamaría al destructor de `Animal`, no de `Dog`/`Cat`, causando fugas de memoria.

### Sobrecarga de Operadores

Subsección que explica cómo redefinir operadores para clases personalizadas, permitiendo sintaxis intuitiva.

#### Operador de Asignación

Muestra la implementación del operador de asignación con gestión correcta de memoria y verificación de auto-asignación.

```cpp
Cat& Cat::operator=(const Cat& f)
{
    if (this != &f)
    {
        _type = f._type;  // Copiamos los atributos simples (no dinámicos)
        if (brain)        // Liberamos la memoria actual del objeto
            delete brain; // para evitar fugas de memoria

        brain = new Brain(*f.brain); // Realizamos una copia profunda del objeto Brain
                                    // No estamos copiando el puntero,
                        // estamos creando un objeto nuevo en memoria con el mismo contenido.
    }
    return (*this);
}
```

La sobrecarga del operador de asignación (`operator=`) debe manejar:
1. **Auto-asignación**: `if (this != &f)` evita problemas cuando se asigna un objeto a sí mismo
2. **Liberación de recursos existentes**: Antes de copiar nuevos recursos, liberar los antiguos
3. **Copia profunda**: Para punteros, crear nuevas copias de los objetos apuntados
4. **Retorno por referencia**: `return *this` permite encadenamiento (`a = b = c`)

El patrón común es: verificar auto-asignación, liberar recursos antiguos, copiar recursos nuevos, retornar `*this`.

#### Operadores de Stream

Ejemplo de sobrecarga del operador `<<` para salida personalizada de objetos, permitiendo integración con flujos.

```cpp
// Permite mostrar un objeto Fixed directamente en un flujo de salida
// por ejemplo: std::cout << fixed;
std::ostream& operator<<(std::ostream& os, const Fixed& fixed)
{
    os << fixed.toFloat(); // lo enviamos al flujo de salida (cout, ofstream, etc.)
    return os;
    // Devolvemos el mismo flujo para permitir encadenar salidas
    // ejemplo: std::cout << a << b << c;
}
```

La sobrecarga de operadores de stream (`<<` para salida, `>>` para entrada) normalmente se hace como funciones globales (no miembros) porque el operador izquierdo es el stream, no el objeto.

Características:
- Primer parámetro: referencia al stream
- Segundo parámetro: referencia constante al objeto a mostrar
- Retorno: referencia al stream para permitir encadenamiento
- Dentro de la función: insertar los datos del objeto en el stream

---

## Gestión de Memoria

Esta sección cubre principios y prácticas para manejo correcto de memoria en C++, incluyendo reglas para gestión.

### Rule of Three

Explica la regla que establece que si una clase necesita destructor personalizado, también necesita constructor de copia.

Si una clase necesita un destructor personalizado, probablemente necesite también:
1. Constructor de copia
2. Operador de asignación

```cpp
class Cat
{
public:
    Cat();                    // Constructor
    Cat(const Cat& f);        // Constructor de copia
    ~Cat();                   // Destructor
    Cat& operator=(const Cat& f);  // Operador de asignación
};
```

La **Regla de Tres** (Rule of Three) establece que si una clase necesita uno de estos tres (destructor, constructor de copia, operador de asignación), probablemente necesite los tres. Esto se debe a que generalmente los tres están relacionados con la gestión de recursos.

Razón: Si una clase maneja recursos (memoria dinámica, archivos, etc.) y necesita un destructor para liberarlos, también necesita:
- Constructor de copia para copiar correctamente los recursos
- Operador de asignación para asignar correctamente los recursos

Si no se definen, el compilador genera versiones por defecto que hacen copias superficiales (shallow copy), lo que puede causar problemas como dobles eliminaciones o fugas de memoria.

### Deep Copy vs Shallow Copy

Subsección que contrasta dos enfoques de copia de objetos, destacando los problemas de shallow copy.

#### Shallow Copy (Problemático)

Muestra copia superficial que duplica punteros pero no datos, causando problemas cuando objetos comparten memoria.

```cpp
// Solo copia el puntero, no los datos
brain = f.brain;  // ¡Ambos objetos apuntan al mismo Brain!
```

**Copia superficial (Shallow Copy)**: Solo copia los valores de los miembros, incluidos los punteros. Ambos objetos terminan apuntando a los mismos datos en memoria.

Problemas:
1. **Doble eliminación**: Si ambos objetos se destruyen, ambos intentarán liberar la misma memoria
2. **Modificaciones compartidas**: Cambiar los datos afecta a ambos objetos
3. **Fugas de memoria**: Si un objeto se destruye y libera la memoria, el otro queda con un puntero colgante

#### Deep Copy (Correcto)

Presenta copia profunda que crea nuevos objetos independientes, asegurando que cada objeto tenga sus recursos.

```cpp
// Crea una nueva copia de los datos
brain = new Brain(*f.brain);  // Cada objeto tiene su propio Brain
```

**Copia profunda (Deep Copy)**: Crea copias independientes de todos los recursos. Cada objeto tiene sus propios datos.

Implementación:
1. Para punteros: asignar nueva memoria y copiar el contenido
2. Para otros recursos: crear nuevos recursos independientes

La copia profunda es más segura pero también más costosa en tiempo y memoria. Es necesaria cuando los objetos deben ser independientes.

---

## STL - Standard Template Library

Esta sección introduce la biblioteca estándar de plantillas de C++, cubriendo contenedores, algoritmos e iteradores.

### Contenedores

Subsección que presenta diferentes tipos de contenedores STL para almacenamiento de datos, cada uno optimizado.

#### std::vector

Describe `std::vector` como contenedor dinámico de array redimensionable, mostrando operación básica de inserción.

Contenedor dinámico usado en múltiples ejercicios:

```cpp
std::vector<int> _myVector;
_myVector.push_back(value);  // Agregar elemento
```

`std::vector` es el contenedor secuencial más utilizado. Características:
- **Tamaño dinámico**: Crece automáticamente cuando se agregan elementos
- **Acceso aleatorio**: `O(1)` mediante `[index]` o `at(index)`
- **Contiguo en memoria**: Los elementos están almacenados consecutivamente
- **Inserción/eliminación**: Eficiente al final (`O(1)` amortizado), costoso en medio (`O(n)`)

Métodos importantes:
- `push_back()`: Añade elemento al final
- `pop_back()`: Elimina el último elemento
- `size()`: Número de elementos
- `capacity()`: Espacio actualmente reservado
- `reserve()`: Reserva capacidad para evitar reasignaciones frecuentes

#### std::map

Presenta `std::map` como contenedor asociativo clave-valor ordenado, usado en BitcoinExchange para mapear.

Contenedor asociativo clave-valor, usado en BitcoinExchange:

```cpp
std::map<int, float> database;
database[date] = exchangeRate;
```

`std::map` es un contenedor asociativo que almacena pares clave-valor ordenados por clave. Características:
- **Claves únicas**: Cada clave aparece una vez como máximo
- **Ordenado**: Las claves se mantienen ordenadas (por defecto ascendente)
- **Acceso logarítmico**: Búsqueda, inserción y eliminación en `O(log n)`
- **Implementación**: Generalmente árbol rojo-negro

Métodos importantes:
- `operator[key]`: Acceso o inserción (crea elemento si no existe)
- `find(key)`: Búsqueda sin crear elemento si no existe
- `insert({key, value})`: Inserción explícita
- `erase(key)`: Eliminación por clave

#### std::list

Muestra `std::list` como lista doblemente enlazada, utilizada en PmergeMe para pruebas comparativas.

Lista enlazada usada en PmergeMe:

```cpp
std::list<int> new_list;
for (size_t i = 0; i < vector.size(); i++)
    new_list.push_back(vector[i]);
```

`std::list` es una lista doblemente enlazada. Características:
- **Inserción/eliminación rápida**: `O(1)` en cualquier posición (con iterador)
- **No acceso aleatorio**: Solo se puede recorrer secuencialmente
- **No contiguo en memoria**: Cada elemento tiene enlaces al anterior y siguiente
- **Estable en iteradores**: Los iteradores no se invalidan por inserciones/eliminaciones (excepto el elemento eliminado)

Útil cuando:
- Se realizan muchas inserciones/eliminaciones en medio de la secuencia
- No se necesita acceso aleatorio
- Se necesita estabilidad en los iteradores

### Algoritmos STL

Subsección que cubre algoritmos genéricos de la STL para operaciones comunes como ordenamiento y búsqueda.

#### std::sort

Muestra `std::sort` para ordenar elementos en contenedores, trabajando con iteradores para definir rangos.

```cpp
std::vector<int> sortedNumbers = _myVector;
std::sort(sortedNumbers.begin(), sortedNumbers.end());
```

`std::sort` es el algoritmo de ordenamiento principal de la STL. Características:
- **Complejidad**: `O(n log n)` en promedio
- **Requerimientos**: Iteradores de acceso aleatorio (funciona con `vector`, `deque`, arrays, pero no con `list`)
- **Estabilidad**: No es estable por defecto (para ordenamiento estable usar `std::stable_sort`)
- **Personalizable**: Se puede proporcionar función de comparación personalizada

Funciona en el rango `[first, last)` (incluye first, excluye last). Es un algoritmo genérico que funciona con cualquier tipo que tenga definidos operadores de comparación.

#### std::max_element y std::min_element

Presenta algoritmos para encontrar elementos extremos en contenedores, devolviendo iteradores a valores.

```cpp
std::vector<int>::iterator minIt = std::min_element(_myVector.begin(), _myVector.end());
std::vector<int>::iterator maxIt = std::max_element(_myVector.begin(), _myVector.end());
```

Estos algoritmos encuentran el elemento mínimo/máximo en un rango:
- `std::min_element`: Retorna iterador al primer elemento mínimo
- `std::max_element`: Retorna iterador al primer elemento máximo
- **Complejidad**: `O(n)` (recorre todo el rango una vez)
- **Funciona con**: Cualquier contenedor con iteradores de entrada

Se pueden personalizar con una función de comparación. Retornan `end()` si el rango está vacío.

#### std::find

Ejemplo de `std::find` en función template que busca valores en contenedores, combinado con `std::distance`.

Usado en el ejercicio easyFind:

```cpp
template <typename T>
int easyFind(std::vector<T>& container, int value)
{
    typename std::vector<T>::iterator it = std::find(container.begin(), container.end(), value);
    if (it != container.end())
        return (std::distance(container.begin(), it));
    throw std::exception();
}
```

`std::find` busca un valor en un rango:
- **Complejidad**: `O(n)` (búsqueda lineal)
- **Retorna**: Iterador al primer elemento encontrado, o `end()` si no se encuentra
- **Requisitos**: El tipo debe tener definido `operator==`

`std::distance` calcula la distancia entre dos iteradores (número de elementos entre ellos). En este caso, convierte el iterador en un índice.

#### std::lower_bound

Muestra `std::lower_bound` para búsqueda binaria eficiente en contenedores ordenados como `std::map`.

Usado en BitcoinExchange para búsqueda binaria eficiente:

```cpp
std::map<int, float>::iterator it = database.lower_bound(dateINT);
if (it != database.begin())
    --it;
```

`std::lower_bound` realiza búsqueda binaria en rangos ordenados:
- **Complejidad**: `O(log n)` para contenedores de acceso aleatorio
- **Requisito**: El rango debe estar ordenado
- **Retorna**: Iterador al primer elemento que no es menor que el valor buscado (primer elemento >= valor)
- **Relacionado**: `std::upper_bound` (primer elemento > valor), `std::equal_range` (ambos)

En el ejemplo, se busca la fecha más cercana no mayor a `dateINT`. Si no se encuentra exactamente, se toma el anterior.

### Iteradores

Explica iteradores como abstracciones para recorrer contenedores de manera uniforme, mostrando diferentes tipos.

Los iteradores permiten recorrer contenedores de manera uniforme:

```cpp
// Iterador constante
std::vector<int>::const_iterator it;

// Iterador reverso
std::vector<int>::reverse_iterator rit;

// Uso en MutantStack
typename MutantStack<T>::iterator begin();
typename MutantStack<T>::iterator end();
```

Los iteradores son objetos que actúan como punteros generalizados para acceder a elementos de contenedores. Tipos:
1. **Iteradores de entrada**: Solo lectura secuencial (`istream_iterator`)
2. **Iteradores de salida**: Solo escritura secuencial (`ostream_iterator`)
3. **Iteradores hacia adelante**: Lectura/escritura secuencial (`forward_list`)
4. **Iteradores bidireccionales**: También pueden retroceder (`list`, `map`, `set`)
5. **Iteradores de acceso aleatorio**: Pueden saltar a cualquier posición (`vector`, `deque`, array)

Operaciones comunes:
- `*it`: Desreferenciar
- `it++`, `it--`: Avanzar/retroceder
- `it1 == it2`, `it1 != it2`: Comparación
- `begin()`, `end()`: Iteradores al inicio y después del final

Los iteradores constantes (`const_iterator`) no permiten modificar los elementos apuntados.

---

## Entrada/Salida de Archivos (I/O)

Esta sección cubre operaciones de lectura y escritura de archivos en C++, incluyendo streams y manejo de errores.

### Streams de Archivos

Subsección que presenta clases para trabajar con archivos, diferenciando entre streams de entrada y salida.

#### std::ifstream (Lectura)

Muestra `std::ifstream` para leer archivos, con ejemplo de BitcoinExchange que procesa líneas de CSV.

Usado en BitcoinExchange para leer el archivo CSV:

```cpp
std::ifstream dataFile("data.csv");
if (!dataFile.is_open())
    throw std::runtime_error("Error: could not open file.");

std::string line;
while (std::getline(dataFile, line))
{
    // Procesar cada línea
}
dataFile.close();
```

`std::ifstream` es para leer archivos. Puntos importantes:
1. **Apertura**: Constructor o método `open()`
2. **Verificación**: Siempre verificar `is_open()` o `good()`
3. **Lectura**: `operator>>` para datos formateados, `std::getline()` para líneas
4. **Fin de archivo**: `eof()` detecta cuando se alcanzó el final
5. **Cierre**: Automático en destructor, pero explícito con `close()` es buena práctica

Modos de apertura (segundo parámetro del constructor):
- `std::ios::in`: Lectura (predeterminado para `ifstream`)
- `std::ios::binary`: Modo binario

#### std::ofstream (Escritura)

Presenta `std::ofstream` para escribir archivos, encapsulado en clase Files que gestiona ambos tipos de streams.

Implementado en el ejercicio Files:

```cpp
class Files
{
private:
    std::ifstream inputFile;
    std::ofstream outputFile;
    
public:
    Files(const std::string& inFileName, const std::string& outFileName);
    std::ifstream& get_file_in();
    std::ofstream& get_file_out();
};
```

`std::ofstream` es para escribir archivos. Similar a `ifstream` pero para salida.

La clase `Files` encapsula ambos streams, lo que es una buena práctica:
- **RAII (Resource Acquisition Is Initialization)**: Los recursos se adquieren en el constructor y se liberan en el destructor
- **Manejo de errores centralizado**: La apertura puede manejarse en un solo lugar
- **Interfaz limpia**: Los usuarios solo interactúan con métodos claros

Modos de apertura para `ofstream`:
- `std::ios::out`: Escritura (predeterminado)
- `std::ios::app`: Añadir al final (append)
- `std::ios::trunc`: Truncar si existe (predeterminado con `out`)
- `std::ios::binary`: Modo binario

### Manejo de Errores en I/O

Muestra técnicas para verificar operaciones de archivo exitosas, con ejemplos que verifican apertura.

```cpp
if (!inputFile.is_open())
    print_error("Cannot open the input file.");

if (!outputFile.is_open())
{
    inputFile.close();
    print_error("Cannot open the output file.");
}
```

El manejo de errores en operaciones de archivo es crucial. Métodos de verificación:
1. `is_open()`: Verifica si el archivo se abrió correctamente
2. `good()`: Verifica si el stream está en estado bueno
3. `fail()`: Verifica si ocurrió un error (pero el stream aún es usable)
4. `bad()`: Verifica si ocurrió un error grave (stream no usable)
5. `eof()`: Verifica si se alcanzó el fin de archivo

Buenas prácticas:
- Siempre verificar después de abrir
- Verificar después de operaciones críticas de lectura/escritura
- Cerrar archivos explícitamente cuando ya no se necesitan
- Manejar errores de forma informativa (decir qué archivo falló y por qué)

### Formato de Archivos

Subsección que cubre procesamiento de formatos de archivo específicos, con énfasis en parsing de CSV.

#### CSV Parsing

Ejemplo de parsing de archivos CSV usando `std::istringstream` y `std::getline`, extrayendo campos.

En BitcoinExchange se procesan archivos CSV:

```cpp
std::istringstream iss(line);
std::string dateStr;
std::string exchangeStr;

if (std::getline(iss, dateStr, ',') && std::getline(iss, exchangeStr))
{
    int dateINT = parse_date(dateStr, "Database");
    float exchange = parse_ammount(exchangeStr, "Database");
    database[dateINT] = exchange;
}
```

CSV (Comma-Separated Values) es un formato común. Para parsearlo:
1. Leer línea completa con `std::getline(file, line)`
2. Crear `std::istringstream` con la línea
3. Extraer campos con `std::getline(iss, field, ',')` (el tercer parámetro es el delimitador)

`std::istringstream` convierte una cadena en un stream, permitiendo usar las mismas operaciones que con archivos o entrada estándar.

Consideraciones para CSV real:
- Campos entre comillas (que pueden contener comas)
- Campos vacíos
- Diferentes delimitadores (punto y coma, tabulador)
- Codificaciones de caracteres

---

## Algoritmos Avanzados

Esta sección presenta algoritmos complejos implementados en los ejercicios, incluyendo ordenamiento y búsqueda.

### Algoritmos de Ordenamiento

Subsección que cubre algoritmos de ordenamiento, con énfasis en algoritmos híbridos que combinan estrategias.

#### Merge-Insertion Sort

Muestra implementación de algoritmo híbrido que combina merge sort e insertion sort, usado en PmergeMe.

Implementado en PmergeMe para comparar rendimiento:

```cpp
// Versión para std::vector
void vector_mergeInsertionSort(std::vector<int>& vector)
{
    if (vector.size() <= 1)
        return;
    
    // Algoritmo de merge-insertion sort
}
```

**Merge-Insertion Sort** (también conocido como Ford-Johnson algorithm) es un algoritmo híbrido:
- **Para pequeños arrays**: Usa insertion sort (eficiente para n pequeño)
- **Para arrays grandes**: Usa merge sort (eficiente para n grande)
- **Complejidad**: `O(n log n)` en el peor caso, pero con constantes menores que merge sort puro

Es el algoritmo de comparación teóricamente óptimo en términos de número de comparaciones, aunque en la práctica no siempre es el más rápido debido a factores de implementación.

En PmergeMe, se implementa para comparar con otros algoritmos y entre diferentes contenedores (`vector` vs `list`).

### Búsqueda Binaria con std::map

Presenta uso de `std::lower_bound` para búsqueda binaria eficiente en mapas ordenados en BitcoinExchange.

Usado en BitcoinExchange para búsqueda eficiente:

```cpp
std::map<int, float>::iterator it = database.lower_bound(dateINT);
if (it != database.begin() && (it == database.end() || it->first != dateINT))
    --it;
```

`std::map` mantiene sus elementos ordenados por clave, permitiendo búsqueda binaria. En el contexto de BitcoinExchange:
1. Se buscan tasas de cambio para fechas específicas
2. Si no hay dato para una fecha exacta, se usa el dato más reciente anterior
3. `lower_bound` encuentra la primera fecha no menor que la buscada
4. Si no es exactamente igual, se retrocede una posición (siempre que no sea el inicio)

Este es un patrón común para búsqueda de "mejor coincidencia" en datos temporales.

### Algoritmo RPN (Notación Polaca Inversa)

Muestra implementación de calculadora RPN que procesa expresiones matemáticas usando pila, con validación.

Implementado en el ejercicio RPN:

```cpp
double rpn(std::string& input)
{
    std::stack<float> stack;
    std::istringstream iss(input);
    std::string token;
    
    while (iss >> token)
    {
        if (check_int(token))
            stack.push(std::atof(token.c_str()));
        else if (token == "+" || token == "-" || token == "*" || token == "/")
            choose_operator(stack, token);
        else
            throw std::runtime_error("Error: Invalid token");
    }
    return stack.top();
}
```

**Notación Polaca Inversa (RPN)** elimina la necesidad de paréntesis. Algoritmo:
1. Leer tokens (números u operadores)
2. Si es número: apilar
3. Si es operador: desapilar operandos, aplicar operación, apilar resultado
4. Al final: el resultado está en la cima de la pila

Ventajas de RPN:
- Sin ambigüedad (no necesita paréntesis ni reglas de precedencia)
- Fácil de implementar con una pila
- Eficiente para evaluar expresiones

En la implementación, `choose_operator` maneja cada operación, incluyendo validación (como división por cero).

### Algoritmos de Validación

Subsección que presenta funciones de validación para datos como fechas y números, esenciales para procesamiento.

#### Validación de Fechas

Muestra funciones para validar y convertir fechas, incluyendo parsing de strings y conversión a formatos.

```cpp
bool is_valid_date(const std::tm& date);
int convert_date_to_int(std::tm& date);
int parse_date(std::string& dateString, std::string file);
```

La validación de fechas incluye:
1. **Formato**: Verificar que la cadena tenga el formato esperado (YYYY-MM-DD)
2. **Valores**: Día, mes y año dentro de rangos válidos
3. **Días del mes**: Considerar meses con 28, 29, 30 o 31 días
4. **Años bisiestos**: Febrero tiene 29 días en años bisiestos

La conversión a entero (como `YYYYMMDD`) facilita la comparación y búsqueda.

#### Validación de Números

Presenta funciones para verificar formatos numéricos en strings, asegurando que datos sean válidos.

```cpp
bool check_int(std::string& str);
bool check_float(std::string& str);
```

Validación de números típica:
- Para enteros: Solo dígitos, opcionalmente signo al inicio
- Para flotantes: Dígitos, un punto decimal, opcionalmente signo y exponente
- Rangos: Verificar que estén dentro de límites representables
- Casos especiales: NaN, infinito

Estas validaciones previenen errores al convertir strings a números.

### Medición de Rendimiento

Muestra técnicas para medir tiempo de ejecución usando `clock()`, comparando rendimiento de algoritmos.

En PmergeMe se compara el rendimiento entre diferentes contenedores:

```cpp
double insert_and_sort_vector(std::vector<int>& vector)
{
    clock_t start = clock();
    // Algoritmo de ordenamiento
    return (static_cast<double>(clock() - start) / CLOCKS_PER_SEC);
}

double insert_and_sort_list(std::vector<int>& vector)
{
    clock_t start = clock();
    // Algoritmo de ordenamiento
    return (static_cast<double>(clock() - start) / CLOCKS_PER_SEC);
}
```

Medición de tiempo en C++98:
- `clock()`: Retorna tiempo de procesador usado (no tiempo real)
- `CLOCKS_PER_SEC`: Constante que define ticks por segundo
- `clock_t`: Tipo para almacenar valores de tiempo

Consideraciones:
- **Tiempo de procesador vs tiempo real**: `clock()` mide tiempo de CPU, no tiempo de reloj
- **Precisión**: Depende del sistema, típicamente microsegundos o milisegundos
- **Ruido**: Ejecuciones múltiples para promediar, excluir tiempo de inicialización

---

## Templates y Programación Genérica

Esta sección cubre templates como mecanismo para programación genérica en C++, permitiendo código reutilizable.

### Templates de Funciones

Subsección que presenta templates de funciones, mostrando cómo crear funciones genéricas que trabajan con cualquier tipo.

#### Templates Básicos

Muestra templates simples para operaciones comunes como intercambio, mínimo y máximo, que funcionan con cualquier tipo.

En el Módulo 07 se implementan templates genéricos para funciones básicas:

```cpp
template <typename T>
void swap(T& a, T& b)
{
    T aux = a;
    a = b;
    b = aux;
}

template <typename T>
T min(T a, T b)
{
    if (a < b)
        return (a);
    return (b);
}

template <typename T>
T max(T a, T b)
{
    if (a > b)
        return (a);
    return (b);
}
```

Los templates de funciones permiten escribir código genérico. Características:
- `template <typename T>`: Declara un parámetro de tipo
- `T` puede ser cualquier tipo (built-in, clase, puntero, etc.)
- El compilador genera una versión específica para cada tipo usado (instanciación)
- Las operaciones dentro deben ser válidas para el tipo (por ejemplo, `operator<` para `min`)

Ventajas:
- **Reutilización**: Mismo código para múltiples tipos
- **Seguridad de tipos**: El compilador verifica tipos en tiempo de compilación
- **Eficiencia**: Código específico generado para cada tipo

#### Templates con Functors

Presenta función template que aplica un functor a elementos de array, combinando templates de tipos y funciones.

Función template `iter` que aplica una función a cada elemento de un array:

```cpp
template <typename T, typename Func>
void iter(T array[], int length, Func func)
{
    for (int i = 0; i < length; i++)
    {
        func(array[i]);
    }
}

template <typename T>
struct PrintData
{
    void operator()(T input) const
    {
        std::cout << input << std::endl;
    }
};
```

**Functors** (objetos función) son objetos con `operator()` definido. Ventajas sobre funciones:
- Pueden tener estado (datos miembro)
- Más eficientes (pueden ser inlineados más fácilmente)
- Pueden ser parcialmente especializados

La función `iter` toma:
- Un array de tipo `T`
- Su longitud
- Un functor de tipo `Func` para aplicar a cada elemento

Esto es similar a `std::for_each` de la STL.

### Templates de Clases

Subsección que cubra templates de clases, mostrando cómo crear clases genéricas que encapsulan estructuras.

#### Clase Template Array

Muestra clase template completa para array dinámico genérico, con constructores, destructor y operadores.

Implementación completa con constructores, destructor y operadores:

```cpp
template <typename T>
class Array
{
public:
    Array(int size);
    Array(const Array& f);
    ~Array();
    Array& operator=(const Array& f);
    
    int size(void);
    void print(void);
    
    const T& operator[](int index) const;
    T& operator[](int index);
    
private:
    T* _array;
    int _size;
};
```

Los templates de clases permiten clases genéricas. En este ejemplo:
- `Array` puede contener cualquier tipo `T`
- Tiene los métodos esenciales (constructor, destructor, copia, asignación)
- Proporciona acceso seguro con `operator[]` (con verificación de límites)

La implementación debe estar disponible en tiempo de compilación, por lo que generalmente se pone en el archivo de cabecera o en un archivo `.tpp` incluido.

#### Implementación en Archivo .tpp

Presenta implementación de métodos template en archivo .tpp separado, mostrando inicialización de array.

```cpp
template <typename T>
Array<T>::Array(int size) : _size(size)
{
    _array = new T[_size];
    for (int i = 0; i < _size; i++)
        _array[i] = T();
}

template <typename T>
T& Array<T>::operator[](int index)
{
    if (index >= _size || index < 0)
        throw (std::out_of_range("Index out of bounds"));
    return (_array[index]);
}
```

Los métodos de clases template también son templates. Características:
- Cada método debe precederse con `template <typename T>`
- El nombre completo de la clase es `Array<T>`
- En el constructor: Inicialización de miembros en lista de inicializadores
- En `operator[]`: Verificación de límites y lanzamiento de excepción

La inicialización `_array[i] = T()` usa el **constructor por defecto** del tipo `T`. Esto requiere que `T` tenga constructor por defecto.

### Templates con Contenedores STL

Subsección que muestra templates avanzados que interactúan con contenedores STL, creando funciones genéricas.

#### Función easyFind

Presenta función template que busca elementos en cualquier contenedor STL compatible, usando iteradores.

Template que funciona con cualquier contenedor:

```cpp
template <typename T>
int easyFind(const T &container, int value)
{
    typename T::const_iterator it = std::find(container.begin(), container.end(), value);
    
    if (it != container.end())
        return (std::distance(container.begin(), it));
    
    std::ostringstream oss;
    oss << "Value: [" << value << "] not found in the container.";
    throw (std::runtime_error(oss.str()));
}
```

Esta función template es genérica:
- Funciona con cualquier contenedor `T` que tenga `begin()`, `end()` e iteradores
- Usa `typename T::const_iterator` para obtener el tipo de iterador
- `std::find` para búsqueda lineal
- `std::distance` para convertir iterador a índice
- Lanza excepción informativa si no encuentra

La palabra `typename` antes de `T::const_iterator` es necesaria porque `const_iterator` es un **tipo dependiente** (depende del parámetro template `T`).

#### Clase Template MutantStack

Muestra clase template que hereda de `std::stack` y añade iteradores, usando `typedef typename`.

Hereda de `std::stack` e implementa iteradores:

```cpp
template <typename T>
class MutantStack : public std::stack<T>
{
public:
    typedef typename std::deque<T>::iterator iterator;
    typedef typename std::deque<T>::reverse_iterator reverse_iterator;
    typedef typename std::deque<T>::const_iterator const_iterator;
    typedef typename std::deque<T>::const_reverse_iterator const_reverse_iterator;
    
    using std::stack<T>::c;
    
    iterator begin();
    iterator end();
    // ... más métodos de iteradores
};
```

`std::stack` es un **adaptador de contenedor** (no un contenedor completo). No proporciona iteradores. `MutantStack`:
1. Hereda de `std::stack<T>`
2. Expone los tipos de iterador del contenedor subyacente (por defecto `std::deque`)
3. Usa `using std::stack<T>::c` para acceder al miembro protegido `c` (el contenedor subyacente)
4. Implementa métodos `begin()`, `end()`, etc. que delegan en `c`

Los `typedef` con `typename` son necesarios porque `std::deque<T>::iterator` es un tipo dependiente.

#### Implementación de Iteradores

Muestra implementación de métodos iteradores que exponen el contenedor subyacente de `std::stack`.

```cpp
template <typename T>
typename MutantStack<T>::iterator MutantStack<T>::begin()
{
    return (c.begin()); 
}

template <typename T>
typename MutantStack<T>::iterator MutantStack<T>::end()
{
    return (c.end()); 
}
```

La implementación es simple: retorna los iteradores del contenedor subyacente `c`. El `typename` antes del tipo de retorno es necesario porque `MutantStack<T>::iterator` es un tipo dependiente.

Esto permite usar `MutantStack` como un contenedor secuencial normal, aunque conceptualmente sea una pila.

### Templates Avanzados en Módulo 09

Subsección que presenta templates utilitarios avanzados para operaciones comunes como impresión.

#### Funciones de Utilidad Genéricas

Muestra templates para imprimir contenedores y verificar si están ordenados, usando iteradores.

```cpp
template <typename T>
void print(const T& container)
{
    typename T::const_iterator it;
    
    for (it = container.begin(); it != container.end(); it++)
        std::cout << *it << " ";
    std::cout << std::endl;
}

template <typename T>
bool isSorted(const T& container)
{
    if (container.empty())
        return (true);
    
    typename T::const_iterator prev = container.begin();
    typename T::const_iterator current = prev;
    current++;
    
    while (current != container.end())
    {
        if (*prev > *current)
            return (false);
        prev++;
        current++;
    }
    return (true);
}
```

Funciones de utilidad genéricas como estas son extremadamente útiles:
- `print`: Imprime cualquier contenedor con iteradores
- `isSorted`: Verifica si cualquier contenedor está ordenado

Ventajas de templates para utilidades:
- Una implementación para todos los contenedores
- Seguridad de tipos (el compilador verifica que los elementos se puedan imprimir o comparar)
- Eficiencia (código específico generado para cada tipo)

---

## Excepciones y Manejo de Errores

Esta sección cubre el sistema de excepciones en C++, incluyendo creación de excepciones personalizadas y manejo.

### Clases de Excepción Personalizadas

Subsección que muestra cómo crear clases de excepción personalizadas heredando de `std::exception`.

#### Excepciones Básicas

Presenta clases de excepción anidadas simples con mensajes fijos, utilizadas para errores específicos.

En el Módulo 05 se definen clases de excepción anidadas:

```cpp
class GradeTooHighException : public std::exception
{
public:
    const char *what() const throw()
    {
        return ("Bureaucrat: TooHighException");
    }
};

class GradeTooLowException : public std::exception
{
public:
    const char *what() const throw()
    {
        return ("Bureaucrat: TooLowException");
    }
};
```

Las excepciones personalizadas deben:
1. Heredar de `std::exception` (o sus derivadas como `std::runtime_error`)
2. Sobrescribir `what()` para retornar una descripción
3. Tener destructor virtual (heredado de `std::exception`)

La especificación `throw()` en `what()` significa que no lanza excepciones (noexcept en C++11+). En C++98, esto ayuda al compilador a optimizar.

Las excepciones anidadas dentro de clases (como `Bureaucrat::GradeTooHighException`) agrupan excepciones relacionadas con esa clase.

#### Excepciones con Constructores Parametrizados

Muestra excepciones con constructores que aceptan parámetros para personalización, almacenando información.

```cpp
class GradeTooHighException : public std::exception
{
public:
    GradeTooHighException(int flag) : _flag(flag) {}
    
    const char *what() const throw();

private:
    int _flag;
};
```

Excepciones con estado permiten:
- Mensajes más informativos
- Diferentes comportamientos según el contexto
- Mejor depuración (más información sobre el error)

El estado se almacena en miembros datos y se usa en `what()` o métodos relacionados.

#### Implementación de what() con Switch

Presenta implementación de `what()` que usa switch para devolver mensajes diferentes según el flag.

```cpp
const char *Form::GradeTooLowException::what() const throw()
{
    switch (_flag)
    {
        case 0: return ("Form: Couldn't create the form, [rank to low]");
        case 1: return ("Form: Couldn't sign the form, [rank to low]");
        case 2: return ("Form: Form already signed");
        default: return ("Form: TooLowException");
    }
}
```

Usar un switch en `what()` permite:
- Una sola clase de excepción para múltiples errores relacionados
- Mensajes específicos según el contexto del error
- Menos clases de excepción (menos código repetitivo)

El flag podría indicar en qué operación falló (crear, firmar, etc.).

### Lanzamiento de Excepciones

Subsección que muestra cómo y dónde lanzar excepciones, incluyendo constructores y métodos que validan.

#### En Constructores

Ejemplo de constructor que lanza excepciones cuando parámetros están fuera de rango, previniendo creación.

```cpp
Bureaucrat::Bureaucrat(std::string name, int grade) : _name(name)
{
    if (MAX_GRADE > grade)
        throw (Bureaucrat::GradeTooHighException());
    if (MIN_GRADE < grade)
        throw (Bureaucrat::GradeTooLowException());
    _grade = grade;
}
```

Lanzar excepciones en constructores es importante cuando:
- Los parámetros son inválidos
- No se pueden adquirir recursos necesarios
- No se puede establecer un estado válido

Si un constructor lanza una excepción:
- El objeto no se construye completamente
- No se llama al destructor (porque el objeto no existe)
- Los miembros ya construidos se destruyen automáticamente (en orden inverso)

#### En Métodos

Muestra método que lanza excepciones cuando operaciones podrían poner al objeto en estado inválido.

```cpp
void Bureaucrat::incrementGrade()
{
    if (MAX_GRADE > (_grade - 1))
        throw (Bureaucrat::GradeTooHighException());
    _grade--;
}
```

Los métodos deben lanzar excepciones cuando:
- No pueden realizar su función
- Los parámetros son inválidos
- El objeto estaría en estado inválido después de la operación
- No se pueden adquirir recursos necesarios

Es mejor lanzar excepciones que retornar códigos de error, porque:
- No se pueden ignorar accidentalmente
- El flujo de control es más claro
- Se separa el código normal del manejo de errores

### Excepciones en Templates

Subsección que muestra cómo lanzar excepciones desde templates, incluyendo excepciones estándar.

#### Lanzamiento en Operadores

Muestra operador de índice en template que lanza `std::out_of_range` cuando el índice está fuera de límites.

```cpp
template <typename T>
T& Array<T>::operator[](int index)
{
    if (index >= _size || index < 0)
        throw (std::out_of_range("Index out of bounds"));
    return (_array[index]);
}
```

Los templates también pueden lanzar excepciones. En este caso:
- Se lanza `std::out_of_range` (excepción estándar)
- El mensaje describe el error
- Esto sigue la convención de los contenedores STL (como `vector::at()`)

Usar excepciones estándar cuando corresponda hace que el código sea más familiar para otros programadores.

#### Excepciones con Mensajes Dinámicos

Presenta creación de mensajes de error dinámicos usando `std::ostringstream`, incorporando valores.

```cpp
std::ostringstream oss;
oss << "Value: [" << value << "] not found in the container.";
throw (std::runtime_error(oss.str()));
```

Mensajes dinámicos son más útiles para depuración. `std::ostringstream` permite:
- Construir mensajes complejos
- Incluir valores variables
- Formatear números, etc.

`std::runtime_error` acepta un `const char*` en su constructor, por lo que `oss.str().c_str()` sería necesario, pero `oss.str()` funciona porque `std::string` se convierte implícitamente a `const char*` (a través de `c_str()`).

### Manejo Complejo de Excepciones

Subsección que muestra patrones avanzados de manejo de excepciones, incluyendo bloques anidados.

#### Bloques try-catch Anidados

Ejemplo de manejo de excepciones en BitcoinExchange donde múltiples operaciones pueden fallar.

En BitcoinExchange:

```cpp
try
{
    dateINT = parse_date(dateStr, "Database");
    exchange = parse_ammount(exchangeStr, "Database");
}
catch(const std::exception& e)
{
    std::cerr << e.what() << '\n';
    continue;
}
```

Bloques try-catch permiten:
- **Contención local de errores**: Un error en una línea no aborta todo el procesamiento
- **Continuación después de errores**: Se puede saltar líneas inválidas y continuar con las siguientes
- **Registro de errores**: Registrar qué salió mal sin detener el programa

Capturar `const std::exception&` es bueno porque:
- Captura todas las excepciones derivadas de `std::exception`
- Por referencia evita copias
- Constante porque generalmente no se modifica

#### Validación Múltiple con Excepciones

Muestra función que valida múltiples condiciones y lanza excepciones específicas, como división por cero.

En RPN:

```cpp
void choose_operator(std::stack<float>& stack, std::string& token)
{
    if (stack.size() < 2)
        throw (std::runtime_error("Error: Not enough numbers."));
    
    double right = stack.top();
    stack.pop();
    double left = stack.top();
    stack.pop();
    
    if (token == "/")
    {
        if (right == 0)
            throw (std::runtime_error("Error: You can't divide by 0."));
        stack.push(left / right);    
    }
}
```

Validación exhaustiva con excepciones:
- Verifica todas las precondiciones
- Lanza excepciones informativas inmediatamente cuando se viola una precondición
- Mensajes claros sobre qué salió mal

Esto es más robusto que verificar después o retornar valores especiales.

### Validación Completa con Excepciones

Presenta función completa que valida entrada exhaustivamente usando múltiples excepciones, asegurando casos.

```cpp
double rpn(std::string& input)
{
    if (input.length() == 0)
        throw (std::runtime_error("Error: Empty argument."));
    
    std::stack<float> stack;
    std::istringstream iss(input);
    std::string token;
    
    while (iss >> token)
    {
        if (check_int(token))
            stack.push(std::atof(token.c_str()));
        else if (token == "+" || token == "-" || token == "*" || token == "/")
            choose_operator(stack, token);
        else
            throw (std::runtime_error("Error: Invalid token: " + token));
    }
    
    if (stack.size() == 0)
        throw (std::runtime_error("Error: Empty argument."));
    if (stack.size() > 1)
        throw (std::runtime_error("Error: Invalid number of symbols."));
    
    return (stack.top());
}
```

Validación completa significa:
- **Validar entrada**: Antes de procesar
- **Validar durante procesamiento**: Cada token
- **Validar resultado**: Después de procesar
- **Mensajes específicos**: Diferentes excepciones/mensajes para diferentes errores

Este enfoque garantiza que la función solo retorna un resultado válido o lanza una excepción explicando por qué falló.

### Excepciones en Algoritmos STL

Muestra cómo validar precondiciones en algoritmos personalizados, lanzando excepciones cuando no se cumplen.

#### Validación en Algoritmos

Ejemplo de algoritmo que verifica tamaño mínimo antes de ejecutar, lanzando excepción informativa.

```cpp
int Span::shortestSpan(void)
{
    if (_myVector.size() < 2)
        throw (std::runtime_error("Can't find the shortestSpan."));
    
    // ... algoritmo
}
```

Algoritmos deben verificar precondiciones:
- ¿Tiene suficientes datos?
- ¿Están los datos en el formato/estado esperado?
- ¿Se pueden adquirir recursos necesarios?

Lanzar excepciones cuando no se cumplen precondiciones es mejor que:
- Retornar valores especiales (pueden ignorarse)
- Comportamiento indefinido (peor opción)
- Aserciones (solo en depuración)

---

## Type Casting

Esta sección cubre los cuatro tipos de conversión en C++, explicando cuándo y cómo usar cada uno.

### static_cast

Subsección que presenta `static_cast` para conversiones seguras y explícitas entre tipos compatibles.

#### Conversiones entre Tipos Primitivos

Muestra `static_cast` para convertir entre tipos numéricos y caracteres, con validación.

```cpp
void write_char(int c)
{
    if (c > 32 && c < 127 && isprint(c))
        std::cout << "char:\t '" << static_cast<char>(c) << "'" << std::endl;
    else
        std::cout << "char:\t Not displayable" << std::endl;
}

void write_int(double d)
{
    int i;
    
    if (d > 2147483647.0)
        std::cout << "int:\t Overflow" << std::endl;
    else if (d < -2147483648.0)
        std::cout << "int:\t Underflow" << std::endl;
    else
    {
        i = static_cast<int>(d);
        std::cout << "int:\t " << i << std::endl;
    }
}
```

`static_cast` es para conversiones seguras y explícitas:
- **Entre tipos relacionados**: Numéricos, punteros en la misma jerarquía, void*
- **No verifica en tiempo de ejecución**: Asume que la conversión es válida
- **Más seguro que C-style cast**: Más visible en el código, menos propenso a errores

En el ejemplo:
1. Conversión de `int` a `char` solo si es imprimible
2. Conversión de `double` a `int` con verificación de desbordamiento
3. `static_cast` hace la conversión una vez verificadas las precondiciones

#### Conversiones Encadenadas

Presenta múltiples conversiones encadenadas usando `static_cast`, transformando un string a diferentes tipos.

```cpp
void print_int(std::string str)
{
    double d;
    int i;
    float f;
    
    d = static_cast<double>(strtod(str.c_str(), NULL));
    i = static_cast<int>(d);
    f = static_cast<float>(d);
    
    // ... mostrar resultados
}
```

Conversiones múltiples pueden ser necesarias. En este ejemplo:
1. String → double (con `strtod`, función de C)
2. double → int (con `static_cast`, posible pérdida de precisión)
3. double → float (con `static_cast`, posible pérdida de precisión)

Cada conversión debe considerarse cuidadosamente por posibles pérdidas o desbordamientos.

### reinterpret_cast

Subsección que explica `reinterpret_cast` para conversiones de bajo nivel entre tipos no relacionados.

#### Conversión de Punteros

Muestra `reinterpret_cast` para serializar punteros a enteros y viceversa, útil para almacenamiento.

```cpp
uintptr_t serialize(Data *ptr)
{
    return (reinterpret_cast<uintptr_t>(ptr));
}

Data *deserialize(uintptr_t raw)
{
    return (reinterpret_cast<Data *>(raw));
}
```

`reinterpret_cast` es para conversiones de bajo nivel y peligrosas:
- **Reinterpreta bits**: No hace conversiones reales, solo reinterpreta los bits
- **Entre tipos no relacionados**: Punteros a enteros, punteros a diferentes tipos
- **Peligroso**: Fácil causar comportamiento indefinido
- **Usos comunes**: Serialización, acceso a hardware, implementación de contenedores de bajo nivel

En el ejemplo:
- `serialize`: Convierte puntero a entero (para almacenar o transmitir)
- `deserialize`: Convierte entero a puntero (recuperar)
- `uintptr_t`: Tipo entero sin signo suficientemente grande para almacenar un puntero

**Advertencia**: Solo usar cuando sea absolutamente necesario y entender completamente las implicaciones.

### dynamic_cast

Subsección que cubre `dynamic_cast` para conversiones seguras en jerarquías polimórficas, identificando tipos.

#### Identificación de Tipos con Punteros

Muestra `dynamic_cast` con punteros que devuelve `nullptr` en fallo, permitiendo intentar conversiones.

```cpp
void identify(Base* p)
{
    {
        A *ptr = dynamic_cast<A *>(p);
        if (ptr)
            std::cout << "Type_PTR: \"A\"";
    }
    {
        B *ptr = dynamic_cast<B *>(p);
        if (ptr)
            std::cout << "Type_PTR: \"B\"";
    }
    {
        C *ptr = dynamic_cast<C *>(p);
        if (ptr)
            std::cout << "Type_PTR: \"C\"";
    }
}
```

`dynamic_cast` es para conversiones seguras en jerarquías polimórficas:
- **Requiere tipos polimórficos**: Al menos una función virtual (generalmente destructor virtual)
- **Con punteros**: Retorna `nullptr` si falla
- **Con referencias**: Lanza `std::bad_cast` si falla
- **Verificación en tiempo de ejecución**: Usa RTTI (Run-Time Type Information)

En el ejemplo, se prueba convertir un puntero `Base*` a diferentes tipos derivados. Solo una conversión tendrá éxito (o ninguna si es `nullptr`).

#### Identificación de Tipos con Referencias

Presenta `dynamic_cast` con referencias que lanza excepciones en fallo, requiriendo bloques try-catch.

```cpp
void identify(Base& p)
{
    try
    {
        A ptr = dynamic_cast<A &>(p);
        std::cout << "Type_REF: \"A\"" << std::endl;
    }
    catch(const std::exception& e)
    {
        PRINT_DEBUG(e.what());
    }
    // ... más tipos
}
```

Con referencias, `dynamic_cast` lanza `std::bad_cast` si falla. Razón:
- Las referencias no pueden ser null
- No hay valor "válido" para retornar en caso de fallo
- Por lo tanto, debe lanzar una excepción

Esto requiere bloques try-catch alrededor de cada conversión.

---
