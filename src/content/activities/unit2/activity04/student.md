#### Experimentos

##### Experimento 1: Leer el estado del botón A

**Objetivo:** Analizar si el botón A se detecta correctamente cuando se presiona y si muestra el comportamiento esperado.

**Hipótesis:** Cuando presione el botón A, el micro:bit debería mostrar un carácter en la pantalla LED; En este caso una A, y no mostrar nada si el botón no está presionado.

**Proceso:** Primeramente conecté el micro:bit al computador. Luego abrí el editor y usando las funciones que investigué en la actividad anterior realicé este pequeño código:

```python
from microbit import *
   
while True:
    if button_a.is_pressed():
        display.show("A")
    else:
        display.clear()
```

- Primero agregué un `` while True:`` para que el código se ejecuté en bucle indefinidamente. Esto para que el programa verifique constantemente si el botón A se está presionando.

- Luego agregué la función de entrada que aprendí en la actividad anterior ``button_a.is_pressed():`` que supuse que era la mejor opción para este experimento.

- Después, usé la función de salida ``display.show("A")`` para probar si funcionaba para lo que suponía.

- Finalmente, agregué el ``else:`` y ``display clear()`` usando ayuda de chatGPT para la sintaxis que sirve para mantener los LEDs apagados si no se está presionando el botón A.

##### Experimento 2: Leer el estado del botón B

**Objetivo:** Analizar si el botón B se detecta correctamente cuando se presiona y si muestra el comportamiento esperado.

**Hipótesis:** Cuando presione el botón B, el micro:bit debería mostrar un carácter en la pantalla LED; en este caso una B, y no mostrar nada si el botón no está presionado.

**Proceso:** Para este experimento simplemente implementé los mismos pasos que en el experimento anterior pero modificando mínimamente el código para que funcionara con las instrucciones indicadas.

```python
from microbit import *

while True:
    if button_b.is_pressed():
        display.show("B")
    else:
        display.clear()
```

- Adicionalmente, integré ambos códigos para que al presionar el botón A, mostrara la A en pantalla; y al presionar el botón B, mostrara la B en pantalla.

```python
from microbit import *

while True:
    if button_a.is_pressed():
        display.show("A")
    elif button_b.is_pressed():
        display.show("B")
    else:
        display.clear()
  ```

- Lo único que cambió fue el ``elif`` que en python se utiliza como un else if en c++ y c#.


