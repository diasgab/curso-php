## Solicitudes web y creación de nuevas páginas

¿Qué hay detras de una solicitud web?

En la primer unidad vimos que la web trabaja con solicitues y respuestas web (en inglés se utiliza Request y Response, de forma que utilizaremos estos términos indistintamente para ir familiarizandonos). Nuestro navegador envía a internet un request HTTP para http://nuestraweb.com/contacto.php. De alguna forma, este request encuentra nuestro servidor y le golpea la puerta. Con un poco de suerte, algún programa que haga las veces de servidor web, como Apache, estará escuchando, abrirá la puerta, buscará en un directorio un archivo llamado contacto.php y procesará todas las etiquetas php. El contenido HTML final será un Response HTTP, y será enviada desde dicho servidor web hasta nuestro navegador.

Entonces todo comenzó cuando enviamos esa solicitud http. De hecho, esa solicitud tiene mucha más información que nuestro nombre de dominio y la página que queremos. Además tiene nuestra dirección IP, la información desde qué navegador estamos iniciando la solicitud y todos los campos y valores en caso que enviemos un formulario.


¿Inspeccionando una solicitud web?

Para ver qué campos tiene un request podemos utilizar la barra de desarrollador de nuestro navegador.

**Nota:** luego de abrir la barra de desarrollador posiblemente debamos refrescar la página actual para ver toda la información. Se recomienda el uso de Google Chrome.

Cada linea es una solicutud web que realizó nuestro navegador. La primer linea será la página que estamos solicitando. Las otras solicitudes son para recursos como css, javascript e imagenes que contenga la página. ¡Si! cada vez que cargamos una página, nuestro navegador realiza multiples solicitudes a internet.

Si hacemos click en la página php solicitada, podremos ver cómo se ve este request http. Parece mucha información. Por ejemplo 'User-Agent' se refiere a qué navegador estamos usando y 'Accept-Language' se refiere a cómo el navegador le informa a nuestro servidor qué idioma hablamos. Por el momento no es relevante, pero podemos obtener toda esta información desde php.

## Creando una nueva página

Para crear una nueva página simplemente podemos crear un nuevo archivo nueva_idea.php en el mismo directorio en el que se encuentra el index.php. Podemos incluir algo de contenido sencillo:

>   ESTA ES MI NUEVA PÁGINA

Para ingreasr a esta nueva página simplemente deberemos ingresar a /nueva_idea.php desde nuestro navegador.

http://localhost/nueva_idea.php

Podemos darle a nuestra página el mismo estilo que tiene nuestro index.php, copiando el header y footer que creamos anteriormente:


<?php require 'layout/encabezado.php'; ?>

ESTA ES MI NUEVA PÁGINA

<?php require 'layout/pie.php'; ?>

Refresca la página para ver los cambios.

## Creando una formulario

Vamos a contruir un formulario para crear nuevas ideas! Por un momento vamos a dejar php de lado y trabajar solamente con html:

```
<h1>Agregar Idea</h1>

<div class="form-group">
    <label for="titulo" class="control-label">Título de la idea</label>
    <input type="text" name="titulo" id="titulo" class="form-control" />
</div>
<div class="form-group">
    <label for="descripcion" class="control-label">Descripción</label>
    <textarea name="descripcion" id="descripcion" class="form-control"></textarea>
</div>
<div class="form-group">
    <label for="categoria" class="control-label">Categoría</label>
    <input type="text" name="categoria" id="categoria" class="form-control" />
</div>
<div class="form-group">
    <label for="autor" class="control-label">Autor</label>
    <input type="text" name="autor" id="autor" class="form-control" />
</div>
<div class="form-group">
    <label for="votos" class="control-label">Votos</label>
    <input type="number" name="votos" id="votos" class="form-control" />
</div>

<!-- ... -->

```

Los classes y id extras solamente son utilizados por Bootstrap, lo que permitirá que nuestro formulario se vea más lindo :)

Desde el punto de vista de php, lo único importante será el atributo "name" de cada elemento. Puede ser cualquier cosa, pero ésta será la forma en que php accederá a los valores de cada campo.

Además, necesitamos incluir todo el código anterior dentro de la etiqueta html `form`. Debemos setear el atributo `action` para que apunte a nuestra página y no podemos olvidar de incluir el atributo method=POST. 

```
<h1>Agregar Idea</h1>

<form action="/nueva_idea.php" method="POST">
    <!-- el resto del formulario va aqui ... -->
</form>

<!-- ... -->

```

Por último, deberemos agregar un botón para enviar el formulario:

```
<button type="submit" class="btn btn-primary">
    <span class="glyphicon glyphicon-heart"></span> Agregar
</button>

<!-- ... -->

```

Refresquemos la página para ver los cambios!

## Enviando el formulario

Comencemos completando el formulario y presionemos el botón **Agregar**.

Mmmm, no pasó nada! La url es la misma y el formulario está vacío nuevamente. De hecho, algo pasó, pero invisible a nuestros ojos. Abre nuevamente la barra de desarrollador (en el tab Red). Cuando pulsamos "Agregar", nuestro navegador envió una solicitud http al servidor. Además de los campos que vimos anteriormente, podemos visualizar que se enviaron los campos del formulario que completamos!


## Solicitudes GET y POST

Existen dos tipos de request: GET y POST. Las solicitudes de tipo GET son utilizadas en la mayoría de las páginas y las de tipo POST son usadas mayormente para el envío de formularios. La diferencia entre estos dos tipos todavía no es relevante, pero GET se utiliza en general para leer datos (por ejemplo obtener el listado de ideas), y las de tipo POST para enviar datos (como los datos de un formulario). request de tipo GET 
GET and POST Requests

> Tip: en verdad existen otros tipos de solicitudes: PUT, HEAD and DELETE. En general son utilizados para las API web, por lo que no son relevantes por el momento.













