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

Este manual está diseñado para llevarte desde cero hasta el nivel necesario para resolver todos los ejercicios del repositorio **CPP_Piscine**. El repositorio contiene 10 módulos progresivos que enseñan C++ siguiendo el estándar C++98, desde conceptos básicos hasta programación avanzada con STL.<cite/>

### Estructura del Repositorio

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

### Estructura Básica de un Programa

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

Todos los módulos usan un sistema de compilación consistente con Makefiles que siguen el estándar C++98:<cite/>

```makefile
CXX = c++
CXXFLAGS = -Wall -Wextra -Werror -Wshadow -std=c++98 -I inc
```

---

## Variables y Tipos de Datos

### Tipos Fundamentales

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

Ejemplo del ejercicio BitcoinExchange:<cite/>

```cpp
int dateINT;
float ammount;
std::string line;
std::map<int, float> database;
```

### Constantes

Usa `const` para declarar valores inmutables:<cite/>

```cpp
Fixed const b(10);
Fixed const c(42.42f);
```

---

## Operadores

### Operadores Aritméticos

En el ejercicio Fixed se implementan operaciones aritméticas con sobrecarga:<cite/>

```cpp
Fixed a;
Fixed b;
Fixed result = a + b;  // Suma
result = a - b;        // Resta
result = a * b;        // Multiplicación
result = a / b;        // División
```

### Operadores de Comparación

```cpp
if (a == b)  // Igualdad
if (a != b)  // Desigualdad
if (a < b)   // Menor que
if (a > b)   // Mayor que
```

### Operadores de Asignación

```cpp
a = b;        // Asignación simple
a += b;       // Suma y asignación
a -= b;       // Resta y asignación
```

---

## Control de Flujo

### Condicionales if-else

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

#### Bucle for

```cpp
for (int i = 0; i < limit; i++)
{
    aux = &_agenda[i % 8];
    grid_printItem(std::to_string(i % 8));
}
```

#### Bucle while

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

### Declaración y Definición

Las funciones en C++ tienen una declaración (prototipo) y una definición:<cite/>

```cpp
// Declaración en el header
void add_contact();
void search_and_print_contact();

// Definición en el archivo .cpp
void PhoneBook::add_contact()
{
    // Implementación
}
```

### Parámetros y Retorno

```cpp
int parse_date(std::string& dateString, std::string file)
{
    std::tm date = {};
    // ... procesamiento
    return (convert_date_to_int(date));
}
```

### Sobrecarga de Funciones

Puedes tener múltiples funciones con el mismo nombre pero diferentes parámetros:<cite/>

```cpp
void addNumber(int value);
void addArray(int array[], size_t size);
void addRange(int min, int max);
```

---

## Arrays y Strings

### Arrays Estáticos

```cpp
int const amounts[] = {42, 54, 957, 432, 1234, 0, 754, 16576};
size_t const amounts_size = sizeof(amounts) / sizeof(int);
```

### std::string

La clase `std::string` proporciona operaciones seguras con cadenas:<cite/>

```cpp
std::string input;
std::getline(std::cin, input);

if (input == "EXIT" || input == "E")
    // procesar
```

### std::vector

Contenedor dinámico usado extensivamente en los ejercicios:<cite/>

```cpp
std::vector<int> _myVector;
std::vector<int> sortedNumbers = _myVector;
std::sort(sortedNumbers.begin(), sortedNumbers.end());
```

---

## Punteros y Referencias

### Punteros

Los punteros almacenan direcciones de memoria. En el ejercicio Animal/Brain:<cite/>

```cpp
Brain* brain;  // Puntero a un objeto Brain

// En el constructor
brain = new Brain();

// En el destructor
delete brain;
```

### Referencias

Las referencias son alias de otras variables:<cite/>

```cpp
std::string const & getType() const;  // Referencia constante
AMateria* & getMateria(int idx);      // Referencia a puntero
```

### Gestión de Memoria

#### new y delete

```cpp
// Asignación dinámica
AMateria* materia = new Ice();

// Liberación de memoria
delete materia;
```

#### Arrays dinámicos

```cpp
// Crear array dinámico
int* mirror = new int[MAX_VAL];

// Liberar array dinámico
delete [] mirror;
```

---

## Programación Orientada a Objetos

### Clases y Objetos

#### Definición de Clase

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

```cpp
Cat::~Cat()
{
    delete brain;
}
```

### Herencia

#### Herencia Simple

