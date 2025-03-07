#### Implementación semáforo en micro:bit

##### Paso 1: definición de estados:

- Lo primero que hice fue definir claramente los estados en los que el semáforo puede estar. Para un semáforo simple, los estados son Rojo, Amarillo y Verde.

##### Paso 2: Establecer los tiempos de duración para cada luz

- Luego, establecí cuántos segundos debe durar cada luz del semáforo antes de cambiar. Estos tiempos son típicos para simular un semáforo básico y proporcionan un ciclo adecuado de cambio entre las luces.

  - Por tanto, usé tiempos peredeterminados para cada estado:

  * **Rojo** = 3seg
  * **Amarillo** = 1seg
  * **Verde** = 5seg
 
##### Paso 3: Inicializar la máquina de estados

- Luego de esto, se debe crear una máquina de estados que maneje la lógica de cambiar entre los estados de semáforo. Por lo que, implementé una clase llamada Semaforo para manejar el cambio de estados.

  * Inicialicé el semáforo en el estado Rojo.
  * Usé un temporizador con ayuda de ChatGPT (start_time = utime.ticks_ms()) para controlar cuánto tiempo ha pasado desde que el semáforo empezó en su estado actual.

##### Paso 4: Programar el cambio de estado

- Después, hay que programar el cambio de un estado a otro después de que haya pasado un cierto tiempo.

  * En cada ciclo de actualización (actualizar()), el programa revisa el estado actual del semáforo.
  * Si el tiempo transcurrido desde start_time supera el tiempo configurado para el estado, el semáforo cambia al siguiente estado:

    **De Rojo a Verde.**
    **De Verde a Amarillo.**
    **De Amarillo a Rojo.**

   * Reinicié el temporizador (start_time = utime.ticks_ms()) cada vez que el semáforo cambia de estado.
 
  ##### Paso 5: Definir las acciones de cada estado

  - En cada estado, el semáforo se debe mostrar una representación visual adecuada en la pantalla ya que los LEDs de la micro:bit solo tienen color rojo.

    **Rojo:** Mostré un corazón en la pantalla para simular la luz roja.
    **Amarillo:** Mostré un cuadrado en la pantalla para simular la luz amarilla.
    **Verde:** Mostré una cara feliz en la pantalla para simular la luz verde.

  ##### Paso 6: Bucle principal

  - Luego, implementé un bucle while True que ejecuta continuamente el método actualizar() de la clase Semaforo. Esto asegura que el semáforo cambie de estado en función del tiempo y repita el ciclo.
 
  ##### Paso 7: Prueba y corrección

  - Finalmente, probé el programa y funcionó perfectamente por lo visto.
 
  ##### Paso 8: Código final

```python
from microbit import *
import utime

ROJO = 0
AMARILLO = 1
VERDE = 2

TIEMPO_ROJO = 3000     # 3 segundos
TIEMPO_AMARILLO = 1000 # 1 segundo
TIEMPO_VERDE = 5000    # 5 segundos

class Semaforo:
    def __init__(self):
        self.estado = ROJO
        self.start_time = utime.ticks_ms()

    def actualizar(self):
        if self.estado == ROJO:
            display.show(Image.HEART)  # Rojo representa corazón (usamos imagen de corazón como simulación)
            if utime.ticks_diff(utime.ticks_ms(), self.start_time) > TIEMPO_ROJO:
                self.estado = VERDE  # Cambiar a verde
                self.start_time = utime.ticks_ms()  # Reiniciar el temporizador

        elif self.estado == AMARILLO:
            display.show(Image.SQUARE)  # Amarillo representa un cuadrado (simulación)
            if utime.ticks_diff(utime.ticks_ms(), self.start_time) > TIEMPO_AMARILLO:
                self.estado = ROJO  # Cambiar a rojo
                self.start_time = utime.ticks_ms()  # Reiniciar el temporizador

        elif self.estado == VERDE:
            display.show(Image.HAPPY)  # Verde representa una carita feliz (simulación)
            if utime.ticks_diff(utime.ticks_ms(), self.start_time) > TIEMPO_VERDE:
                self.estado = AMARILLO  # Cambiar a amarillo
                self.start_time = utime.ticks_ms()  # Reiniciar el temporizador

semaforo = Semaforo()

while True:
    semaforo.actualizar()

```
  
 
  
