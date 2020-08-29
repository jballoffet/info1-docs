# Guía de Estilo para C

No hay una forma correcta de estilizar el código. Pero definitivamente hay muchas formas incorrectas (o al menos, malas). Aun así, Info1 le pide que se adhiera a las convenciones siguientes para que podamos analizar de manera confiable el estilo de su código. De manera similar, las empresas suelen adoptar sus propias convenciones de estilo para toda la empresa.

## Largo de Línea

Por convención, la longitud máxima de una línea de código es de 80 caracteres en C, lo cual históricamente se basa en que los monitores de tamaño estándar de antiguos terminales de computadora podían mostrar 24 líneas verticalmente y 80 caracteres horizontalmente. Aunque la tecnología moderna ha dejado obsoleta la necesidad de mantener las líneas con un límite de 80 caracteres, sigue siendo una guía que debe considerarse una "parada suave", y una línea de 100 caracteres debería ser la más larga que se escribe en C; de lo contrario, los lectores necesitarán desplazarse horizontalmente al momento de leer el código. Si se necesitan más de 100 caracteres, puede ser el momento de repensar los nombres de las variables o el diseño en general.

```c
// Las siguientes líneas de código primero le piden al usuario que ingrese dos valores enteros y luego multiplica esos dos valores enteros juntos para que puedan usarse más adelante en el programa.
int first_collected_integer_value_from_user = get_int("Ingrese un numero entero: ");
int second_collected_integer_value_from_user = get_int("Ingrese otro numero entero: ");
int product_of_the_two_integer_values_from_user = first_collected_integer_value_from_user * second_collected_integer_value_from_user;
```

## Comentarios

Los comentarios hacen que el código sea más legible, no solo para otros (por ejemplo, los docentes) sino también para usted, especialmente cuando pasan horas, días, semanas, meses o años entre cuando se escribió y cuando se pretende leer su propio código. Comentar muy poco es malo. Comentar demasiado es malo. Cúal es el punto justo? Comentar cada varias líneas de código (es decir, bloques interesantes) es una guía decente. Trate de escribir comentarios que respondan a una o ambas de estas preguntas:

1. ¿Qué hace este bloque?
1. ¿Por qué implementé este bloque de esta manera?

