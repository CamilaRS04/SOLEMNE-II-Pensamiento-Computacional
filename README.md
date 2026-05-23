# SOLEMNE-II-Pensamiento-Computacional
Nombre del proyecto: Sistema visual generativo e interactivo — Órbitas

Autora: Camila Romo



---------------------


**proyecto**

Es un sistema visual generativo hecho en p5.js donde distintos círculos orbitan continuamente desde el centro de la pantalla. El sistema cambia constantemente según la interacción del usuario.

--

**que se ve en pantalla**

Se observan círculos de distintos tamaños girando alrededor del centro del canvas. Algunas órbitas incluyen un halo semitransparente que genera más profundidad visual. El fondo es negro y los colores cambian dependiendo de la paleta seleccionada.

--

**que elementos visuales aparecen**

Aparecen círculos en movimiento, halos transparentes y variaciones de color en tonos turquesa, verde y rojo oscuro.

--


**que inputs utilizo**

Mouse en X: controla la cantidad de órbitas
Mouse en Y: controla el tamaño de las formas
Teclas A, S y D: cambian la paleta de colores

--

**que outputs genera**

Este proyecto genera un sistema visual dinámico que responde en tiempo real al movimiento del mouse y al teclado, produciendo distintas composiciones visuales

--

--------------------------------------------------------

**REFERENTES**
---Vera Molnár
---Alexander Calder

**MI IDEA CENTRAL**
-------------------------------------------------

La idea que quería explorar era que con reglas matemáticas simples se pueden generar imágenes que nunca se repiten. Me interesaba que el resultado no dependiera de mí dibujando algo, sino de que el sistema lo fuera generando solo según lo que yo le diera como parámetros.


Lo relaciono con el diseño generativo y también con el arte cinético. Con el diseño generativo porque en ningún momento dibujé las formas a mano, todo sale de reglas y números

-----------------------------------------------------------------

¿Que se hace en este sketch?

Básicamente se dibuja círculos que estan ahí desde el centro de la pantalla, mientras mueves el mouse cambia cuántos círculos hay y qué tan grandes son. Con el teclado puedes cambiar los colores entre tres paletas distintas.

Proceso de desarrollo (con errores incluidos) 

**Primer intento** — demasiado simple Lo primero que hice fue solo dibujar un círculo en el centro y hacerlo girar. Funcionaba pero era aburrido, nada cambiaba con el mouse ni el teclado. La pauta pedía interactividad así que eso no servía.

-

**Segundo intento** — el random() me generó un problema Cuando agregué random() para variar el color, me di cuenta que el sketch "parpadeaba" demasiado fuerte porque random() se llama 60 veces por segundo. Al principio pensé que estaba mal escrito el código, pero en realidad era intencional, solo que tenía los rangos muy amplios. Los achiqué y quedó mejor.

-

**Tercer intento** — el for no giraba bien las órbitas Cuando metí el loop for para dibujar varias órbitas, todas se apilaban en el mismo punto. Me olvidé de usar push() y pop() antes y después de la rotación. Sin eso, cada iteración del loop acumulaba la rotación anterior y todo se iba torciendo. Agregué el push() y pop() y ahí sí se separaron bien

-

**Cuarto intento** — me faltaba la función propia y el segundo condicional revisé los requisitos de la pauta y me di cuenta que no tenía ninguna función definida por mí, solo las de p5.js. Tampoco tenía dos condicionales, solo uno para la paleta. Así que separé toda la lógica de dibujo en una función llamada **dibujarOrbita()** y dentro le agregué un segundo condicional para que las órbitas pares tuvieran un halo extra

-
importante: función propia (dibujarOrbita)

----------------------------------------------------------------------
---------- **FOTOS REFERENCIA**

<img width="739" height="733" alt="image" src="https://github.com/user-attachments/assets/0b2e7fe6-ef5c-470c-93cb-d2c89019130e" />
<img width="734" height="739" alt="image" src="https://github.com/user-attachments/assets/16f082c3-c491-4485-bbe5-3bf1378f62e8" />
<img width="742" height="737" alt="image" src="https://github.com/user-attachments/assets/cdb6e8ec-a619-48dc-bf63-5b901edbd2c7" />


--------------------------------------------------------
Explicación de paso del código estuve viendo  bastantes referencias, en el tipo de interacciones, colores y mas, tambien en las clases y usé algunos comandos que explicó la profe

Dejaré algunos comandos y explicaciones mas detalladas que quizas olvido y me gustaria recordar:

--
1. Variable paleta paleta = 'turquesa'; se guarda el nombre de la paleta activa, La pongo fuera de todo para que tanto draw() como keyPressed() puedan verla y modificarla. Si la pusiera adentro de una función se reiniciaría sola