```cpp
class ScavTrap : public virtual ClapTrap
{
public:
    ScavTrap();
    void guardGate();
};
```

#### Herencia Múltiple y Virtual

```cpp
class DiamondTrap : public ScavTrap, public FragTrap
{
public:
    DiamondTrap();
    void whoAmI();
};
```

### Polimorfismo

#### Funciones Virtuales

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

#### Operador de Asignación

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

```cpp
std::ostream& operator<<(std::ostream& os, const Fixed& fixed)
{
    os << fixed.toFloat();
    return os;
}
```

---

## Gestión de Memoria

### Rule of Three

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

#### Shallow Copy (Problemático)

```cpp
// Solo copia el puntero, no los datos
brain = f.brain;  // ¡Ambos objetos apuntan al mismo Brain!
```

#### Deep Copy (Correcto)

```cpp
// Crea una nueva copia de los datos
brain = new Brain(*f.brain);  // Cada objeto tiene su propio Brain
```

---

## STL - Standard Template Library

### Contenedores

#### std::vector

Contenedor dinámico usado en múltiples ejercicios:<cite/>

```cpp
std::vector<int> _myVector;
_myVector.push_back(value);  // Agregar elemento
```

#### std::map

Contenedor asociativo clave-valor, usado en BitcoinExchange:<cite/>

```cpp
std::map<int, float> database;
database[date] = exchangeRate;
```

#### std::list

Lista enlazada usada en PmergeMe:<cite/>

```cpp
std::list<int> new_list;
for (size_t i = 0; i < vector.size(); i++)
    new_list.push_back(vector[i]);
```

### Algoritmos STL

#### std::sort

```cpp
std::vector<int> sortedNumbers = _myVector;
std::sort(sortedNumbers.begin(), sortedNumbers.end());
```

#### std::max_element y std::min_element

```cpp
std::vector<int>::iterator minIt = std::min_element(_myVector.begin(), _myVector.end());
std::vector<int>::iterator maxIt = std::max_element(_myVector.begin(), _myVector.end());
```

#### std::find

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

Usado en BitcoinExchange para búsqueda binaria eficiente:<cite/>

```cpp
std::map<int, float>::iterator it = database.lower_bound(dateINT);
if (it != database.begin())
    --it;
```

### Iteradores

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

### Streams de Archivos

#### std::ifstream (Lectura)

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

#### CSV Parsing

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

### Algoritmos de Ordenamiento

#### Merge-Insertion Sort

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

Usado en BitcoinExchange para búsqueda eficiente:<cite/>

```cpp
std::map<int, float>::iterator it = database.lower_bound(dateINT);
if (it != database.begin() && (it == database.end() || it->first != dateINT))
    --it;
```

### Algoritmo RPN (Notación Polaca Inversa)

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

#### Validación de Fechas

```cpp
bool is_valid_date(const std::tm& date);
int convert_date_to_int(std::tm& date);
int parse_date(std::string& dateString, std::string file);
```

#### Validación de Números

```cpp
bool check_int(std::string& str);
bool check_float(std::string& str);
```

### Medición de Rendimiento

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

### Templates de Funciones

#### Templates Básicos

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

#### Clase Template Array

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

#### Función easyFind

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

#### Funciones de Utilidad Genéricas

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

### Clases de Excepción Personalizadas

#### Excepciones Básicas

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

#### En Constructores

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

```cpp
void Bureaucrat::incrementGrade()
{
    if (MAX_GRADE > (_grade - 1))
        throw (Bureaucrat::GradeTooHighException());
    _grade--;
}
```

### Excepciones en Templates

#### Lanzamiento en Operadores

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

```cpp
std::ostringstream oss;
oss << "Value: [" << value << "] not found in the container.";
throw (std::runtime_error(oss.str()));
```

### Manejo Complejo de Excepciones

#### Bloques try-catch Anidados

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

#### Validación en Algoritmos

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

### static_cast

#### Conversiones entre Tipos Primitivos

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

#### Conversión de Punteros

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

#### Identificación de Tipos con Punteros

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

## Conclusiones y Próximos Pasos

### Resumen del Recorrido

Este manual ha cubierto todos los conceptos necesarios para completar los 10 módulos del repositorio CPP_Piscine:

1. **Fundamentos básicos** de C++ (Módulos 00-01)
2. **Programación orientada a objetos** con clases, herencia y polimorfismo (Módulos 02-04)
3. **Manejo avanzado de errores** con excepciones personalizadas (Módulo 05)
4. **Conversiones de tipo** con los cuatro tipos de casting (Módulo 06)
5. **Programación genérica** con templates (Módulo 07)
6. **Contenedores y algoritmos STL** (Módulo 08)
7. **Algoritmos avanzados** y estructuras de datos complejas (Módulo 09)

