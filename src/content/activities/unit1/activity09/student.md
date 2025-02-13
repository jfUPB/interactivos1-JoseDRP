#### Desarrollo actividad 9

- Teniendo en cuenta que tengo poco conocimiento con JavaScript, traté de hacer uso del diseño generativo mencionado en actividades anteriores. Lo primero que hice fue redactar un prompt para darselo a chatGPT. Este fue el prompt que redacté:

"Realiza un programa en javascript que genere patrones visuales de manera aleatoria. Usa funciones matemáticas simples como random(),sin(),cos(). Luego explica brevemente el código línea por línea para entenderlo mejor."

- ChatGPT me entregó el siguiente código:

  El programa utiliza círculos distribuidos a lo largo del lienzo, y las posiciones y tamaños de estos círculos se modifican aleatoriamente en función de las funciones trigonométricas.

[Enlace al proyecto](https://editor.p5js.org/JoseDRP/sketches/1HAGo1vKy)

``` js
function setup() {
  createCanvas(400, 400);
  noFill();
}
  function draw() {
  background(255);

  // Modificamos el número de círculos en función de una constante
  let numCircles = 10;

  // Para cada círculo, vamos a calcular su posición y radio usando funciones trigonométricas
  for (let i = 0; i < numCircles; i++) {
  let angle = map(i, 0, numCircles, 0, TWO_PI); // Ángulo para cada círculo
  let radius = 100 * sin(frameCount * 0.01 + i); // Radio variable usando sin()
  
  let x = width / 2 + radius * cos(angle); // Posición x usando cos()
  let y = height / 2 + radius * sin(angle); // Posición y usando sin()
  
  // Establecemos un color aleatorio para cada círculo
  stroke(random(255), random(255), random(255));
  
  // Dibujamos el círculo
  ellipse(x, y, 50 + radius * 0.5, 50 + radius * 0.5);
  }
}
```

- Luego de esto, introduje este código al simulador p5.js para verificar si funcionaba correctamente y al ejecutarlo me entregó lo siguiente:

![image](../../../../assets/u1-a9-i1.png)

- El código funcionó correctamente como se puede ver, por lo que finalmente le pedí a ChatGPT que me explicara básicamente línea por línea para entender su funcionamiento

##### Explicación del código:
**setup():** Se establece un lienzo de 400x400 píxeles y se elimina el relleno de las figuras para dibujar solo los bordes.

**draw():** Se ejecuta repetidamente para actualizar los patrones. En cada frame, se dibujan 10 círculos.

###### Cálculos de posición y tamaño:

Utilizamos la función sin() y cos() para calcular la posición de cada círculo, creando un patrón circular dinámico.
sin(frameCount * 0.01 + i) y cos(angle) modifican la posición y el radio de los círculos.

El frameCount hace que los círculos se muevan con el tiempo, creando un patrón animado.
Colores aleatorios: Cada círculo tiene un color de trazo aleatorio que cambia en cada ciclo de dibujo.
