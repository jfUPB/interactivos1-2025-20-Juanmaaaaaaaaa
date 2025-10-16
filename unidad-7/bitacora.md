
# Evidencias de la unidad 7

## Actividad 1

### ¿Qué URL de Dev Tunnels obtuviste? ¿Por qué crees que necesitamos usar esta URL en lugar de http://localhost:3000 o la IP local de tu computador para que el celular se conecte?

URL: https://v5t21ss5-3000.use2.devtunnels.ms/

Porque localhost solo es accesible desde el propio computador donde corre el servidor y el celular no puede acceder a localhost de tu PC, ya que son dispositivos distintos conectados a redes diferentes.Por otro lado, Dev Tunnels crea un túnel público y seguro que permite exponer temporalmente tu servidor local (en este caso, el puerto 3000) a internet. Así, el navegador del celular puede conectarse al mismo servidor Node.js a través de esa URL.

### Describe brevemente qué hace npm install y npm start.

- npm install: descarga e instala todas las dependencias del proyecto, en este caso, express y socket.io. Esto se hace solo la primera vez.

- npm start: ejecuta el script definido en el package.json, lo que inicia el servidor local en el puerto 3000.

### ¿Qué mensajes observaste en la terminal del servidor al conectar el cliente de escritorio y el cliente móvil? ¿Eran diferentes los mensajes o identificadores?

Solo se observo esto:

    New client connected
    New client connected

Por lo que no hay forma de diferenciarlos.

### Describe el comportamiento observado: ¿Funcionó la interacción? ¿Hubo algún retraso (latencia)?

- En el computador: aparecía un círculo rojo en el lienzo de p5.js.

- En el celular: se mostraba el mensaje “Touch to move the circle”.

Al mover el dedo sobre la pantalla, el círculo rojo del navegador en el computador se movía en tiempo real siguiendo el movimiento, sin embargo, si se notó una latencia minima.

### Evidencias

<img width="1915" height="1043" alt="Captura de pantalla 2025-10-16 125530" src="https://github.com/user-attachments/assets/f8f35805-5500-4c0e-baab-c7ebf81c1292" />

<img width="1919" height="1079" alt="Captura de pantalla 2025-10-16 125633" src="https://github.com/user-attachments/assets/b428563e-68f2-474e-8a4c-0068c7687bd6" />

<img width="1919" height="1079" alt="Captura de pantalla 2025-10-16 125652" src="https://github.com/user-attachments/assets/cb124d5c-a524-4d25-bd70-f9fd71a497b3" />


## Actividad 2

### Explica con tus propias palabras: ¿Por qué es necesario Dev Tunnels en este escenario y cómo funciona conceptualmente?

Dev Tunnels es necesario porque el servidor que ejecutamos con Node.js en localhost:3000 solo es accesible desde el propio computador, y el celular no puede conectarse a esa dirección. Esta herramienta crea un túnel seguro entre Internet y el servidor local, generando una URL pública temporal que redirige todas las solicitudes al puerto 3000 del equipo. Así, permite que dispositivos externos, como el celular, se comuniquen con la aplicación de escritorio a través de Internet de forma segura y sencilla.

### Describe la función de touchMoved() y por qué se usa la variable threshold en el cliente móvil.

La función touchMoved() se ejecuta automáticamente cuando el usuario mantiene el dedo sobre la pantalla y lo mueve, capturando las coordenadas del toque con mouseX y mouseY. Estas coordenadas se envían al servidor mediante Socket.io para actualizar la posición del círculo en el computador. La variable threshold se utiliza para evitar que se envíen demasiados mensajes por movimientos mínimos, filtrando solo los cambios significativos y haciendo la comunicación más eficiente y fluida.

### Compara brevemente Dev Tunnels con simplemente usar la IP local. ¿Cuáles son las ventajas y desventajas de cada uno?

Dev Tunnels permite acceder al servidor desde cualquier red a través de una conexión segura HTTPS, mientras que la IP local solo funciona si los dispositivos están en la misma red Wi-Fi y puede verse afectada por firewalls o configuraciones del router. Aunque Dev Tunnels puede tener un poco más de latencia, ofrece mayor seguridad y facilidad de uso. En cambio, usar la IP local es más rápido pero limitado a entornos de red local, por lo que Dev Tunnels resulta más práctico para pruebas remotas o desde dispositivos móviles.

### Coloca en tu bitácora capturas de pantalla del sistema completo funcionando. Esto lo puedes hacer abriendo tanto el mobile como el desktop en tu computador y tomando una captura de pantalla de todos los involucrados (celular, computador y terminal).

