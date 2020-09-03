# Guía de Estilo para C

No hay una forma correcta de estilizar el código. Pero definitivamente hay muchas formas incorrectas (o al menos, malas). Aun así, info1 le pide que se adhiera a las convenciones siguientes para que podamos analizar de manera confiable el estilo de su código. De manera similar, las empresas suelen adoptar sus propias convenciones de estilo.

Las reglas de coherencia más importantes son las que rigen la denominación. El estilo de un nombre nos informa inmediatamente qué tipo de cosa es la entidad nombrada: un tipo, una variable, una función, una constante, una macro, etc., sin necesidad de buscar la declaración de esa entidad. El motor de coincidencia de patrones en nuestro cerebro se basa en gran medida en estas reglas de denominación.

## Tabla de Contenido

- [Largo de Línea](#largo-linea)
- [Comentarios](#comentarios)
- [Espacios Verticales](#espacios-verticales)
- [Indentación](#indentacion)
- [Condicionales](#condicionales)
- [Bucles](#bucles)
- [Funciones](#funciones)
- [Variables](#variables)
- [Punteros](#punteros)
- [Macros y Constantes Simbólicas](#macros-constantes-simbolicas)
- [Estructuras, Enumeraciones y Typedefs](#estructuras-enumeraciones-typedefs)
- [Archivos source y header](#archivos-source-header)
- [Operadores](#operadores)
- [Últimas palabras](#ultimas-palabras)
- [Referencias](#referencias)

## Largo de Línea

Por convención, la longitud máxima de una línea de código es de 80 caracteres en C, lo cual históricamente se basa en que los monitores de tamaño estándar de antiguos terminales de computadora podían mostrar 24 líneas verticalmente y 80 caracteres horizontalmente. Aunque la tecnología moderna ha dejado obsoleta la necesidad de mantener las líneas con un límite de 80 caracteres, sigue siendo una guía que debe considerarse una "parada suave", y una línea de 100 caracteres debería ser la más larga que se escriba en C; de lo contrario, los lectores necesitarán desplazarse horizontalmente al momento de leer el código. Si se necesitan más de 100 caracteres, puede ser el momento de repensar los nombres de las variables o el diseño en general.

```c
// Las siguientes líneas de código primero le piden al usuario que ingrese dos valores enteros y luego multiplica esos dos valores enteros juntos para que puedan usarse más adelante en el programa.
int first_collected_integer_value_from_user = get_int("Ingrese un numero entero: ");
int second_collected_integer_value_from_user = get_int("Ingrese otro numero entero: ");
int product_of_the_two_integer_values_from_user = first_collected_integer_value_from_user * second_collected_integer_value_from_user;
```

## Comentarios

Los comentarios hacen que el código sea más legible, no solo para otros (por ejemplo, los docentes) sino también para usted, especialmente cuando pasan horas, días, semanas, meses o años entre cuando escribió y cuando pretende leer su propio código. Pero recuerde: si bien los comentarios son muy importantes, el mejor código es **autodocumentado**. Dar nombres sensatos a tipos y variables es mucho mejor que usar nombres oscuros que luego deben explicar mediante comentarios.

Comentar muy poco es malo. Comentar demasiado es malo. ¿Cuál es el punto justo? Comentar cada varias líneas de código (es decir, bloques interesantes) es una guía decente. Trate de escribir comentarios que respondan a una o ambas de estas preguntas:

1. ¿Qué hace este bloque?
1. ¿Por qué implementé este bloque de esta manera?

Dentro de las funciones, intercale los comentarios con el código y manténgalos cortos (idealmente, una línea), de lo contrario, será difícil distinguir los comentarios del código, incluso con [resaltado de sintaxis](https://es.wikipedia.org/wiki/Resaltado_de_sintaxis). Coloque el comentario encima de la o las líneas a las que se aplica. No es necesario escribir oraciones completas, pero escriba en mayúscula la primera palabra del comentario (a menos que sea el nombre de una función, variable o similar) y deje un espacio entre el `//` y el primer carácter de su comentario, como en:

```c
// Convierto de Fahrenheit a Celsius
float celsius_degrees = 5.0 / 9.0 * (fahrenheit_degrees - 32.0);
```

En otras palabras, no haga esto:

```c
//Convierto de Fahrenheit a Celsius
float celsius_degrees = 5.0 / 9.0 * (fahrenheit_degrees - 32.0);
```

Ni esto:

```c
// convierto de Fahrenheit a Celsius
float celsius_degrees = 5.0 / 9.0 * (fahrenheit_degrees - 32.0);
```

Ni esto:

```c
float celsius_degrees = 5.0 / 9.0 * (fahrenheit_degrees - 32.0); // Convierto de Fahrenheit a Celsius
```

Al comenzo de sus archivos `.c` y `.h` debe haber un comentario que resuma lo que hace su programa (o ese módulo en particular), e información acerca del autor y fecha de creación del archivo, por ejemplo:

```c
/*!
 * @file   hola.c
 * @brief  Saluda al mundo.
 * @author John Doe <john.doe@example.com>
 * @date   Sep 21, 2020
 */
```

Encima de la declaración (prototipo) de cada una de sus funciones (excepto, quizás, `main`), debe haber un comentario que resuma lo que hace dicha función, por ejemplo:

```c
/*!
 * @brief Calcula el cuadrado de n.
 *
 * @param[in] n Valor de entrada.
 * @return	  El cuadrado del valor de entrada.
 */
int square(int n);

int square(int n)
{
    return n * n;
}
```

El correcto formato en los comentarios permitirá generar la documentación de forma automática, haciendo uso de la herramienta [Doxygen](https://www.doxygen.nl/index.html).

Por último, recuerde prestar atención a la puntuación, la ortografía y la gramática; es más fácil leer comentarios bien escritos que mal escritos.

## Espacios Verticales

Minimice el uso de espacios verticales en blanco.

Esto es más un principio que una regla: no utilice líneas en blanco cuando no sea necesario. En particular, no ponga más de una o dos líneas en blanco entre funciones, evite comenzar las funciones con una línea en blanco, no termine las funciones con una línea en blanco y sea parco con el uso de líneas en blanco. Una línea en blanco dentro de un bloque de código sirve como un salto de párrafo en prosa: separa visualmente dos pensamientos.

El principio básico es: cuanto más código cabe en una pantalla, más fácil es seguir y comprender el flujo de control del programa. Utilice espacios en blanco a propósito para proporcionar separación en ese flujo.

## Indentación

Indente el código con **4 (cuatro)** espacios a la vez para dejar en claro qué bloques de código están dentro de otros. Si usa la tecla `Tab` de su teclado para hacerlo, asegúrese de que su editor de texto esté configurado para convertir tabs (`\t`) en cuatro espacios; de lo contrario, es posible que su código no se imprima o no se muestre correctamente en la computadora de otra persona, ya que `\t` se renderiza de manera diferente en diferentes editores.

A continuación se muestra un código indentado correctamente:

```c
// Imprime los argumentos de línea de comando, de uno por línea.
int i, j, n;
for (i = 0; i < argc; i++)
{
    n = strlen(argv[i]);
    for (j = 0; j < n; j++)
    {
        printf("%c", argv[i][j]);
    }
    printf("\n");
}
```

## Condicionales

### if-else

Las estructuras condicionales `if-else` deben tener el siguiente estilo:

```c
if (x > 0)
{
    printf("x es positivo\n");
}
else if (x < 0)
{
    printf("x es negativo\n");
}
else
{
    printf("x es cero\n");
}
```

Observe como:

- las llaves se encuentran bien **alineadas**, cada una en su propia línea, dejando perfectamente claro lo que hay dentro del bloque;
- hay un **único** espacio luego de cada `if`; 
- hay un **único** espacio alrededor de `>` y alrededor de `<`;
- **no** hay ningún espacio inmediatamente luego de cada `(` o inmediatamente antes de cada `)`; y
- cada invocación a `printf` se encuentra indentada con **4** espacios.

Para ahorrar espacio, a algunos programadores les gusta mantener la primera llave en la misma línea que la condición en sí, pero no lo recomendamos, ya que es más difícil de leer, así que evite hacer esto:

```c
if (x < 0) {
    printf("x es negativo\n");
} else if (x > 0) {
    printf("x es positivo\n");
}
```

Y definitivamente no haga esto:

```c
if (x < 0)
    {
    printf("x es negativo\n");
    }
else
    {
    printf("x no es negativo\n");
    }
```

### Switch

Las estructuras condicionales `switch` deben tener el siguiente estilo:

```c
switch (n)
{
    case -1:
        printf("n es -1\n");
        break;

    case 1:
        printf("n es 1\n");
        break;

    default:
        printf("n no es -1 ni 1\n");
        break;
}
```

Observe como:

- cada llave se encuentra en su **propia** línea;
- hay un **único** espacio luego de `switch`; 
- **no** hay ningún espacio inmediatamente luego de cada `(` o inmediatamente antes de cada `)`;
- los `case` del `switch` se encuentran indentados con **4** espacios;
- el cuerpo de los `case` se encuentran indentados con **4** espacios más; y
- cada `case` (incluyendo `default`) termina con un `break`.

## Bucles

### for

Las estructuras repetitivas `for` deben tener el siguiente estilo:

```c
for (int i = 0; i < LIMIT; i++)
{
    for (int j = 0; j < LIMIT; j++)
    {
        for (int k = 0; k < LIMIT; k++)
        {
            // Haz algo.
        }
    }
}
```

Observe como:

- cada llave se encuentra en su **propia** línea;
- hay un **único** espacio luego de `for`;
- **no** hay ningún espacio inmediatamente luego de cada `(` o inmediatamente antes de cada `)`; y
- el cuerpo del bucle (un comentario en este caso) se encuentra indentado con **4** espacios.

Siempre que necesite variables temporales para la iteración, use `i`, luego` j`, luego `k`, a menos que nombres más específicos hagan que su código sea más legible. Si necesita más de tres variables para la iteración, ¡podría ser el momento de repensar su diseño!

### while

Las estructuras repetitivas `while` deben tener el siguiente estilo:

```c
while (condición)
{
    // Haz algo.
}
```

Observe como:

- cada llave se encuentra en su **propia** línea;
- hay un **único** espacio luego de `while`;
- **no** hay ningún espacio inmediatamente luego de cada `(` o inmediatamente antes de cada `)`; y
- el cuerpo del bucle (un comentario en este caso) se encuentra indentado con **4** espacios.

### do ... while

Las estructuras repetitivas `do ... while` deben tener el siguiente estilo:

```c
do
{
    // Haz algo.
} while (condición);
```

Observe como:

- las llaves se encuentran bien **alineadas**;
- el `while` se encuentra en la **misma** línea que la llave de cierre, separados entre sí por **1** espacio;
- hay un **único** espacio luego de `while`;
- **no** hay ningún espacio inmediatamente luego de cada `(` o inmediatamente antes de cada `)`; y
- el cuerpo del bucle (un comentario en este caso) se encuentra indentado con **4** espacios.

## Funciones

De acuerdo con [C99](http://en.wikipedia.org/wiki/C99), asegúrese de declarar `main` así:

```c
int main(void)
{
    // ...
    return 0;
}
```

o así:

```c
int main(int argc, char* argv[])
{
    // ...
    return 0;
}
```

o incluso así:

```c
int main(int argc, char** argv)
{
    // ...
    return 0;
}
```

En cuanto a sus propias funciones, asegúrese de definirlas de manera similar, con cada llave en su propia línea y con el tipo de retorno en la misma línea que el nombre de la función, tal como lo hemos hecho con `main`.

### Largo de las funciones

Implemente funciones pequeñas y enfocadas.

Si bien es cierto que las funciones largas a veces son apropiadas, si una función supera las **40** líneas, considere si se puede dividir sin dañar la estructura del programa.

Incluso si su función larga funciona perfectamente ahora, alguien que la modifique en unos meses puede precisar agregar un nuevo comportamiento. Esto podría resultar en errores difíciles de encontrar. Mantener sus funciones breves y simples facilita que otras personas lean y modifiquen su código. Las funciones pequeñas también son más fáciles de testear.

### Estilo

Los nombres de las funciones deben estar todos en minúsculas, con guiones bajos (`'_'`) entre las palabras. Por ejemplo:

```c
// Correcto
void my_function(void);
void myfunction(void);

// Incorrecto
void MYFunction(void);
void myFunction();
```

## Variables

Debido a que info1 usa [C99](http://en.wikipedia.org/wiki/C99), no defina todas sus variables en la parte superior de sus funciones sino, más bien, cuándo y dónde las necesita. Además, de visibilidad a sus variables lo más estrictamente posible. Por ejemplo, si solo se necesita `i` por el bien de un bucle, declare `i` dentro del mismo bucle:

```c
for (int i = 0; i < LIMIT; i++)
{
    printf("%i\n", i);
}
```

Aunque está bien usar variables como `i`, `j` y `k` para la iteración, la mayoría de las variables deben tener un nombre más específico. Si está sumando algunos valores, por ejemplo, llame a su variable `suma`. Si el nombre de su variable justifica dos palabras (por ejemplo, `is_ready`), coloque un guión bajo entre ellas, una convención popular en C.

Utilice nombres que describan el propósito o la intención de la variable. No se preocupe por ahorrar espacio horizontal, ya que es mucho más importante hacer que su código sea inmediatamente comprensible para un nuevo lector. Minimice el uso de abreviaturas que probablemente sean desconocidas para alguien ajeno a su proyecto (especialmente acrónimos e iniciales). No abrevie eliminando letras dentro de una palabra. Como regla general, una abreviatura probablemente esté bien si aparece en Wikipedia.

Si declara varias variables del mismo tipo a la vez, está bien declararlas juntas, como en:

```c
int apples, bananas, strawberries;
```

Sólo no inicialice algunas sí pero otras no, como en:

```c
int apples = 0, bananas, strawberries = 0;
```

### Visibilidad

**Evite** utilizar variables globales siempre que sea posible, ya que esto genera alto acoplamiento entre distintos módulos y no es considerado una buena práctica de programación. 

### Estilo

Los nombres de las variables (incluidos los parámetros de las funciones) deben estar todos en **minúsculas**, con **guiones bajos** (`'_'`) entre las palabras. Por ejemplo:

```c
char table_name[20];
int count;
```

## Punteros

Al declarar un puntero, escriba el `*` junto al tipo de dato, como en:

```c
int* p;
```

**No** lo escriba junto a la variable, como en:

```c
int *p;
```

Es una buena práctica **siempre** inicializar los punteros al momento de la declaración, por ejemplo, así:

```c
int* p = NULL;
```

o así:

```c
int a;
int* p = &a;
```

Para evitar posibles errores, tenga cuidado de declarar punteros por **separado** de no punteros, como en:

```c
int* p;
int n;
```

Y **no** declare punteros en una misma línea, como en:

```c
int* p, * n;
```

### Valor cero

Para punteros, prefiera `NULL` a `0`. Si bien los valores son equivalentes, `NULL` parece más un puntero para el lector, y algunos compiladores de C proporcionan definiciones especiales de `NULL` que les permiten dar warnings útiles. **Nunca** use `NULL` para valores numéricos (enteros o de punto flotante).

Utilice `'\0'` para el caracter nulo en strings, ya que usar el tipo correcto hace que el código sea más legible (por más que su valor sea cero).

Utilice el valor literal `0` sólo para variables de tipo numérico.

## Macros y Constantes Simbólicas

Las macros y constantes simbólicas deben ser declaradas como se muestra a continuación, en **mayúsculas** y con guiones bajos (`'_'`) entre las palabras. Por ejemplo:

```c
#define PI_ROUNDED 3.14
#define MIN(a, b) ((a) < (b) ? (a) : (b))
```

## Estructuras, Enumeraciones y Typedefs

### Estructuras

Declare una `estructura` como un tipo de la siguiente manera:

```c
typedef struct Student
{
    char* name;
    int age;
} Student;
```

Observe como:

- las llaves se encuentran bien **alineadas**;
- los miembros se encuentran indentados con **4** espacios; y
- el nuevo tipo de dato se encuentra tanto luego de `struct`, como en la **misma** línea que la llave de cierre, separados entre sí por **1** espacio.

Colocar el tipo de dato utilizando el mismo nombre, tanto en la definición de la estructura como en el `typedef`, permite colocar miembros que sean punteros al mismo tipo que el de la estructura sin tener que realizar más cambios, por ejemplo:

```c
typedef struct Node
{
    int value;
    struct Node* next;
} Node;
```

#### Estilo

Los nombres de los miembros de datos de la estructura, al igual que las variables, deben estar todos en **minúsculas**, con **guiones bajos** (`'_'`) entre las palabras. Por ejemplo:

```c
typedef struct Student 
{
  char first_name[20];
  char last_name[20];
  int age;
} Student;
```

### Enumeraciones

Declare una `enumeracion` como un tipo de la siguiente manera:

```c
typedef enum Boolean
{
    FALSE = 0,
    TRUE,
} Boolean;
```

Observe como:

- las llaves se encuentran bien **alineadas**;
- los valores posibles se encuentran indentados con **4** espacios; y
- el nuevo tipo de dato se encuentra tanto luego de `enum`, como en la **misma** línea que la llave de cierre, separados entre sí por **1** espacio.

#### Estilo

Los nombres de los posibles valores de la enumeración, al igual que las constantes simbólicas, deben estar todos en **mayúsculas**, con **guiones bajos** (`'_'`) entre las palabras. Por ejemplo:

```c
typedef enum ReturnErrors
{
    OK = 0,
    OUT_OF_MEMORY,
    MALFORMED_INPUT,
} ReturnErrors;
```

### Typedef

Los nombres de todos los tipos (`structs`, `enums` y `typedefs`) tienen la misma convención de nomenclatura. Los nombres de los tipos deben **comenzar** con una letra **mayúscula** y tener una letra **mayúscula** para cada palabra nueva, **sin** guiones bajos. Por ejemplo:

```c
// Structs
typedef struct MyStruct
{ 
    // ...
} MyStruct;

// Enums
typedef enum MyEnum
{
    // ...
} MyEnum;

// Typedefs
typedef char* String;
```

## Archivos Source y Header

En general, cada archivo `.c` debe tener un archivo `.h` asociado. Existen algunas excepciones comunes, como tests unitarios y pequeños archivos `.c` que contienen sólo una función `main()`.

### La guarda #define

Todos los archivos header deben tener guardas `#define` para prevenir inclusiones múltiples. El formato del nombre de la constante simbólica debe ser `PROYECTO_PATH_ARCHIVO_H_`.

Para garantizar que sea único, deben basarse en la ruta completa en el árbol de origen de un proyecto. Por ejemplo, el archivo foo/src/bar/baz.h en el proyecto `foo` debe tener la siguiente guarda:

```c
#ifndef FOO_BAR_BAZ_H_
#define FOO_BAR_BAZ_H_

...

#endif  // FOO_BAR_BAZ_H_
```

### Estilo

Los nombres de los archivos deben estar todos en **minúsculas**, con **guiones bajos** (`'_'`) entre las palabras. Por ejemplo:

```
my_module.c
my_module.h
my_module_test.c
```

Los archivos fuente deben terminar en `.c` y los archivos de encabezado deben terminar en `.h`.

## Operadores

Los operadores de asignación siempre tienen espacios a su alrededor. Por ejemplo:

```c
// Correcto
x = 0;
```

Otros operadores binarios también suelen tener espacios a su alrededor, pero está bien eliminar espacios alrededor de los factores. Los paréntesis no deben tener espacios del lado interno. Por ejemplo:

```c
// Correcto
v = w * x + y / z;
v = w*x + y/z;
v = w * (x + z);
```

No coloque espacios que separen a los operadores unarios y sus argumentos. Por ejemplo:

```c
// Correcto
x = -5;
++x;
if (x && !y) ...
```

### sizeof

Prefiera `sizeof(nombre_de_variable)` a `sizeof(tipo)`.

Use `sizeof(nombre_de_variable)` cuando tome el tamaño de una variable en particular, ya que se actualizará adecuadamente si alguien cambia el tipo de variable ahora o más tarde. Puede usar `sizeof(tipo)` para el código que no está relacionado con ninguna variable en particular.

## Últimas Palabras

Use el sentido común y **SEA CONSISTENTE**.

El objetivo de tener pautas de estilo es tener un vocabulario común de codificación para que la gente pueda concentrarse en lo **que** está diciendo, en lugar de en **cómo** lo está diciendo. Las reglas de estilo globales aquí presentadas sirven para que la gente conozca el vocabulario y manejen un lenguaje común.

OK, suficiente cháchara sobre escritura de código; el código en sí es mucho más interesante. **¡A programar, que te diviertas!**

## Referencias

Guía de estilo inspirada y basada en:

- https://cs50.readthedocs.io/style/c/
- https://github.com/MaJerle/c-code-style
