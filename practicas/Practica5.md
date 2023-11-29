# Conteo de elementos de un mismo color

El color es una de las características que nos permite a los seres humanos identificar y clasificar los objetos. La percepción visual del color se genera en nuestro cerebro a partir de las ondas electromagnéticas reflejadas por los objetos y captadas por los ojos. 
Si a un humano se le pide la tarea de detectar en una imagen los objetos de un color en específico(supongamos rojo), este podrá realizar la tarea sin mayor dificultad(a menos que padezca algun mal genetico o enfermedad que le impida ver adecuadamente los colores), pero para el computador, se deben emplear metodos de color, que son una serie de formulas que sirven para separar el color en base a rangos numéricos.

La segmentación de color es una técnica fundamental en el campo de visión por computadora, utilizada para aislar áreas específicas de una imagen basándose en sus propiedades cromáticas. El problema de contar segmentos de un color se presenta en numerosos contextos, desde la identificación de objetos en fotografías hasta aplicaciones más avanzadas como el seguimiento de elementos específicos en secuencias de video. 

En este ensayo se verá la resolución de un problema de segmentación de color, usando la librería de opencv, que tiene algunos metodos que sirven para separar los canales de color en una imagen y segmentar el color dependiendo del rango que se le dé, a continuación se explica un poco que son los espacios de color para entender como funciona esta segmentación.

## ¿Qué son los espacios de color?

En el espacio de color más común, RGB (Rojo Verde Azul), los colores se representan en términos de sus componentes rojo, verde y azul. En términos más técnicos, RGB describe un color como una tupla de tres componentes. Cada componente puede tomar un valor entre 0 y 255, donde la tupla (0, 0, 0)representa el negro y (255, 255, 255)representa el blanco.
La combinación de estos tres canales de color da como resultado todos los colores que nosotros vemos en una imagen, pero no es la unica manera de combinar estos canales.
Existen más espacios de color, como el CMYK, HED, HSV, HSL, entre otros, que difieren en el orden de las capas o componentes del color y por lo tanto, muestran un resultado distinto.[1](#referencias)
Pero, ¿de que manera nos ayuda el intercambio de canales de color a la hora de intenta separar los objetos de un color dentro de una imagen?
Explicado de manera simple, en un programa, con ayuda de la librería opencv, se hace el cambio de un espacio de color a otro para, con la ayuda de cierto rango de color separar los objetos de un color, específicamente los objetos de color rojo.

```python
import cv2 as cv
import numpy as np

img=cv.imread('foto1.jpeg',1)
img2 = cv.cvtColor(img, cv.COLOR_BGR2RGB)
img3 = cv.cvtColor(img2, cv.COLOR_RGB2HSV)

umbralBajo=(0, 80, 80  )
umbralAlto=(10, 255, 255)
umbralBajoB=(170, 80,80)
umbralAltoB=(180, 255, 255)
```

La primera parte de la resolución de este problema consiste en cargar la imagen y pasarla al espacio de color HSV para, a partir de aquí aislar el color.
Los valores del umbral alto y bajo son los correspondientes a los valores rojos, si se quisiera, se puede ajustar un poco más este para aceptar más colores o para hacerlo menos sensible, se tienenn dos ya que el color rojo tiene dos rangos numericos.
Una vez hecho esto, se hace la creación de máscaras binarias, se generan dos máscaras, cada una identificando píxeles dentro de un rango específico de color, las mascaras son una matriz del tamaño de la imagen, con valores 0 y 1 (0 y 255) correspondientes a donde encontró o aisló el color del umbral que específicamos y en el resultado se muestran los valores de la imagen original que se encuentran donde la mascara tiene valores 255.
 
```python
mascara1 = cv.inRange(img3, umbralBajo, umbralAlto)
mascara2 = cv.inRange(img3, umbralBajoB, umbralAltoB)

mascara = mascara1 + mascara2

resultado = cv.bitwise_and(img, img, mask=mascara)

cv.imshow('resultado', resultado)
cv.imshow('mascara', mascara)

cv.waitKey(0)
cv.destroyAllWindows()
```

Este código mostrará la fragmentación de los objetos de color rojo en una imagen.

## Conteo

Ahora bien, ¿Cómo podemos contar estos segmentos de color?
En un ejercicio anterior, se hizo el conteó de islas, que es la acumulación de celdas de un color diferente dentro de una matriz, en este caso, se sigue la misma lógica, ya que, la mascara del umbral, contiene acumulaciones de valores 255, correspondientes a los lugares donde se encuentran los objetos de color rojo, por lo que solo hay que ajustar el método de conteo de islas que hice anteriormente para que funcione con la máscara, que al final es una matriz de valores también.


```python

def contar_objetos(matriz):
    objetos_contados = 0

    for i in range(len(matriz)):
        for j in range(len(matriz[0])):
            if matriz[i][j] == 255:
                objetos_contados += 1
                explorar_objeto(matriz, i, j)

    return objetos_contados

def explorar_objeto(matriz, i, j):
    if 0 <= i < len(matriz) and 0 <= j < len(matriz[0]) and matriz[i][j] == 255:
        matriz[i][j] = 0  # Marcar el píxel como visitado

        explorar_objeto(matriz, i - 1, j - 1)
        explorar_objeto(matriz, i, j - 1)
        explorar_objeto(matriz, i + 1, j - 1)
        explorar_objeto(matriz, i - 1, j)
        explorar_objeto(matriz, i + 1, j)
        explorar_objeto(matriz, i - 1, j + 1)
        explorar_objeto(matriz, i, j + 1)
        explorar_objeto(matriz, i + 1, j + 1)

```

El código es el mismo que se usó anteriormente para el problema del conteo de islas, recorre la matriz en busca del valor 255, cuando lo encuentra aumenta el contador y de manera recursiva se va a visitar todos los vecinos de esa celda de la matriz para marcarlos como visitados, para así no contar cada pixel como otro objeto y seguir recorriendo la matriz.
Al realizar el conteo podría salir un valor muy alto, por ejemplo en mi caso me sale que son 104 objetos contados, ya que, por la luz de la imagen podría haber pequeños fragmentos de color rojo separados unos de otros, entonces el metodo cuenta como diferentes objetos todos estos pequeños puntos, esto se podría arreglar ajustando el umbral, pero dependerá de la imagen.
También existe un metodo para contar los objatos a partir de identificar los contornos de otro color en una imagen, pero, de manera más manual, esta es la manera de resolver este problema.

# Conslusión

Como vimos, la segmentación de color es un proceso muy util para la visión computacional ya que, le permite a la maquina identificar objetos, por ejemplo, si nosotros como humanos, vemos una imagen con frutas y se nos pide identificar las manzanas, podremos hacerlo muy fácilmente, si es que hemos visto una manzana anteriormente, pero si a un computador se le pide realizar el mismo proceso tendrá que hacerlo en base a las características que tienen las manzanas, una de estas características podría ser el color, por ello es necesario usar segmentación de color,sacado con ayuda de los diferentes espacios de color que existen y formulas que nos ayudaran a separar algunos colores de otros.

# Referencias

[Python, R. (2018, septiembre 26). Image segmentation using color spaces in OpenCV + Python. Realpython.com; Real Python. https://realpython.com/python-opencv-color-spaces/

](https://realpython.com/python-opencv-color-spaces/)