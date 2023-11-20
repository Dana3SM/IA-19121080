# Tic Tac Toe de tres dimmensiones
## Estrategia
* Comenzar por una celda cualquiera, por ejemplo, la de la esquina. Se tiene una epsecie de marcador en esta ficha para seguir buscando movimientos.
    * Si el jugador incició primero la primera ficha puesta será la que bloqueé el movimiento del contrincante.
* En la siguiente iteracion, y a partir de la primera ficha tirada, se analizan las casillas ordenadas linealmente que esten desocupadas, es decir, se analizan las dos casillas de enfrente, de los lados, hacia abajo, etc, siempre y cuando esa fila o columna esten dos desoupadas(completamente libre).
    * De lo contrario (si no hay dos casillas en forma líneal libre) se buscan dos libres en cualquier diagonal.
* Cuando se cierre el camino se buscan las casillas libres (se repite el procedimiento), pero ahora a partir de la segunda ficha tirada,es decir el marcador pasa a la segunda ficha que se puso y así sucesivamente.
* Si no hay dos espacios vacios en linea o diagonal, busca el especio vacio mas cercano y ahora el marcador pasa a esta casilla..

## Medida de rendimiento
- En cuantos pasos gana o empata.
- Numero de victorias.


# Gallina, lechuga y Collote
### Secuencia de percepcion
* Se analiza cual es el depredador de todos los elementos a cruzar.
* Se analiza a cuales se puede comer cada elemento.
* El que tenga menos o ningun depredador se queda, junto con otro elemento que no sea su depredador (en este caso, la lechuga no es depredador de nadie y el collote no come lechugas)
    * Entonces nos llevamos la gallina
* En la siguiente iteración, hará lo mismo, como el collote es el más fuerte se queda y nos llevamos la lechuga.
* Al llegar del otro lado, se aplica el mismo proceso, la lechuga se queda porque no es depredador de nadie pero la gallina sí y nos llevamos a la gallina.
* En la siguiente dejamos la gannina y nos llevamos al collote...

#### Medida de rendimiento
- Que todos los elementos pasen sin ser comidos.
- En el menor numero de movimientos.

# Canibales y Monjes
### Secuencia de percepcion
* Se mandan dos iguales (dos canibales por ejemplo) y se regresa 1
* Se vuelven a mandar dos canibales hasta equilibrar ambos lados. Despues uno de ellos regresa el barco.
* Se comparan  cuantos monjes se tienen que mandar para que el numero del otro lado no sea menor al de canibales. Entonces se mandan 2.
* Se comparan  cuantos se tienen que mandar de regreso para que el numero del otro lado no sea menor al de canibales. Entonces se mandan uno de cada uno.
* En cada iteración, se comparan las posibles parejas a mandar para que, que siempre y cuando del otro lado o del mismo, al llegar no haya más canibales que monjes.
#### Medida de rendimiento
- Cuantas veces se va y regresa el barco.
- Que nunca haya mayor cantidad de canibales ni monjes de ninún lado.

# Ranas
### secuencia de percepción
* Se acerca la primera rana, la azul en este caso (brinca al espacio vacío).
* La rana del otro lado (roja) la salta.
* la rana azul rellena el espacio.
* la rana roja la salta
* La segunda rana azul rellena el espacio
* La rana roja lo salta
* La primera rana azul rellena el espacio
* La rana roja de la esquina lo salta
* La rana azul rellana el espacio.
* En este punto ya no hay más movimientos.

| A | A | A |   | R | R | R |
| - | - | - | - | - | - | - |
| A | A |   | A | R | R | R |
| A | A | R | A |   | R | R |
| A | A | R |   | A | R | R |
| A | A | R | R | A |   | R |
| A | A | R | R |   | A | R |
| A | A | R | R | R | A |   |
| A | A | R | R | R |   | A |



# Modelado del ponyfest

*Entradas posibles: 3 enradas correspondientes al año de los ultimos ponyfest, a si se hizo o no, y a que tan contenta salió la gente, en este caso podrían ser solo dos entradas, que serían si se realizó o no (1 o 0) y si la gente quedó contenta o no (0,1).
*Salidas esperadas: la salida es un alto o bajo, correspondiente a si se realizará el siguiente evento.


