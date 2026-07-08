# PL Interpreter

Intérprete didáctico desarrollado en C++ con Flex y Bison para la asignatura **Procesadores de Lenguajes**. El proyecto implementa un pequeño lenguaje de programación con variables, constantes, expresiones aritméticas y lógicas, cadenas, estructuras de control, entrada/salida y ejecución mediante un árbol de sintaxis abstracta (AST).

## Descripción

Este repositorio contiene el código fuente de un intérprete capaz de leer y ejecutar programas con extensión `.p`. El lenguaje soportado permite escribir scripts sencillos con operaciones matemáticas, manejo de cadenas, condicionales, bucles y estructuras `switch`.

El proyecto está organizado en varios módulos:

* `parser/`: analizador léxico y sintáctico construido con Flex y Bison.
* `ast/`: definición y evaluación del árbol de sintaxis abstracta.
* `table/`: tabla de símbolos, variables, constantes, palabras reservadas y funciones predefinidas.
* `error/`: gestión de errores léxicos, sintácticos y de ejecución.
* `examples/`: programas de prueba escritos en el lenguaje interpretado.

## Características principales

* Interpretación de programas `.p`.
* Modo interactivo si se ejecuta sin archivo de entrada.
* Análisis léxico con Flex.
* Análisis sintáctico con Bison.
* Evaluación mediante AST.
* Tabla de símbolos para variables, constantes, palabras clave y funciones.
* Variables numéricas, booleanas y de cadena.
* Constantes predefinidas:

  * `pi`
  * `e`
  * `gamma`
  * `deg`
  * `phi`
  * `true`
  * `false`
* Funciones matemáticas predefinidas:

  * `sin`
  * `cos`
  * `log`
  * `log10`
  * `exp`
  * `sqrt`
  * `integer`
  * `abs`
* Operadores aritméticos:

  * `+`
  * `-`
  * `*`
  * `/`
  * `//`
  * `mod`
  * `^`
  * `!`
  * `++`
  * `--`
* Operadores relacionales:

  * `=`
  * `<>`
  * `>`
  * `<`
  * `>=`
  * `<=`
* Operadores lógicos:

  * `and`
  * `or`
  * `not`
* Concatenación de cadenas con `||`.
* Entrada y salida con `read`, `read_string` y `print`.
* Estructuras de control:

  * `if ... then ... else ... end_if`
  * `while ... do ... end_while`
  * `repeat ... until`
  * `for ... from ... to ... step ... do ... end_for`
  * `switch ... case ... default ... end_switch`
* Funciones de consola:

  * `clear_screen`
  * `place(fila, columna)`

## Estructura del proyecto

```text
Proyecto_final/
└── Proyecto_final/
    ├── ast/
    │   ├── ast.cpp
    │   ├── ast.hpp
    │   └── makefile
    ├── error/
    │   ├── error.cpp
    │   ├── error.hpp
    │   └── makefile
    ├── examples/
    │   ├── ejemplos_basicos/
    │   ├── ejemplos_clase/
    │   └── ejemplos_elaborados/
    ├── includes/
    │   └── macros.hpp
    ├── parser/
    │   ├── interpreter.l
    │   ├── interpreter.y
    │   └── makefile
    ├── table/
    │   ├── table.cpp
    │   ├── table.hpp
    │   ├── init.cpp
    │   ├── init.hpp
    │   └── clases auxiliares de símbolos
    ├── interpreter.cpp
    └── makefile
```

## Requisitos

Para compilar el proyecto necesitas tener instalados:

* `g++`
* `make`
* `flex`
* `bison`
* librería de Flex (`-lfl`)

En sistemas Linux basados en Debian/Ubuntu puedes instalarlos con:

```bash
sudo apt update
sudo apt install build-essential flex bison
```

## Compilación

Sitúate en el directorio principal del proyecto:

```bash
cd Proyecto_final/Proyecto_final
```

Compila el intérprete con:

```bash
make
```

Esto generará el ejecutable:

```bash
interpreter.exe
```

Para limpiar los archivos generados:

```bash
make clean
```

## Uso

### Ejecutar un archivo `.p`

```bash
./interpreter.exe examples/ejemplos_basicos/test01_variables_y_asignaciones.p
```

