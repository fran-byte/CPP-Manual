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
17. [Conclusiones y Próximos Pasos](#conclusiones-y-próximos-pasos)

---

## Introducción

Esta sección presenta el manual y su propósito, explicando que está diseñado para guiar a través del repositorio de los proyectos CPP de 42 que contiene 10 módulos progresivos que enseñan C++ desde lo básico hasta conceptos avanzados utilizando el estándar C++98.

Este manual está diseñado para llevarte desde cero hasta el nivel necesario para resolver todos los ejercicios del repositorio **CPP_Piscine**. El repositorio contiene 10 módulos progresivos que enseñan C++ siguiendo el estándar C++98, desde conceptos básicos hasta programación avanzada con STL.<cite/>

### Estructura del Repositorio

Presenta una tabla organizada de los 10 módulos del repositorio, mostrando el enfoque principal y ejercicios clave de cada uno para proporcionar una visión general del aprendizaje progresivo.

El repositorio está organizado en 10 módulos, cada uno enfocado en conceptos específicos:<cite/>

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

---

## Fundamentos de C++

Esta sección cubre los conceptos básicos esenciales de programación en C++, incluyendo la estructura de programas, directivas de preprocesador y sistemas de compilación con Makefiles.

### Estructura Básica de un Programa

Explica que todo programa C++ comienza con la función `main()`, mostrando un ejemplo práctico del ejercicio PhoneBook que ilustra un bucle principal de entrada de usuario.

Todo programa en C++ comienza con la función `main()`. Observa la estructura básica en el ejercicio PhoneBook:<cite/>

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

### Directivas de Preprocesador

Describe las directivas `#include` para incluir cabeceras, diferenciando entre cabeceras estándar de la biblioteca y cabeceras personalizadas del proyecto.

Las directivas `#include` permiten incluir cabeceras. En este repositorio se usan dos tipos:<cite/>

```cpp
// Cabeceras estándar
#include <iostream>
#include <string>
#include <fstream>

// Cabeceras propias
#include "PhoneBook.hpp"
```

### Compilación y Makefiles

Muestra el sistema de compilación estandarizado usado en todos los módulos, con Makefiles que siguen el estándar C++98 y configuraciones de flags específicas.

Todos los módulos usan un sistema de compilación consistente con Makefiles que siguen el estándar C++98:<cite/>

```makefile
CXX = c++
CXXFLAGS = -Wall -Wextra -Werror -Wshadow -std=c++98 -I inc
```

---

## Variables y Tipos de Datos

Esta sección presenta los tipos de datos fundamentales en C++, métodos de declaración e inicialización, y el uso de constantes para valores inmutables.

### Tipos Fundamentales

Lista los tipos básicos de datos utilizados en los ejercicios del repositorio, incluyendo tipos primitivos y la clase `std::string` para manejo de cadenas.

En los ejercicios del repositorio encontrarás los siguientes tipos básicos:<cite/>

```cpp
int         // Números enteros
float       // Números decimales de precisión simple
double      // Números decimales de precisión doble
char        // Caracteres
bool        // Valores booleanos (true/false)
std::string // Cadenas de texto
```

### Declaración e Inicialización

Muestra ejemplos prácticos de declaración e inicialización de variables, usando el ejercicio BitcoinExchange para ilustrar tipos comunes.

Ejemplo del ejercicio BitcoinExchange:<cite/>

```cpp
int dateINT;
float ammount;
std::string line;
std::map<int, float> database;
```

### Constantes

Explica el uso de la palabra clave `const` para declarar valores inmutables, con ejemplos tomados del ejercicio Fixed.

Usa `const` para declarar valores inmutables:<cite/>

```cpp
Fixed const b(10);
Fixed const c(42.42f);
```

---

## Operadores

Esta sección cubre los diferentes tipos de operadores en C++, incluyendo operadores aritméticos, de comparación y de asignación.

### Operadores Aritméticos

Muestra operadores aritméticos básicos implementados mediante sobrecarga en el ejercicio Fixed, permitiendo operaciones matemáticas con objetos.

En el ejercicio Fixed se implementan operaciones aritméticas con sobrecarga:<cite/>

```cpp
Fixed a;  // Ya lo veremos más adelante pero Fixed es un tipo de objeto.
Fixed b;
Fixed result = a + b;  // Suma
result = a - b;        // Resta
result = a * b;        // Multiplicación
result = a / b;        // División
```

### Operadores de Comparación

Presenta operadores de comparación comunes utilizados en estructuras condicionales para evaluar relaciones entre valores.

```cpp
if (a == b)  // Igualdad
if (a != b)  // Desigualdad
if (a < b)   // Menor que
if (a > b)   // Mayor que
```

### Operadores de Asignación

Explica operadores de asignación simple y compuestos que modifican el valor de variables u objetos mediante operaciones combinadas.

```cpp
a = b;        // Asignación simple
a += b;       // Suma y asignación
a -= b;       // Resta y asignación
```

---

## Control de Flujo

Esta sección describe estructuras de control para dirigir la ejecución del programa, incluyendo condicionales y bucles.

### Condicionales if-else

Muestra estructuras condicionales utilizadas en el ejercicio PhoneBook para procesar comandos de entrada del usuario.

Ejemplo del ejercicio PhoneBook:<cite/>

```cpp
if (input == "EXIT" || input == "E")
    PB->print_error("\033[0;31mExit program.\033[0m");
if (input == "ADD" || input == "A")
{
    std::cout << "\e[0;32mAdding contact...\e[0;37m" << std::endl;
    PB->add_contact();
}
```

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

---

## Funciones

Esta sección cubre la creación y uso de funciones en C++, incluyendo declaración, definición, parámetros, retorno y sobrecarga.

### Declaración y Definición

Explica la separación entre declaración (prototipo) en archivos de cabecera y definición (implementación) en archivos de código fuente.

Las funciones en C++ tienen una declaración (prototipo) y una definición:<cite/>

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

### Parámetros y Retorno

Muestra ejemplos de funciones con parámetros y valores de retorno, ilustrando cómo las funciones procesan datos.

```cpp
int parse_date(std::string& dateString, std::string file)
{
    std::tm date = {};
    // ... procesamiento
    return (convert_date_to_int(date));
}
```

### Sobrecarga de Funciones

Presenta el concepto de sobrecarga de funciones, permitiendo múltiples funciones con el mismo nombre pero diferentes parámetros.

Puedes tener múltiples funciones con el mismo nombre pero diferentes parámetros:<cite/>

```cpp
void addNumber(int value);
void addArray(int array[], size_t size);
void addRange(int min, int max);
```

---

## Arrays y Strings

Esta sección cubre estructuras de datos básicas para almacenamiento de elementos, incluyendo arrays estáticos y cadenas de texto.

### Arrays Estáticos

Muestra la declaración e inicialización de arrays estáticos con tamaño fijo, y cómo calcular el tamaño del array.

```cpp
int const amounts[] = {42, 54, 957, 432, 1234, 0, 754, 16576};
size_t const amounts_size = sizeof(amounts) / sizeof(int);
```

### std::string

Presenta la clase `std::string` como alternativa segura y flexible a arrays de caracteres, con métodos para entrada/salida.

La clase `std::string` proporciona operaciones seguras con cadenas:<cite/>

```cpp
std::string input;
std::getline(std::cin, input);

if (input == "EXIT" || input == "E")
    // procesar
```

### std::vector

Introduce `std::vector` como contenedor dinámico versátil de la STL, mostrando operaciones básicas como inserción.

Contenedor dinámico usado extensivamente en los ejercicios:<cite/>

```cpp
std::vector<int> _myVector;
std::vector<int> sortedNumbers = _myVector;
std::sort(sortedNumbers.begin(), sortedNumbers.end());
```

---

## Punteros y Referencias

Esta sección explica mecanismos para manejar memoria y crear alias de variables, fundamentales para gestión de recursos.

### Punteros

Describe punteros como variables que almacenan direcciones de memoria, con ejemplos de uso en el ejercicio Animal/Brain.

Los punteros almacenan direcciones de memoria. En el ejercicio Animal/Brain:<cite/>

```cpp
Brain* brain;  // Puntero a un objeto Brain

// En el constructor
brain = new Brain();

// En el destructor
delete brain;
```

### Referencias

Explica referencias como alias de variables existentes, mostrando ejemplos de referencias constantes y referencias a punteros.

Las referencias son alias de otras variables:<cite/>

```cpp
std::string const & getType() const;  // Referencia constante
AMateria* & getMateria(int idx);      // Referencia a puntero
```

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

#### Arrays dinámicos

Presenta la creación y eliminación de arrays dinámicos usando `new[]` y `delete[]`, con ejemplo de array de enteros.

```cpp
// Crear array dinámico
int* mirror = new int[MAX_VAL];

// Liberar array dinámico
delete [] mirror;
```

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

#### Constructores

Presenta diferentes tipos de constructores: por defecto y de copia, con ejemplos que muestran inicialización.

```cpp
// Constructor por defecto
PhoneBook::PhoneBook() : _id(0)
{
    // inicialización
}

// Constructor de copia
Cat::Cat(const Cat& f) : Animal(f)
{
    brain = NULL;
    *this = f;
}
```

#### Destructor

Ejemplo de destructor que libera memoria dinámica, mostrando la importancia de limpieza de recursos.

```cpp
Cat::~Cat()
{
    delete brain;
}
```

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
    void makeSound() const override;     // Sobrescritura
};
```

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
    zoo[i]->makeSound();  // Llamada polimórfica
```

