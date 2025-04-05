#### Explicación de concurrencia en el programa

Este programa para la micro:bit simula un sistema de máquina de estados finitos en el que la pantalla cambia entre diferentes expresiones faciales en función del tiempo y la interacción con el botón A.

- **El uso de una máquina de estados:** El código mantiene un seguimiento del estado actual y cambia de estado en función del tiempo o la interacción del usuario.

- **Temporización con utime.ticks_ms():** En lugar de detener la ejecución con sleep(), se usa la diferencia de tiempo transcurrido para decidir cuándo cambiar de estado.

- **Manejo de eventos con button_a.was_pressed():** Se revisa constantemente si el botón A ha sido presionado, permitiendo una reacción inmediata sin bloquear el flujo del programa.

De esta manera, el programa parece realizar múltiples tareas a la vez: controla el tiempo para los cambios automáticos de estado y también responde a las interacciones del usuario sin que una tarea interrumpa la otra.

En resumen, el código hace que la pantalla de la micro:bit cambie de cara automáticamente con el tiempo y también reaccione cuando presionas el botón A. El programa revisa rápidamente dos cosas en un bucle:

- Si ha pasado el tiempo para cambiar de cara.
- Si presionaste el botón.

Como revisa estas dos cosas muchas veces por segundo, parece que está haciendo ambas al mismo tiempo. Eso es lo que llamamos concurrencia en este caso.

#### Vectores de prueba

Cada vector de prueba consta de:

- **Condiciones iniciales:** Estado actual del sistema antes de iniciar la prueba.
- **Eventos generados:** Botón presionado o tiempo transcurrido.
- **Resultados esperados:** Estado final y la imagen mostrada.
- **Resultados obtenidos:** Estado final y la imagen mostrada después de ejecutar la prueba.

##### Vector de prueba 1: Transición automática de HAPPY a SMILE

- **Condiciones iniciales:** El sistema está en estado STATE_HAPPY con la imagen 😊.
- **Evento generado:** Se espera que pase 1500 ms sin presionar ningún botón.
- **Resultado esperado:** Cambio al estado STATE_SMILE, mostrando la imagen 😀.
- **Resultado obtenido:** ✅ Correcto (El sistema cambió de HAPPY a SMILE automáticamente).

##### Vector de prueba 2: Interrupción manual de SMILE a HAPPY
- **Condiciones iniciales:** El sistema está en estado STATE_SMILE con la imagen 😀.
- **Evento generado:** Se presiona el botón A antes de que pasen los 1000 ms del intervalo de SMILE.
- **Resultado esperado:** Cambio inmediato al estado STATE_HAPPY, mostrando la imagen 😊.
- **Resultado obtenido:** ✅ Correcto (El sistema respondió al botón sin esperar el tiempo programado).

##### Vector de prueba 3: Transición forzada de HAPPY a SAD
- **Condiciones iniciales:** El sistema está en estado STATE_HAPPY con la imagen 😊.
- **Evento generado:** Se presiona el botón A.
- **Resultado esperado:** Cambio inmediato al estado STATE_SAD, mostrando la imagen ☹️ y estableciendo un temporizador de 2000 ms.
- **Resultado obtenido:** ✅ Correcto (El botón cambió el estado sin esperar el tiempo programado).