Dentro de las funciones, intercale los comentarios con el código y manténgalos cortos (idealmente, una línea), de lo contrario, será difícil distinguir los comentarios del código, incluso con [resaltado de sintaxis](https://es.wikipedia.org/wiki/Resaltado_de_sintaxis). Coloque el comentario encima de la o las líneas a las que se aplica. No es necesario escribir oraciones completas, pero escriba en mayúscula la primera palabra del comentario (a menos que sea el nombre de una función, variable o similar), termine con un punto, y deje un espacio entre el `//` y el primer carácter de su comentario, como en:

```c
// Convert Fahrenheit to Celsius.
float c = 5.0 / 9.0 * (f - 32.0);
```

En otras palabras, no haga esto:

```c
//Convert Fahrenheit to Celsius
float c = 5.0 / 9.0 * (f - 32.0);
```

Ni esto:

```c
// convert Fahrenheit to Celsius
float c = 5.0 / 9.0 * (f - 32.0);
```

Ni esto:

```c
float c = 5.0 / 9.0 * (f - 32.0); // Convert Fahrenheit to Celsius
```

Al comenzo de sus archivos .c y .h debe haber un comentario que resuma lo que hace su programa (o ese archivo en particular), e información acerca del autor y fecha de creación del archivo, por ejemplo:

```c
/*!
 * @file   hola.c
 * @brief  Saluda al mundo.
 * @author Javier Balloffet <javier.balloffet@gmail.com>
 * @date   Sep 7, 2018
 */
```

Encima de la declaración (prototipo) de cada una de sus funciones (excepto, quizás, `main`), debe haber un comentario que resuma lo que está haciendo su función, por ejemplo:

```c
/*!
 * @brief Devuelve el cuadrado de n.
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

El correcto formato en los comentarios, permitirá generar la documentación de forma automática, con la herramienta [Doxygen](https://www.doxygen.nl/index.html).

## Condicionales

Las estructuras condicionales deben tener el siguiente estilo:

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
- cada invocación a `printf` se encuentra indentada con **4** espacios;
- hay un **único** espacio alrededor de `>` y alrededor de `<`; y
- **no** hay ningún espacio inmediatamente luego de cada `(` o inmediatamente antes de cada `)`.

Para ahorrar espacio, a algunos programadores les gusta mantener la primera llave en la misma línea que la condición en sí, pero no lo recomendamos, ya que es más difícil de leer, así que no haga esto:

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

## Switches

Declare un `switch` como se muestra a continuación:

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

- cada llave se encuentra en su propia línea;
- hay un único espacio luego de `switch`;
- no hay ningún espacion inmediatamente luego de cada `(` o inmediatamente antes de cada `)`;
- los cases del switch se encuentran indentados con 4 espacios;
- el cuerpo de los cases se encuentran indentados con 4 espacios más; y
- cada `case` (incluyendo `default`) terminan con un `break`.

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

No declare `main` así:

```c
int main()
{
    // ...
    return 0;
}
```

o así:

```c
void main()
{
    // ...
}
```

o así:

```c
int
main()
{
    // ...
    return 0;
}
```

En cuanto a sus propias funciones, asegúrese de definirlas de manera similar, con cada llave en su propia línea y con el tipo de retorno en la misma línea que el nombre de la función, tal como lo hemos hecho con `main`.

## Indentación

Indente el código con cuatro espacios a la vez para dejar en claro qué bloques de código están dentro de otros. Si usa la tecla Tab de su teclado para hacerlo, asegúrese de que su editor de texto esté configurado para convertir tabs (`\t`) en cuatro espacios; de lo contrario, es posible que su código no se imprima o no se muestre correctamente en la computadora de otra persona, ya que `\t` se renderiza de manera diferente en diferentes editores.

A continuación se encuentra un código muy bien indentado correctamente:

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

## Bucles

### for

Siempre que necesite variables temporales para la iteración, use `i`, luego` j`, luego `k`, a menos que nombres más específicos hagan que su código sea más legible:

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

Si necesita más de tres variables para la iteración, ¡podría ser el momento de repensar su diseño!

### while

Declare bucles `while` como se muestra a continuación:

```c
while (condición)
{
    // Haz algo.
}
```

Observe como:

- cada llave se encuentra en su propia línea;
- hay un único espacio luego de `while`;
- no hay ningún espacio inmediatamente luego de cada `(` o inmediatamente antes de cada `)`; y
- el cuerpo del bucle (un comentario en este caso) se encuentra indentado con 4 espacios.

### do ... while

Declare bucles `do ... while` como se muestra a continuación:

```c
do
{
    // Haz algo.
}
while (condición);
```

Observe como:

- cada llave se encuentra en su propia línea;
- hay un único espacio luego de `while`;
- no hay ningún espacio inmediatamente luego de cada `(` o inmediatamente antes de cada `)`; y
- el cuerpo del bucle (un comentario en este caso) se encuentra indentado con 4 espacios.

## Punteros

Al declarar un puntero, escriba el `*` junto al tipo de dato, como en:

```c
int* p;
```

No lo escriba junto a la variable, como en:

```c
int *p;
```

Siempre inicialice los punteros al momento de la declaración, por ejemplo, así:

```c
int* p = NULL;
```

o así:

```c
int* p = &a;
```

## Variables

Debido a que Info1 usa [C99](http://en.wikipedia.org/wiki/C99), no defina todas sus variables en la parte superior de sus funciones sino, más bien, cuándo y dónde las necesita. Además, de visibilidad a sus variables lo más estrictamente posible. Por ejemplo, si solo se necesita `i` por el bien de un bucle, declare `i` dentro del mismo bucle:

```c
for (int i = 0; i < LIMIT; i++)
{
    printf("%i\n", i);
}
```

Aunque está bien usar variables como `i`,` j` y `k` para la iteración, la mayoría de las variables deben tener un nombre más específico. Si está sumando algunos valores, por ejemplo, llame a su variable `suma`. Si el nombre de su variable justifica dos palabras (por ejemplo, `is_ready`), coloque un guión bajo entre ellas, una convención popular en C.

Si declara varias variables del mismo tipo a la vez, está bien declararlas juntas, como en:

```c
int quarters, dimes, nickels, pennies;
```

Sólo no inicialice algunos sí pero no otros, como en:

```c
int quarters, dimes = 0, nickels = 0 , pennies;
```

También tenga cuidado de declarar punteros por separado de no punteros, como en:

```c
int* p;
int n;
```

Y no declare punteros en una misma línea, como en:

```c
int* p, * n;
```

## Estructuras

Declare una `estructura` como un tipo de la siguiente manera, con cada llave en su propia línea, los miembros correctamente indentados y con el nombre del tipo también en su propia línea:

```c
typedef struct
{
    char* name;
    int age;
}
Student;
```

Si la `estructura` contiene como miembro un puntero a otra `estructura` del mismo tipo, declare a la `estructura` para que tenga un nombre idéntico al tipo, sin usar guiones bajos:

```c
typedef struct Node
{
    int n;
    struct Node *next;
}
Node;
```
