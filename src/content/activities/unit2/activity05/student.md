#### Experimento recepción de datos seriales

- Para comenzar con este experimento, utilicé la actividad 12 como punto de partida. En este punto creé 2 botones en la interfaz de p5 para que al presionarlos, los LEDs cambiaran y así formar figuras diferentes. Aquí logré entender el funcionamiento de la micro:bit a la hora de comunicar datos seriales tanto de un lado como del otro.

- Lo que quise a hacer para este nuevo experimento fue que al presionar el botón comenzara una serie de imagenes continuas que pasen cada segundo, algo como una animación; y al presionar el botón STOP, la animación pare. Es algo similar a la actividad base pero con dificultad añadida.

 - Primero le pregunté a chat gpt con el siguiente prompt:

"Anteriormente, hice un programa en el que al presionar un boton en la interfaz de p5.js cambiaba unas figuras. Pero solo cada vez que presionaba cambiaba. Estos eran los codigos: (Aquí van los códigos del ejercicio mencionado)"

"Ahora, quiero hacer que al presionar un boton en la interfaz de p5.js, la tarjeta muestre una serie de imágenes continuas y al presionar otro botón, paren"

- ChatGPT generó el siguiente código:

p5.js:
```js
let port;
let connectBtn;
let startBtn, stopBtn;
let isAnimating = false; // Variable para controlar la animación

function setup() {
    createCanvas(400, 400);
    background(220);

    // Conexión con el puerto serie
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);

    // Botones virtuales en la pantalla
    startBtn = createButton('Start Animation');
    startBtn.position(50, 350);
    startBtn.mousePressed(startAnimation);

    stopBtn = createButton('Stop Animation');
    stopBtn.position(200, 350);
    stopBtn.mousePressed(stopAnimation);

    // Deshabilitar el botón de detener al inicio
    stopBtn.attribute('disabled', true);
}

function draw() {
    if (!port.opened()) {
        connectBtn.html('Connect to micro:bit');
    } else {
        connectBtn.html('Disconnect');
    }
}

function startAnimation() {
    if (port.opened()) {
        isAnimating = true;
        port.write('START');  // Enviar comando para iniciar la secuencia
        startBtn.attribute('disabled', true);  // Deshabilitar el botón de inicio
        stopBtn.attribute('disabled', false);  // Habilitar el botón de detener
    }
}

function stopAnimation() {
    if (port.opened()) {
        isAnimating = false;
        port.write('STOP');  // Enviar comando para detener la secuencia
        stopBtn.attribute('disabled', true);  // Deshabilitar el botón de detener
        startBtn.attribute('disabled', false);  // Habilitar el botón de inicio
    }
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close();
    }
}
```

MicroPython:

```py
from microbit import *
import time

# Inicializa el UART
uart.init(baudrate=115200)

# Lista de imágenes para mostrar
images_list = [Image.HAPPY, Image.SAD, Image.SURPRISED, Image.HEART]

# Variable para controlar la animación
animating = False

def start_animation():
    global animating
    animating = True
    while animating:
        for img in images_list:
            display.show(img)
            sleep(500)  # Mostrar cada imagen durante 500 ms
            if not animating:  # Si se ha detenido, salir del bucle
                break

def stop_animation():
    global animating
    animating = False
    display.clear()  # Limpiar la pantalla

# Bucle principal
while True:
    # Espera por los comandos de la interfaz
    if uart.any():
        data = uart.read(1)
        if data:
            if data[0] == ord('S'):  # Comando 'S' para empezar la animación
                start_animation()
            elif data[0] == ord('T'):  # Comando 'T' para detener la animación
                stop_animation()

    # También controla si el botón A o B son presionados en la micro:bit
    if button_a.is_pressed():
        uart.write('A')  # Enviar 'A' cuando el botón A es presionado
        sleep(500)
    if button_b.is_pressed():
        uart.write('B')  # Enviar 'B' cuando el botón B es presionado
        sleep(500)

```
 
- Al probar esto, ví que funcionaba casi perfectamente, exceptuando el botón de STOP que aparece desactivado en todo momento y no es posible parar la animación. Para solucionar esto simplemente agregué una función que comprueba si la animación está activa (usando la variable isAnimating), y actualiza el estado de los botones "Start" y "Stop" según corresponda.