El intérprete solo acepta archivos con extensión `.p`.

### Modo interactivo

También puede ejecutarse sin argumentos:

```bash
./interpreter.exe
```

En este modo, el intérprete procesa las instrucciones introducidas por teclado.

## Ejemplo básico

```text
x := 5;
y := 10;

print 'Valor de x: ' || x || '\n';
print 'Valor de y: ' || y || '\n';
print 'Suma: ' || x + y || '\n';

if (x < y) then
  print 'x es menor que y\n';
else
  print 'x no es menor que y\n';
end_if;
```

## Ejemplo con bucle `for`

```text
factorial := 1;
n := 5;

for i from 2 to n step 1 do
  factorial := factorial * i;
end_for;

print 'Factorial de ' || n || ': ' || factorial || '\n';
```

## Ejemplo con cadenas

```text
nombre := 'Dani';

print 'Hola, ' || nombre || '\n';

read_string(apellido);
print 'Apellido introducido: ' || apellido || '\n';
```

## Sintaxis del lenguaje

### Asignaciones

```text
variable := expresion;
```

También se permiten asignaciones múltiples:

```text
a := b := c := 10;
```

### Salida por pantalla

```text
print expresion;
```

### Lectura de números

```text
read(variable);
```

### Lectura de cadenas

```text
read_string(variable);
```

### Condicionales

```text
if (condicion) then
  instrucciones;
else
  instrucciones;
end_if;
```

### Bucle `while`

```text
while (condicion) do
  instrucciones;
end_while;
```

### Bucle `repeat until`

```text
repeat
  instrucciones;
until (condicion);
```

### Bucle `for`

```text
for i from inicio to fin step incremento do
  instrucciones;
end_for;
```

El `step` puede omitirse en la construcción interna del AST, usando un incremento por defecto de `1`.

### Switch

```text
switch (expresion)
  case valor:
    instrucciones;
  case otro_valor:
    instrucciones;
  default:
    instrucciones;
end_switch
```

## Comentarios

El lenguaje soporta comentarios de una línea:

```text
# Esto es un comentario
```

También soporta comentarios de bloque anidados:

```text
(*
  Comentario de bloque
  (* comentario anidado *)
*)
```

## Ejemplos incluidos

El repositorio incluye diferentes programas de prueba:

* Ejemplos básicos para variables, operadores, condicionales, bucles, lectura, cadenas y funciones matemáticas.
* Ejemplos de clase como menús interactivos.
* Ejemplos elaborados con problemas más completos.

Algunos archivos útiles para probar el intérprete:

```bash
./interpreter.exe examples/ejemplos_basicos/test01_variables_y_asignaciones.p
./interpreter.exe examples/ejemplos_basicos/test08_switch_case_default.p
./interpreter.exe examples/ejemplos_basicos/test13_funciones_matematicas.p
./interpreter.exe examples/ejemplos_clase/menu.p
```

## Funcionamiento interno

El flujo principal del intérprete es:

1. Se inicializa la tabla de símbolos con constantes, palabras reservadas y funciones predefinidas.
2. Flex analiza la entrada y genera tokens.
3. Bison valida la gramática y construye el AST.
4. El AST evalúa las instrucciones en orden.
5. Las variables se consultan y actualizan mediante la tabla de símbolos.
6. Los errores léxicos, sintácticos y de ejecución se gestionan desde el módulo `error`.

## Objetivo del proyecto

El objetivo de este repositorio es servir como proyecto práctico de Procesadores de Lenguajes, mostrando el proceso completo de creación de un intérprete:

* diseño léxico,
* diseño sintáctico,
* construcción de árbol de sintaxis abstracta,
* gestión de tabla de símbolos,
* evaluación de expresiones,
* ejecución de sentencias,
* manejo de errores,
* y pruebas mediante programas de ejemplo.

## Tecnologías utilizadas

* C++
* Flex
* Bison
* Makefile
* Doxygen, opcional para documentación

## Autor

Proyecto académico desarrollado para la asignatura **Procesadores de Lenguajes** por:
- Carlos de la Torre Frías
  GitHub: [@CarlosDT191](https://github.com/CarlosDT191)]
- Daniel Grande Rubio
  GitHub: [@Dani93414](https://github.com/Dani93414)
