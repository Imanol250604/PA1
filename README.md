# README — PA1: Algoritmos y Estructuras de Datos

> **Curso:** ALGORITMO Y ESTRUCTURA DE DATOS BASADOS EN INTELIGENCIA ARTIFICIAL
> **Código:**   4682
> **Evaluación:** PA1  

## 1. Integrantes


| Integrante | Rol |
|---|---|
| Roy Granados Aguilar | Desarrollo de la Actividad 1 y 2 | 
| Imanol Ponce de León | Desarrollo de la Actividad 3 y 4 |

## 2. Caso de trabajo

Una coordinación académica necesita organizar información de talleres estudiantiles. En esta primera
etapa del sistema se trabajará únicamente con estructuras lineales estáticas. El equipo debe proponer
una solución para registrar cantidades de inscritos, ordenar resultados, realizar consultas puntuales y
representar la distribución de estudiantes por aulas y horarios.

### Actividad 1 – Conceptos fundamentales

#### 1.1 Diferencia entre estructura estática y dinámica

Una **estructura estática** tiene un tamaño definido que no cambia durante la ejecución del programa. En cambio, una **estructura dinámica** puede modificar su tamaño según las necesidades del programa.

#### 1.2 ¿Por qué utilizar arreglos y matrices?

Para esta primera etapa es adecuado utilizar arreglos y matrices porque conocemos previamente la cantidad de datos que vamos a manejar.

El **vector** permite almacenar de forma ordenada la cantidad de inscritos de cada taller y acceder a cada valor mediante su índice.

La **matriz** permite organizar la cantidad de estudiantes utilizando filas para representar las aulas y columnas para representar los horarios.

Los vectores almacenan datos homogéneos de manera ordenada y permiten acceder a ellos mediante índices, de acuerdo con lo trabajado en clase.

#### 1.3 Relación entre dato, algoritmo y estructura de datos

Los **datos** son los valores que necesitamos procesar, como la cantidad de inscritos de un taller.

La **estructura de datos** permite organizar estos valores mediante vectores y matrices.

Finalmente, los **algoritmos** establecen los pasos necesarios para procesar los datos. Por ejemplo, recorrer un vector para encontrar la mayor o menor cantidad de inscritos.

Un algoritmo es una secuencia ordenada de pasos que permite llegar a la solución de un problema.

---

### Actividad 2 – Arreglo unidimensional

La cantidad de inscritos en los talleres está representada por el siguiente vector:

```text
[28, 15, 34, 21, 19, 40, 12, 26]
```

#### 2.1 Representación gráfica

```text
Índice:  0   1   2   3   4   5   6   7
        ┌───┬───┬───┬───┬───┬───┬───┬───┐
Valor:  │28 │15 │34 │21 │19 │40 │12 │26 │
        └───┴───┴───┴───┴───┴───┴───┴───┘
```

Cada elemento del vector se identifica mediante su posición o índice.

#### 2.2 Obtener el valor máximo y mínimo

El algoritmo comienza tomando el primer elemento como valor máximo y mínimo. Después recorre los demás elementos y realiza las comparaciones correspondientes.

##### Pseudocódigo

```text
INICIO
    inscritos ← [28, 15, 34, 21, 19, 40, 12, 26]

    mayor ← inscritos[0]
    menor ← inscritos[0]

    PARA i ← 1 HASTA longitud(inscritos) - 1 HACER

        SI inscritos[i] > mayor ENTONCES
            mayor ← inscritos[i]
        FIN SI

        SI inscritos[i] < menor ENTONCES
            menor ← inscritos[i]
        FIN SI

    FIN PARA

    MOSTRAR "Mayor:", mayor
    MOSTRAR "Menor:", menor
FIN
```

**Resultado:**

```text
Mayor = 40
Menor = 12
```

##### Código Java

```java
int mayor = inscritos[0];
int menor = inscritos[0];

for (int i = 1; i < inscritos.length; i++) {

    if (inscritos[i] > mayor) {
        mayor = inscritos[i];
    }

    if (inscritos[i] < menor) {
        menor = inscritos[i];
    }
}
```

#### 2.3 Insertar un nuevo valor

Para insertar un elemento en una posición determinada se crea un nuevo vector con una posición adicional.