### Sobrecarga de Operadores

Subsección que explica cómo redefinir operadores para clases personalizadas, permitiendo sintaxis intuitiva.

#### Operador de Asignación

Muestra la implementación del operador de asignación con gestión correcta de memoria y verificación de auto-asignación.

```cpp
Cat& Cat::operator=(const Cat& f)
{
    if (this != &f)
    {
        _type = f._type;
        if (brain)
            delete brain;
        brain = new Brain(*f.brain);
    }
    return (*this);
}
```

#### Operadores de Stream

Ejemplo de sobrecarga del operador `<<` para salida personalizada de objetos, permitiendo integración con flujos.

```cpp
std::ostream& operator<<(std::ostream& os, const Fixed& fixed)
{
    os << fixed.toFloat();
    return os;
}
```

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

### Deep Copy vs Shallow Copy

Subsección que contrasta dos enfoques de copia de objetos, destacando los problemas de shallow copy.

#### Shallow Copy (Problemático)

Muestra copia superficial que duplica punteros pero no datos, causando problemas cuando objetos comparten memoria.

```cpp
// Solo copia el puntero, no los datos
brain = f.brain;  // ¡Ambos objetos apuntan al mismo Brain!
```

#### Deep Copy (Correcto)

Presenta copia profunda que crea nuevos objetos independientes, asegurando que cada objeto tenga sus recursos.

