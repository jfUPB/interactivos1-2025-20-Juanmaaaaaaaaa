# Unidad 1

## 🤔 Fase: Reflect

### Actividad 7 

*Parte 1: recuperación de conocimiento (Retrieval Practice)*

Basándote en los ejemplos que vimos de sistemas físicos interactivos al iniciar el curso, describe las tres características que definen a un sistema físico interactivo.

Que todos poseen un input, un process y un output.

Explica el modelo input-process-output de Patrick Hübner usando como ejemplo el sistema que construiste con micro:bit y p5.js en la Actividad 06. ¿Cuál fue el input, cuál fue el proceso y cuál fue el output?

Input: Presionar el botón A o B del micro:bit.

Proceso: El micro:bit detecta el botón presionado y envía un mensaje (“A” o “B”) por UART.

Output: En p5.js, ese mensaje cambia la posición del círculo, basandose en restaerle o sumarle a la posición en x del círculo.

¿Cuál es la función de la línea uart.write('A') en el código del micro:bit y qué función en p5.js se encarga de “escuchar” ese mensaje?

La funcion de la línea uart.write('A') en el código del micro:bit es mandar el mensaje de A o B, y la función que se encarga de escuchar el mensaje es port.read() o al menos es el que permita que se conecten entre ambos.

¿Cuál es la diferencia fundamental entre el arte/diseño tradicional y el arte/diseño generativo?

La diferencia mas notoria es que el tradicional es creado directamente por el autor, teniendo un control completo del resultado. Por otro lado, el generativo es creado mediante algoritmos creando una serie de reglas que permiten crear distintas creaciones basadas en una serie de reglas.

Imagina que quieres que un círculo en p5.js cambie a un color aleatorio cada vez que sacudes el micro:bit. Describe qué tendrías que programar en el micro:bit y qué tendrías que programar en p5.js para lograrlo.

micro:bit 

from microbit import *
import random

uart.init(baudrate=115200)

while True:
    if accelerometer.was_gesture('shake'):
        uart.write('S')
    sleep(100)

En el microbit se crea una variable aleatoria y se manda al p5, y se manda que cada vez que se mueve se envie la letra S y se pone sleep para que se vaya actualizando.

p5.js

let port;
let connectBtn;
let connectionInitialized = false;
let circleColor;

  function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton("Connect to micro:bit");
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
    circleColor = color(255);  
  }


function draw() {
  background(200);
  fill(circleColor);
  ellipse(200, 200, 100, 100);

  if (port.availableBytes() > 0) {
    let dataRx = port.read(1);
    if (dataRx == 'S') {
      circleColor = color(random(255), random(255), random(255));
    }
  }
}

function connectBtnClick() {
    if (!port.opened()) {
      port.open("MicroPython", 115200);
      connectionInitialized = false;
    } else {
      port.close();
    }
}

En el p5 se usa variables para la conección del microbit y para el color del círculo, en el setup se crea todo lo que tiene que ver como con la interfaz (para conectar el microbit, para el fondo, para iniciar el puerto, etc) y el valor inicial de la variable de color. En el draw se crea el circulo y se le asigna el valor del color y lee si le envían un menssaje "S" que le cambia de forma random el color. Y por ultimo, el connectBtnClick() que es para el boton de conección con el microbit.


*Parte 2: reflexión sobre tu proceso (Metacognición)*

¿Qué fue más desafiante para ti en esta unidad: la parte conceptual (entender qué es un sistema físico interactivo) o la parte técnica (hacer que el micro:bit y p5.js se comunicaran)? ¿Por qué?

Yo creo que ambos tienen un nivel de dificultad parecido, pues son temas antes vistos en la carrera provocando que lleguemos sin saber bien lo que estamos desarrollando en clase.

Describe el momento “¡Aha!” que tuviste cuando lograste que una acción en el micro:bit (presionar un botón, sacudirlo) tuviera un efecto visible en el canvas de p5.js por primera vez. ¿Qué fue lo que entendiste en ese instante?

Cuando pasó eso fue porque me funcionó todo a la primera y el microbit sl sacudirlo mostró un corazón todo bello, y entendí al instante que podía disfrutar de este tipo de cosas.

Al inicio de la unidad te pregunté: “¿Este curso para qué me sirve?”. Después de experimentar y construir tu primer prototipo, ¿Cómo ha cambiado o se ha vuelto más concreta tu respuesta a esa pregunta?



Ahora estoy mas confunzo que antes, pues hay un mundo gigante por explorar.

El tutorial de la Actividad 05 te llevó paso a paso. ¿Cómo te sentiste con ese método de aprendizaje? ¿Te dio seguridad o preferirías haberlo intentado por tu cuenta desde el principio?

Me permitió seguridad, pero siento que es muy fácil perderse en este tipo de descripción pues se necesita la explicación previa del profesor, y si este va rápido, te pierdes el doble.



### Actividad 8

Elaboro de la misma forma la actividad 6, sin embargo tenemos diferencias, pero minimas que no afectan el resultado, como la cantidad que se le suma o resta a la posición en x.

### Actividad 9

Continuar: ¿Qué actividad, video o ejemplo de esta unidad te resultó más inspirador o te ayudó más a entender el potencial de los sistemas físicos interactivos?

Fue el de los vj en general, pues no tenía idea de este mundo y me pareció sorprendente lo que hacen.

Dejar de hacer: ¿Hubo alguna parte que te pareció demasiado abstracta, muy rápida o confusa? ¿Hay algo que crees que podríamos cambiar para que sea más claro?

Creo que la clase esta bien pero queda corta para la cantidad de información, por lo que cuando ya nos toca desarrollar a nosotros la mayoría de veces nos toca hacerlo en la casa por el tiempo, en vez de en clase, cuando recien vimos el tema y lo comprendemos de la mejor forma.

Empezar a hacer: ¿Qué te genera más curiosidad ahora? ¿Te gustaría explorar más sensores del micro:bit (luz, temperatura), crear visualizaciones más complejas en p5.js o ver más ejemplos de proyectos artísticos?

me gustarían ambos porque la idea es ir explorando este mundo que no conocemos.

Balance inspiración vs. técnica: ¿Cómo sentiste el equilibrio entre ver los videos inspiradores de la Actividad 01 y la parte técnica de conectar las herramientas en las actividades 03-06?

Confuso, porque es difícil relacionar algo tan complejo con algo tan sencillo.

Comentario adicional: ¿Hay algo más que quieras compartir sobre tu experiencia en esta unidad introductoria?

No, gracias :D