Ejemplo: insertar el valor `30` en la posición `2` (tercer elemento). La posición válida de inserción debe estar entre `0` y `longitud(vector)`, ambos incluidos.

**Antes:**

```text
Índice:  0   1   2   3   4   5   6   7
Valor:  28  15  34  21  19  40  12  26
```

**Después:**

```text
Índice:  0   1   2   3   4   5   6   7   8
Valor:  28  15  30  34  21  19  40  12  26
```

La inserción forma parte de las operaciones sobre vectores vistas en clase.

##### Pseudocódigo

```text
INICIO
    Crear nuevoVector con tamaño longitud(vector) + 1

    PARA i ← 0 HASTA posicion - 1 HACER
        nuevoVector[i] ← vector[i]
    FIN PARA

    nuevoVector[posicion] ← nuevoValor

    PARA i ← posicion HASTA longitud(vector) - 1 HACER
        nuevoVector[i + 1] ← vector[i]
    FIN PARA

    RETORNAR nuevoVector
FIN
```

##### Código Java

```java
static int[] insertar(int[] vector, int valor, int posicion) {

    int[] nuevo = new int[vector.length + 1];

    for (int i = 0; i < posicion; i++) {
        nuevo[i] = vector[i];
    }

    nuevo[posicion] = valor;

    for (int i = posicion; i < vector.length; i++) {
        nuevo[i + 1] = vector[i];
    }

    return nuevo;
}
```

#### 2.4 Ordenamiento de menor a mayor

Se utiliza **Bubble Sort**, comparando elementos vecinos. Si el elemento de la izquierda es mayor que el de la derecha, ambos intercambian sus posiciones.

##### Pseudocódigo

```text
INICIO

    PARA i ← 0 HASTA longitud(vector) - 2 HACER

        PARA j ← 0 HASTA longitud(vector) - 2 HACER

            SI vector[j] > vector[j + 1] ENTONCES

                temporal ← vector[j]
                vector[j] ← vector[j + 1]
                vector[j + 1] ← temporal

            FIN SI

        FIN PARA

    FIN PARA

FIN
```

##### Código Java

```java
for (int i = 0; i < v.length - 1; i++) {

    for (int j = 0; j < v.length - 1; j++) {

        if (v[j] > v[j + 1]) {

            int temp = v[j];
            v[j] = v[j + 1];
            v[j + 1] = temp;
        }
    }
}
```

Al ordenar el vector original de ocho elementos (sin la inserción del ejemplo anterior), el resultado es:

```text
[12, 15, 19, 21, 26, 28, 34, 40]
```

#### 2.5 Costo aproximado

En la implementación utilizada existen dos ciclos `for` anidados. La cantidad de operaciones aumenta aproximadamente de forma cuadrática respecto al tamaño del vector.

```text
Mejor caso: O(n²)
Peor caso: O(n²)
```

En esta implementación concreta no existe una condición que detenga anticipadamente el algoritmo cuando el vector ya está ordenado. Por eso los ciclos continúan realizando las comparaciones.

El análisis de eficiencia considera los recursos utilizados por el algoritmo, entre ellos el tiempo de ejecución y la cantidad de operaciones.

---

### Actividad 3 – Matriz bidimensional

Se utilizará una matriz de **4 filas × 5 columnas**, donde las filas representan las aulas y las columnas los bloques horarios, como solicita la PA1.

#### 3.1 Representación de la matriz

```text
             H0  H1  H2  H3  H4
           ┌───┬───┬───┬───┬───┐
Aula 0     │20 │15 │25 │10 │18 │
Aula 1     │12 │22 │30 │16 │14 │
Aula 2     │25 │20 │18 │24 │21 │
Aula 3     │15 │17 │20 │28 │19 │
           └───┴───┴───┴───┴───┘
```

En Java:

```java
int[][] ocupacion = {
    {20, 15, 25, 10, 18},
    {12, 22, 30, 16, 14},
    {25, 20, 18, 24, 21},
    {15, 17, 20, 28, 19}
};
```

Cada elemento se identifica mediante dos índices: uno correspondiente a la fila y otro a la columna.

#### 3.2 Total de estudiantes por aula

