## Trabajando con archivos & JSON

Por el momento nuestro array de ideas está escrito de forma manual y no es dinámico en absoluto. Eventualmente, vamos a traer este array desde una base de datos y permitir a los usuarios agregar nuevas ideas. PEro antes de llegar a esa instancia vamos a pretender que alguien nos brinda un archivo que contiene todas las ideas posibles. Nuestro objetivo será leer ese archivo y transformar su contenido en un array de PHP que sea similar en estructura al array que creamos de forma manual.
 
 Para hacer las cosas más simples, puedes utilizar el archivo ideas.json` que aparece en este directorio.
 
 Puedes abrir el archivo para ver su contenido:

```
[
  {
    "titulo": "Aplicación móvil",
    "descripcion": "Es una aplicación para conectar amigos",
    "categoria": "Mobile",
    "autor": "Juan Carlos",
    "votos": 8
  },
  {
    "titulo": "Pulsera inteligente",
    "descripcion": "Sirve para medir el ritmo cardíaco",
    "categoria": "Accesorios",
    "autor": "Laura Macilla",
    "votos": 3
  },
  {
    "titulo": "Taza que mantiente temperatura",
    "descripcion": "Nunca más tendrás un café frio",
    "categoria": "Accesorios",
    "autor": "Pedro Aster",
    "votos": 5
  },
  {
    "titulo": "Auto inteligente",
    "descripcion": "El primer vehículo que no require de un conductor humano",
    "categoria": "Automotor",
    "autor": "Carla Micón",
    "votos": 9
  }
]
```

Antes de continuar, hablemos un poco sobre JSON, que no tiene nada que ver con PHP, excepto que PHP lo puede leer. JSON es un formato de texto que puede ser utilizado para representar información de forma estructurada, como los detalles de una idea:

```
{
    "titulo": "Auto inteligente",
    "descripcion": "El primer vehículo que no require de un conductor humano",
    "categoria": "Automotor",
    "autor": "Carla Micón",
    "votos": 9
}
```

Cualquier array en PHP tiene su equivalente como una cadena de texto en JSON, y podemos convertir un array PHP en JSON y viceversa. De hecho, existe una función llamada `json_encode` que toma como parámetro un array en PHP y devuelve el string equivalente en JSON. Podemos utilizarla para ver cuál es el resultado pasando como parámetro nuestro array:

```
var_dump(json_encode($ideas));die;
```

Cuando refrescamos la página, podemos ver que el JSON es equivalente a nuestro array, de forma similar a lo que tenemos en ideas.json.

> **TIP:** la visualización en JSON puede ser un tanto confusa. Podemos utilizar el sitio http://www.freeformatter.com/json-formatter.html para visualizar los datos de forma más estructurada. Este formatter no cambia la estructura del string JSON que le pasemos, sino solamente su visualización.

La razón por la que existe JSON es para que diferentes sistemas se puedan comunicar. Imagina si nuestra aplicación guardaría archivos que deban ser envíados e interpretados por otra aplicación totalmente distinta. JSON puede ser leido por cualquier lenguaje como python o javascript. JSON es una forma ideal de compartir datos y es uno de los formatos por defacto que se utiliza en las API modernas. 

Supongamos ahora que existe alguna otra parte de nuestra aplicación que permite que los usuarios agreguen ideas a nuestro archivo ideas.json. Nuestro trabajo será leer el contenido de este archivo para poder mostrar el listado completo.

### Abriendo y leyendo archivos

Para leer el contenido de un archivo podemos utilizar la función file_get_contents (buscar en php.net). Como podemos ver en la documentación, esta función oslamente necesita como parámetro el nombre de un archivo. La misma función se encargará de abrirlo y retornar su contenido como un string.

Probemos su uso y guardemos el resultado en una variable:

```
$ideasJson = file_get_contents('ideas.json');
var_dump($ideasJson);die;
```

Cuando refresquemos la página veremos el contenido del string JSON!.

### Transformar JSON en un array de PHP

Volviendo al objetivo inicial, nuestra idea es poder transformar el string JSON del archivo ideas.json en un array de php. Hasta el momento solamente utilizamos json_encode para transformar un array php en un string JSON. Por lo tanto es razonable que el camino inverso sea utilizando json_decode:

```
$ideasJson = file_get_contents('ideas.json');
$ideas = json_decode($ideasJson);
var_dump($ideas);die;
```

Cuando refrescamos la página, el resultado es muy parecido a lo que necesitamos. Pero en vez de un array vemos algo como "stdClass". Esto es un objeto en PHP, pero por el momento no es necesario comprender de qué se trata. En cambio, si vamos a la documentación de json_decode, podemos ver que existe un segundo parámetro opcional el cual tiene como valor predeterminado false. En cambio, si fuese true, el resultado de la función sería un array asociativo:


```
$ideasJson = file_get_contents('ideas.json');
$ideas = json_decode($ideasJson, true);
var_dump($ideas);die;
```

¡Perfecto! Es igual al array que estuvimos construyendo a mano. Ya podemos integrarlo a nuestro código:


```
<?php

    $ideasJson = file_get_contents('ideas.json');
    $ideas = json_decode($ideasJson, true);
    
    // debemos eliminar las ideas individuales $idea1, $idea2, $idea3
    
    $mensajeBienvenida = 'Bienvenido a un mundo de ideas';
    $ideasCount = count($ideas);
?>
<dv class="container">
    <div class="row">
        <?php 
            foreach($ideas a $idea) {
                echo '<div class="col-md-4">';
                echo '<h2>'. $idea['nombre'] .'</h2>';
                echo '</div>';
            }
        ?>
    </div>
</div>
```

> **NOTA:** la función count() sirve para contar elementos de un array. En el ejemplo anterior estamos asignando a $ideasCount un valor entero que contiene el total de las ideas obtenidas del archivo ideas.json.

Retomando el desafío de la unidad 2, imprimamos todos los atributos de una idea: nombre, descripcion, categoria, autor y votos.


### Guardando a un archivo

¿Qué pasaría si quisieramos guardar datos en un archivo? Si vamos a la documentación de php de file_get_contents, veremos una función relacionada: file_put_contents. Su utilización también es muy simple. Solamente debemos pasarle un string y un nombre de archivo y la propia función se encargará de crear ese archivo con el contenido del string.

### Otras formas de trabajar con archivos

PHP tiene una amplia gama de funciones para trabajar con archivos además de file_get_contents y file_put_contents. Por ejemplo fopen, fread, fwrite and fclose. Por el momento, no hace falta que las utilicemos, salvo que estemos trabajando con archivos muy grandes.