![WhatsApp Image 2025-10-16 at 1 27 46 PM](https://github.com/user-attachments/assets/91eade3a-fc3c-4eda-8f91-913899d8a5eb)

<img width="1915" height="1043" alt="Captura de pantalla 2025-10-16 125530" src="https://github.com/user-attachments/assets/f8f35805-5500-4c0e-baab-c7ebf81c1292" />

<img width="1919" height="1079" alt="Captura de pantalla 2025-10-16 125633" src="https://github.com/user-attachments/assets/b428563e-68f2-474e-8a4c-0068c7687bd6" />

<img width="1919" height="1079" alt="Captura de pantalla 2025-10-16 125652" src="https://github.com/user-attachments/assets/cb124d5c-a524-4d25-bd70-f9fd71a497b3" />

## Actividad 3

### ¿Cuál es la función principal de express.static(‘public’) en este servidor? ¿Cómo se compara con el uso de app.get(‘/ruta’, …) del servidor de la Unidad 6?

express.static('public') monta una carpeta como servidor de archivos estáticos: cualquier archivo dentro de public (HTML, JS, CSS, imágenes) se sirve directamente por su ruta relativa sin escribir handlers adicionales; por ejemplo public/desktop/index.html será accesible en /desktop/index.html. En cambio app.get('/ruta', ...) crea una ruta dinámica con código JavaScript que se ejecuta cuando llega una petición a esa URL (puede renderizar plantillas, enviar JSON, aplicar lógica, etc.). express.static es para servir recursos estáticos de forma simple y eficiente; app.get es para manejar peticiones dinámicas o personalizadas.

### Explica detalladamente el flujo de un mensaje táctil: ¿Qué evento lo envía desde el móvil? ¿Qué evento lo recibe el servidor? ¿Qué hace el servidor con él? ¿Qué evento lo envía el servidor al escritorio? ¿Por qué se usa socket.broadcast.emit en lugar de io.emit o socket.emit en este caso?

En el cliente móvil touchMoved() (o la lógica equivalente en p5.js) captura mouseX/mouseY y envía esas coordenadas mediante Socket.io con algo como socket.emit('message', {x, y}). En el servidor io.on('connection', socket => socket.on('message', message => { ... })) recibe ese evento 'message' y ejecuta el callback; dentro de ese callback el servidor registra el mensaje (console.log) y retransmite usando socket.broadcast.emit('message', message'). Ese 'message' retransmitido lo reciben los clientes conectados (por ejemplo el escritorio) mediante su propio socket.on('message', ...), que actualiza el canvas. El servidor actúa solo como repetidor/relay: recibe, puede inspeccionar/loggear, y reenvía.

### Si conectaras dos computadores de escritorio y un móvil a este servidor, y movieras el dedo en el móvil, ¿Quién recibiría el mensaje retransmitido por el servidor? ¿Por qué?

socket.emit enviaría el mensaje únicamente al socket que originó el evento (es decir, de vuelta al móvil), lo que no nos sirve aquí; io.emit enviaría a todos los sockets incluidos el emisor (el móvil), causando que el móvil reciba su propio mensaje y en algunos flujos genere duplicados o efectos no deseados. socket.broadcast.emit envía el mensaje a todos los demás clientes conectados excepto el que lo emitió, que es exactamente lo que queremos: que el escritorio (y otros clientes distintos del móvil) reciban la actualización sin reenviarla al móvil origen.
Al mover el dedo en el móvil el servidor retransmitirá con socket.broadcast.emit, por lo que los dos navegadores de escritorio (y cualquier otro cliente conectado distinto del móvil origen) recibirán el mensaje; el móvil origen no lo recibirá. Esto ocurre porque broadcast excluye al socket remitente y entrega la información a todos los demás sockets conectados.

### ¿Qué información útil te proporcionan los mensajes console.log en el servidor durante la ejecución?

Los console.log muestran eventos clave para depuración: cuándo se conecta un cliente (New client connected), cuándo llegan mensajes táctiles (Received message => {x,y}) y cuándo se desconecta un cliente (Client disconnected). Con esos logs puedes verificar que las conexiones funcionan, inspeccionar el contenido de los mensajes (coordenadas), medir frecuencia/volumen de mensajes y detectar desconexiones inesperadas. Si necesitas más detalle para depurar, puedes ampliar los logs para incluir socket.id, timestamps o el tamaño/payload del mensaje.

## Actividad 4

Realiza un diagrama donde muestres el flujo completo de datos y eventos entre los tres componentes: móvil, servidor y escritorio. Puedes ilustrar con un ejemplo de coordenadas táctiles (x, y) y cómo viajan a través del sistema.

El flujo de comunicación entre el cliente móvil, el servidor y el cliente de escritorio ocurre en tiempo real a través de Socket.IO. Todo comienza en el cliente móvil, donde la función touchMoved() detecta cuando el usuario mantiene el dedo sobre la pantalla y lo mueve. En ese momento, el programa captura las coordenadas del toque usando las variables mouseX y mouseY. Luego, crea un objeto con esos datos, por ejemplo {type: "touch", x: 150, y: 220}, y lo envía al servidor mediante la instrucción socket.emit('message', touchData).

El servidor Node.js recibe este mensaje gracias al evento socket.on('message', message). Cuando el servidor lo recibe, lo muestra en la consola con console.log("Received message =>", message) para confirmar que llegaron los datos correctamente. Después, el servidor no guarda la información ni la procesa, sino que actúa como un intermediario: usa socket.broadcast.emit('message', message) para reenviar el mensaje a todos los demás clientes conectados, excepto al que lo envió.

Finalmente, el cliente de escritorio escucha los mensajes que llegan desde el servidor con el evento socket.on('message', data). Cuando recibe el objeto con las coordenadas táctiles, verifica que el tipo sea 'touch' y actualiza las variables circleX y circleY con los valores de x y y. Luego, en cada ciclo de la función draw(), el programa redibuja el círculo rojo en la nueva posición, reflejando en tiempo real el movimiento del dedo que se realizó en el celular.


## Rúbrica


| Criterio | Nota 3  |
|----------|----------------------|
| **Profundidad de la Indagación** | Realmente contesté todas las preguntas formuladas en la unidad y traté de entenderlas a fondo por medio de investigación.  |
| **Calidad de la Experimentación** | Realicé experimentos con un propósito. Verifiqué que sí se está cumpliendo con lo pedido en la unidad. Verifiqué el orden y la lógica detrás de todos los puntos que desarrollé. |
| **Análisis y Reflexión** | Relacioné los resultados obtenidos con la teoría y reflexioné sobre los errores como parte del aprendizaje. |
| **Apropiación y Articulación de Conceptos** | Mostré comprensión clara de los conceptos estudiados en la unidad |
