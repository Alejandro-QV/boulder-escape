Boulder Escape (Selva Profunda)

Juego 3D hecho con Three.js para la evaluación T2 de Computación Gráfica y Visual (Unidad II, semana 10). Un explorador corre solo por un camino en medio de la selva y una roca gigante lo va persiguiendo. El jugador solo mueve al personaje de lado a lado y tiene que esquivar los obstáculos que van apareciendo.

Autor: Gabriel Alejandro Quispe Vasquez

Cómo ejecutarlo

Usé Three.js r128 y lo dejé en la carpeta libs, así que no hace falta internet.

La textura de la roca se carga con TextureLoader desde un archivo (textures/stone.jpg), y los navegadores no dejan cargar imágenes así cuando abres el index.html con doble clic. Por eso hay que abrirlo con un servidor local. Dos formas fáciles:

Con Python, dentro de la carpeta del proyecto: python -m http.server 8000 y luego entrar a http://localhost:8000
Con VS Code: instalar la extensión Live Server, clic derecho sobre index.html y "Open with Live Server".

Si igual lo abren con doble clic, el juego funciona, pero la roca usa una textura de respaldo que genera el propio código y en la consola aparece un aviso.

Controles
A / D o flechas izquierda / derecha: mover al personaje
Barra espaciadora: saltar
Enter, R o el botón "Jugar de Nuevo": reiniciar cuando pierdes
Archivos
index.html: todo el código (HTML, estilos y JavaScript). Está dividido en secciones con comentarios: configuración, escena, materiales, texturas, camino, escenario, personaje, roca, obstáculos y bucle del juego.
libs/three.min.js: la librería Three.js.
textures/stone.jpg: textura de piedra de la roca gigante. Es la única imagen que usa el proyecto. Las demás texturas (corteza, piedra de los obstáculos, hongos) las dibujo con canvas desde el código.

No usé modelos 3D importados. El personaje está armado con cilindros, cajas y esferas de Three.js.

Qué hice para cada requerimiento

REQ-01, escenario. La escena tiene una PerspectiveCamera, una luz ambiental y una direccional con sombras, un camino con textura y un suelo. Todo se actualiza con requestAnimationFrame(). La cámara está detrás del personaje y lo sigue.

RF02, personaje. Es un explorador con sombrero, mochila y bufanda, hecho solo con geometrías básicas. Empieza en el centro del camino y se mueve con A/D o las flechas. Tiene un límite (MAX_X) para que no se salga del camino. También le puse animación de carrera y de salto.

RF03, roca gigante. Es una SphereGeometry con la textura de piedra cargada con TextureLoader. Está detrás del personaje y se ve desde la cámara. Gira todo el tiempo según la velocidad, para que parezca que rueda.

RF04, obstáculos. Los obstáculos puntiagudos son conos (ConeGeometry, función buildSpikes). Aparecen en un carril al azar, se mueven hacia el personaje y cuando pasan se vuelven a colocar al fondo, así que salen nuevos todo el tiempo. Para que nunca sea imposible esquivarlos, siempre hay una distancia mínima entre ellos y dos obstáculos seguidos no caen en el mismo carril.

RF05, movimiento automático. El personaje corre solo y el jugador solo controla el movimiento lateral. En realidad lo que se mueve es el camino, la decoración y los obstáculos, que van hacia la cámara, y la velocidad sube a medida que avanzas.