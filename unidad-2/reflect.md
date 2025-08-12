# Unidad 2


## 🤔 Fase: Reflect

### Actividad 6

Parte 1: recuperación de conocimiento (Retrieval Practice)

Describe con tus palabras qué es una máquina de estados. ¿Cuáles son sus cuatro componentes fundamentales que has utilizado en esta unidad?

Una máquina de estados es una técnica de programación que permite organizar el comportamiento de un sistema en diferentes "estados" que responden a ciertos eventos, y que cambian a otros estados según ciertas condiciones. Los cuatro componentes fundamentales utilizados son: Estados, eventos, transiciones y acciones.

Explica por qué la técnica de máquina de estados es tan útil para gestionar la “concurrencia” (atender un temporizador y botones “al mismo tiempo”) en un dispositivo con un solo hilo de ejecución como el micro:bit. ¿Qué problema soluciona en comparación con usar funciones como sleep()?

La máquina de estados permite manejar varias tareas a la vez en el micro:bit sin bloquear el programa, porque evita usar funciones que paran la ejecución, revisando eventos continuamente.

Imagina que tienes que añadir una nueva funcionalidad a la bomba temporizada: si se agita (shake) el micro:bit mientras la cuenta regresiva está activa, el tiempo se reduce a la mitad. ¿Cómo modificarías tu diagrama de máquina de estados para incluir este nuevo evento y acción?

Añadiría una transición nueva desde el estado "ARMED", donde el evento sea “Shake” y la acción asociada sea reducir el tiempo restante a la mitad.

Explica qué es un “vector de prueba” y por qué es una herramienta crucial para verificar que una máquina de estados funciona como se espera.

Un vector de prueba es una lista de combinaciones de eventos y estados que se usa para verificar que una máquina de estados responde correctamente.

Parte 2: reflexión sobre tu proceso (Metacognición)

¿Qué parte del diseño de la bomba temporizada te resultó más desafiante: crear el diagrama de estados (Actividad 04) o traducir ese diagrama a código MicroPython (Actividad 05)? ¿Por qué?

Me resultó más desafiante traducir el diagrama a código MicroPython (Actividad 05), porque aunque el diagrama ayuda a tener una visión clara, llevar esa lógica al código y manejar bien las variables, los eventos y la estructura del programa se me hace más complejo.

Describe un error o “bug” que encontraste al implementar tu programa. ¿Cómo te ayudó pensar en términos de estados, eventos y transiciones a identificar y solucionar el problema?

No me fije bien si tuve algun bug o algo, funcionaba bien pero supongo que faltaron más pruebas.

El problema de la bomba era complejo. ¿Qué estrategia usaste para abordarlo? ¿Comenzaste con una versión simple y añadiste funcionalidades poco a poco?

Realmente para crear el programa fue a punta de prueba y error pero como dije anteriormente no hubo un problema al final que me haya afectado de gran forma.

Ahora que entiendes el patrón de máquina de estados, ¿En qué otro tipo de proyecto o sistema de entretenimiento digital crees que podrías aplicarlo?

Se podría aplicar en un proyecto donde cada cierto tiempo muestre una palabra distinta por un tiempo y si se hace shake cambie de palabra, como para jugar un "¿quien soy?".



### Actividad 7

Esta muy bien implementado todo, sin embargo, debería fijarse un poco más en el orden de su bitacora pues puede llegar a ser confuso.



### Actividad 8

Continuar: ¿Qué actividad, explicación o ejemplo de esta unidad te ayudó más a entender el poder de las máquinas de estados? ¿Qué elemento consideras que es indispensable y debería mantener?

La actividad en clase de la actividad de maquina de estados.

Dejar de hacer: ¿Hubo algún paso o actividad que te pareció confuso, innecesariamente complicado o que aportó poco a tu aprendizaje? ¿Qué cambiarías o eliminarías?

ninguno.

Empezar a hacer: ¿Qué te habría ayudado a entender mejor?

Mas ejemplos, pues puede llegar a ser confuso con solo un ejemplo y complicado implementar lo mismo a un ejercicio completamente distinto.

Ritmo y dificultad: En una escala del 1 (muy fácil) al 5 (muy difícil), ¿Cómo calificarías la dificultad de pasar del análisis de un programa (Actividad 03) al diseño desde cero de uno complejo (Actividad 04 y 05)? ¿Por qué?

Un 3 0 4, por la forma de plantear tan distinta.

Comentario adicional: ¿Hay algo más que te gustaría compartir sobre tu proceso de aprendizaje en esta unidad? ¿Algún momento de frustración o de “¡Aha!” que quieras destacar?

no :D.

## Corrección actividades anteriores

### Actividad 1