dibujarOrbita() function dibujarOrbita(i, cantidad, radio, tamaño) { let r, g, b;

----------------------------------------
// Condicional 1 — paleta if (paleta == 'turquesa') { r = map(i, 0, cantidad, 0, 60); g = map(i, 0, cantidad, 180, 255); b = random(180, 255); } else if (paleta == 'miku') { r = 0; g = map(i, 0, cantidad, 120, 220); b = random(150, 240); } else { r = map(i, 0, cantidad, 120, 220); g = 40; b = random(40, 100); } ----condicional 1*

// Condicional 2 if (i % 2 == 0) { noFill(); stroke(r, g, b, 60); strokeWeight(tamaño * 0.6); ellipse(radio, 0, tamaño * 2.2); noStroke(); }

---------------------------------------------------------------
fill(r, g, b, 180); noStroke(); ellipse(radio, 0, tamaño); } ----condicional 2* -------

Esta es la función que definí, esta recibe el número de orbita i, el total cantidad, la distancia al centro radio y el tamaño del círculo LO QUE DEBO RECORDAR Adentro tiene dos condicionales:

El primero revisa cuál paleta está activa y calcula los colores El segundo revisa si la órbita es par (i % 2 == 0) y si lo es le dibuja un anillo extra semitransparente antes del círculo principal

keyPressed() *esta funcion ya la vimos keyPressed() { if (key == 'a' || key == 'A') paleta = 'turquesa'; if (key == 's' || key == 'S') paleta = 'verdeazul'; if (key == 'd' || key == 'D') paleta = 'oscura'; }

p5.js llama a esta función automáticamente cuando presionas una tecla

frameCountContador que sube en 1 cada frame. Multiplicado por 0.01 da la animación suave de rotación

i % 2 == 0El operador % da el resto de una división. Si el resto al dividir por 2 es 0, el número es par

--------------------------------------------------------------------

CONTROLES control efecto Mouse a la derecha ---> Más órbitas Mouse hacia abajo ---> Órbitas más grandes Tecla A ---> Paleta turquesa Tecla S ---> Paleta verdeazul Tecla D ---> Paleta roja burdeo


------------------------------------- 

COMANDOS Y SUS FUNCIONES *recordar importante

**MATEMÁTICAS Y AZAR**

**map(valor, min1, max1, min2, max2)** 
Convierte un número de un rango a otro. Traduje el mouse en cantidad y tamaño.

**random(a, b)**  
Devuelve un número al azar entre a y b. Lo usé para variar el color cada frame.

**i % 2 == 0**
El % da el resto de una división. Si es 0, el número es par.

**frameCount**
Contador que sube 1 por frame. Da la animación suave de rotación.


**TRANSFORMACIONES**

**push()** 
Guarda el estado actual de posición y rotación para no afectar lo que viene después.

**pop()**  
Restaura el estado guardado por push(). Siempre van juntos.

**translate(x, y)**
Mueve el origen del dibujo a otro punto. Lo usé para centrar las órbitas.

***rotate(ángulo)**  
Rota todo lo que se dibuje después de esta línea.


**COLOR Y RELLENO**

**fill(r, g, b, a)** 
Define el color de relleno. El cuarto valor es la transparencia (0–255).

**noFill()**
Desactiva el relleno. La figura queda transparente por dentro.

**stroke(r, g, b, a)** 
Define el color del borde de la figura.

**noStroke()**  
Desactiva el borde. La figura queda sin contorno.

**strokeWeight(n)**  
Define el grosor del borde en píxeles.



**FIGURAS**
**ellipse(x, y, tamaño)**  
Dibuja un círculo en la posición dada con el tamaño indicado.



----------------------------------------------------------

que me costó?

Lo otro que me costó fue el map(). Me confundía el orden de los parámetros. Tuve que probarlo varias veces con números concretos para entender que primero va el valor que quiero convertir, luego el rango de donde viene, y al final el rango a donde quiero llevarlo.

La función propia dibujarOrbita() al principio me pareció innecesario separarla, pero cuando la usé me di cuenta que el draw() quedó mucho más ordenado y fácil de leer. Si tuviera que cambiar cómo se ven los círculos, sé exactamente a qué función ir.

En general el sketch quedó como yo quería. Me gusta que con solo mover el mouse cambia bastante la forma visual, no es solo un cambio de color sino que cambia cuántos elementos hay y qué tan grandes son.






--------------------------------📊**DIAGRAMA DE FLUJO**📊-----------------------------------------


<img width="438" height="837" alt="image" src="https://github.com/user-attachments/assets/390ba9b7-39c8-4bbb-af33-9909078ceaff" />

