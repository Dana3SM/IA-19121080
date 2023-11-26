# Juego de alfiles

## Introducción

El juego de ajedrez es conocido por su complejidad estratégica y táctica. Cada una de las piezas de ambos bandos tienen diferentes movimientos dependiendo deque pieza sea, ademas de que el objetivo sea atacar al rey y a las piezas oponentes, si tuvieramos que diseñar un agente que juegue al ajedrez, este tendría que tener todos loss posibles estados de las piezas, para poder anticipar o planear hacia donde moverse y saber que hacer despues de que la pieza del oponente se mueva, pero si todas las piezas fueran iguales serían un poco más simple, este problema podría ser resuelto con una secuencia más simple y corta, como en el problema que se plantea a continuación.

Se tienen ocho alfiles (cuatro negros y cuatro blancos) en un tablero deajedrez reducido, el tablero tiene 4 columnas y 5 filas. El problema consiste en hacerque los alfiles negros intercambien sus posiciones con los blancos, ningún alfildebe atacar en ningún momento otro del color opuesto. Se deben alternarlos movimientos, primero uno blanco, luego uno negro, luego uno blanco yasí sucesivamente. ¿Cuál es el mínimo número de movimientos en que sepuede conseguir?.El juego se ve de la siguiente manera:

|  N   |  N   |  N   |  N   |
|  -   |  -   |  -   |  -   |
|  -   |  -   |  -   |  -   |
|  -   |  -   |  -   |  -   |
|  B   |  B   |  B   |  B   |

Donde las letras B representan un alfil blanco y las N un alfil negro.

En este ensayo, se analiza una solución para el problema específico, que es intercambiar posiciones entre alfiles blancos y negros en un tablero de ajedrez reducido. La meta es lograr este intercambio sin que ningún alfil ataque a otro del color opuesto y además, buscar el menor número de movimientos posibles.


## Solución

Primero, debemos saber cual es la medida de rendimiento, en este caso, es que se logre resolver con el menor número de movimientos posibles, como si cada movimiento "gastara" energía, por así decirlo.

Para descurbir el número de movimientos necesarios para que todos los alfiles estén como la solución lo plantea, primero debemos darnos cuenta de, que dado que del otro lado hay una fila de alfiles del otro color, los cuales no pueden ser derribados por el oponente, estos deberán quitarse del camino para poder despejarlo. Entonces, los alfiles de abmos colores deberán hacer movimientos espejo, ya que, al intentar solucionar de otra manera, muchas veces algunos alfiles bloqueaban a otros y se quedaba sin solución o con un número de movimientos demasiado e inecesariamente grande para el problema, que en realidad no es tan complejo.
También es necesario conocer como se mueven las piezas, es decir, en que dirección y cuantas casillas pueden avanzar.
Así también, en el camino a encontrar la solución, encontré que los movimientos espejo no podpian ser tan cuál espejo, no se aplica el mismo movimiento al alfil de abajo del otro color, sino que se aplica el movimiento al alfil de la esquina o diagonal opuesta.


### Identificación del entorno

* Se sabe que los alfiles `se mueven en diagonal` el número de casillas que sean necesarias.
* En este caso, los alfiles no pueden "comer" o atacar otros alfiles, por lo que, si hay algun alfil en esa dirección, están bloqueados.
* El objetivo de la solución es llegar del otro lado con el menor número de movimientos posibles, por ello, se optará por `avanzar la mayor cantidad de casillas posible`. 
* Los movimientos se repetirán en forma de `espejo invertido`, ya que, de otra menera los alfiles se bloquean.
* Es importante realizar los mismos movimientos de ambos lados, ya que, las reglas dicen que cada uno debe hacer unmovimiento a la vez despues del otro, y al ser movimientos alternados, iremos quitando los de un lado para colocar los del otro, así susesivamente.
* Algo muy importante a considerar, es que el objetivo es llegar al otro lado, por lo que, la prioridad es avanzar en ese sentido, hacia el lado contrario de su lugar de origen, por lo que en cualquier secuencia se prioriza ir en ese sentido.

Con estos datos se procede a encontrar una solución y una secuencia de percepción.

### Desarrollo de la solución