Describe detalladamente cómo funciona este ejemplo.

El programa implementa un semáforo en MicroPython para el micro:bit mediante una máquina de estados con tres estados, ROJO, AMARILLO y VERDE, donde cada uno es representado por un LED en el display. El único evento que provoca el cambio de estado es el paso del tiempo medido con utime.ticks_ms(), y las acciones realizadas incluyen encender el LED correspondiente, limpiar el display, cambiar el estado, reiniciar el temporizador y ajustar la duración de cada color.

¿Cuáles son los estados en el programa?

- Init, estado inicial. Se registra el tiempo de inicio (startTime) y se muestra el pixelState inicial en el display; luego pasa a WaitTimeout.
- WaitTimeout, estado normal de espera. Aquí se compara el tiempo transcurrido con interval y, si toca, se realiza la acción de alternar el brillo.


¿Cuáles son los eventos/inputs en el programa?

- Evento principal: el paso del tiempo, medido con utime.ticks_ms().
- Evento de inicialización: la primera llamada a update() que hace la transición desde Init a WaitTimeout.
- Input, paso del tiempo.

¿Cuáles son las acciones en el programa?

- display.set_pixel(x, y, pixelState): escribe el brillo en el display micro:bit (acción visible). 
- self.startTime = utime.ticks_ms(): registra el tiempo de referencia (acción interna).
- Alternar pixelState entre 9 y 0 cuando el intervalo se cumple (acción lógica).
- Cambio de self.state de "Init" a "WaitTimeout" (acción de transición de estado).


### Actividad 2

Escribe el código que soluciona este problema en tu bitácora.

    from microbit import *
    import utime
    
    class Semaforo:
        def __init__(self):
            self.state = "ROJO"
            self.startTime = utime.ticks_ms()
            self.interval = 0
            self.set_interval(3000)  
    
        def set_interval(self, ms):
            self.interval = ms
            self.startTime = utime.ticks_ms()
    
        def mostrar_color(self):
            display.clear()
            if self.state == "ROJO":
                display.set_pixel(2, 0, 9)  
            elif self.state == "AMARILLO":
                display.set_pixel(2, 2, 9)  
            elif self.state == "VERDE":
                display.set_pixel(2, 4, 9)  
    
        def update(self):
            if utime.ticks_diff(utime.ticks_ms(), self.startTime) > self.interval:
        
                if self.state == "ROJO":
                    self.state = "VERDE"
                    self.set_interval(3000) 
                elif self.state == "VERDE":
                    self.state = "AMARILLO"
                    self.set_interval(1000)  
                elif self.state == "AMARILLO":
                    self.state = "ROJO"
                    self.set_interval(3000) 
    
                
                self.mostrar_color()

Identifica los estados, eventos y acciones en tu código.

- Estados:
ROJO, LED superior encendido.
AMARILLO, LED central encendido.
VERDE, LED inferior encendido.

- Eventos:
Tiempo transcurrido

- Acciones:
Encender un LED específico en la columna central, según el estado.
Borrar el display antes de encender el nuevo LED.
Cambiar el estado de la máquina.
Reiniciar el temporizador.
Ajustar la duración del siguiente estado.


### Actividad 3

Explica por qué decimos que este programa permite realizar de manera concurrente varias tareas.

Porque gracias a la máquina de estados y el uso de utime.ticks_ms(), el programa puede:
- Mostrar una imagen en pantalla.
- Al mismo tiempo detectar pulsaciones del botón.
- Y controlar temporizadores para cambiar de estado automáticamente.
Todo sin detener ninguna de estas funciones por una espera bloqueante (sleep). Esto crea la ilusión de que varias tareas ocurren a la vez.


Identifica los estados, eventos y acciones en el programa.

Estados
- STATE_INIT.
- STATE_HAPPY. 
- STATE_SMILE. 
- STATE_SAD.

Eventos
- Tiempo transcurrido.
- Pulsación de botón A.

Acciones
- Mostrar imagen en pantalla.
- Reiniciar temporizador.
- Ajustar nuevo intervalo.
- Actualizar el estado actual.


Describe y aplica al menos 3 vectores de prueba para el programa. Para definir un vector de prueba debes llevar al sistema a un estado, generar los eventos y observar el estado siguiente y las acciones que ocurrirán. Por tanto, un vector de prueba tiene unas condiciones iniciales del sistema, unos resultados esperados y los resultados realmente obtenidos. Si el resultado obtenido es igual al esperado entonces el sistema pasó el vector de prueba, de lo contrario el sistema puede tener un error.


### Actividad 4

Diagrama que no dejó subir github

![flowchart](https://i.imgur.com/u01XcRv.png)

