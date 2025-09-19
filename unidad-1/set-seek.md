# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 1

¿Cómo podrías aplicar lo que has visto en tu perfil profesional?

En mi caso, puedo usar estos sistemas para desarrollar experiencias en entretenimiento digital que combinen lo físico y lo virtual, como videojuegos inmersivos, instalaciones interactivas o prototipos de interfaces.

### Actividad 2

¿Cómo podrías aplicar lo que has visto en tu perfil profesional?

Podría usar estas técnicas para crear entornos visuales interactivos, gráficos dinámicos para videojuegos o herramientas que generen contenido artístico de manera automática.

### Actividad 3

- Inputs: Botones A y B del micro:bit, sacudir el dispositivo, y el botón de Send Love en p5.js.

- Proceso: La señal enviada por el micro:bit a través del puerto serial y que se interpreta en p5.js, que decide qué acción realizar según el dato recibido.

- Outputs: La mariposa y corazón en la pantalla del micro:bit, y el círculo en p5.js que cambia de color (rojo, amarillo o verde).

### Actividad 4

Link p5.js: https://editor.p5js.org/Juanmaaaaaaaaa/sketches/FJko1SMnm

Codigo:

    let x;
    let y;
    let r;
    
    function setup() {
      createCanvas(400, 400);
      x = random(width);
      y = random(height);
      r = sin(x * 0.05) * 100 + 150;
    }
    
    
    function draw() {
      background(0);
      
        
        fill(random(255), random(255), random(255), 150);
        ellipse(x, y, r * 0.1, r * 0.1);
      
    }

