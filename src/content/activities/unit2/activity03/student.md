#### Exploración micro:bit y MicroPython

**1. Entradas Micro:bit:**
- Botones A y B
- Sensor de Movimiento o acelerómetro
- Sensor de Luz
- Entrada de señal de radio

**2. Salidas Micro:bit**
- Pantalla de luces LED
- Altavoz
- Conexión Bluetooth
- Salida de comunicación serial

**3. Funciones de MicroPython para entradas y salidas**

**- button_a.is_pressed():** Devuelve True si el botón A está presionado.

```python
if button_a.is_pressed():
display.show("A")
```

**- accelerometer.get_x():** Lee la aceleración en el eje X.

```python
x = accelerometer.get_x()
if x > 200:
    display.show("Right")
```

**- pin0.read_analog():** Lee un valor analógico de un pin de entrada.

```python
value = pin0.read_analog()
display.show(value)
```

**- display.show():** Muestra texto o gráficos en la pantalla LED.

```python
display.show("HELLO")
```

**- pin0.write_digital(1):** Envía una señal digital al pin especificado.

```python
pin0.write_digital(1)
```

**music.play():** Reproduce una melodía utilizando el altavoz.

```python
from microbit import music
music.play(music.POWER_UP)
```