### Habilidades Desarrolladas

A lo largo de estos módulos, has desarrollado habilidades en:

- **Diseño de clases** siguiendo principios SOLID
- **Gestión de memoria** manual y automática
- **Sobrecarga de operadores** y funciones
- **Patrones de diseño** como Factory, Singleton, etc.
- **Algoritmos eficientes** con complejidad temporal y espacial
- **Templates** para programación genérica
- **STL** para estructuras de datos y algoritmos predefinidos

### Próximos Pasos Recomendados

1. **Proyectos personales**: Aplica estos conceptos en proyectos propios
2. **Estándares modernos**: Explora C++11, C++14, C++17 y C++20
3. **Patrones de diseño**: Estudia patrones avanzados como Observer, Strategy, etc.
4. **Optimización**: Aprende técnicas de profiling y optimización de código
5. **Contribuir a open source**: Participa en proyectos de código abierto
6. **Especialización**: Enfócate en áreas como game dev, sistemas embebidos, HPC, etc.

### Recursos Adicionales

- **Documentación oficial**: cppreference.com
- **Comunidades**: Stack Overflow, Reddit r/cpp, CppCon
- **Libros recomendados**:
  - "Effective Modern C++" de Scott Meyers
  - "The C++ Programming Language" de Bjarne Stroustrup
  - "C++ Templates: The Complete Guide" de David Vandevoorde

### Consejos Finales

1. **Practica regularmente**: La consistencia es clave para dominar C++
2. **Revisa código de otros**: Aprende de proyectos open source bien estructurados
3. **Escribe código limpio**: Sigue guías de estilo y principios de clean code
4. **Aprende herramientas**: Dominia debuggers (gdb), profilers (valgrind), y build systems (CMake)
5. **Mantente actualizado**: C++ evoluciona constantemente

¡Felicidades por completar este recorrido por C++! Has desarrollado una base sólida que te permitirá enfrentar desafíos de # Manual Completo de C++ - CPP 42

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

Este manual está diseñado para llevarte desde cero hasta el nivel necesario para resolver todos los ejercicios del repositorio **CPP_Piscine**. El repositorio contiene 10 módulos progresivos que enseñan C++ siguiendo el estándar C++98, desde conceptos básicos hasta programación avanzada con STL.<cite/>

### Estructura del Repositorio

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

### Estructura Básica de un Programa

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

Todos los módulos usan un sistema de compilación consistente con Makefiles que siguen el estándar C++98:<cite/>

```makefile
CXX = c++
CXXFLAGS = -Wall -Wextra -Werror -Wshadow -std=c++98 -I inc
```

---

## Variables y Tipos de Datos

### Tipos Fundamentales

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

Ejemplo del ejercicio BitcoinExchange:<cite/>

```cpp
int dateINT;
float ammount;
std::string line;
std::map<int, float> database;
```

### Constantes

Usa `const` para declarar valores inmutables:<cite/>

```cpp
Fixed const b(10);
Fixed const c(42.42f);
```

---

## Operadores

### Operadores Aritméticos

En el ejercicio Fixed se implementan operaciones aritméticas con sobrecarga:<cite/>

```cpp
Fixed a;
Fixed b;
Fixed result = a + b;  // Suma
result = a - b;        // Resta
result = a * b;        // Multiplicación
result = a / b;        // División
```

### Operadores de Comparación

```cpp
if (a == b)  // Igualdad
if (a != b)  // Desigualdad
if (a < b)   // Menor que
if (a > b)   // Mayor que
```

### Operadores de Asignación

```cpp
a = b;        // Asignación simple
a += b;       // Suma y asignación
a -= b;       // Resta y asignación
```

---

## Control de Flujo

### Condicionales if-else

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

#### Bucle for

```cpp
for (int i = 0; i < limit; i++)
{
    aux = &_agenda[i % 8];
    grid_printItem(std::to_string(i % 8));
}
```

#### Bucle while

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

### Declaración y Definición

Las funciones en C++ tienen una declaración (prototipo) y una definición:<cite/>

```cpp
// Declaración en el header
void add_contact();
void search_and_print_contact();

// Definición en el archivo .cpp
void PhoneBook::add_contact()
{
    // Implementación
}
```

### Parámetros y Retorno