```cpp
// Crea una nueva copia de los datos
brain = new Brain(*f.brain);  // Cada objeto tiene su propio Brain
```

---

## STL - Standard Template Library

Esta sección introduce la biblioteca estándar de plantillas de C++, cubriendo contenedores, algoritmos e iteradores.

### Contenedores

Subsección que presenta diferentes tipos de contenedores STL para almacenamiento de datos, cada uno optimizado.

#### std::vector

Describe `std::vector` como contenedor dinámico de array redimensionable, mostrando operación básica de inserción.

Contenedor dinámico usado en múltiples ejercicios:<cite/>

```cpp
std::vector<int> _myVector;
_myVector.push_back(value);  // Agregar elemento
```

#### std::map

Presenta `std::map` como contenedor asociativo clave-valor ordenado, usado en BitcoinExchange para mapear.

Contenedor asociativo clave-valor, usado en BitcoinExchange:<cite/>

```cpp
std::map<int, float> database;
database[date] = exchangeRate;
```

#### std::list

Muestra `std::list` como lista doblemente enlazada, utilizada en PmergeMe para pruebas comparativas.

Lista enlazada usada en PmergeMe:<cite/>

```cpp
std::list<int> new_list;
for (size_t i = 0; i < vector.size(); i++)
    new_list.push_back(vector[i]);
```

