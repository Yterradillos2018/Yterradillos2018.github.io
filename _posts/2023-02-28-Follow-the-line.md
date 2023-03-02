---
title:  "Follow The Line"
mathjax: true
layout: post
categories:
  -github
  -website
---

## Explicación del Codigo 
Hola a todos, en este blog de robótica vamos a analizar un código que nos permitirá entender cómo funciona un controlador PD en un robot.

El código comienza con la importación de las bibliotecas necesarias, como GUI, HAL, numpy y cv2. GUI es la biblioteca que permite la visualización de
imágenes, HAL es la biblioteca que interactúa con el hardware y los sensores del robot, numpy es una biblioteca que proporciona una serie de funciones
matemáticas útiles y cv2 es una biblioteca de procesamiento de imágenes.

A continuacion, se establecen tres variables que son importantes para el controlador PD, E_PREV, E_SUM y K_P, K_D. E_PREV es la variable que guarda el
valor del error de la iteración anterior, E_SUM es la variable que acumula todos los errores anteriores, K_P y K_D son las constantes de ganancia
proporcional y derivativa del controlador PD.

La variable CONTADOR se establece en cero, ya que se utilizará más adelante en el código. La variable imagen obtiene la imagen actual de la cámara.

Luego viene el bucle while, que se ejecuta constantemente. Primero, se muestra la imagen actual utilizando la biblioteca GUI.showImage(imagen). A
continuación, se recorta la imagen en una región de interés específica utilizando la función imagen_recortada = imagen[100:300, 100:550].

Después, se establecen los límites RGB para filtrar el color rojo en la imagen. Se crea una máscara utilizando la función cv2.inRange(imagen_recortada,
limite_inferior, limite_superior). La máscara es una imagen binaria que representa los píxeles que cumplen con las condiciones establecidas por los
límites.

Luego, se define el centroide de la imagen recortada utilizando la función cv2.moments(mascara). CX y CY son las coordenadas del centroide, que se
utilizan más adelante en el código.

Se dibuja un círculo en el centroide utilizando la función cv2.circle(imagen_recortada, (int(CX), int(CY)), 2, (255, 0, 0), 6).

A continuación, se extrae la primera CX, que es cuando el coche está centrado, y se establece en la variable cx_centrado. La variable CONTADOR se
establece en 1 para que no se extraiga CX nuevamente.

Luego, se construye el controlador PD utilizando la fórmula:

U = K_P * E + K_D * (E - E_PREV)

donde U es la salida del controlador, E es el error actual, K_P y K_D son las constantes de ganancia proporcional y derivativa y E_PREV es el error de la
iteración anterior.

Si U está entre -0.5 y 0.5, se incrementa la velocidad del robot hasta que alcance el límite de 6 unidades. Si U no cumple esta condición, la velocidad
se establece en 3.

Finalmente, se establecen las velocidades lineal y angular utilizando las funciones HAL.setV(speed) y HAL.setW(U). La vista del coche se muestra una vez
más utilizando la función GUI.showImage(imagen).

