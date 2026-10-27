# Wedding_website  
Una web de boda en HTML, CSS y JavaScript, pensada para compartir vuestra historia, las fotos, los horarios y las ubicaciones, recibir confirmaciones de asistencia y proponer una playlist.  

El diseño y la lógica están en un único archivo, index.html. No necesita instalar paquetes, utilizar Node.js ni configurar una base de datos. El formulario utiliza Formspree (requiere creación de cuenta, que es gratuita); los mapas y la playlist dependen de servicios externos.  

Esta guía explica cómo adaptar el proyecto con tus propias fotos, textos y detalles.  
1. Haz una copia del proyecto en tu cuenta de GitHub mediante Fork, o descarga sus archivos y súbelos a un repositorio propio.  
2. Asegúrate de que el archivo de la página se llama index.html, no index.html.txt.  
3. Conserva las imágenes junto a index.html, o actualiza las rutas si decides moverlas a otra carpeta.  
4. Abre el archivo con un editor de texto, como Visual Studio Code. También puedes editarlo desde GitHub con el icono del lápiz.  

#### PARA SUSTITUIR LAS FOTOS:

La forma más sencilla es dar a tus imágenes los mismos nombres que espera el código y anadirlas a tu repositorio, eliminando las anteriores.  
Las fotos corresponden a:  

foto_portada.jpeg	: Fondo de la portada  
foto_pareja1.jpeg	: Primera foto de la galería  
foto_pareja2.jpeg	: Segunda foto de la galería  
foto_pareja3.jpg	: Tercera foto de la galería  
foto_pareja4.jpeg	: Cuarta foto de la galería  
foto_iglesia.png	: Imagen de la ceremonia  
foto_celebracion.png	: Imagen de la celebración  

Las extensiones importan: .jpg, .jpeg y .png. Las mayúsculas también deben coincidir.  

Si prefieres otros nombres/extensiones, cambia las referencias correspondientes en index.html. La portada está en el CSS, dentro de .hero:  

url('mi-portada.jpg') center/cover no-repeat;  

Las demás imágenes están en etiquetas HTML:  

&lt;img src="mi-foto.jpg" alt="La pareja durante un viaje"&gt;  

#### PARA CAMBIAR LOS NOMBRES, LA HISTORIA Y LOS DETALLES:

Busca estas etiquetas o identificadores en el archivo index.html:  
A continuacion se indica: Qué personalizar	/ Dónde buscar.  

Nombre que aparece en la pestaña del navegador	/ &lt;title&gt;  
Nombres de la pareja	/ &lt;h1&gt; dentro de la portada  
Fecha y ciudad visibles	/ El párrafo inmediatamente después del &lt;h1&gt;  
Historia y texto de bienvenida	/ &lt;section id="nosotros"&gt;  
Texto, horarios e imágenes de la ceremonia y celebración	/ &lt;section id="detalles"&gt;  
Direcciones, enlaces y mapas	/ &lt;section id="lugares"&gt;  
Playlist / &lt;section id="playlist"&gt;  
Sección opcional de lista de bodas /	&lt;section id="lista-bodas"&gt;  
Preguntas del formulario y fecha límite	/ &lt;section id="rsvp"&gt;  
Despedida al final de la página	/ &lt;footer&gt;  

#### PARA CAMBIAR EL CONTADOR:

Cambiar la fecha visible de la portada no cambia el contador. Busca al final del archivo:  

const weddingDate = new Date('...');  

Sustituye el valor por la fecha y hora de tu ceremonia. Utiliza el formato:  

const weddingDate = new Date('2030-06-15T18:00:00+02:00');  

#### PARA ACTUALIZAR UBICACIONES Y MAPAS:

Cada ubicación tiene tres partes independientes que debes revisar:  
1. El nombre y la dirección que lee el invitado.  
2. El enlace href del botón para abrir Google Maps.  
3. La dirección src del &lt;iframe&gt; que muestra el mapa integrado.  

Para el botón puedes utilizar una búsqueda de Google Maps:  

&lt;a  
  href="https://www.google.com/maps/search/?api=1&amp;amp;query=TU+LUGAR+Y+DIRECCION"  
  target="_blank"  
  rel="noopener noreferrer"&gt;  
  Abrir en Google Maps  
&lt;/a&gt;  

Sustituye TU+LUGAR+Y+DIRECCION por el lugar correcto. Para el mapa integrado, puedes obtener el código desde la opción de compartir e insertar un mapa de Google Maps y sustituir el &lt;iframe&gt; de esa ubicación.  

#### PARA CAMBIAR EL FORMULARIO:

