#### Solución actividad 6

Luego de hacer el proceso de exploración con la tarjeta micro:bit, estas son mis respuestas:

**1.** En el punto 15 vemos que el Input son los botones con los que enviamos información desde la tarjeta hasta el sistema para que realice una salida por medio de la pantalla que sería el Output. Las instrucciones de este ejercicio son, en su mayoría, realizadas por la siguiente línea de código:

``` js
function draw() {

    if(port.availableBytes() > 0){
        let dataRx = port.read(1);
        if(dataRx == 'A'){
            fill('red');
        }
        else if(dataRx == 'B'){
            fill('yellow');
        }
        else{
            fill('green');
        }
        background(220);
        ellipse(width / 2, height / 2, 100, 100);
        fill('black');
        text(dataRx, width / 2, height / 2);
    }
```

**2.** Tal y como vimos en el punto 15, aquí también tenemos una entrada; sin embargo, este se diferencia de la anterior en que el dispositivo de entrada parece ser un sensor de movimiento. Al agitar la tarjeta micro:bit, recibimos un output pintando un color verde en la pantalla.

**3.** En el punto 17, vemos un proceso diferente de los 2 puntos anteriores, pues ahora el dispositivo de entrada ahora es el mouse con el que presionamos el botón virtual en el editor de código. Al presionar el botón, recibimos una salida en los leds de la tarjeta micro:bit, pintando un corazón, seguido de una cara feliz.


