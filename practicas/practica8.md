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