1. Enumeración y movimientos iniciales.

Comenzamos asignando números a los alfiles negros y blancos, siguiendo un patrón específico. Estos números indican el orden en el que se moverán los alfiles, el agente llevará un conteo para no  errar en el orden. Se enumeran por ejemplo `los alfiles negros del 1 al 4 de izquierda a derecha`, mientras que los blancos se invierte el orden, estarán enumerados `del 1 al 4 de derecha a izquierda`.
Como ya se había mencionado los alfiles buscarán avanzar la mayor cantidad de casillas posibles, por lo que, la dirección(izquierda o derecha) en la que vayan, dependerá de donde hay más espacios vacios, siempre y cuando sea hacia el frente(al lado contrario de donde se comenzó)
primer alfil de cada color buscará avanzar la mayor cantidad de recuadros posibles en diagonal, preferentemente hacia adelante.

2.Selección de Direcciones de Movimiento.
En cada turno, cada alfil evalúa las direcciones disponibles y elige la que le permita avanzar la mayor cantidad de casillas, tomando en cuenta que esta este direccionada hacia la meta. Si hay dos opciones equivalentes, se prefiere la que acerque al alfil a sus compañeros del mismo color. Este enfoque estratégico asegura una coordinación efectiva entre los alfiles.

3. Superación de Obstáculos.
El agente lleva una secuencia de movimientos para llevar un control y que la estrategia funcione de acuerdo al plan, se comienza el movimiento por, por ejemplo, el alfíl negro número 1, siguiendo el blanco número 1 y así `susesivamente`.
Si un alfil tiene todos los caminos que llevan hacia el frente bloqueados, se prioriza el movimiento del siguiente alfil en la secuencia. Esta estrategia evita bloqueos y garantiza que los alfiles continúen avanzando hacia sus destinos finales.

4. Movimientos Espejo.
Para evitar saltos en la numeración y mantener la sincronización entre alfiles del mismo número pero de colores opuestos, se implementan movimientos espejo. Si un alfil salta un número, el alfil del otro color también salta un número en la secuencia, por ejemplo, si se salta el negro número 3, sin importar que al mover el negro número 4 se libera el camino del blanco número 3, este también habrá saltado un número en la secuencia de movimiento, esto para mantener la coherencia en el intercambio.

5. Llegada a la Meta.
La estrategia culmina con la llegada de los alfiles a sus destinos finales. A medida que cada alfil avanza, se crea una formación específica que permite a los alfiles posteriores moverse de manera eficiente.
Cuando un alfíl llega a la meta, este ya no se mueve, ya no regresa.

### Secuencia de percepción.

*Como se enumeran, los alfiles negros ahora serán representados como N1,N2,N3 Y N4, respectivamente y los blancos como B1, B2, B3 Y B4 .

|  N1  |  N2  |  N3  |  N4  |
|  -   |  -   |  -   |  -   |
|  -   |  -   |  -   |  -   |
|  -   |  -   |  -   |  -   |
|  B4  |  B3  |  B2  |  B1  |

Y sus movimientos se verán de la siguiente manera:
1.

|  -   |  N2  |  N3  |  N4  |
|  -   |  -   |  -   |  -   |
|  -   |  -   |  -   |  -   |
|  -   |  -   |  -   |  N1  |
|  B4  |  B3  |  B2  |  B1  |

2.

|  -   |  N2  |  N3  |  N4  |
|  B1  |  -   |  -   |  -   |
|  -   |  -   |  -   |  -   |
|  -   |  -   |  -   |  N1  |
|  B4  |  B3  |  B2  |  -   |

3.

|  -   |  -   |  N3  |  N4  |
|  B1  |  -   |  -   |  -   |
|  -   |  -   |  -   |  N2  |
|  -   |  -   |  -   |  N1  |
|  B4  |  B3  |  B2  |  -   |

4.

|  -   |  -   |  N3  |  N4  |
|  B1  |  -   |  -   |  -   |
|  B2  |  -   |  -   |  N2  |
|  -   |  -   |  -   |  N1  |
|  B4  |  B3  |  -   |  -   |

5.

