---
title:  "Vacuum Cleaner"
mathjax: true
layout: post
categories:
  -github
  -website
---

## Explicación del Codigo 

En este primer post del blog de Robótica voy a dar una pequeña explicación sobre como he desarrollado la primera práctica de la asignatura. Para esta
práctica tenemos que hacer el código python para una aspiradora robot. Tendremos que implementar lo aprendido en clase en La platarforma Unibotics la
cual nos permitirá introducir codigo python y ver una simulacion de lo que estamos implementado con este código.

El objetivo será hacer un video de 5 minutos de dicha simulación y en este tiempo intentar conseguir la mejor puntuacion posible. Para ello en nuestro
código python tendremos que tener como funciones diferentes estados en los que puede estar nuestro robot por ejemplo: esperando a chocar, chocado, 
girando a la izquierda, girando a la derecha, etc.

El codigo empezará con un while True para hacer un bucle infinito de nuestro codigo. Dentro del while True lo unico que vamos a tener será la función
execute que va a ser la funcion que se va a estar ejecutando todo el rato en bucle infinito y que corresponderia a nuestro primer estado del robot, 
el estado "ejecutando". Dentro de la función execute lo primero que hago es sacar un numero aleatorio del 1 al 10 y tras esto imprimiremos por el 
terminal los datos de los laseres, tanto los de la izquierda como los de la derecha y el centro. Para ello hemos usado la función HAL.getLaserData() la
cual devuelve los datos de los laseres. También he creado una función "average_laser_data(laser_data, min_angle, max_angle)" la cual da una media de los
datos de los laseres entre un angulo minimo y un angulo máximo.

Tras imprimir los datos de los laseres por terminal lo siguiente que haremos será comprobar si hemos terminado de hacer la espiral inicial. Si 
spiral_done == False entonces esto significará que no hemos terminado de hacer la espiral por lo cual entramos en una parte del código por el otro
lado si spiral_done == True pasaremos al siguiente estado que será bumpandgo.

Primero voy a explicar brevemente como he hecho la espiral del principio para ello he creado una variable inicializada a False la cual he llamado
spiral_done, siempre que esta variable este en False vamos a hacer que nuestro robot se desplace hacia adelante y que ademas gire, esto lo hacemos con
las 2 siguientes instrucciones:  HAL.setV(spiral_speed) HAL.setW(2). Además tambien vamos a tener que ir aumentando poco a poco la velocidad y para ello
usamos la siguiente linea spiral_speed += 0.03 (cada vez que la condición spiral_done == False se cumpla aumentaremos un 0.03 la velocidad de la 
espiral). Seguido a esto tendremos un if en el cual si se cumple alguna de las condiciones que aparecen pondremos las siguientes lineas de código:

            spiral_done = True
            spiral_speed  = 0.2
            HAL.setW(0)
            rospy.sleep(0.75)
 
 Esto nos cambiara la variable de spiral_done a true lo que determinará que ya hemos terminado de hacer nuestra espiral inicial y ya no volveremos a 
 entrar nunca más a esta parte del código.
 
 Lo siguiente a explicar sería la función bunandgo(). Esta función su primera instrucción será la de hacer que el robot se mueva hacia adelante
 (HAL.setV(2)). Después tendremos que comprobar si el robot se ha chocado por la izquierda, por la derecha o por el centro con la función 
 HAL.getBumperData().state. Dependiendo por que lado se choque vamos a girar hacia un lado o hacia el otro, incluso si nos chocamos por el centro
 tendremos opción a hacer un giro de 180ª. Para esto ultimo tenemos la función bump(), que lo unico que hará será girar el robot a izquierdas o a 
 derechas dependiendo de por que parte nos hayamos chocado.
 
 Para terminar todo lo explicado anteriormente se repitirá en un bucle infinito.
 
 [Aqui](https://www.youtube.com/channel/UCasNVT5uSNgtYm2MVWf0zKg) dejo un enlace al video de la ejecución de todo lo explicado anteriormente.
 
 {% include embed.html url="https://www.youtube.com/watch?v=teLzl2Px4YA" %}








