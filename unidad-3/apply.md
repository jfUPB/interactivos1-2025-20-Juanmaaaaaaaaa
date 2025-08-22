# Unidad 3


## 🛠 Fase: Apply

### Actividad 6

### Actividad 7

código p5.js

    let bombTask;
    let port;
    let connectBtn;
    let connectionInitialized = false;
     
    function setup() {
      createCanvas(400, 400);
      background(220);
      port = createSerial();
      connectBtn = createButton("Connect to micro:bit");
      connectBtn.position(80, 300);
      connectBtn.mousePressed(connectBtnClick);
    }
     
    function setup() {
      createCanvas(400, 400);
      background(220);
        port = createSerial();
        connectBtn = createButton("Connect to micro:bit");
        connectBtn.position(80, 300);
        connectBtn.mousePressed(connectBtnClick);
      textAlign(CENTER, CENTER);
      textSize(32);
      bombTask = new BombTask();
    }
     
    function draw() {
      background(0);
      bombTask.update();
      bombTask.display();
    }
     
    class BombTask {
      constructor() {
        this.PASSWORD = ['A', 'B', 'A'];
        this.key = new Array(this.PASSWORD.length).fill('');
        this.keyindex = 0;
        this.count = 20;
        this.startTime = millis();
        this.state = 'CONFIG';
      }
      update() {
          if (this.state === 'ARMED') {
            if (millis() - this.startTime > 1000) {
              this.startTime = millis();
              this.count = max(this.count - 1, 0);
            }
          if (this.count === 0) {
            this.state = 'EXPLODED';
          }
        }
      }
      display() {
        fill(255);
        if (this.state === 'EXPLODED') {
          // Mostrar símbolo de calavera (simple dibujo)
          text('💀', width/2, height/2);
        } else {
          text(this.count, width/2, height/2);
        }
      }
      pressButtonA() {
        if (this.state === 'CONFIG') {
          this.count = min(this.count + 1, 60);
        } else if (this.state === 'ARMED') {
          if (this.keyindex < this.key.length) {
            this.key[this.keyindex] = 'A';
            this.keyindex++;
            this.checkPassword();
          }
        }
      }
      pressButtonB() {
        if (this.state === 'CONFIG') {
          this.count = max(this.count - 1, 10);
        } else if (this.state === 'ARMED') {
          if (this.keyindex < this.key.length) {
            this.key[this.keyindex] = 'B';
            this.keyindex++;
            this.checkPassword();
          }
        }
      }
      shake() {
        if (this.state === 'CONFIG') {
          this.startTime = millis();
          this.state = 'ARMED';
          this.keyindex = 0;
          this.key.fill('');
        }
      }
      reset() {
        if (this.state === 'EXPLODED') {
          this.count = 20;
          this.startTime = millis();
          this.state = 'CONFIG';
        }
      }
      checkPassword() {
        if (this.keyindex === this.key.length) {
          let passIsOK = true;
          for (let i = 0; i < this.key.length; i++) {
            if (this.key[i] !== this.PASSWORD[i]) {
              passIsOK = false;
              break;
            }
          }
          if (passIsOK) {
            this.count = 20;
            this.state = 'CONFIG';
          }
          this.keyindex = 0;
          this.key.fill('');
        }
      }
    }
     
    function keyPressed() {
    if(port.availableBytes() > 0){
            let dataRx = port.read(1); 
           if(dataRx == 'A'){
                if (key === 'A') {
                bombTask.pressButtonA();
             } 
            }
       if(dataRx == 'A'){
                if (key === 'A') {
                bombTask.pressButtonA();
             } 
            }
            if (key === 'A') {
                bombTask.pressButtonA();
            } else if (key === 'B') {
                bombTask.pressButtonB();
            } else if (key === 'S') {
                bombTask.shake();
            } else if (key === 'T') {
              bombTask.reset();
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

Enlace: <iframe src="https://editor.p5js.org/Juanmaaaaaaaaa/full/0CkeuZ5h5"></iframe>