Para obtener el total por aula se recorre cada fila y se suman sus columnas.

##### Pseudocódigo

```text
INICIO

    PARA i ← 0 HASTA cantidadFilas - 1 HACER

        total ← 0

        PARA j ← 0 HASTA cantidadColumnas - 1 HACER
            total ← total + ocupacion[i][j]
        FIN PARA

        MOSTRAR "Total Aula", i, ":", total

    FIN PARA

FIN
```

**Resultados:**

```text
Aula 0 = 88
Aula 1 = 94
Aula 2 = 108
Aula 3 = 99
```

#### 3.3 Total de estudiantes por horario

Para obtener el total por horario se mantiene fija una columna y se recorren las filas.

##### Pseudocódigo

```text
INICIO

    PARA j ← 0 HASTA cantidadColumnas - 1 HACER

        total ← 0

        PARA i ← 0 HASTA cantidadFilas - 1 HACER
            total ← total + ocupacion[i][j]
        FIN PARA

        MOSTRAR "Total Horario", j, ":", total

    FIN PARA

FIN
```

**Resultados:**

```text
H0 = 72
H1 = 74
H2 = 93
H3 = 78
H4 = 72
```

#### 3.4 Celda con mayor ocupación

Para encontrar la celda con mayor ocupación se almacena el primer elemento como valor máximo y posteriormente se compara con los demás valores.

##### Pseudocódigo

```text
INICIO

    mayor ← ocupacion[0][0]
    filaMayor ← 0
    columnaMayor ← 0

    PARA i ← 0 HASTA cantidadFilas - 1 HACER

        PARA j ← 0 HASTA cantidadColumnas - 1 HACER

            SI ocupacion[i][j] > mayor ENTONCES

                mayor ← ocupacion[i][j]
                filaMayor ← i
                columnaMayor ← j

            FIN SI

        FIN PARA

    FIN PARA

    MOSTRAR "Mayor ocupación:", mayor
    MOSTRAR "Aula:", filaMayor
    MOSTRAR "Horario:", columnaMayor

FIN
```

**Resultado:**

```text
Mayor ocupación = 30 estudiantes
Aula = 1
Horario = 2
```

#### 3.5 ¿Por qué es necesario recorrer varias posiciones?

Para identificar la celda con mayor ocupación es necesario recorrer las posiciones de la matriz, ya que no conocemos de antemano dónde se encuentra el valor más alto.

Durante el recorrido, cada elemento se compara con el mayor encontrado hasta ese momento. Si aparece un valor superior, se actualizan el valor máximo, la fila y la columna.

---

### Actividad 4 – Matrices especiales

La última actividad solicita definir una **matriz cuadrada** y una **matriz dispersa**, además de plantear un ejemplo académico de matriz dispersa.

#### 4.1 Matriz cuadrada

Una **matriz cuadrada** es aquella que tiene la misma cantidad de filas y columnas.

Ejemplo:

```text
Matriz 3 × 3

┌───┬───┬───┐
│ 5 │ 2 │ 8 │
├───┼───┼───┤
│ 1 │ 4 │ 7 │
├───┼───┼───┤
│ 3 │ 6 │ 9 │
└───┴───┴───┘
```

Tiene:

```text
3 filas
3 columnas
```

Por lo tanto, es una matriz cuadrada. Las matrices cuadradas forman parte de los tipos de matrices trabajados en la sesión correspondiente.

#### 4.2 Matriz dispersa

Una **matriz dispersa** es aquella en la que la mayoría de sus elementos tienen valor cero.

Como ejemplo académico podemos representar aulas y horarios:

```text
             H0  H1  H2  H3  H4
           ┌───┬───┬───┬───┬───┐
Aula 0     │ 0 │ 0 │20 │ 0 │ 0 │
Aula 1     │ 0 │ 0 │ 0 │ 0 │15 │
Aula 2     │ 0 │ 0 │ 0 │ 0 │ 0 │
Aula 3     │25 │ 0 │ 0 │ 0 │ 0 │
           └───┴───┴───┴───┴───┘
```

En este caso, `0` representa que no existen estudiantes registrados en esa combinación de aula y horario.

