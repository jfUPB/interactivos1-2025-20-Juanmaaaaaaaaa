# Unidad 3

## 🔎 Fase: Set + Seek

### Actividad 01 

1. ¿Qué ventajas tiene usar una clase (class) en este caso para representar un semáforo?

Reutilización, puedes crear varios semáforos sin duplicar código.
Encapsulamiento: cada semáforo tiene sus propios atributos (tiempos, posición, estado) sin interferir con otros.

Legibilidad, el código queda más organizado y fácil de mantener.

Escalabilidad, agregar más semáforos o cambiar su comportamiento es más fácil.

2. ¿Puedes ver cómo la técnica de programación con máquinas de estado y funciones no bloqueantes permite que varios semáforos funcionen al mismo tiempo?
Sí, porque cada semáforo ejecuta su propio ciclo update() y avanza de estado de forma independiente, además el código no usa sleep() ni bucles, lo que permite que se atiendan varios objetos y los semáforos parecen funcionar al mismo tiempo.

