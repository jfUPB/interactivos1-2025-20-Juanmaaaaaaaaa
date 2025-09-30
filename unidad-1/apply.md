# Unidad 1


## 🛠 Fase: Apply

### Actividad 5

El sistema físico interactivo conecta el micro:bit con p5.js a través de comunicación serial.

- Cuando el botón A está presionado, el micro:bit envía la letra A.
- Cuando no está presionado, envía N.
- En p5.js, este dato se interpreta en cada frame: si recibe A, el cuadrado se pinta de rojo; si recibe N, se pinta de verde.

El problema inicial era que el cuadrado solo cambiaba por un frame y volvía a verde. La solución consistió en enviar constantemente el estado del botón (A o N), lo que mantiene actualizado el color del cuadrado.

### Actividad 6

Link p5.js: https://editor.p5js.org/Juanmaaaaaaaaa/sketches/euovdjEXp

Código p5.js:

    let port;
    let x = 200;
    let connectBtn;
    let connectionInitialized = false;
        
    function setup() {
      createCanvas(400, 400);
      port = createSerial();
      connectBtn = createButton("Connect to micro:bit");
      connectBtn.position(80, 300);
      connectBtn.mousePressed(connectBtnClick);
    }
        
    function draw() {
      background(220);
    
      if (port.opened() && !connectionInitialized) {
        port.clear();
        connectionInitialized = true;
      }
    
      ellipse(x, height / 2, 50, 50);
    
        if (port.availableBytes() > 0) {
          let dataRx = port.read(1);
          if (dataRx == "A") {
            x -= 10;
          } else if (dataRx == "B") {
              x += 10; 
          }
        }
    
     
    
        if (!port.opened()) {
          connectBtn.html("Connect to micro:bit");
        } else {
          connectBtn.html("Disconnect");
        }
      }
    
      function connectBtnClick() {
        if (!port.opened()) {
          port.open("MicroPython", 115200);
        } else {
          port.close();
        }
    }


Microbit código:

    from microbit import *
    
    while True:
        if button_a.is_pressed():
            uart.write('A')
        elif button_b.is_pressed():
            uart.write('B')
        sleep(100)