**Justificación:** esta matriz es dispersa porque la mayoría de sus posiciones contienen el valor cero y solo unas pocas contienen información de ocupación. En un contexto académico puede utilizarse cuando existen muchas combinaciones de aulas y horarios sin estudiantes y solo algunas presentan registros.

---


## 3. Cómo ejecutar o revisar

Este README puede revisarse directamente en GitHub o en un visor Markdown. En la carpeta revisada solo se encontraron el README y el enunciado PDF; no se encontró un archivo Java ejecutable.

**Pasos de revisión:**

1. Revisar los conceptos de la Actividad 1 y la relación entre datos, estructuras y algoritmos.
2. Seguir los recorridos del vector original y comprobar su máximo, mínimo, inserción y ordenamiento. El ordenamiento mostrado utiliza el vector original; si se ordena el vector con el valor insertado, el resultado incluye también el 30.
3. Sumar las filas y columnas de la matriz y ubicar la celda de mayor ocupación, usando índices desde cero.
4. Comparar las matrices cuadrada y dispersa y revisar su justificación.

**Ejecución Java pendiente:** para ejecutar los fragmentos será necesario integrarlos en una clase con un método `main`, declarar los vectores y llamar a los métodos correspondientes. No se incluyen comandos que presupongan un archivo inexistente.

## 4. Evidencias

Las representaciones, pseudocódigos y resultados esperados están incluidos en la sección 2. Los siguientes valores sirven para comprobar manualmente el desarrollo; no representan capturas de una ejecución Java.

| Operación | Resultado esperado |
|---|---|
| Máximo del vector original | 40 |
| Mínimo del vector original | 12 |
| Insertar 30 en el índice 2 | [28, 15, 30, 34, 21, 19, 40, 12, 26] |
| Ordenar el vector original | [12, 15, 19, 21, 26, 28, 34, 40] |
| Totales por aula | 88, 94, 108, 99 |
| Totales por horario | 72, 74, 93, 78, 72 |
| Mayor ocupación | 30, en aula 1 y horario 2 |
| Suma de todos los valores de la matriz | 389 |

**Pendiente:** agregar capturas de la ejecución y enlaces al código o a los commits cuando estén disponibles.

## 5. Matriz de participación

La siguiente matriz registra los aportes informados por el equipo. La participación en pruebas y los aportes adicionales de documentación quedan por confirmar. La exposición no se realizó.

| Integrante | Desarrollo | Pruebas | Documentación | Exposición | Evidencia de participación |
|---|---|---|---|---|---|
| Yasier Araceli Fernández Villavicencio | Actividad 2 completa | Alta | Alta | No  | Commits, avances, etc. |
| Claudio Garcia Perez | Actividad 3: apartados 3.1 y 3.2 | Media | Media | No | Commits, avances, etc. |
| Gustavo Aarón Cruz Mírez | Actividad 3: apartados 3.3 a 3.5 | Media | Media | No | Commits, avances, etc. |
| Percy Daniel Perez Rojas | Actividad 4 completa | Media | Media | No | Commits, avances, etc. |
| Joseph Gianmarco Soberon Leon | Actividad 1 | Alta | Alta | No | Commits, avances, etc. |

## 6. Video de exposición

**Estado:** La exposición no se realizó por falta de tiempo.

**Video público de YouTube:** No disponible; no se realizó la exposición.

## 7. Conclusiones

- Los vectores permiten organizar los inscritos de los talleres y resolver búsquedas de máximos y mínimos mediante un recorrido. Para insertar un dato en un arreglo de tamaño fijo se crea otro arreglo con una posición adicional.
- Las matrices permiten relacionar aulas y horarios. Los recorridos por filas y columnas producen los totales correspondientes; para ubicar el máximo también se conservan sus índices.
- Bubble Sort compara elementos vecinos e intercambia los que están desordenados. La versión trabajada, sin salida anticipada, tiene costo O(n²) tanto en el mejor como en el peor caso.
- Una matriz cuadrada tiene igual número de filas y columnas; una dispersa contiene mayormente ceros. Si se utiliza una representación que almacene solo los valores no nulos y sus posiciones, puede reducirse el almacenamiento; una matriz rectangular convencional no obtiene ese ahorro automáticamente.

---

**Última actualización:** 21/09/2026
…]()