### Algoritmos STL

Subsección que cubre algoritmos genéricos de la STL para operaciones comunes como ordenamiento y búsqueda.

#### std::sort

Muestra `std::sort` para ordenar elementos en contenedores, trabajando con iteradores para definir rangos.

```cpp
std::vector<int> sortedNumbers = _myVector;
std::sort(sortedNumbers.begin(), sortedNumbers.end());
```

#### std::max_element y std::min_element

Presenta algoritmos para encontrar elementos extremos en contenedores, devolviendo iteradores a valores.

```cpp
std::vector<int>::iterator minIt = std::min_element(_myVector.begin(), _myVector.end());
std::vector<int>::iterator maxIt = std::max_element(_myVector.begin(), _myVector.end());
```

#### std::find

Ejemplo de `std::find` en función template que busca valores en contenedores, combinado con `std::distance`.

Usado en el ejercicio easyFind:<cite/>

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

#### std::lower_bound

Muestra `std::lower_bound` para búsqueda binaria eficiente en contenedores ordenados como `std::map`.

Usado en BitcoinExchange para búsqueda binaria eficiente:<cite/>

```cpp
std::map<int, float>::iterator it = database.lower_bound(dateINT);
if (it != database.begin())
    --it;
```

### Iteradores

Explica iteradores como abstracciones para recorrer contenedores de manera uniforme, mostrando diferentes tipos.

Los iteradores permiten recorrer contenedores de manera uniforme:<cite/>

```cpp
// Iterador constante
std::vector<int>::const_iterator it;

// Iterador reverso
std::vector<int>::reverse_iterator rit;

// Uso en MutantStack
typename MutantStack<T>::iterator begin();
typename MutantStack<T>::iterator end();
```

---

## Entrada/Salida de Archivos (I/O)

Esta sección cubre operaciones de lectura y escritura de archivos en C++, incluyendo streams y manejo de errores.

### Streams de Archivos

Subsección que presenta clases para trabajar con archivos, diferenciando entre streams de entrada y salida.

#### std::ifstream (Lectura)

Muestra `std::ifstream` para leer archivos, con ejemplo de BitcoinExchange que procesa líneas de CSV.

Usado en BitcoinExchange para leer el archivo CSV:<cite/>

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

#### std::ofstream (Escritura)

Presenta `std::ofstream` para escribir archivos, encapsulado en clase Files que gestiona ambos tipos de streams.

Implementado en el ejercicio Files:<cite/>

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

### Formato de Archivos

Subsección que cubre procesamiento de formatos de archivo específicos, con énfasis en parsing de CSV.

#### CSV Parsing

Ejemplo de parsing de archivos CSV usando `std::istringstream` y `std::getline`, extrayendo campos.

En BitcoinExchange se procesan archivos CSV:<cite/>

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

---

## Algoritmos Avanzados

Esta sección presenta algoritmos complejos implementados en los ejercicios, incluyendo ordenamiento y búsqueda.

### Algoritmos de Ordenamiento

Subsección que cubre algoritmos de ordenamiento, con énfasis en algoritmos híbridos que combinan estrategias.

#### Merge-Insertion Sort

Muestra implementación de algoritmo híbrido que combina merge sort e insertion sort, usado en PmergeMe.

Implementado en PmergeMe para comparar rendimiento:<cite/>

```cpp
// Versión para std::vector
void vector_mergeInsertionSort(std::vector<int>& vector)
{
    if (vector.size() <= 1)
        return;
    
    // Algoritmo de merge-insertion sort
}
```

### Búsqueda Binaria con std::map

Presenta uso de `std::lower_bound` para búsqueda binaria eficiente en mapas ordenados en BitcoinExchange.

Usado en BitcoinExchange para búsqueda eficiente:<cite/>

