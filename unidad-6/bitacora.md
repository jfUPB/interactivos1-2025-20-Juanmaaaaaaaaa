
# Evidencias de la unidad 6

## Actividad 1

### ¿Qué ocurrió en la terminal cuando ejecutaste npm install? ¿Cuál crees que es su propósito?

-El comando revisó el archivo package.json del proyecto.
- Se descargó e instaló las dependencias necesarias (120 paquetes en este caso).
- Se auditó los paquetes y se reportó que no había vulnerabilidades.
- Se mostró un aviso de que hay una nueva versión de npm disponible (10.9.3 → 11.6.0)

Esto sirve para instalar todas las dependencias que el proyecto necesita para poder ejecutarse correctamente.



### ¿Qué mensaje específico apareció en la terminal después de ejecutar npm start? ¿Qué indica este mensaje?

    Server is listening on http://localhost:3000

Este mensaje indica que el proyecto arrancó un servidor local y está escuchando peticiones en el puerto 3000.
Es decir, ahora puedes abrir tu navegador e ir a http://localhost:3000 para interactuar con la aplicación.

### Describe lo que ves inicialmente en page1 y page2 en tu navegador.

Se puede observar un círculo con una circunferencia negra y su interior rojo, un fondo blanco y una línea negra que apunta hacia la derecha en el caso de la página 1 y hacia la izquierda en el caso de la página 2.

### ¿Qué mensajes aparecieron en la terminal del servidor cuando abriste page1 y page2?

    
    A user connected - ID: WlV8zyq9POnCwX1mAAAB    //Cuando se abrió la página 1
    Received win1update from ID: WlV8zyq9POnCwX1mAAAB Data: { x: 1714, y: -21, width: 733, height: 491 }
    Debug - Connected clients: 1, Page1: 1, Page2: 0, Synced: 0
    Sync status: pages=false, synced=false, clients=1
    A user connected - ID: cBv6g2zd_-MLINoLAAAD    //Cuando se abrió la página 2
    Received win2update from ID: cBv6g2zd_-MLINoLAAAD Data: { x: 2630, y: 143, width: 663, height: 361 }
    Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 0
    Sync status: pages=true, synced=false, clients=2
    Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 1
    Sync status: pages=true, synced=false, clients=2
    Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 1
    Sync status: pages=true, synced=false, clients=2
    Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
    All clients are fully synced

### Describe qué sucede en ambas páginas del navegador cuando mueves una de las ventanas. ¿Cambia algo visualmente? ¿Qué mensajes aparecen (si los hay) en la consola del navegador (usualmente accesible con F12 -> Pestaña Consola) y en la terminal del servidor?

A nivel visual, cuando se mueve una de las ventanas, la línea negra persigue al centro del circulo de la otra pagina haciendo que se vea como que las líneas de ambas pestañas estén como conectados y se vean como solo una línea.

Mensajes consola del navegador:

<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/db0a64a4-e525-4973-9a20-fd78b043c38e" />

Mensajes terminal del servidor:

<img width="1173" height="598" alt="image" src="https://github.com/user-attachments/assets/3ab05093-61c4-4580-8128-82fbbaa8ea5e" />


### Evidencias

<img width="1466" height="750" alt="Captura de pantalla 2025-09-23 110841" src="https://github.com/user-attachments/assets/6cd79b09-02b6-4f1b-8140-30b850cfe13d" />

<img width="1465" height="733" alt="Captura de pantalla 2025-09-23 110809" src="https://github.com/user-attachments/assets/b5c59b2a-d3a7-4fa7-9881-173680229458" />

<img width="1919" height="1079" alt="Captura de pantalla 2025-09-23 110745" src="https://github.com/user-attachments/assets/5437a0f1-1158-4b54-9a42-ad4c8ccd342e" />


## Actividad 2

### Piensa en cómo te conectas a Internet en casa o en la Universidad. ¿Usas Wi-Fi? ¿Un cable de red? Eso es simplemente tu “rampa de acceso” a la gran red de carreteras. ¿Qué pasaría si esa rampa se corta? Anota tus ideas.

En mi casa me conecto principalmente por Wi-Fi, y en la universidad también. Si esa “rampa de acceso” se corta (por ejemplo, se cae el Wi-Fi o el cable de red), perdería la conexión con toda la red: no podría abrir páginas web, enviar correos o acceder a servicios en la nube. En otras palabras, mi computador seguiría funcionando localmente, pero estaría “aislado” del resto del mundo.


