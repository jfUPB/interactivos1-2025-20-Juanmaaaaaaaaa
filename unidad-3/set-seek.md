# Unidad 3

## 🔎 Fase: Set + Seek

### Actividad 1

1. ¿Qué ventajas tiene usar una clase (class) en este caso para representar un semáforo?

Que puedes crear varios semáforos sin duplicar código, cada semáforo tiene sus propios atributos sin interferir con otros y agregar más semáforos o cambiar su comportamiento es más fácil.

2. ¿Puedes ver cómo la técnica de programación con máquinas de estado y funciones no bloqueantes permite que varios semáforos funcionen al mismo tiempo?
Sí, porque cada semáforo ejecuta su propio ciclo update() y avanza de estado de forma independiente, además el código no usa sleep() ni bucles, lo que permite que se atiendan varios objetos y los semáforos parecen funcionar al mismo tiempo.

### Actividad 3 

¿Cómo enviarás los eventos del serial?

A través de la aplicación dada por el profe la cual lee las letras que se presionan en el teclado las cuales el micro bit las lee como para activar el evento por medio de las letras A, B, S y T.

### Actividad 5

Construye el modelo de la bomba 3.0. Como ya tienes el código puedes tener un modelo muy preciso.

![bitacora.jpg](https://i.imgur.com/YNDP6xC.jpeg)

Crear una tabla con los vectores de prueba. La tabla debe tener 4 columnas por vector y puedes agrupar vectores en un gran vector. Las columnas son:
- Estado inicial
- Evento disparador
- Acciones
- Estado final


| Estado inicial | Evento disparador    | Acciones                                            | Estado final     |
| -------------- | -------------------- | --------------------------------------------------- | ---------------- |
| CONFIG         | A                    | count++ (máx 60), mostrar nuevo valor               | CONFIG           |
| CONFIG         | B                    | count-- (mín 10), mostrar nuevo valor               | CONFIG           |
| CONFIG         | S                    | Guardar tiempo inicial, iniciar countdown           | ARMED            |
| ARMED          | Timer (1 seg)        | count--, actualizar display, si count=0             | ARMED / EXPLODED |
| ARMED          | A                    | Guardar A en secuencia                              | ARMED            |
| ARMED          | B                    | Guardar B en secuencia                              | ARMED            |
| ARMED          | Secuencia (A,B,A)    | Reset count=20, volver a configurar                 | CONFIG           |
| ARMED          | Secuencia incorrecta | Reset secuencia, sin cambio en contador             | ARMED            |
| EXPLODED       | T (touch logo)       | Reset count=20, limpiar display                     | CONFIG           |


