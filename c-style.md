# Guía de Estilo para C

No hay una forma correcta de estilizar el código. Pero definitivamente hay muchas formas incorrectas (o al menos, malas). Aun así, info1 te pide que te adhieras a las convenciones siguientes para que podamos analizar de manera confiable el estilo de tu código. De manera similar, las empresas suelen adoptar sus propias convenciones de estilo.

Las reglas de coherencia más importantes son las que rigen la denominación. El estilo de un nombre nos informa inmediatamente qué tipo de cosa es la entidad nombrada: un tipo, una variable, una función, una constante, una macro, etc., sin necesidad de buscar la declaración de esa entidad. El motor de coincidencia de patrones en nuestro cerebro se basa en gran medida en estas reglas de denominación.

## Tabla de Contenido

- [Largo de Línea](#largo-de-línea)
- [Comentarios](#comentarios)
- [Espacios Verticales y Líneas en Blanco](#espacios-verticales-y-líneas-en-blanco)
- [Indentación](#indentación)
- [Condicionales](#condicionales)
- [Bucles](#bucles)
- [Funciones](#funciones)
- [Variables](#variables)
- [Punteros](#punteros)
- [Macros y Constantes Simbólicas](#macros-y-constantes-simbólicas)
- [Estructuras, Enumeraciones y Typedefs](#estructuras-enumeraciones-y-typedefs)
- [Archivos Fuente (Source) y Encabezado (Header)](#archivos-fuente-(source)-y-encabezado-(header))
- [Operadores](#operadores)
- [Últimas palabras](#últimas-palabras)
- [Referencias](#referencias)

## Largo de Línea

Por convención, la longitud máxima de una línea de código es de 80 caracteres en C, lo cual históricamente se basa en que los monitores de tamaño estándar de antiguos terminales de computadora podían mostrar 24 líneas verticalmente y 80 caracteres horizontalmente. Aunque la tecnología moderna ha dejado obsoleta la necesidad de mantener las líneas con un límite de 80 caracteres, sigue siendo una guía que debe considerarse una "parada suave", y una línea de 100 caracteres debería ser la más larga que se escriba en C; de lo contrario, los lectores necesitarán desplazarse horizontalmente al momento de leer el código. Si se necesitan más de 100 caracteres, puede ser el momento de repensar los nombres de las variables o el diseño en general. 

En otras palabras, evitá hacer cosas como la siguiente:

```c
// Las siguientes líneas de código primero le piden al usuario que ingrese dos valores enteros y luego multiplica esos dos valores enteros juntos para que puedan usarse más adelante en el programa.
int primer_numero_entero_ingresado_por_el_usuario = obtener_int("Ingrese un numero entero: ");
int segundo_numero_entero_ingresado_por_el_usuario = obtener_int("Ingrese otro numero entero: ");
int producto_de_los_dos_numeros_enteros_ingresados_por_el_usuario = primer_numero_entero_ingresado_por_el_usuario * segundo_numero_entero_ingresado_por_el_usuario;
```

## Comentarios

Los comentarios hacen que el código sea más legible, no solo para otros (por ejemplo, los docentes) sino también para vos, especialmente cuando pasan horas, días, semanas, meses o años entre cuando escribiste y cuando pretendés leer tu propio código. Pero recordá: si bien los comentarios son muy importantes, el mejor código es **autodocumentado**. Dar nombres sensatos a tipos y variables es mucho mejor que usar nombres oscuros que luego se deben explicar mediante comentarios.

Comentar muy poco es malo. Comentar demasiado es malo. ¿Cuál es el punto justo? Comentar cada varias líneas de código (es decir, bloques interesantes) es una guía decente. Tratá de escribir comentarios que respondan a una o ambas de estas preguntas:

1. ¿Qué hace este bloque?
1. ¿Por qué implementé este bloque de esta manera?

Dentro de las funciones, intercalá los comentarios con el código y mantenelos cortos (idealmente, una línea), de lo contrario, será difícil distinguir los comentarios del código, incluso con [resaltado de sintaxis](https://es.wikipedia.org/wiki/Resaltado_de_sintaxis). Colocá el comentario encima de la o las líneas a las que se aplica. No es necesario escribir oraciones completas, pero escribí en mayúscula la primera palabra del comentario (a menos que sea el nombre de una función, variable o similar) y dejá un espacio entre el `//` y el primer caracter del comentario, como en:

```c
// Convierto de Fahrenheit a Celsius
float grados_celsius = 5.0 / 9.0 * (grados_fahrenheit - 32.0);
```

En otras palabras, no hagas esto:

```c
//Convierto de Fahrenheit a Celsius
float grados_celsius = 5.0 / 9.0 * (grados_fahrenheit - 32.0);
```

Ni esto:

```c
// convierto de Fahrenheit a Celsius
float grados_celsius = 5.0 / 9.0 * (grados_fahrenheit - 32.0);
```

Ni esto:

```c
float grados_celsius = 5.0 / 9.0 * (grados_fahrenheit - 32.0); // Convierto de Fahrenheit a Celsius
```

Al comienzo de tus archivos `.c` y `.h` debe haber un comentario que resuma lo que hace tu programa (o ese módulo en particular), e información acerca del autor y la fecha de creación del archivo, por ejemplo:

```c
/*!
 * @file   hola.c
 * @brief  Saluda al mundo.
 * @author John Doe <john.doe@example.com>
 * @date   Sep 21, 2020
 */
```

Encima de la declaración (prototipo) de cada una de tus funciones (excepto quizás `main`), debe haber un comentario que resuma lo que hace dicha función, por ejemplo:

```c
/*!
 * @brief Calcula el cuadrado de n.
 *
 * @param[in] n Valor de entrada.
 * @return	  El cuadrado del valor de entrada.
 */
int cuadrado(int n);

int cuadrado(int n)
{
    return n * n;
}
```

El correcto formato en los comentarios permitirá generar la documentación de forma automática, haciendo uso de la herramienta [Doxygen](https://www.doxygen.nl/index.html).

Por último, recordá prestar atención a la puntuación, la ortografía y la gramática; es más fácil leer comentarios bien escritos que mal escritos.

## Espacios Verticales y Líneas en Blanco

Minimizá el uso de espacios verticales en blanco.

Esto es más un principio que una regla: no utilices líneas en blanco cuando no sea necesario. En particular, no pongas más de una o dos líneas en blanco entre funciones, evitá comenzar las funciones con una línea en blanco, no termines las funciones con una línea en blanco y sea parco con el uso de líneas en blanco. Una línea en blanco dentro de un bloque de código sirve como un salto de párrafo en prosa: separa visualmente dos pensamientos.

El principio básico es: cuanto más código cabe en una pantalla, más fácil es seguir y comprender el flujo de control del programa. Utilizá espacios en blanco a propósito para proporcionar separación en ese flujo.

## Indentación

Indentá (colocá sangrías) el código con **4 (cuatro)** espacios a la vez para dejar en claro qué bloques de código están dentro de otros. Si usás la tecla `Tab` de tu teclado para hacerlo, asegurate de que tu editor de texto esté configurado para convertir tabs (`\t`) en cuatro espacios; de lo contrario, es posible que tu código no se imprima o no se muestre correctamente en la computadora de otra persona, ya que `\t` se renderiza de manera diferente en diferentes editores.

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

Observá como:

- las llaves se encuentran bien **alineadas**, cada una en su propia línea, dejando perfectamente claro lo que hay dentro del bloque;
- hay un **único** espacio luego de cada `if`; 
- hay un **único** espacio alrededor de `>` y alrededor de `<`;
- **no** hay ningún espacio inmediatamente luego de cada `(` o inmediatamente antes de cada `)`; y
- cada invocación a `printf` se encuentra indentada con **4** espacios.

Para ahorrar espacio, a algunos programadores les gusta mantener la primera llave en la misma línea que la condición en sí, pero no lo recomendamos, ya que es más difícil de leer, así que **evitá** hacer esto:

```c
if (x < 0) {
    printf("x es negativo\n");
} else if (x > 0) {
    printf("x es positivo\n");
}
```

Y definitivamente **no** hagas esto:

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

Y **siempre** colocá llaves, por más que el bloque sea de una sola línea, por lo cual **tampoco** hagas esto:

```c
if (x < 0)
    printf("x es negativo\n");
else
    printf("x no es negativo\n");
```

Finalmente, en caso de requerir evaluar múltiples condiciones, recordá utilizar paréntesis y dejar un espacio entre los paréntesis y los operadores lógicos:

```c
if ((x > 2) && (x < 5))
{
    printf("x es mayor que 2 y menor que 5\n");
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

Observá como:

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
int i, j, k;
for (i = 0; i < LIMITE; i++)
{
    for (j = 0; j < LIMITE; j++)
    {
        for (k = 0; k < LIMITE; k++)
        {
            // Hacé algo.
        }
    }
}
```

Observá como:

- cada llave se encuentra en su **propia** línea;
- hay un **único** espacio luego de `for`;
- **no** hay ningún espacio inmediatamente luego de cada `(` o inmediatamente antes de cada `)`; y
- el cuerpo del bucle (un comentario en este caso) se encuentra indentado con **4** espacios.

Siempre que necesites variables temporales para la iteración, usá `i`, luego` j`, luego `k`, a menos que nombres más específicos hagan que tu código sea más legible. Si necesitas más de tres variables para la iteración, ¡podría ser el momento de repensar tu diseño!

### while

Las estructuras repetitivas `while` deben tener el siguiente estilo:

```c
while (condición)
{
    // Hacé algo.
}
```

Observá como:

- cada llave se encuentra en su **propia** línea;
- hay un **único** espacio luego de `while`;
- **no** hay ningún espacio inmediatamente luego de cada `(` o inmediatamente antes de cada `)`; y
- el cuerpo del bucle (un comentario en este caso) se encuentra indentado con **4** espacios.

### do ... while

Las estructuras repetitivas `do ... while` deben tener el siguiente estilo:

```c
do
{
    // Hacé algo.
} while (condición);
```

Observá como:

- las llaves se encuentran bien **alineadas**;
- el `while` se encuentra en la **misma** línea que la llave de cierre, separados entre sí por **1** espacio;
- hay un **único** espacio luego de `while`;
- **no** hay ningún espacio inmediatamente luego de cada `(` o inmediatamente antes de cada `)`; y
- el cuerpo del bucle (un comentario en este caso) se encuentra indentado con **4** espacios.

## Funciones

De acuerdo con [C99](http://en.wikipedia.org/wiki/C99), asegurate de declarar `main` así:

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

En cuanto a tus propias funciones, asegurate de definirlas de manera similar, con cada llave en su propia línea y con el tipo de retorno en la misma línea que el nombre de la función, tal como lo hicimos con `main`.

### Largo de las funciones

Implementá funciones pequeñas y enfocadas. La idea es que cada función represente una técnica para lograr un único objetivo y que por lo tanto tenga una única responsabilidad. Recordá también que el nombre de la función debe tratar de dejar en evidencia el propósito de la misma.

Si bien es cierto que las funciones largas a veces son apropiadas, si una función supera las **40** líneas, considerá si se puede dividir sin dañar la estructura del programa.

Incluso si tu función larga funciona perfectamente ahora, alguien que la modifique en unos meses puede precisar agregar un nuevo comportamiento. Esto podría resultar en errores difíciles de encontrar. Mantener tus funciones breves y simples facilita que otras personas lean y modifiquen tu código. Las funciones pequeñas también son más fáciles de testear.

Particularmente en la función `main`, uno debe esforzarse por no tener demasiadas líneas de código. Tener una función `main` larga suele indicar una falta de abstracción, lo que significa que tu código no se ha dividido lo suficiente en funciones lógicas más pequeñas. Recordá que la función `main` no debe contener detalles de bajo nivel, sino que debe ser una descripción general de alto nivel de la solución (diseño [Top-Down](https://es.wikipedia.org/wiki/Top-down_y_bottom-up)).

### Estilo

Los nombres de las funciones deben estar todos en **minúsculas**, con guiones bajos (`'_'`) entre las palabras. Por ejemplo:

```c
// Correcto
void mi_funcion(int a);

// Incorrecto
void mifuncion(int a);
void MIFuncion(int a);
void miFuncion(int a);
void MiFuncion(int a);
```

## Variables

Siempre declará todas tus variables locales al **comienzo** de las funciones, antes de la primera sentencia. Aunque está bien usar variables como `i`, `j` y `k` para una iteración, la mayoría de las variables deben tener un nombre más específico. Si estás sumando algunos valores, por ejemplo, llamá a tu variable `suma`.

Utilizá nombres que describan el propósito o la intención de la variable. Minimizá el uso de abreviaturas que probablemente sean desconocidas para alguien ajeno a tu proyecto (especialmente acrónimos e iniciales). No abrevies eliminando letras dentro de una palabra. Como regla general, una abreviatura probablemente esté bien si aparece en Wikipedia.

Si declarás varias variables del mismo tipo a la vez, está bien declararlas juntas, como en:

```c
int manzanas, bananas, frutillas;
```

Sólo evitá inicializar algunas sí pero otras no, como en:

```c
int manzanas = 0, bananas, frutillas = 0;
```

**Nunca** modifiques el largo de arreglos estáticos en forma dinámica. En su lugar, utilizá asignación de memoria dinámica con las funciones estándar de C `malloc()` y `free()`.

```c
// Incorrecto
void mi_funcion(int largo)
{
    int arreglo[largo];
    // ...
}
```

### Visibilidad

**Evitá** utilizar variables globales siempre que sea posible, ya que esto genera alto acoplamiento entre distintos módulos y no es considerado una buena práctica de programación.

### Estilo

Los nombres de las variables (incluidos los parámetros de las funciones) deben estar todos en **minúsculas**, con **guiones bajos** (`'_'`) entre las palabras. Por ejemplo:

```c
char nombre_tabla[20];
int cantidad;
```

## Punteros

Al declarar un puntero, escribí el `*` junto al tipo de dato, como en:

```c
int* p;
```

**No** lo escribas junto a la variable, como en:

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

Para evitar posibles errores, expresá las declaraciones de punteros por **separado** de las declaraciones de variables que no correspondan a punteros, como en:

```c
int* p;
int n;
```

Y **no** declares varios punteros en una misma línea, como en:

```c
int* p, * n;
```

Finalmente, en el caso de requerir evaluar que el valor de un puntero es distinto (o igual) a `NULL`, escribí la operación lógica para hacerlo más explícito:

```c
if (p != NULL)
{
    printf("p es distinto de NULL\n");
}
```

### Valor cero

Para punteros, preferí usar `NULL` a `0`. Si bien los valores son equivalentes, `NULL` parece más un puntero para el lector, y algunos compiladores de C proporcionan definiciones especiales de `NULL` que les permiten dar warnings útiles. **Nunca** uses `NULL` para valores numéricos (enteros o de punto flotante).

Utilizá `'\0'` para el caracter nulo en strings, ya que usar el tipo correcto hace que el código sea más legible (por más que su valor sea también cero).

Utilizá el valor literal `0` sólo para variables de tipo numérico.

## Macros y Constantes Simbólicas

### Estilo

Las macros y constantes simbólicas deben ser declaradas como se muestra a continuación, en **mayúsculas** y con guiones bajos (`'_'`) entre las palabras. Por ejemplo:

```c
#define PI_REDONDEADO 3.14
#define MIN(a, b) ((a) < (b) ? (a) : (b))
```

### Magic numbers

Un magic number (número mágico) es un número en el código que parece arbitrario y no tiene contexto ni significado. Esto es considerado un antipatrón porque dificulta la comprensión y el mantenimiento del código. Evitá colocar magic numbers siempre que sea posible:

```c
// Incorrecto
float calcular_perimetro_circulo(float radio)
{
    return 6.28 * radio;
}

// Correcto
#define PI_REDONDEADO 3.14

float calcular_perimetro_circulo(float radio)
{
    return 2.0 * PI_REDONDEADO * radio;
}
```

## Estructuras, Enumeraciones y Typedefs

### Estructuras

Declará una `estructura` como un tipo de la siguiente manera:

```c
typedef struct Estudiante
{
    char* nombre;
    int edad;
} Estudiante;
```

Observá como:

- las llaves se encuentran bien **alineadas**;
- los miembros se encuentran indentados con **4** espacios; y
- el nuevo tipo de dato se encuentra tanto luego de `struct`, como en la **misma** línea que la llave de cierre, separados entre sí por **1** espacio.

Colocar el tipo de dato utilizando el mismo nombre, tanto en la definición de la estructura como en el `typedef`, permite colocar miembros que sean punteros al mismo tipo que el de la estructura sin tener que realizar más cambios, por ejemplo:

```c
typedef struct Nodo
{
    int valor;
    struct Nodo* proximo;
} Nodo;
```

#### Estilo

Los nombres de los miembros de datos de la estructura, al igual que las variables, deben estar todos en **minúsculas**, con **guiones bajos** (`'_'`) entre las palabras. Por ejemplo:

```c
typedef struct Estudiante 
{
    char primer_nombre[20];
    char segundo_nombre[20];
    char apellido[20];
    int edad;
} Estudiante;
```

### Enumeraciones

Declará una `enumeracion` como un tipo de la siguiente manera:

```c
typedef enum Booleano
{
    FALSO = 0,
    VERDADERO,
} Booleano;
```

Observá como:

- las llaves se encuentran bien **alineadas**;
- los valores posibles se encuentran indentados con **4** espacios; y
- el nuevo tipo de dato se encuentra tanto luego de `enum`, como en la **misma** línea que la llave de cierre, separados entre sí por **1** espacio.

#### Estilo

Los nombres de los posibles valores de la enumeración, al igual que las constantes simbólicas, deben estar todos en **mayúsculas**, con **guiones bajos** (`'_'`) entre las palabras. Por ejemplo:

```c
typedef enum Errores
{
    OK = 0,
    SIN_MEMORIA,
    DATOS_INCORRECTOS,
} Errores;
```

### Typedef

Los nombres de todos los tipos (`structs`, `enums` y `typedefs`) tienen la misma convención de nomenclatura. Los nombres de los tipos deben **comenzar** con una letra **mayúscula** y tener una letra **mayúscula** para cada palabra nueva, **sin** guiones bajos. Por ejemplo:

```c
// Structs
typedef struct MiStruct
{ 
    // ...
} MiStruct;

// Enums
typedef enum MiEnum
{
    // ...
} MiEnum;

// Typedefs
typedef char* String;
```

## Archivos Fuente (Source) y Encabezado (Header)

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

### Includes

Se debe evitar colocar `#include` en archivos header, salvo que sea estrictamente necesario (por ejemplo, debido a la necesidad de incluir la declaración de un nuevo tipo de dato). Esto permite que quien incluya nuestro archivo de encabezado no incluya además múltiples archivos de encabezado, los cuales incluso podrían ser incompatibles con los suyos.

Por lo tanto, **evitá** hacer esto:

```c
// hola.c
#include "hola.h"

void saludar(void)
{
    printf("Hola mundo\n");
}

// hola.h
#ifndef HOLA_H_
#define HOLA_H_

#include <stdio.h>

/*!
 * @brief Saluda al mundo.
 */
void saludar(void);

#endif  // HOLA_H_
```

Y **preferí** hacer esto:

```c
// hola.c
#include <stdio.h>
#include "hola.h"

void saludar(void)
{
    printf("Hola mundo\n");
}

// hola.h
#ifndef HOLA_H_
#define HOLA_H_

/*!
 * @brief Saluda al mundo.
 */
void saludar(void);

#endif  // HOLA_H_
```

### Estilo

Los nombres de los archivos deben estar todos en **minúsculas**, con **guiones bajos** (`'_'`) entre las palabras. Por ejemplo:

```
mi_modulo.c
mi_modulo.h
mi_modulo_test.c
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

No coloques espacios que separen a los operadores unarios y sus argumentos. Por ejemplo:

```c
// Correcto
x = -5;
++x;
if (x && !y) ...
```

### sizeof

Preferí `sizeof(nombre_de_variable)` a `sizeof(tipo)`.

Usá `sizeof(nombre_de_variable)` cuando tome el tamaño de una variable en particular, ya que se actualizará adecuadamente si alguien cambia el tipo de variable ahora o más tarde. Podés usar `sizeof(tipo)` para aquel código que no esté relacionado con ninguna variable en particular.

## Últimas Palabras

Usá el sentido común y **SÉ CONSISTENTE**.

El objetivo de tener pautas de estilo es tener un vocabulario común de codificación para que la gente pueda concentrarse en lo **que** estás diciendo, en lugar de en **cómo** lo estás diciendo. Las reglas de estilo globales aquí presentadas sirven para que la gente conozca el vocabulario y manejen un lenguaje común.

OK, suficiente cháchara sobre escritura de código; el código en sí es mucho más interesante. **¡A programar, que te diviertas!**

## Referencias

Guía de estilo inspirada y basada en:

- https://cs50.readthedocs.io/style/c/
- https://github.com/MaJerle/c-code-style
- https://google.github.io/styleguide/cppguide.html