### ¿Puedes identificar otros ejemplos de relaciones Cliente-Servidor en tu vida diaria (no necesariamente digitales)? Por ejemplo, al pedir comida en un restaurante. ¿Quién es el cliente y quién el servidor? ¿Qué se pide y qué se entrega?

En un restaurante: el cliente soy yo que hago el pedido, y el servidor es el mesero/cocina que trae la comida. Yo pido un plato, y me entregan la comida lista.

En una biblioteca: el cliente es la persona que pide un libro, y el servidor es el bibliotecario que entrega el libro.

En una tienda: el cliente pide un producto, el servidor (cajero o dependiente) entrega el artículo.


### Toma la URL de tu sitio web favorito. Intenta identificar el protocolo, el nombre de dominio y la ruta (si la hay). ¿Qué crees que pasa si solo escribes el nombre de dominio (ej. www.google.com) sin una ruta específica? ¿Qué “página por defecto” crees que te envía el servidor?

Ejemplo: https://www.youtube.com/watch?v=uqn0UGAt6oc

Protocolo: https://

Dominio: www.youtube.com

Ruta: /watch?v=uqn0UGAt6oc

Si solo escribo el dominio www.youtube.com, el servidor me envía por defecto la página principal de YouTube (inicio con videos recomendados). Esto se debe a que el servidor suele tener configurado un archivo por defecto, normalmente llamado index.html.


### Compara HTTP con los protocolos seriales que usaste. ¿Qué similitudes encuentras? ¿Qué diferencias clave ves? ¿Por qué crees que HTTP necesita ser más complejo que un simple envío de bytes como hacías con el micro:bit?

- Similitudes: Ambos definen un conjunto de reglas para que dos dispositivos se entiendan. Envían datos de un lado al otro.

- Diferencias: El protocolo serial es muy básico (solo envío de bytes crudos), mientras que HTTP incluye información adicional como cabeceras, métodos (GET, POST), códigos de estado y tipos de contenido.

- Razón de la complejidad: HTTP necesita ser más complejo porque en la web se transmiten datos muy variados (texto, imágenes, videos, formularios). Hace falta estructura para que navegador y servidor sepan qué se está enviando y cómo interpretarlo.


### Piensa en una página web simple, como un formulario de login. ¿Qué parte crees que es HTML? ¿Qué parte es CSS? ¿Qué parte es JavaScript?

- HTML: Los campos de texto (usuario, contraseña) y el botón de “Iniciar sesión”.
- CSS: El color del botón, el tamaño de la letra, la disposición del formulario en la pantalla.
- JavaScript: La validación de que los campos no estén vacíos, mostrar el mensaje “Contraseña incorrecta” sin recargar la página.


### Compara el bucle draw() de p5.js con este modelo de “esperar a que algo pase y reaccionar”. ¿Qué ventajas crees que tiene el modelo basado en eventos para una interfaz de usuario web? ¿Sería eficiente tener un bucle draw() redibujando toda la página 60 veces por segundo si nada ha cambiado?

- El modelo basado en eventos es más eficiente porque solo actúa cuando el usuario hace algo (clic, escribir, mover el ratón).

- No sería eficiente redibujar toda la página 60 veces por segundo si nada cambia, sería un desperdicio de recursos.

- Con eventos, el navegador se mantiene ligero y responde justo en el momento necesario.


### ¿Por qué crees que podría ser útil usar JavaScript tanto en el cliente (navegador) como en el servidor? ¿Se te ocurre alguna ventaja para los desarrolladores?

- Permite compartir código entre cliente y servidor.

- Facilita el trabajo en equipo y reduce la necesidad de cambiar constantemente entre diferentes lenguajes.


### Resume con tus propias palabras la diferencia fundamental entre una comunicación HTTP tradicional y una comunicación usando WebSockets/Socket.IO. ¿En qué tipo de aplicaciones has visto o podrías imaginar que se usa esta comunicación en tiempo real?

- HTTP tradicional: El cliente pide y el servidor responde, como un correo que envías y recibes. La comunicación no es continua.

- WebSockets/Socket.IO: Se abre un canal permanente, como una llamada telefónica, donde cliente y servidor pueden enviarse mensajes en tiempo real sin tener que “pedir” de nuevo cada vez.

Ejemplos de uso:

- Aplicaciones de chat (WhatsApp Web, Messenger).

- Juegos online en tiempo real.

- Aplicaciones colaborativas como Google Docs.

- Seguimiento en tiempo real de posiciones.

### Actividad 3

Experimenta 1

- Detén el servidor si está corriendo.
- Cambia la primera ruta de /page1 a /pagina_uno.
- Inicia el servidor.

