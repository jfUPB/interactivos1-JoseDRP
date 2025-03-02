#### Análisis y respuestas del código planteado

##### ¿Cómo funciona el programa?

Este programa hace que dos píxeles en la pantalla de la micro:bit parpadeen. La pantalla de la micro:bit tiene una secuencia de 5x5 píxeles, y cada píxel puede tener un brillo entre 0 (apagado) y 9 (encendido).

El programa utiliza una clase llamada Pixel, que maneja cada píxel individualmente. Cada objeto Pixel tiene su posición en la pantalla (por ejemplo, (0,0) o (4,4)), un intervalo de tiempo para decidir cada cuánto cambiar su estado (por ejemplo, 1 segundo o medio segundo) y un estado inicial (0 o apagado).

**Lógica del programa:**

- Cuando el programa comienza, el píxel se inicializa en un estado de apagado (0) y se guarda el tiempo en que empezó.

- Luego, el programa espera un intervalo de tiempo. Después de que ese tiempo pasa, cambia el estado del píxel entre apagado (0) y encendido (9), y actualiza la pantalla para reflejar este cambio.

- Finalmente, repite este ciclo. El programa siempre está esperando y luego cambiando el estado del píxel de acuerdo con el tiempo que ha pasado.

##### ¿Cuáles son los estados de este programa?

Los estados representan momentos en los que el programa espera que ocurran ciertos eventos, como el paso del tiempo o la actualización de un píxel. Los estados que pude identificar en este programa son:

- En el estado **Init**, el píxel aún no ha comenzado a parpadear. En este estado, el programa solo establece el tiempo de inicio.

- En el estado **WaitTimeout**, el programa espera un intervalo de tiempo. Una vez que ha pasado el tiempo suficiente, el programa cambia el estado del píxel y lo muestra en la pantalla.

##### ¿Cuáles son los eventos de este programa?

Los eventos son los momentos que el programa "observa" o espera mientras está en un estado. Son condiciones que deben cumplirse para que el programa cambie de estado o ejecute alguna acción. Los eventos que pude identificar son:

 - En el estado **Init**, el evento es el inicio del temporizador (cuando el tiempo startTime se graba, lo que marca que el píxel está listo para cambiar de estado).
 
 - En el estado **WaitTimeout**, el evento es que el intervalo de tiempo transcurra. Es decir, el programa evalúa si el tiempo transcurrido desde startTime ha superado el interval especificado. Si este evento ocurre (el tiempo ha pasado), el programa cambia el estado del píxel.
 
##### ¿Cuáles son las acciones en este programa?

Las acciones son las actividades que el programa realiza en respuesta a los eventos que ocurren durante un estado. Las acciones que pude identificar son:

 - En el estado **Init**, la acción es establecer el startTime (el tiempo en que comienza el proceso) y cambiar el estado a **WaitTimeout**.

 - En el estado **WaitTimeout**, la acción es:

   * Verificar si el intervalo de tiempo ha pasado.
   * Si el evento ocurre, el estado del píxel se invierte entre 0 (apagado) y 9 (encendido) para simular el parpadeo.
   * Luego, la pantalla se actualiza usando display.set_pixel(self.pixelX, self.pixelY, self.pixelState) para reflejar el nuevo estado del píxel.
   * Después de ejecutar la acción, el tiempo startTime se reinicia para comenzar de nuevo el ciclo.

