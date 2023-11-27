# Introducción a la Inteligencia Artificial: El papelde la heurística

## Heurística

Como en la resolución de un problema anterior que eea similar(el conteo de islas en una matriz), este problema pretende que se recorra la matriz en busca de ciertos valores, en este caso, recorrerá las casillas que tengan ceros, ya que este es camino libre y no visitado,cuando lo recorra, irá marcando los visitados para no regresar por ahí y no errar, hasta llegar a la salida, que será la que tenga un valor 2 de visitado y ademas esté en una orilla(que alguno de los indíces sea 0 o la última posición de filas o columnas).

En otras palabras,el algoritmo deberá funcionar de la siguiente manera:

* Deberá buscar primero un valor 0, que ademas esté en alguna orilla, es decir, que la posisión i o j sean 0 o la última posición de filas o columnas, ya que este valor será la entrada.
* A partir de aqui, de manera recursiva irá recorriendo las posiciones que le sean posibles, es decir, tiene 4 formas de movimiento, que es hacia arriba, hacia abajo o hacia cualquiera de los lados en el caso de los que no son orillas, entonces, se irá llamando a la función  explorar por cada uno de los movimientos, para marcar como visitada la casilla en curso y sus vecinos(solo en caso de que sean 0, ya que por ahí pasa el laberinto).
* Si el algoritmo encuentra otro valor diferente de 0 ahí parará, es decir, si por ejemplo, recorre un camino que está cerrado ya habrá marcado todas estas casillas como visitadas y no intentará recorrer las paredes, ni hacer un bucle infinito, ya que las casillas visitadas, ahora en vez de ser 0, serán 2, entonces la recursión hará que regrese al último punto donde aún habia oportunidad de avanzar.
* El algoritmo encuentra la salida cuando encuentra una casilla con 2 y por lo menos alguno de los indices esté en un extremo de la matriz.

## Algoritmo de solución

El algoritmo se basa en una matriz de n x m con números 0 que representan el camino libre y 1 que representan la pared del laberinto.
Este deberá tener una función para explorar, es decir moverse desde una casilla hacia todas las direcciones posibles (izquierda, derecha, arriba y abajo) y marcarlas como visitadas.
Despues de encontrar la entrada(Una casilla del arreglo con el valor 0 que esté en alguno de los límites de los indices) comienza a explorar de manera recursiva.
La función explorar se llama a sí misma para marcar los vecinos como visitados y a partir de cada uno de estos marcar también los vecinos de los vecinos, de manera `Recursiva`.
Si la matriz tuviera un conjunto de ceros(camino) pero que no sean alcanzables desde la entrada (que tengan como obstaculos una pared de 1) estos jamás serán marcados como visitados.
Al final buscará la salida que es un valor 2(ya que este es un valor que ya ha sido recorrido, es decir, es alcanzable llegar a él desde la entrada, ya que si no lo fuera no estaría visitado) encontrado en los límites del arreglo.

## Código

```python
laberinto = [
    [1,1,1,1,1,1,1,1,1],
    [0,0,0,0,0,0,1,0,1],
    [1,1,1,0,1,1,1,0,1],
    [1,0,0,0,1,0,1,0,1],
    [1,0,1,1,1,0,1,0,1],
    [1,0,0,0,0,0,0,0,1],
    [1,0,1,1,1,0,1,0,1],
    [0,0,1,0,0,0,1,0,1],
    [1,1,1,1,1,1,1,1,1],
    ]

def encontrar_salida(laberinto):
    filas = len(laberinto)
    columnas = len(laberinto[0])

    # Función recursiva para marcar los vecinos como visitados
    def explorar(i, j):
        if 0 <= i < filas and 0 <= j < columnas and laberinto[i][j] == 0:
            laberinto[i][j] = 2  # Marcar como visitado

            # Movimientos posibles: arriba, abajo, izquierda, derecha
            movimientos = [(-1, 0), (1, 0), (0, -1), (0, 1)]

            for dx, dy in movimientos:
                explorar(i + dx, j + dy)

    entrada = [(i, j) for i in range(filas) for j in range(columnas) if laberinto[i][j] == 0 and (i == 0 or i == filas - 1 or j == 0 or j == columnas - 1)][0]

    # Llamar a la función explorar desde la entrada
    explorar(entrada[0], entrada[1])

    # Encontrar la salida del laberinto
    salida = [(i, j) for i in range(filas) for j in range(columnas) if laberinto[i][j] == 2 and (i == 0 or i == filas - 1 or j == 0 or j == columnas - 1) and (i, j) != entrada][0]

    return salida

salida_encontrada = encontrar_salida(laberinto)
print("Coordenada de salida:", salida_encontrada)

```