```cpp
std::map<int, float>::iterator it = database.lower_bound(dateINT);
if (it != database.begin() && (it == database.end() || it->first != dateINT))
    --it;
```

### Algoritmo RPN (Notación Polaca Inversa)

Muestra implementación de calculadora RPN que procesa expresiones matemáticas usando pila, con validación.

Implementado en el ejercicio RPN:<cite/>

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

### Algoritmos de Validación

Subsección que presenta funciones de validación para datos como fechas y números, esenciales para procesamiento.

#### Validación de Fechas

Muestra funciones para validar y convertir fechas, incluyendo parsing de strings y conversión a formatos.

```cpp
bool is_valid_date(const std::tm& date);
int convert_date_to_int(std::tm& date);
int parse_date(std::string& dateString, std::string file);
```

#### Validación de Números

Presenta funciones para verificar formatos numéricos en strings, asegurando que datos sean válidos.

```cpp
bool check_int(std::string& str);
bool check_float(std::string& str);
```

### Medición de Rendimiento

Muestra técnicas para medir tiempo de ejecución usando `clock()`, comparando rendimiento de algoritmos.

En PmergeMe se compara el rendimiento entre diferentes contenedores:<cite/>

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

---

## Templates y Programación Genérica

Esta sección cubre templates como mecanismo para programación genérica en C++, permitiendo código reutilizable.

### Templates de Funciones

Subsección que presenta templates de funciones, mostrando cómo crear funciones genéricas que trabajan con cualquier tipo.

#### Templates Básicos

Muestra templates simples para operaciones comunes como intercambio, mínimo y máximo, que funcionan con cualquier tipo.

En el Módulo 07 se implementan templates genéricos para funciones básicas:<cite/>

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

#### Templates con Functors

Presenta función template que aplica un functor a elementos de array, combinando templates de tipos y funciones.

Función template `iter` que aplica una función a cada elemento de un array:<cite/>

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

### Templates de Clases

Subsección que cubra templates de clases, mostrando cómo crear clases genéricas que encapsulan estructuras.

#### Clase Template Array

Muestra clase template completa para array dinámico genérico, con constructores, destructor y operadores.

Implementación completa con constructores, destructor y operadores:<cite/>

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

### Templates con Contenedores STL

Subsección que muestra templates avanzados que interactúan con contenedores STL, creando funciones genéricas.

#### Función easyFind

Presenta función template que busca elementos en cualquier contenedor STL compatible, usando iteradores.

Template que funciona con cualquier contenedor:<cite/>

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

#### Clase Template MutantStack

Muestra clase template que hereda de `std::stack` y añade iteradores, usando `typedef typename`.

Hereda de `std::stack` e implementa iteradores:<cite/>

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

---

## Excepciones y Manejo de Errores

Esta sección cubre el sistema de excepciones en C++, incluyendo creación de excepciones personalizadas y manejo.

### Clases de Excepción Personalizadas

Subsección que muestra cómo crear clases de excepción personalizadas heredando de `std::exception`.

#### Excepciones Básicas

Presenta clases de excepción anidadas simples con mensajes fijos, utilizadas para errores específicos.

En el Módulo 05 se definen clases de excepción anidadas:<cite/>

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

#### Excepciones con Mensajes Dinámicos

Presenta creación de mensajes de error dinámicos usando `std::ostringstream`, incorporando valores.

```cpp
std::ostringstream oss;
oss << "Value: [" << value << "] not found in the container.";
throw (std::runtime_error(oss.str()));
```

### Manejo Complejo de Excepciones

Subsección que muestra patrones avanzados de manejo de excepciones, incluyendo bloques anidados.

#### Bloques try-catch Anidados

Ejemplo de manejo de excepciones en BitcoinExchange donde múltiples operaciones pueden fallar.

En BitcoinExchange:<cite/>

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

#### Validación Múltiple con Excepciones

Muestra función que valida múltiples condiciones y lanza excepciones específicas, como división por cero.

En RPN:<cite/>

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

---