```cpp
int parse_date(std::string& dateString, std::string file)
{
    std::tm date = {};
    // ... procesamiento
    return (convert_date_to_int(date));
}
```

### Sobrecarga de Funciones

Puedes tener múltiples funciones con el mismo nombre pero diferentes parámetros:<cite/>

```cpp
void addNumber(int value);
void addArray(int array[], size_t size);
void addRange(int min, int max);
```

---

## Arrays y Strings

### Arrays Estáticos

```cpp
int const amounts[] = {42, 54, 957, 432, 1234, 0, 754, 16576};
size_t const amounts_size = sizeof(amounts) / sizeof(int);
```

### std::string

La clase `std::string` proporciona operaciones seguras con cadenas:<cite/>

```cpp
std::string input;
std::getline(std::cin, input);

if (input == "EXIT" || input == "E")
    // procesar
```

### std::vector

Contenedor dinámico usado extensivamente en los ejercicios:<cite/>

```cpp
std::vector<int> _myVector;
std::vector<int> sortedNumbers = _myVector;
std::sort(sortedNumbers.begin(), sortedNumbers.end());
```

---

## Punteros y Referencias

### Punteros

Los punteros almacenan direcciones de memoria. En el ejercicio Animal/Brain:<cite/>

```cpp
Brain* brain;  // Puntero a un objeto Brain

// En el constructor
brain = new Brain();

// En el destructor
delete brain;
```

### Referencias

Las referencias son alias de otras variables:<cite/>

```cpp
std::string const & getType() const;  // Referencia constante
AMateria* & getMateria(int idx);      // Referencia a puntero
```

### Gestión de Memoria

#### new y delete

```cpp
// Asignación dinámica
AMateria* materia = new Ice();

// Liberación de memoria
delete materia;
```

#### Arrays dinámicos

```cpp
// Crear array dinámico
int* mirror = new int[MAX_VAL];

// Liberar array dinámico
delete [] mirror;
```

---

## Programación Orientada a Objetos

### Clases y Objetos

#### Definición de Clase

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

```cpp
Cat::~Cat()
{
    delete brain;
}
```

### Herencia

#### Herencia Simple

```cpp
class ScavTrap : public virtual ClapTrap
{
public:
    ScavTrap();
    void guardGate();
};
```

#### Herencia Múltiple y Virtual

```cpp
class DiamondTrap : public ScavTrap, public FragTrap
{
public:
    DiamondTrap();
    void whoAmI();
};
```

### Polimorfismo

#### Funciones Virtuales

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

#### Operador de Asignación

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

```cpp
std::ostream& operator<<(std::ostream& os, const Fixed& fixed)
{
    os << fixed.toFloat();
    return os;
}
```

---

## Gestión de Memoria

### Rule of Three

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

#### Shallow Copy (Problemático)

```cpp
// Solo copia el puntero, no los datos
brain = f.brain;  // ¡Ambos objetos apuntan al mismo Brain!
```

#### Deep Copy (Correcto)

```cpp
// Crea una nueva copia de los datos
brain = new Brain(*f.brain);  // Cada objeto tiene su propio Brain
```

---

## STL - Standard Template Library

### Contenedores

#### std::vector

Contenedor dinámico usado en múltiples ejercicios:<cite/>

```cpp
std::vector<int> _myVector;
_myVector.push_back(value);  // Agregar elemento
```

#### std::map

Contenedor asociativo clave-valor, usado en BitcoinExchange:<cite/>

```cpp
std::map<int, float> database;
database[date] = exchangeRate;
```

#### std::list

Lista enlazada usada en PmergeMe:<cite/>

```cpp
std::list<int> new_list;
for (size_t i = 0; i < vector.size(); i++)
    new_list.push_back(vector[i]);
```

### Algoritmos STL

#### std::sort

```cpp
std::vector<int> sortedNumbers = _myVector;
std::sort(sortedNumbers.begin(), sortedNumbers.end());
```

#### std::max_element y std::min_element

```cpp
std::vector<int>::iterator minIt = std::min_element(_myVector.begin(), _myVector.end());
std::vector<int>::iterator maxIt = std::max_element(_myVector.begin(), _myVector.end());
```

#### std::find

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

Usado en BitcoinExchange para búsqueda binaria eficiente:<cite/>

```cpp
std::map<int, float>::iterator it = database.lower_bound(dateINT);
if (it != database.begin())
    --it;
```

### Iteradores

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

### Streams de Archivos

