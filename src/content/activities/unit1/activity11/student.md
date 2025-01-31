#### Desarrollo actividad 11

- Al igual que en los demás ejercicios, tomé como base el código creado en la actividad 6. Luego simplemente localicé el lugar del código en el que cambia el color para modificarlo y que simplemente cambie la posición.

Este fue el lugar:

```js
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

- Finalmente, le pedí a chatGPT que modificara ese fragmento de código para mover el circulo en el eje x con los botones. Este es el código final:

[Enlace al proyecto](https://editor.p5js.org/JoseDRP/sketches/V8JAG4epS)

```js
let port;
let connectBtn;
let circleX = 200;  // Posición inicial del círculo en el eje X
let circleY = 200;  // Posición del círculo en el eje Y (fijo en el centro)

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
    let sendBtn = createButton('Send Love');
    sendBtn.position(220, 300);
    sendBtn.mousePressed(sendBtnClick);
    fill('white');
}

function draw() {
    if (port.availableBytes() > 0) {
        let dataRx = port.read(1);
        
        // Si el botón A se presiona, mover el círculo hacia la izquierda
        if (dataRx == 'A') {
            circleX -= 10;  // Mueve el círculo hacia la izquierda
        }
        // Si el botón B se presiona, mover el círculo hacia la derecha
        if (dataRx == 'B') {
            circleX += 10;  // Mueve el círculo hacia la derecha
        }

        // Asegurarse de que el círculo no se salga del canvas
        circleX = constrain(circleX, 50, width - 50);

        // Dibujar el círculo en la nueva posición
        background(220);
        fill('blue');
        ellipse(circleX, circleY, 50, 50);  // Dibuja el círculo con diámetro de 50px
        fill('black');
        text(dataRx, width / 2, height / 2);
    }

    // Cambiar el texto del botón dependiendo del estado de la conexión
    if (!port.opened()) {
        connectBtn.html('Connect to micro:bit');
    } else {
        connectBtn.html('Disconnect');
    }
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);  // Conecta con el puerto del micro:bit (ajustar el nombre según sea necesario)
    } else {
        port.close();  // Cierra la conexión
    }
}

function sendBtnClick() {
    port.write('h');
}
```