No funciona.
<img width="1827" height="809" alt="Captura de pantalla 2025-10-03 005201" src="https://github.com/user-attachments/assets/7915967d-f394-434d-b27f-bcef74b81786" />

Intenta acceder a http://localhost:3000/page1. ¿Funciona?

Si, si funciona.
<img width="1807" height="831" alt="Captura de pantalla 2025-10-03 005249" src="https://github.com/user-attachments/assets/e106cab9-2ca0-41f3-a5f8-e09b60cb55d7" />

Ahora intenta acceder a http://localhost:3000/pagina_uno. ¿Funciona?

No, no funciona.
<img width="1787" height="785" alt="Captura de pantalla 2025-10-03 005307" src="https://github.com/user-attachments/assets/187585dc-34ba-4b89-8173-b46b3ccb9a6c" />

¿Qué te dice esto sobre cómo el servidor asocia URLs con respuestas? Restaura el código.

El servidor asocia cada URL con una respuesta específica.Ademas, si cambias el nombre de la ruta, la URL anterior deja de estar disponible, aunque el archivo detrás siga existiendo.

Experimenta 2

- Asegúrate de que el servidor esté corriendo (npm start).
- Abre http://localhost:3000/page1 en una pestaña. Observa la terminal del servidor. ¿Qué mensaje ves? Anota el ID.

El mensaje:

      A user connected - ID: lYrLl6VFmAOOX8pbAAAB
      Received win1update from ID: DsJyo7OeRPGNhYZBAAAH Data: { x: 1617, y: -61, width: 615, height: 541 }
      Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 1
      Sync status: pages=true, synced=false, clients=2
      Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 1
      Sync status: pages=true, synced=false, clients=2
      Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
      All clients are fully synced

ID: lYrLl6VFmAOOX8pbAAAB
  
Abre http://localhost:3000/page2 en OTRA pestaña. Observa la terminal. ¿Qué mensaje ves? ¿El ID es diferente?

El mensaje:

    A user connected - ID: sZxgIDpJjfUS9XebAAAD
    Received win2update from ID: hVHwSMZnHQMtEmz_AAAJ Data: { x: 2396, y: 86, width: 865, height: 378 }
    Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 1
    Sync status: pages=true, synced=false, clients=2
    Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 1
    Sync status: pages=true, synced=false, clients=2
    Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
    All clients are fully synced

ID: sZxgIDpJjfUS9XebAAAD

El ID de ambos es diferente.


Cierra la pestaña de page1. Observa la terminal. ¿Qué mensaje ves? ¿Coincide el ID con el que anotaste?

    User disconnected - ID: sZxgIDpJjfUS9XebAAAD

Si coinciden los ID.

Cierra la pestaña de page2. Observa la terminal.

El mensaje:

    User disconnected - ID: lYrLl6VFmAOOX8pbAAAB
    User disconnected - ID: sZxgIDpJjfUS9XebAAAD

Evidencias:

<img width="1015" height="552" alt="image" src="https://github.com/user-attachments/assets/0607667c-98d8-4bf4-bec4-9678c3062cc4" />

<img width="1774" height="898" alt="Captura de pantalla 2025-10-03 010855" src="https://github.com/user-attachments/assets/2182ab7d-54c6-4dc4-92d2-2a5c94b139d2" />

Experimenta 3

Inicia el servidor y abre page1 y page2.
Mueve la ventana de page1. Observa la terminal del servidor. ¿Qué evento se registra (win1update o win2update)? ¿Qué datos (Data:) ves?

El win2update, los datos que veo es el tamaño de la pestaña y la posición en x y y de la pestaña.

<img width="1786" height="983" alt="image" src="https://github.com/user-attachments/assets/611f8ad1-f129-439b-8caf-091bb00f0423" />

Mueve la ventana de page2. Observa la terminal. ¿Qué evento se registra ahora? ¿Qué datos ves?

Ahora se registra win1update, los datos que veo es el tamaño de la pestaña y la posición en x y y de la pestaña.
<img width="1873" height="939" alt="image" src="https://github.com/user-attachments/assets/d046fe45-5961-4aa1-9f72-e5dbc287ed02" />

Experimento clave: cambia socket.broadcast.emit(‘getdata’, page1); por socket.emit(‘getdata’, page1); (quitando broadcast). Reinicia el servidor, abre ambas páginas. Mueve page1. ¿Se actualiza la visualización en page2? ¿Por qué sí o por qué no? (Pista: ¿A quién le envía el mensaje socket.emit?). Restaura el código a broadcast.emit.
