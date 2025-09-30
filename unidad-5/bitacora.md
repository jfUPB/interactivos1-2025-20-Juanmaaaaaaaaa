
# Evidencias de la unidad 5

### Actividad 01 
1. ¿Cómo se realiza la comunicación micro:bit ↔ p5.js?
El micro:bit envía los valores de xValue, yValue, aState y bState en formato de texto plano (ASCII), separados por comas y terminados en un salto de línea. p5.js recibe esa cadena por puerto serial, la divide y convierte los datos a números o booleanos.
2. ¿Qué protocolo se usa en el envío de datos ASCII?
El protocolo consiste en:
•	Separar valores con coma ,.
•	Finalizar cada paquete con salto de línea \n.
Esto hace que p5.js sepa dónde empieza y termina cada paquete.
3. ¿Cómo se leen los datos en p5.js (ASCII)?
Se usa port.readUntil("\n") para leer la cadena completa, después split(",") para separar valores.
4. ¿Cómo se detectan los eventos A pressed y B released?
Se comparan el estado actual y el anterior:
•	Si antes era false y ahora es true → “A pressed”.
•	Si antes era true y ahora es false → “B released”.
5. Capturas de pantalla.
 
 <img width="975" height="525" alt="image" src="https://github.com/user-attachments/assets/5cfb8111-40d1-4913-b72f-85cf4b79dde8" />

 <img width="975" height="526" alt="image" src="https://github.com/user-attachments/assets/53ff4e9b-af4e-4fe6-9099-863a25bd9329" />

<img width="975" height="525" alt="image" src="https://github.com/user-attachments/assets/7d9446fc-bff7-4480-958f-f8620c68e509" />


### Actividad 02
- Captura el resultado del experimento anterior. ¿Por qué se ve este resultado?

 <img width="975" height="529" alt="image" src="https://github.com/user-attachments/assets/57f3855d-c5b3-4841-9592-ea809512448a" />

Se ve este resultado porque así es como se están enviando los datos desde el microbit

- Captura el resultado del experimento anterior. Lo que ves ¿Cómo está relacionado con esta línea de código?
data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
 
<img width="975" height="527" alt="image" src="https://github.com/user-attachments/assets/f0ef04bf-b911-4f8d-a8ad-cfc0a87859c2" />

El resultado en hex refleja directamente esta estructura: 4 bytes para xValue y yValue, y 1 byte para cada botón.

- ¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII?

Ventajas del binario

-- Más compacto.
-- Más rápido de enviar y procesar.
-- Menos ambigüedad: cada byte tiene un significado fijo.

Desventajas del binario

-- Difícil de leer sin herramientas.
-- Más complicado de depurar manualmente.

- Captura el resultado del experimento. ¿Cuántos bytes se están enviando por mensaje? ¿Cómo se relaciona esto con el formato '>2h2B'? ¿Qué significa cada uno de los bytes que se envían?

 <img width="975" height="527" alt="image" src="https://github.com/user-attachments/assets/d7a6670f-db9d-4b8b-b6bf-ad48311b2cf2" />

Se envían 6 bytes por mensaje:

2 bytes → xValue (entero corto con signo).
2 bytes → yValue (entero corto con signo).
1 byte → aState (0 o 1).
1 byte → bState (0 o 1).

El total coincide con la definición '>2h2B'.


- Recuerda de la unidad anterior que es posible enviar números positivos y negativos para los valores de xValue y yValue. ¿Cómo se verían esos números en el formato '>2h2B'?

Cómo se usan enteros cortos con signo (h), los valores se representan en complemento a dos:

-- Un número positivo (+200) se vería como 00 C8 en hex.
-- Un número negativo (-200) se vería como FF 38 en hex.

De esta forma, el receptor sabe si el valor es positivo o negativo.

- Captura el resultado del experimento. ¿Qué diferencias ves entre los datos en ASCII y en binario? ¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII? ¿Qué ventajas y desventajas ves en usar un formato ASCII en lugar de binario?


<img width="975" height="527" alt="image" src="https://github.com/user-attachments/assets/5e0051f1-7790-4a36-815a-7f5786b2f2d7" />


Diferencias observadas:

-- En binario se ven 6 bytes (difíciles de leer, pero compactos).
-- En ASCII se ve texto claro como -123,456,0,1, mucho más fácil de entender.

Ventajas del binario:

-- Compacto y eficiente.
-- Menos consumo de ancho de banda.
-- Ideal para comunicación rápida y con muchos datos.

Desventajas del binario:

-- Difícil de depurar a simple vista.
-- Se necesita conocer exactamente el formato para interpretarlo.

Ventajas del ASCII:

-- Legible para humanos sin necesidad de herramientas.
-- Fácil de depurar y probar rápidamente.
-- Portable entre sistemas sin preocuparse por endianness.

Desventajas del ASCII:

-- Más bytes por cada dato → menos eficiente.
-- Conversión de texto ↔ número consume más tiempo de CPU.

### Actividad 3

 <img width="975" height="528" alt="image" src="https://github.com/user-attachments/assets/aaabb391-623b-4090-977b-fd596f1ac8dd" />


 - Explica por qué en la unidad anterior teníamos que enviar la información delimitada y además marcada con un salto de línea y ahora no es necesario.

