#### Sonidos con micro:bit 

- Esta actividad fue más sencilla, simplemente usé chatGPT para pedirle que al presionar los botones de micro:bit, reprodujera 2 melodías diferentes. Aquí no hubo ningún fallo.

  Estos fueron los códigos:

**p5.js**

```js
let soundA;
let soundB;

function preload() {
  soundA = loadSound('soundA.mp3'); // Carga un archivo de sonido o usa una frecuencia
  soundB = loadSound('soundB.mp3');
}

function setup() {
  createCanvas(400, 200);
  textAlign(CENTER, CENTER);
  textSize(32);
}

function draw() {
  background(220);
  text('Presiona A o B', width / 2, height / 2);
}

function keyPressed() {
  if (key === 'A' || key === 'a') {
    if (!soundA.isPlaying()) {
      soundA.play();
    }
  } else if (key === 'B' || key === 'b') {
    if (!soundB.isPlaying()) {
      soundB.play();
    }
  }
}
```
**MicroPython**
```py
from microbit import *
import music

while True:
    if button_a.is_pressed():
        # Tocar una melodía o un tono cuando se presiona el botón A
        music.play(music.PYTHON)
        
    if button_b.is_pressed():
        # Tocar otro tono o melodía cuando se presiona el botón B
        music.play(music.DADADADUM)
        
    sleep(100)  # Para evitar lecturas repetidas rápidas
```

- Finalmente, le pregunté por el funcionamiento línea por línea de este código a ChatGPT para comprenderlo de una mejor manera.
