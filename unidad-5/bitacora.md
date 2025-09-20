
# Evidencias de la unidad 5

## Actividad 1

- Describe cómo se están comunicando el micro:bit y el sketch de p5.js. ¿Qué datos envía el micro:bit?
El micro:bit y el sketch en p5.js se comunican mediante el puerto serial (UART). El micro:bit recoge datos de sus sensores internos (acelerómetro y botones A y B) y los envía en formato de texto ASCII por el puerto serial.
- ¿Cómo es la estructura del protocolo ASCII usado?
xValue, valor del acelerómetro en el eje X.
yValue, valor del acelerómetro en el eje Y.
aState, estado del botón A (True si está presionado, False si no).
bState, estado del botón B (True si está presionado, False si no).
- Muestra y explica la parte del código de p5.js donde lee los datos del micro:bit y los transforma en coordenadas de la pantalla.
  
            data = "{},{},{},{}\n".format(xValue, yValue, aState, bState)
            uart.write(data)

-- Valores en texto plano (ASCII). {}
-- Separados por comas ,.
-- Cada grupo de datos termina con un salto de línea \n.
- ¿Cómo se generan los eventos A pressed y B released que se generan en p5.js a partir de los datos que envía el micro:bit?
Se compara el estado actual con el anterior:
  Si el botón A pasa de no presionado a presionado, se lanza el evento A pressed.
  Si el botón B pasa de presionado a no presionado, se lanza el evento B released.
- Capturas de pantalla de los algunos dibujos que hayas hecho con el sketch.
