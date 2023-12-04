# Proyecto-Computacion-Tolerante-Fallas
 
índice 
Contenido
índice	1
Proyecto	2
Página web	2
Localstorage	5
Docker	7
Docker hub	8
Referencias	9

 
Proyecto
Página web
EL programa principal que será subido a Docker es una página web, esta página web es para el equipo universitario de Rugby de la UdeG dicha pagina ayuda al administrador (entrenador) a llevar un cierto control de los jugadores y sus reacciones a los entrenamientos ya que por medio de esta pagina con ayuda de cuestionarios que los atletas contestan antes y después de una sesión el entrenador puede saber cómo están físicamente. 

 
Esta seria la vista principal de la página.
 Aquí tenemos lo que seria un formulario para registro que es la parte una parte importante que de este proyecto ya que este formulario tiene implementado un localstorage esto nos ayuda a que si el usuario que se va a registrar por alguna circunstancia no logra enviar el formulario este se guarde con los datos que dejo ya escritos, cabe resaltar que esto será hasta que se de en el botón de enviar, luego de esto esa información ya no estar almacenada en el localstorage.
Localstorage

¿Qué es? 
localStorage es una propiedad que acceden al objeto Storage y tienen la función de almacenar datos de manera local, localStorage almacena la información de forma indefinida o hasta que se decida limpiar los datos del navegador.

¿Cómo lo usamos en el formulario de registro?
-	Para almacenar los datos usamos una función llamada “setItem(key, value)”
•	Key seria la clave única o el campo.
•	Value sería el valor que se le esta pasando a ese campo
 
Esto pasara cada que la siguiente función se active:
 
Esto lo que hace es que espera que suceda algún evento como “IMPUT”, “SELECT” 0 “TEXTAREA”

-	Para recuperar los datos guardados usamos la función “getItem(key)”
Ahora solo accederíamos al campo que deseamos recuperar con esta función.
 
Adicional a esto llenamos los campos con los valores obtenidos, si es que el usuario capturo todos los datos pues se recuperaran todos, si se quedó a la mitad solo se guardaran eso. 

-	Para borrar los datos una ves que el formulario se envió 
 
Principalmente esta parte es la que nos ayudara a esto:
 
Cuando se detecta que el usuario hace click en el botón “enviar” primer se guardan los datos y luego se borrara el localstorage con “localStorage.clear()”


Docker

Docker es una plataforma de software que le permite crear, probar e implementar aplicaciones rápidamente. Docker empaqueta software en unidades estandarizadas llamadas contenedores que incluyen todo lo necesario para que el software se ejecute, incluidas bibliotecas, herramientas de sistema, código y tiempo de ejecución. Con Docker, puede implementar y ajustar la escala de aplicaciones rápidamente en cualquier entorno con la certeza de saber que su código se ejecutará.
Primero usando Docker y una imagen llamada Nginx, que es necesaria para montar lo que serían páginas web en Docker. 
¿Qué es Nginx? es un servidor web/proxy inverso ligero de alto rendimiento y un proxy para protocolos de correo electrónico como IMAP/POP3. Es software libre y de código abierto, licenciado bajo la Licencia BSD simplificada.

Comenzamos usando este comando 
Comando para construir la imagen:
docker build -t webserver .
 

este creará la imagen, la llamaremos webserver, cuando vayamos a Docker veremos que ya estará nuestra imagen creada. 
 
Este comando lo usamos en una terminal de Linux para Windows 
En la misma terminal pondremos el siguiente comando:
Correr imagen de forma local:
docker run -it --rm -d -p 8080:80 --name web webserver
Aquí Podemos cambiar el puerto, en nuestro caso se usamos ese.
 

Ver lista de imágenes corriendo:
docker ps
Así veremos que imágenes están corriendo si le damos veremos que la imagen que creamos estará ya corriendo y para comprobar solamente haríamos lo que sigue:
 
Si nos metemos al localhost en ese puerto veremos que nuestra página ya estará activa. 
 

Ahora si queremos que no solamente este local nuestra imagen podremos subirla a Docker hub
Docker hub

El Docker Hub es un registro para repositorios de software en la nube, es decir, actúa como una especie de biblioteca para las imágenes Docker. Es un servicio en línea que contiene repositorios públicos y privados.
Para iniciar con ello también usaremos una terminal.
Crear imagen para subirla a Docker hub:
docker build -t slonder/sitiorugby:latest .
 
 
sloder es el usuario y sitiorugby es como se llamará esta imagen en lo que sería Docker hub.
Para subir lo que sería la imagen:
Subir imagen a Docker hub:
docker push slonder/sitiorugby:latest
 
Con esto ya veríamos en Docker hub nuestra imagen que acabamos de crear y subir.
 

Para darnos cuenta de que esto ya no esta de manera local lo que haremos es borrar la primera imagen que creamos e intentar entrar al puerto y deberíamos ver que no es posible ya que dicha imagen ya no se encuentra disponible. 
 
 

Ahora ya borrado eso lo que haremos es terminar de correr un último comando:
docker run -it --rm -d -p 8080:80 --name web slonder/sitiorugby:latest
Este intentara buscar de manera local la imagen, como no la encontrara la buscara en la ruta que le pasamos, debería correr sin problemas ya que esta imagen si la encontrara en Docker hub y será posible ver la página que subimos. 
 
 

 
Referencias
Contenedores de Docker | ¿Qué es Docker? | AWS. (s. f.). Amazon Web Services, Inc. https://aws.amazon.com/es/docker/
Contenedor Docker para servidor HTTP NginX. (2020, 26 noviembre). Leonardo J. Caballero G. https://lcaballero.wordpress.com/2020/11/26/contenedor-docker-para-servidor-http-nginx/#:~:text=Docker%2C%20es%20una%20plataforma%20para,correo%20electr%C3%B3nico%20como%20IMAP%2FPOP3.
Equipo editorial de IONOS. (2023, 24 agosto). Tutorial de Docker: Introducción a la popular plataforma de contenedores. IONOS Digital Guide. https://www.ionos.mx/digitalguide/servidores/configuracion/tutorial-docker-instalacion-y-primeros-pasos/#:~:text=El%20Docker%20Hub%20es%20un,contiene%20repositorios%20p%C3%BAblicos%20y%20privados.