#### std::ifstream (Lectura)

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

#### CSV Parsing

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

### Algoritmos de Ordenamiento

#### Merge-Insertion Sort

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

Usado en BitcoinExchange para búsqueda eficiente:<cite/>

```cpp
std::map<int, float>::iterator it = database.lower_bound(dateINT);
if (it != database.begin() && (it == database.end() || it->first != dateINT))
    --it;
```

### Algoritmo RPN (Notación Polaca Inversa)

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

#### Validación de Fechas

```cpp
bool is_valid_date(const std::tm& date);
int convert_date_to_int(std::tm& date);
int parse_date(std::string& dateString, std::string file);
```

#### Validación de Números

```cpp
bool check_int(std::string& str);
bool check_float(std::string& str);
```

### Medición de Rendimiento

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

### Templates de Funciones

#### Templates Básicos

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

#### Clase Template Array

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

#### Función easyFind

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

#### Funciones de Utilidad Genéricas

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

### Clases de Excepción Personalizadas

#### Excepciones Básicas

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

#### En Constructores

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

```cpp
void Bureaucrat::incrementGrade()
{
    if (MAX_GRADE > (_grade - 1))
        throw (Bureaucrat::GradeTooHighException());
    _grade--;
}
```

### Excepciones en Templates

#### Lanzamiento en Operadores

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

```cpp
std::ostringstream oss;
oss << "Value: [" << value << "] not found in the container.";
throw (std::runtime_error(oss.str()));
```

### Manejo Complejo de Excepciones

#### Bloques try-catch Anidados

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

#### Validación en Algoritmos

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

### static_cast

#### Conversiones entre Tipos Primitivos

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

#### Conversión de Punteros

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

#### Identificación de Tipos con Punteros

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

## Conclusiones y Próximos Pasos

### Resumen del Recorrido

Este manual ha cubierto todos los conceptos necesarios para completar los 10 módulos del repositorio CPP_Piscine:

1. **Fundamentos básicos** de C++ (Módulos 00-01)
2. **Programación orientada a objetos** con clases, herencia y polimorfismo (Módulos 02-04)
3. **Manejo avanzado de errores** con excepciones personalizadas (Módulo 05)
4. **Conversiones de tipo** con los cuatro tipos de casting (Módulo 06)
5. **Programación genérica** con templates (Módulo 07)
6. **Contenedores y algoritmos STL** (Módulo 08)
7. **Algoritmos avanzados** y estructuras de datos complejas (Módulo 09)

### Habilidades Desarrolladas

A lo largo de estos módulos, has desarrollado habilidades en:

- **Diseño de clases** siguiendo principios SOLID
- **Gestión de memoria** manual y automática
- **Sobrecarga de operadores** y funciones
- **Patrones de diseño** como Factory, Singleton, etc.
- **Algoritmos eficientes** con complejidad temporal y espacial
- **Templates** para programación genérica
- **STL** para estructuras de datos y algoritmos predefinidos

### Próximos Pasos Recomendados

1. **Proyectos personales**: Aplica estos conceptos en proyectos propios
2. **Estándares modernos**: Explora C++11, C++14, C++17 y C++20
3. **Patrones de diseño**: Estudia patrones avanzados como Observer, Strategy, etc.
4. **Optimización**: Aprende técnicas de profiling y optimización de código
5. **Contribuir a open source**: Participa en proyectos de código abierto
6. **Especialización**: Enfócate en áreas como game dev, sistemas embebidos, HPC, etc.

### Recursos Adicionales

- **Documentación oficial**: cppreference.com
- **Comunidades**: Stack Overflow, Reddit r/cpp, CppCon
- **Libros recomendados**:
  - "Effective Modern C++" de Scott Meyers
  - "The C++ Programming Language" de Bjarne Stroustrup
  - "C++ Templates: The Complete Guide" de David Vandevoorde

### Consejos Finales

1. **Practica regularmente**: La consistencia es clave para dominar C++
2. **Revisa código de otros**: Aprende de proyectos open source bien estructurados
3. **Escribe código limpio**: Sigue guías de estilo y principios de clean code
4. **Aprende herramientas**: Dominia debuggers (gdb), profilers (valgrind), y build systems (CMake)
5. **Mantente actualizado**: C++ evoluciona constantemente

¡Felicidades por completar este recorrido por C++! Has desarrollado una base sólida que te permitirá enfrentar desafíos de programación complejos y seguir creciendo como desarrollador.programación complejos y seguir creciendo como desarrollador.