La web recoge nombre, apellidos, email, teléfono, asistencia, necesidad de autobús, restricciones alimentarias y un mensaje. Las respuestas se envían a Formspree, no se guardan en GitHub. Para ello:  
1. Crea tu cuenta en Formspree (Gratis).  
2. Crea un formulario y configura dónde quieres recibir las respuestas.  
3. Copia su dirección de envío, con formato https://formspree.io/f/TU_FORM_ID.  
4. Sustituye el destino anterior en los dos lugares donde aparece en el código.  

Primero, en el HTML:  

&lt;form id="rsvpForm" action="https://formspree.io/f/TU_FORM_ID" method="POST"&gt;  

Después, en el JavaScript:  

const response = await fetch("https://formspree.io/f/TU_FORM_ID"  

5. Personaliza las preguntas  

Puedes modificar los textos de las etiquetas y las opciones de los desplegables. Los campos que quieras enviar deben conservar un atributo name. El atributo required marca los campos obligatorios.  

6. Actualiza la fecha límite, el mensaje de confirmación y la pregunta sobre autobuses. Mantén id="rsvpForm" e id="successMessage" salvo que actualices también sus referencias en JavaScript.  

Prueba el formulario únicamente después de configurar tu propio destino y confirma que la respuesta llega a tu cuenta. Mostrar la página por sí solo no comprueba el envío.  

#### PARA CAMBIAR LA PLAYLIST DE SPOTIFY:

En la sección playlist hay un botón y un reproductor. Debes actualizar ambos.  
- Botón: sustituye su href por el enlace de tu playlist.  
- Reproductor: en Spotify, abre la playlist y utiliza Compartir -&gt; Insertar playlist. Copia el &lt;iframe&gt; generado y sustituye el actual.  

El reproductor utiliza una URL de inserción como esta:  

&lt;iframe  
  style="border-radius:12px"  
  src="https://open.spotify.com/embed/playlist/TU_PLAYLIST_ID"  
  width="100%"  
  height="380"  
  frameborder="0"  
  allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"  
  loading="lazy"&gt;  
&lt;/iframe&gt;  

Usa la URL /embed/playlist/ para el reproductor, no el enlace normal de compartir. Si quieres que los invitados añadan canciones, configura además las opciones de colaboración de tu playlist en Spotify; incrustarla en la web no activa esa función.  

#### PARA CAMBIAR COLORES Y ESTILO:

Los colores principales están al principio del CSS, dentro de :root:  

:root {  
  --bg: #f7f3ee;  
  --paper: #fffdf9;  
  --text: #2f2a26;  
  --muted: #7a6f67;  
  --accent: #8f6f5a;  
  --accent-soft: #e7d9cc;  
  --line: #ddd2c7;  
}  

La tipografía principal está en body:  

font-family: Georgia, "Times New Roman", serif;  

RECUERDA COMPROBAR QUE TODO FUNCIONA CORRECTAMENTE ANTES DE PUBLICARLA!  
Para ello, abre index.html en el navegador para revisar el diseño. Para probarla desde un servidor local, si tienes Python instalado, ejecuta este comando en la carpeta del proyecto:  

python3 -m http.server 8000  

En algunos equipos el comando es python -m http.server 8000. Después abre http://localhost:8000. Para detener el servidor, pulsa Ctrl+C en la terminal. Comprueba si esta lista para publicacion y no hay elementos de la version original.  

#### PARA PUBLICARLA CON GITHUB:

Para esta web estática puedes publicar directamente desde una rama:  
1. Sube index.html y tus imágenes a la raíz de tu repositorio.  
2. Abre Settings → Pages.  
3. En Build and deployment → Source, selecciona Deploy from a branch.  
4. Selecciona la rama donde están tus archivos, normalmente main, y la carpeta /(root).  
5. Pulsa Save y espera a que termine la publicación.  
6. Abre la dirección que muestra GitHub Pages. Para un repositorio de proyecto suele tener el formato https://TU_USUARIO.github.io/TU_REPOSITORIO/.  

Las actualizaciones que guardes en esa rama se publicarán de nuevo. Comprueba el resultado en Actions si una actualización no aparece o falla.  

La web publicada será accesible desde su URL. El formulario depende de una conexión a internet y de la configuración de Formspree; no necesitas poner contraseñas ni claves privadas en el HTML para utilizar su dirección pública de envío.  

AUTORIA Y REUTILIZACION  

Web original desarrollada por Natalia Pérez Jiménez con AI-assisted tools. Esta guía explica su personalización; no incorpora una licencia de software ni concede derechos sobre las fotografías.  
