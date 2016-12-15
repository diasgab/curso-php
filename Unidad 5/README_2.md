## Leyendo datos de una solicitud web

Para acceder desde PHP a los datos enviados con el formulario utilizaremos la variable global $_POST. Veamos qué contenido tiene:

````
<?php var_dump($_POST); ?>
````

Agrega este código al comienzo del script php, completa el formulario nuevamente y envíalo. Podremos ver claramente cómo se imprime un array asociativo con los valores de la variable $_POST.

## ¿De dónde proviene la variable $_POST? ##

Anteriormente vimos que si tratamos de referenciar a variables que no existen, PHP lanzará un mesaje de error notificando el inconveniente:

````
<?php var_dump($_POST); ?>
<?php var_dump($variablePrueba); ?>
````

Si probamos el código anterior obtendremos un mensaje de advertencia de php.

El secreto es: $_POST es una de las llamadas variables globales. Estas variables están siempre definidas y disponibles para ser utilzadas en nuestros script PHP como cualquier variable regular que definamos.
 
 Otras variables globales incluyen $_GET, $_SERVER y algunas otras. Más tarde volveremos sobre estas variables, pero lo que todas tienen en común es que estas variables globales nos brindan información sobre las solicitudes HTTP enviadas por el navegador.

## Obteniendo las variables del formualrio ##

Eventualmente guardaremos esta nueva idea en algún lugar, como una base de datos. Per por el momento, asignemos cada parámetro que recibimos a una variable e imprimamos el resultado para probar el funcionamiento. Pondremos este código al inicio de nuestro script, donde incluiremos toda la lógica de php:


````
<?php
$titulo = $_POST['titulo'];
$descripcion = $_POST['descripcion'];
$categoria = $_POST['categoria'];
$autor = $_POST['autor'];
$votos = $_POST['votos'];

var_dump($titulo, $descripcion, $categoria, $autor, $votos);die;
?>
````

Como podemos ver, la función var_dump acepta un número ilimitado de parámetros. En general las funciones de php aceptan 0, 1, 2 o más argumentos. Pero no son muchas las funcioanes que aceptan un número indefinido de parámetros como lo es var_dump.


## Comportamiento de $_POST ante solicitudes GET ##

Si recargamos la página sin enviar el formualrio nuevamente (posicionandonos en la barra de navegación y pulsando Enter) veremos mensajes de error indicando que las variables que usamos de $_POST no están definidas. 

Para solucionar este inconveniente podemos utilizar una función que ya vimos con anterioridad (array_key_exists()) de forma que nos aseguremos que al utilizar una variable ésta realmente exista.

````
<?php
if (array_key_exists('titulo', $_POST)) {
    $titulo = $_POST['titulo'];
} else {
    $titulo = 'Una idea sin un título';
}
````

Podemos utilizar una variante muy similar llamada isset(). 

````
<?php
if (isset($_POST['titulo'])) {
    $titulo = $_POST['titulo'];
} else {
    $titulo = '';
}
````

Repite este bloque para todas las variables:


````
<?php
if (isset($_POST['descripcion'])) {
    $descripcion = $_POST['descripcion'];
} else {
    $descripcion = '';
}

if (isset($_POST['categoria'])) {
    $categoria = $_POST['categoria'];
} else {
    $categoria = '';
}

if (isset($_POST['autor'])) {
    $autor = $_POST['autor'];
} else {
    $autor = '';
}

if (isset($_POST['votos'])) {
    $votos = $_POST['votos'];
} else {
    $votos = '';
}

var_dump($titulo, $descripcion, $categoria, $autor, $votos);die;
````

Si refrescamos la página veremos que todos los mensajes de error desaparecen. El código funciona, pero lo deseable es que seamos un poco más inteligentes. Cuando hacemos una solicitud GET, no queremos estar analizando todas las variables de POST (ya que estará vacía), sino que solamente hay que imprimir el formulario. Solamente queremos ejecutar toda la lógica cuando realmente enviemos un solicitud POST.