|  -   |  -   |  -   |  N4  |
|  B1  |  -   |  -   |  N3  |
|  B2  |  -   |  -   |  N2  |
|  -   |  -   |  -   |  N1  |
|  B4  |  B3  |  -   |  -   |

6.

|  -   |  -   |  -   |  N4  |
|  B1  |  -   |  -   |  N3  |
|  B2  |  -   |  -   |  N2  |
|  B3  |  -   |  -   |  N1  |
|  B4  |  -   |  -   |  -   |

7.

|  -   |  -   |  -   |  -   |
|  B1  |  -   |  -   |  N3  |
|  B2  |  N4  |  -   |  N2  |
|  B3  |  -   |  -   |  N1  |
|  B4  |  -   |  -   |  -   |

8.

|  -   |  -   |  -   |  -   |
|  B1  |  -   |  -   |  N3  |
|  B2  |  N4  |  B4  |  N2  |
|  B3  |  -   |  -   |  N1  |
|  -   |  -   |  -   |  -   |

9.

|  -   |  -   |  -   |  -   |
|  B1  |  -   |  -   |  N3  |
|  B2  |  N4  |  B4  |  N2  |
|  B3  |  -   |  -   |  -   |
|  -   |  -   |  N1  |  -   |

10.

|  -   |  B1  |  -   |  -   |
|  -   |  -   |  -   |  N3  |
|  B2  |  N4  |  B4  |  N2  |
|  B3  |  -   |  -   |  -   |
|  -   |  -   |  N1  |  -   |

11.

|  -   |  B1  |  -   |  -   |
|  -   |  -   |  -   |  N3  |
|  B2  |  N4  |  B4  |  -   |
|  B3  |  -   |  -   |  -   |
|  -   |  N2  |  N1  |  -   |

12.

|  -   |  B1  |  B2  |  -   |
|  -   |  -   |  -   |  N3  |
|  -   |  N4  |  B4  |  -   |
|  B3  |  -   |  -   |  -   |
|  -   |  N2  |  N1  |  -   |

13. Notemos que en este caso el número que sigue de moverse es el negro número 3, pero este tiene todos los caminos bloqueados, por lo que el contador de orden de movimientos pasa al siguiente elemento, el 4, esto aplicará para ambos colores, segpun las reglas que establecimos, aunque el siguiente movimiento le despeje el camino al blanco número 3.

|  -   |  B1  |  B2  |  -   |
|  -   |  -   |  -   |  N3  |
|  -   |  -   |  B4  |  -   |
|  B3  |  -   |  -   |  -   |
|  -   |  N2  |  N1  |  N4  |

14.

|  B4  |  B1  |  B2  |  -   |
|  -   |  -   |  -   |  N3  |
|  -   |  -   |  -   |  -   |
|  B3  |  -   |  -   |  -   |
|  -   |  N2  |  N1  |  N4  |

15.

|  B4  |  B1  |  B2  |  -   |
|  -   |  -   |  -   |  -   |
|  -   |  -   |  -   |  -   |
|  B3  |  -   |  -   |  -   |
|  N3  |  N2  |  N1  |  N4  |

16.

|  B4  |  B1  |  B2  |  B3  |
|  -   |  -   |  -   |  -   |
|  -   |  -   |  -   |  -   |
|  -   |  -   |  -   |  -   |
|  N3  |  N2  |  N1  |  N4  |



## Conclusión

Establecer algunas reglas como el movimiento igual para ambas partes, ayuda a establecer una estrategia más segura basada en `lógica` en vez de `adivinación`, para evitar bucles o gastar demasiados movimientos  de manera inecesaria.
La resolución del problema de intercambio de alfiles en el ajedrez no solo requiere movimientos individuales cuidadosamente planificados, sino también una coordinación estratégica entre los alfiles de cada color. La implementación de movimientos espejo, la preferencia por direcciones más beneficiosas y la adaptabilidad frente a obstáculos son elementos clave para lograr el intercambio de manera eficiente y sin conflictos.
Esta creación de una estrategia hará que, diseñar un agente sea una tarea más fácil que darle una lista de pasos enorme, en vez de solo algunas reglas y además, hará que el agente sea fácilmente escalable y ajustable a otros problemas.