Ahora, los datos se envían en binario con longitud fija (6 bytes). Como siempre son exactamente 6 bytes, el receptor sabe que cada 6 bytes completos corresponden a un paquete. Ya no hace falta un salto de línea. Pues antes los paquetes tenían tamaño variable porque los datos se enviaban como texto.

- Compara el código de la unidad anterior relacionado con la recepción de los datos seriales que ves ahora. ¿Qué cambios observas?

Antes:

-- Se recibía una cadena de texto ("500,524,True,False\n").
-- Se separaban los valores con .split(",").
-- Se convertían manualmente a enteros o booleanos.

Ahora:

-- Se leen 6 bytes exactos con port.readBytes(6).
-- Se interpreta el contenido con un DataView (getInt16, getUint8).

- ¿Qué ves en la consola? ¿Por qué crees que se produce este error?
 
<img width="975" height="527" alt="image" src="https://github.com/user-attachments/assets/03323382-786c-4723-94c1-c0130089b82d" />


Se observa lo de la imagen, realmente no se muy bien porque es pero según el texto puede ser por un error en la comunicación serial.


 - Analiza el código, observa los cambios. Ejecuta y luego observa la consola. ¿Qué ves?

<img width="975" height="529" alt="image" src="https://github.com/user-attachments/assets/846df457-ca32-43ff-b0d3-6778347bb726" />

 
A diferencia de antes, ahora la consola no manda todo el mensaje que esta siendo enviado por el microbit.


- ¿Qué cambios tienen los programas y ¿Qué puedes observar en la consola del editor de p5.js?

 <img width="975" height="527" alt="image" src="https://github.com/user-attachments/assets/df145ec9-4fad-4d04-b553-28415f23220d" />


El código de micro:bit ahora envía los datos en binario con struct.pack en lugar de texto ASCII.
En p5.js ya no se usan cadenas ni split(","); ahora se leen bloques de 6 bytes con DataView y se extraen los valores (getInt16, getUint8).
Para evitar errores, se agregó un sistema de framing con un byte de inicio (header 0xAA) y un checksum al final.
El receptor mantiene un buffer y solo procesa los paquetes que cumplen con el formato correcto.

### Actividad 04

Link p5: https://editor.p5js.org/Juanmaaaaaaaaa/sketches/zKkbVZpRX 

Primeramente, lo que decidí hacer es coger el código que ya tenía de la unidad anterior e intentar cambiarlo para que funcionara con el formato que se pedía, el que enviaba el microbit. Sin embargo, me dio errores por no tener asignadas bien las variables puesto que por comodidad en la unidad anterior lo tenía como mouseX y mouseY, pero en el código la parte que leía la información enviada estaba con otro nombre.

 <img width="975" height="526" alt="image" src="https://github.com/user-attachments/assets/41a4a792-4e60-4c46-b76e-182da98aee11" />


Ya arreglado este error, al seguir probando el código me di cuenta que no estaba usando bien los estados, pues tenia todo muy desorganizado, pues en la unidad anterior no utilice bien lo de los estados por lo que una línea no cuadraba, pues tome el código de la actividad 3.

 <img width="975" height="528" alt="image" src="https://github.com/user-attachments/assets/304f3f97-d410-427f-834f-947cfe6658df" />


Como en la unidad anterior no use bien lo de los estados pensé en que pasaría si solo quitaba esa línea de código y para mi sorpresa dejo que la aplicación funcionara, pero apareció otro error. Aunque en la imagen se ve que funciona y pues funcionaba, pero la aplicación parpadeaba de forma repetitiva haciendo que se vea una pantalla totalmente oscura. 

 <img width="975" height="524" alt="image" src="https://github.com/user-attachments/assets/e405b737-ed6f-4798-8044-71fd3302fa79" />


Finalmente, decidí que ese código que tenía ahí era una aberración y que tenia que cuadrar bien los estados por lo que tomé como ejemplo la actividad anterior y base mi código en los estados presentes allí, para tener un código mas ordenado y saber que pasaba si había un error. Al final no hubo error alguno, pues el código funciono completamente bien (Además metí lo del framing que no estaba antes y por eso también estaba raro, pues leía 6 bits, cuando eran 8 bits por el código del microbit).

 <img width="975" height="530" alt="image" src="https://github.com/user-attachments/assets/f0a35e07-d3e1-4168-b4cd-4f5c6acc15fc" />


## Rúbrica


| Criterio | Nivel 4.4 (Logrado) |
|----------|----------------------|
| **Profundidad de la Indagación** | Realmente contesté todas las preguntas formuladas en la unidad y traté de entenderlas a fondo por medio de investigación y con la ayuda de Inteligencia Artificial. Pues la Inteligencia Artificial va a ayudarme a responder preguntas que tengo acerca de determinados puntos. |
| **Calidad de la Experimentación** | Realicé experimentos con un propósito. Verifiqué que sí se está cumpliendo con lo pedido en la unidad. Verifiqué el orden y la lógica detrás de todos los puntos que desarrollé. |
| **Análisis y Reflexión** | Relacioné los resultados obtenidos con la teoría y reflexioné sobre los errores como parte del aprendizaje. |
| **Apropiación y Articulación de Conceptos** | Mostré comprensión clara de los conceptos estudiados en la unidad y los utilice a la hora de la aplición |
