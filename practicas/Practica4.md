# Conteo de Islas

## Introducción

Teniendo una cuadricula de NxM casillas, donde, hay algunas agrupaciones con diferente color, solucionar el problema de contar las `islas` formadas por el otro color, una Isla es el conjunto de una o varias casillas de otro color que se encuentran juntas, el conteo tiene que ser de manera recursiva y una Isla no puede ser contada dos o más veces, aunque tenga más de una casilla.
Partiendo de que hay que recorrer toda la matriz para contar las Islas, que, serán representadas con números(1 los que hay que contar y 0 los que no) y encontrar una manera de que los cuadros que sean parte de una Isla no se vuelvan a contar.

## Métodos para la solución

### Recursividad

Primero debemos definir brevemente que es la recursividad, ya que es un elemento clave en la resolución de este problema, la recursividad se puede definir como una técnica de programación que nos permite que un bloque de instrucciones se ejecute n veces. Remplaza en ocasiones a estructuras repetitivas.
Este concepto será de gran utilidad para este problema en especifico, ya que, en matrices demasiado grandes, repetir código se haría tedioso.
Además, como vimos en el problema anterior, en el diseño de un programa o agente que resuelva un problema, siempre será mejor crear un aestrategia lógica que siga algunos pasos, que tenga una secuecia más fácil o, en este caso, repetitiva, para que sea más fácil para el ordenador ejecutar el siguiente paso.

## Solución

El problema de contar islas en una matriz, donde las islas están representadas por conjuntos de unos adyacentes, es un desafío interesante que involucra la exploración y el marcado de regiones dentro de la matriz. Para abordar este problema, se puede desarrollar una solución eficiente y recursiva, para, sin la necesidad de hacer mucho código, el programa pueda llamarse a spi mismo y contar las Islas en una matriz del número de casillas que sea necesario, sin contar de más o contar cada cuadrito de la Isla.
En primer lugar, la solución implica recorrer cada celda de la matriz, y al encontrar una celda con el valor 1, se debe iniciar una función que explore y cuente la isla a la que pertenece esa celda. La función de conteo de islas también debe marcar las celdas visitadas para evitar el doble conteo.

### Función de conteo y recursividad

La recursividad juega un papel crucial en este enfoque. Después de encontrar una celda con el valor 1, la función se llama a sí misma para explorar las celdas adyacentes, ya que estas pertenecen a la misma isla. Es esencial tener en cuenta las restricciones de índices para evitar errores y asegurar que todas las celdas adyacentes se examinen correctamente.Por ejemplo, estando en la posición `[i,j]`, deberá llamar a la funcion para contar, la cual agregará uno al contador de islas y dentro se llama a si misma, pero con todas las casillas vecinas, verificando que existan esas posisiones, es decir, las posiciones `[i-1,j-1]`,`[i,j-1]`,`[i+1,j-1]`,`[i-1,j]`,  `[i+1,j]`,`[i-1,j+1]`,`[i,j+1]`,`[i+1,j+1]`.

Además, para evitar el doble conteo de una isla, se puede marcar la celda visitada cambiando su valor a 2. De esta manera, cuando la función se encuentre con una celda marcada, sabrá que ya ha sido contada en una isla anterior y evitará su conteo nuevamente.
También es muy importante que, cuando el programa encuentre ceros en los vecinos de la matriz, corte el proceso de recursión, ya que de otra manera, al encontrarse con el primer 1, seguirá mandando todos los vecinos al conteo y siempre devilverá que solo existe una Isla, lo cuál será incorrecto.

El algoritmo recursivo garantiza una exploración completa de cada isla en la matriz, lo que lleva a un conteo preciso y eficiente. Además, al utilizar el marcado de celdas visitadas, se mejora el rendimiento al evitar operaciones innecesarias.

### Implementación en Python

La implementación en Python de la solución propuesta se basa en una función principal llamada `contar_islas` y una función auxiliar `explorar_isla`. Estas funciones trabajan juntas para explorar y contar las islas en la matriz, asegurando que cada isla se cuente una sola vez y evitando el doble conteo.

```python

def contar_islas(matriz):
    islas_contadas = 0

    for i in range(len(matriz)):
        for j in range(len(matriz[0])):
            if matriz[i][j] == 1:
                islas_contadas += 1
                explorar_isla(matriz, i, j)

    return islas_contadas

def explorar_isla(matriz, i, j):
    if 0 <= i < len(matriz) and 0 <= j < len(matriz[0]) and matriz[i][j] == 1:
        matriz[i][j] = 2  # Marcamos la celda como visitada

        explorar_isla(matriz, i - 1, j - 1)
        explorar_isla(matriz, i, j - 1)
        explorar_isla(matriz, i + 1, j - 1)
        explorar_isla(matriz, i - 1, j)
        explorar_isla(matriz, i + 1, j)
        explorar_isla(matriz, i - 1, j + 1)
        explorar_isla(matriz, i, j + 1)
        explorar_isla(matriz, i + 1, j + 1)

# Ejemplo de uso
matriz_ejemplo = [
    [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
    [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
    [0,0,1,1,0,0,0,0,0,0,0,0,1,1,1,1,0,0,0,0],
    [0,0,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
    [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,1,0],
    [0,0,0,0,0,0,0,0,0,0,0,1,1,0,0,0,1,0,1,0],
    [0,0,0,0,0,0,0,0,0,0,0,1,1,0,0,0,1,0,1,0],
    [0,0,0,0,0,0,0,0,0,0,0,1,1,0,0,0,1,0,1,0],
    [0,0,0,0,0,0,0,0,0,0,0,1,1,0,0,0,0,0,0,0],
    [0,0,1,1,1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0],
    [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
    ]

total_islas = contar_islas(matriz_ejemplo)
print("Número total de islas:", total_islas)
matriz_ejemplo

```
En este ejemplo, el programa devuelve 6 islas, ya que hay seis conjuntos de Islas en diferentes puntos de la matriz y al final se imprime la matriz de nuevo, para verificar que ahora los unos(1) han sido cambiados por ceros(0).

## Conclusión

La solución propuesta aborda eficientemente el problema de contar islas en una matriz mediante un enfoque recursivo. La recursividad permite explorar todas las celdas vecinas de una isla de manera sistemática, garantizando un conteo preciso y evitando el doble conteo de islas individuales.

Si cambiaramos el tamaño de la matriz o el lugar donde se encuentran las celdas, este programa seguiría funcionando, ya que la recursividad ayuda a buscar islas sin importar el tamaño de matriz.