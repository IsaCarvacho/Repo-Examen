# Examen-Vasquez-Carvacho 

## Viviendo la disforia  
### Por Ayelen Vásquez e Isabella Carvacho  

Nuestro proyecto se basa en crear una experiencia de lo que puede sentir una persona con disforia, el vivir en un cuerpo que no se siente propio y todos los pensamientos que conlleva pasar por una crisis de disforia. Terminamos el proyecto con una pequeña estadística y un mensaje reflexivo.  
Elegimos representarlo a través de la imagen de una persona mirándose al espejo, tanto su cuerpo como sus ojos no se muestran, representando una manera de cómo se debe sentir una persona con disforia al verse al espejo. De a poco empiezan a aparecer mensajes, esto es lo que estaría pensando la persona con disforia al no reconocer el cuerpo en el que habita como suyo. Después se ven partículas puntiagudas acercándose a la persona para representar la presión y agobio que esta siente. Finalmente, llegamos a una pantalla que activa la cámara y nos muestra el mensaje de "La prevalencia registrada de disforia de género aumentó sustancialmente en niños y jóvenes entre 2011 y 2021, especialmente en mujeres. El tratamiento psicológico, junto a una red de apoyo, son cruciales para acompañar a una persona con disforia de género."  

### Explicación decisiones de diseño en la programación  
Imagen en blanco y negro --> Representar soledad y tristeza de no pertenecer en tu propio cuerpo.  
Imagen borrosa --> Tapar justo el pecho de la persona, ya que la sociedad nos define generalmente por nuestros órganos sexuales. También tapar los ojos, para representar no querer verse al espejo.  
Lluvia de mensajes --> Representar que los pensamientos no los podemos controlar y solo se inmiscuyen en nuestra vida.  
Partículas puntiagudas --> Estas partículas representan el estrés y la confusión al experimentar disforia.  
Activar la cámara web y vernos en pantalla --> Como esta es una experiencia inmversiva, quisimos llevarlo un poco más allá, porque pasamos de ver una persona ajena a nosotres a vernos a nosotres mismes en pantalla. Representamos una situación por la que pasan otras personas pero "¿qué pasaría si fuera yo en esta situación?.  
![Collage](https://i.pinimg.com/736x/dc/d9/18/dcd91847c344c3b69411d1037ad38533.jpg)


### Input/Output  

| Input | --> | Output |
| :--- | :---: | ---: |
| loadImage, loadFont | --> | Cargar recursos externos | 
| createCanvas(windowWidth, windowHeight); | --> | Redimensionar el lienzo de p5.js |
| video = createCapture(VIDEO); | --> | Activa la cámara web del usuario |
| random(); | --> | Genera un valor random al elemento que se lo estamos aplicando |
| push(); y pop(); | --> | Protege las configuraciones de los valores que estan adentro |
| resizeCanvas(windowWidth, windowHeight); | --> | Ajustar el tamaño de pantalla al deseado |
|  background(x); | --> | Elegir el color de fondo del lienzo en valores RGB | 
|  pantalla1/2/3/...(); | --> | Crear estados | 
|  fill(x); | --> | Rellenar con color RGB una figura | 
| textAlign(CENTER, CENTER); | --> | Alinear el texto al centro | 
| textFont(x); | --> | Elegir tipografía para el texto | 
| translate(x); | --> | Transladar una figura |
| rotate (x); | --> | Rotar una figura |
| imageMode(CENTER); | --> | Centrar la imagen al centro del lienzo | 
| if (estado > 3) { estado = 0; } | --> | Sí el estado llega a mayor que 3, cambia a 0 y reinicia las pantallas |

### Pensamiento Computacional  
El pensamiento computacional estuvo presente durante todo el desarrollo de la pieza, ya que tuvimos que dividir la experiencia en distintos estados para organizar cada interacción y facilitar la programación. También identificamos patrones repetitivos, como las frases y las figuras, utilizando arrays y loops (for) para gestionar varios elementos de manera más eficiente y a la vez. También trabajamos la abstracción al enfocarnos solo en la información que realmente necesitábamos. Por ejemplo, aunque el reconocimiento facial detecta muchos puntos del rostro, utilizamos únicamente los necesarios para ubicar la imagen en la frente, evitando procesar datos que no aportaban a la interacción. A través de distintos algoritmos controlamos los cambios de estado, el movimiento de los elementos visuales y la respuesta a las acciones de la usuaria. Finalmente, fue necesario analizar y corregir problemas relacionados con la adaptación a diferentes tamaños de pantalla, lo que implicó probar, ajustar y reorganizar partes del código para lograr una experiencia interactiva coherente y funcional.

### Referentes   

Imagenes que aparecen cuando buscamos sobre disforia  
![1](https://i.pinimg.com/736x/f5/e9/43/f5e943bf083f05c147c1314212d60acd.jpg)  
Usamos el trabajo de nuestros compañeres Javiera Corral y Julio Andreé para saber cómo era el código para el uso de cámara web con imagen  
[TrabajoCorralAndree](https://editor.p5js.org/StarBerryChiscake/sketches/9coSmJDBw)  

### Diagrama de flujo  
[Diagrama](https://drive.google.com/file/d/15V9wIHzHXrYHxolZ6_Q11Yz4S9Yy21BD/view)

### Código examen p5.js

//-------------------------------------------------------------------------------//
// EXAMEN // ISABELLA CARVACHO Y AYELEN VÁSQUEZ //
// DISFORIA DE GÉNERO //
//-------------------------------------------------------------------------------//
// FRASES
let Frases = []; // Creamos un Array para ingresar las frases 
let Lluvia = []; // Array que guarda las partículas
let listaFrases = [ //Creamosla lista de frases
  "No encajo",
  "Error",
  "¿Quién soy?",
  "Confusión",
  "Desconexión",
  "Rechazo",
];

// FIGURAS
let formas = []; // Creamos un array vacío 
let cantidad = 60; // Defino el total de figuras 
let imaEstrella; // Ingreso variable para la imagen

// CÁMARA
let captura; // Nos permite usar la cámara web
let faceMesh; //Variable que guardar el modelo de IA (Facemesh) de ml5js.
let options = { 
  maxFaces: 1, // detector cuántos rostros puede reconocer al mismo tiempo.
  refineLandmarks: false, //
  flipped: false
  //// Configuración del reconocimiento facial, reconoce solo una cara (maxFaces), no busca detalles avanzados(refineLandmarks) y no voltea la imagen de la cámara (flipped).
};
let faces = [];  //Base de datos donde la IA guardará las coordenas del rostro.

// REFERENCIA
let referencia;

// IMÁGENES 
let imaFondo; // 
let imagenAtencion = []; //Lista para guardar las imagenes que subimos a files.
let imaPantalla2;
let imaPantalla3;
// TEXTOS
let textoError;

// ESTADOS
let estado = 0;
let botonSiguiente; //Definimos esta variable para poder cambiar de un estado a otro 


//
function gotFaces(result) {
  //Función de respuesta de la IA, result contiene toda la información que recopiló la IA de ml5js.
  faces = result; //Guardamos los resultados dentro de la variable faces para usarlas en nuestro draw.
}


//
//
// PRELOAD
//
//


function preload() {
  textoError = loadFont("CODE Bold.otf");
  imaFondo = loadImage("disforia.jpeg");
  imaEstrella = loadImage("ImaEstrella.png");

 //Funcion para cargar los archivos antes de iniciar.
  faceMesh = ml5.faceMesh(options); //Inicializamos el modelo faceMesh de ml5js y dándole las configuraciones que guardamos en el let options.
 //Cargamos png error
  imagenAtencion = loadImage("atencion.png");
  imaPantalla2 = loadImage ("Pantalla2.png");
  imaPantalla3 = loadImage ("Pantalla3.png");
}

//
// SETUP
//
 function cambiarEstado() {
  estado++;
  if (estado > 3) estado = 0;
}
function setup() {

  createCanvas(windowWidth, windowHeight);
  referencia = min(width, height);

  //Botones
  botonSiguiente = createButton('Presiona para continuar');
  botonSiguiente.position(windowWidth/2 - botonSiguiente.width/2, height   * 0.75); 

  botonSiguiente.center("horizontal");
 
  
  // Cuando se haga clic en el BOTÓN, se ejecutará la acción de           cambiar de un estado a otro
  botonSiguiente.mousePressed(cambiarEstado);

  
  video = createCapture(VIDEO); //Activa la cámara web del usuario.
  video.size(640, 480); //Configuramos la resolución del video para que coincida con el lienzo.
  video.hide(); // Sirve para ocultar el video original que p5js crea por defecto abajo del lienzo.
  faceMesh.detectStart(video, gotFaces); //Empezamos a decirle a ml5js que analice el video continuamente y cuando detecte un rostro llamará a la función "gotFaces" para darnos los datos.
  console.log("ml5 version:", ml5.version);
  
  // CREACIÓN DE FRASES
  for(let i = 0; i < 30; i++){ 

  Frases.push({

    x: random(width), //
    y: random(-height, 0),
    velocidad: random(2,5),
    texto: random(listaFrases), //aca definimos con random la aparición de                                    las frases que aparecerán en el lienzo. 
    tamaño: random(16,30)

  });
  }

  // CREACIÓN DE FIGURAS
  for (let i = 0; i < cantidad; i++) { //// Definimos nuestra variable con el nombre i, variable que funcionará como contador y que partirá desde cero. Luego le decimos al programa que i se siga repitiendo mientras i sea menor que la variable cantidad que definimos como 60. Por último, le decimos al For que esta variable i se vaya reptiendo, hasta llegar a las 60 figuras, por eso la suma de la misma.

    let lado = floor(random(4)); // Acá definimos otra variable para poder decirle al programa desde donde aparecerán las figuras. Por ende definimos "lado" como tal y el código random que hará que aparezcan de un número entre el 1-4, que representan las cuatro esquinas del sketch. Floor como tal es para definir que este número del 1 a 4 no sean decimales. "Floor" como tal lo saque de la IA porque no sabía y no entendía como hacer que la variable apareciera alrededor y no solo en un lado.

    // Aca creamos dos variables más que definirán las                  posiciones de las figuras que se activen por el For
    let x;
    let y;

    // DECLARAMOS NUESTRAS CONDICIONALES
    // aquí estoy usando condicionales, para decidir desde qué lado aparecerá        cada figura
    // la variable "lado" tiene un número random: 0, 1, 2 o 3
    // dependiendo del número, cambia la posición de la figura.
    if (lado == 0) { // Si nuestro lado es 0 
      x = random(width); //genera una posición horizontal random
      y = 0; //significa la parte superior del canvas, de arriba
    }

    else if (lado == 1) { // Si nuestro lado es 1
      x = width; //Define la posición horizontal
      y = random(height); // Genera una posición vertical random.
    }

    else if (lado == 2) { //Si nuestro lado es 2
      x = random(width); // Hace que la figura aparezca en                                cualquier posición horizontal.
      y = height; // Define la posición vertical.
    }

    else { // Si no pasa ninguna condición anterior, entonces                  automaticamente será 3
      x = -0; //Para que aparezcan de la izquierda, por eso el -
      y = random(height); // Cualquier posición vertical
      //Todo esto sirve para que las figuras parezcan invadir el         sketch desde distintos bordes y no desde un solo lugar.
    
    }

    formas.push({
      x: x, //Acá guardamos la posición horizontal
      y: y, //Acá guardamos la posicioón vertical 

      inicioX: x, // guardamos la posición original // donde                          nació cada figura
      inicioY: y, // variable que usaremos para la interacción                        con el mouse
         
    // teniendo las posiciones de las figuras podremos hacer lo         siguiente:

      size: random(30, 80), //Acá decimos que a la forma se le asignara un tamaño random de 30 a 80
      rot: random(TWO_PI), //Acá creamos una rotación random para cada figura. //TWO_PI visto en clases, para crear este movimiento nervioso, lo que hace es elegir un ángulo random entre 0° y 360°. Por lo que la figura se verá rotada.
      velocidad: random(0.5, 1.5) //Acá declaramos que la velocidad variará entre 0.5 a 1.5.

    });
  }
}

//
// RESIZE
//

function windowResized() {

  //Para que se ajuste al tamaño de pantalla que el usuario desee
  resizeCanvas(windowWidth, windowHeight);
  referencia = min(width, height);

}

//
// DRAW
//
function draw() {

  background(220);

  switch (estado) { //Definimos nuestros estados

    case 0:
      pantalla1();
      break;

    case 1:
      pantalla2();
      break;

    case 2:
      pantalla3();
      break;

    case 3:
      pantalla4();
      break;
  }


      let anchoAtencion = width / 3; //Determinamos el ancho de nuestra imagen
      let altoAtencion = height / 3; //Determinamos el alto de nuestra imagen

    }

//
// PANTALLA 1
//

function pantalla1() {

  image(imaFondo, 0, 0, width, height);

  fill(255); //Color 
  textAlign(CENTER, CENTER); //texto al centro
  textFont(textoError); //texto 
  textSize(referencia * 0.04); //tamaño

  text(
    "¿TE SIENTES CÓMODA CON TU CUERPO?",
    //posición
    width / 2, //Posición mitad del lienzo
    height * 0.65 //
  );
}

//
// PANTALLA 2
//

function pantalla2() {

  image(imaPantalla2, 0, 0, width, height);
  
  fill(255);
  textAlign(CENTER);

 //Creamos el for, donde i como contador empezará desde cero y el cual este empezará a recorrer todo el array de Frases que definimos  
  for(let i = 0; i < Frases.length; i++){ 

    let p = Frases[i];
    textSize(p.tamaño);

    text(
      p.texto,
      p.x,
      p.y
    );

    p.y += p.velocidad;
    if(p.y > height + 50){

      p.y = random(-300, -50);
      p.x = random(width);

    }
  }
}

//
// PANTALLA 3
//

function pantalla3() {

  image(imaPantalla3, 0, 0, width, height);

   text(
    "mantén presionado",
    //posición
    width / 2, //Posición mitad del lienzo
    height * 0.65 //
      );

   text(
    "¿SIENTES?",
    //posición
    width / 2, //Posición mitad del lienzo
    height * 0.65 //
      );
  
  for (let i = 0; i < formas.length; i++) {

    let f = formas[i];

    // Movimiento nervioso
    f.x += random(-1.5, 1.5);
    f.y += random(-1.5, 1.5);

    // Interacción
    if (mouseIsPressed) {

      let dx = width / 2 - f.x;
      let dy = height / 2 - f.y;

      f.x += dx * 0.004 * f.velocidad;
      f.y += dy * 0.004 * f.velocidad;

    } else {

      f.x = lerp(f.x, f.inicioX, 0.04);
      f.y = lerp(f.y, f.inicioY, 0.04);

    }

    push();

    translate(f.x, f.y);
    rotate(f.rot);

    tint(255, 150);

    imageMode(CENTER);
    image(
      imaEstrella,
      0,
      0,
      f.size,
      f.size
    );

    pop();
  }

}

//
// PANTALLA 4
//

function pantalla4() {

  //Función Draw que se ejecuta a 60fps de forma continua.
  image(video, 0, 0, width, height); //Dibuja el video de la cámara en el lienzo cubriendo todo el espacio con width y height.
 for (let i = 0; i < faces.length; i++) {
    // let 1 es el primer valor que tiene el computador, al no haber nadie frente a la cámara i vale 0 y como 0 < 0(faces.length) la condición es false y no se ejecuta nada.Si hay alguien frente a la cámara i pasa a valer 1 y como 0 < 1(faces.length) la condición es verdadera y se ejecuta el programa.
    let face = faces[i]; // Toma el rostro que se está analizando de la lista faces y lo guarda en la variable face.


    if (face.keypoints && face.keypoints[9]) {
      //Determinamos la posición de la frente de la cara que según la biblioteca de ml5js se encuentra en el número 9.
      let xRostro = face.keypoints[9].x; //Creamos la variable let xRostro para guardar la posición horizontal de la cara. Con ".x" le pedimos al punto 9 su valor en el eje X; a cuántos pixeles de distancia se encuentra la frente desde el borde horizontal de la pantalla.
      let yRostro = face.keypoints[9].y; //Creamos la variable let yRostro para guardar la posición vertical de la cara. Con ".y" le pedimos al punto 9 su valor en el eje Y; a cuántos pixeles de distancia se encuentra la frente desde el borde vertical de la pantalla.

      let anchoAtencion = width / 3; //Determinamos el ancho de nuestra imagen
      let altoAtencion = height / 3; //Determinamos el alto de nuestra imagen

      image(
        imagenAtencion, //Dibujamos la imagen seleccionada sobre el video
        xRostro - anchoAtencion / 2, //Desplazamos la imagen a la izquierda a la mitad de su ancho para que quede centrada en el eje x, al restarle la mitad la bandera se centra con el centro de nuestra frente.
        yRostro - 50, //Restamos 50 pixeles en el eje Y para que la bandera se posicione por encima de los ojos.
        anchoAtencion, //Le asignamos el ancho ya definido en let anchoBandera
        altoAtencion //le asignamos el alto ya definido en let altoBandera.

        
      );
    }
 }
}

//-------------------------------------------------------------------------------//
// CAMBIO DE ESTADO
//

function cambiarEstado() {

  estado++;

  if (estado > 3) {
    estado = 0;
  }

}

Link a nuestro examen en p5.js