## Detectando solicitudes POST y GET ##

La respuesta está en otra de las variables globales que mencionamos anteriormente: $_SERVER.

Imprimamos esta variable par aver su contenido:

````
<?php
var_dump($_SERVER);die;
````

La información que veremos es sobre la solicitud HTTP que acabamos de enviar. Por ejemplo HTTP_USER_AGENT. Esta información proviene de los encabezados de incluye el navegador cuando envía una petición.

También hay una clave que se llama REQUEST_METHOD. ¡Esta es la información que estabamos buscando!
See that REQUEST_METHOD key? Ah ha! That’s the HTTP method, which is GET right now.

Ahora podemos simplemente utilizar una sentencia IF para chequear si la solicitud enviada es POST o GET.

````
<?php
if ($_SERVER['REQUEST_METHOD'] == 'POST') {

    // ...

    var_dump($titulo, $descripcion, $categoria, $autor, $votos);die;
}
````

## Guardando ideas ##

De alguna forma queremos guardar las ideas que vayamos creando. Todavía no hablamos de base de datos, pero sí trabajamos con archivos json. Y este tipo de archivos es fácil de actualizar y leer. Sería como la función básica de una báse de datos. Así que si podemos encontrar la forma de actualizar nuestro archivo ideas.json, ya estaremos listos para seguir adelante.

En primer lugar, podemos reutilizar la función get_ideas para obtener un array con todas las ideas existentes. 

````
<?php
if ($_SERVER['REQUEST_METHOD'] == 'POST') {

    // ...
    $ideas = get_ideas();
    var_dump($titulo, $descripcion, $categoria, $autor, $votos);die;
}
````

Luego, tendremos que crear un array asociativo que represente una nueva idea a ser agregada. Debemos asegurarnos de utilizar las mismas claves que están definidas en el archivo json. 

````
<?php
if ($_SERVER['REQUEST_METHOD'] == 'POST') {

    // ...
    $ideas = get_ideas();
    
    $nuevaIdea = array(
        'titulo' => $titulo,
        'descripcion' => $descripcion,
        'categoria' => $categoria,
        'autor' => $autor,
        'votos' => $votos,
    );
    var_dump($titulo, $descripcion, $categoria, $autor, $votos);die;
}
````

Bien! Ahora debemos agregar esta nueva idea al array de $ideas.

````
<?php
if ($_SERVER['REQUEST_METHOD'] == 'POST') {

    // ...
    $ideas = get_ideas();
    
    $nuevaIdea = array(
        'titulo' => $titulo,
        'descripcion' => $descripcion,
        'categoria' => $categoria,
        'autor' => $autor,
        'votos' => $votos,
    );
    
    $ideas[] = $nuevaIdea;
    
    var_dump($titulo, $descripcion, $categoria, $autor, $votos);die;
}
````

Recuerda que los corchetes vacíos le dicen a PHP que queremos agregar un elemento en el array de $ideas, sin importar la clave que ocupe en dicho array. PHP eligirá una clave automáticamente al asignar este nuevo elemento.

## Guardando al archivo ideas.json ##
 
Hasta el momento, le array $ideas tendrá todas las ideas existentes y además nuestra nueva idea recién creada. Basicamente representa lo que deseamos guardar en nuestro archivo ideas.json.
 
 Primero deberemos transformar nuestro array $ideas en una cadena json utilizando la función json_encode. Luego utilizaremos la función file_put_contents() para guardar dicho archivo:
 
 ````
 <?php
 ...
 $ideas[] = $nuevaIdea;
  $json = json_encode($ideas);
  file_put_contents('ideas.json', $json);
 ````
 
 
 Refresquemos la página y veremos si funciona. Deberemos volver a nuestro listado inicial de ideas para ver si se guardó correctamente la idea que agregamos.
