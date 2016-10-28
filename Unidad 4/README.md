## Estructura de control if

Comencemos a hacer nuestro código más inteligente. Modifica el archivo ideas.json y elimina la clave "votos" solamente de la primer idea. Cuando refresquemos la página, veremos un error de php similar al siguiente:

```
Undefined index: votos in /path/to/index.php on line 95
```

Imprimamos la variable $idea dentro del bucle foreach para ver qué está sucediendo

```
<?php foreach ($ideas as $idea) { ?>
    <?php var_dump($idea); ?>
    ...
<?php } ?>
```

Como veremos, cada idea es un array asociativo. Pero la idea "Aplicación móvil" no cuenta con el atributo votos. Cada vez que una referencia a una clave de un array no existe, PHP emitirá un mensaje de error. Por lo tanto, si sabemos que existe la posibilidad de que la clave "votos" no esté definida, deberíamos chequearlo antes e imprimirla solo en caso que exista.

Como en la mayoría de los lenguajes, la sentencia if tiene la siguiente forma:
```
if (expresión)
  sentencia
```

Particularmente en PHP lo podemos utilizar como sigue:

```
<?php 
    foreach($ideas a $idea) {
        echo '<div class="col-md-4">';
        echo '<h2>'. $idea['nombre'] .'</h2>';`
        if (true) {
            echo '<p>'. $idea['votos'] .'</p>';
        }
        echo '</div>';
    }
?>
```

En el ejemplo anterior estamos utilizando un valor boolean true directamente como condición, por lo que siempre va a ingresar al bloque de código inmediatamente inferior (contenido entre {}).

Para chequear si una clave está definida en un array podemos utilizar la función `array_key_exists`. El primer argumento es la clave, el segundo el array a chequear y el resultado es un booleano. 

```
<?php 
    foreach($ideas a $idea) {
        echo '<div class="col-md-4">';
        echo '<h2>'. $idea['nombre'] .'</h2>';`
        if (array_key_exists('votos', $idea)) {
            echo '<p>'. $idea['votos'] .'</p>';
        }
        echo '</div>';
    }
?>
```

### If-else

En vez de dejar de imprimir el valor de votos en caso que no se encuentre definido, probemos de imprimir el string "Indefinido" en caso que no exista esta clave:

```
if (array_key_exists('votos', $idea)) {
    echo '<p>'. $idea['votos'] .'</p>';
} else {
    echo '<p>Indefinido</p>';
}
```

### Combinando condiciones If

Supongamos que las ideas se clasifican como "Interesante" o "Irrelevante" en función de la cantidad de votos. Si la cantidad de votos es mayor o igual a 6, la idea será clasificada como "Interesante". En caso que los votos sean menos de 6 será cladificada como "Irrelevante".
 
 ```
 if (array_key_exists('votos', $idea)) {
    if ($idea['votos'] >= 6) {
        echo '<p>'. $idea['votos'] .' (Interesante)</p>';
    } else {
     echo '<p>'. $idea['votos'] .' (Irrelevante)</p>';
    }
 } else {
     echo '<p>Indefinido</p>';
 }
 ```

### Operadores de comparación

Los operadores se pueden utilizar en una expresión dentro de la sentencia if.

```
$a == $b            Chequea igualdad luego de la conversión de tipos
$a === $b           Chequea igualdad incluyendo el tipo de datos
$a != $b o $a <> $b Chequea si $a es distinto de $b
$a > $b
$a >= $b
$a < $b
$a <= $b
```

### Operadores lógicos

```
&& and
|| or
```

## Reorganizando nuestro código

En todos los ejercicios llevados a cabo hasta el momento, estuvimos mezclando php con html. No es una buena práctica que la lógica de nuestra aplicación se mezcle con etiquetas html ya que ocasiona que nuestro código sea difícil de mantener. Vamos a reorganizar un poco nuestro código para evitar este inconveniente a futuro.

## Vuelta a funciones

 En la sección anterior nos ocupamos de cargar un array con información procedente de un archivo json. Como ya mencionamos la idea es que a futuro podamos traer esa información desde una base de datos. Lo que pretendemos es encapsular la obtención de esta información (en nuestro caso de las _ideas_).

```
$ideasJson = file_get_contents('../recursos/ideas.json');
$ideas = json_decode($ideasJson);
```

Queremos que la variable $ideas se cargue con los datos procedentes de una función, en donde encapsularemos la lectura del archivo. Creemos entonces una función que simplemente nos devuelva un array de $ideas:

```
function getIdeas() 
{
    $ideasJson = file_get_contents('../recursos/ideas.json');
    return json_decode($ideasJson);
}
```

La sentencia `return` permite especificar qué variable retorna la función. Una función puede retornar cualquier tipo de dato de php, como integers, string, arrays, boolean, etc
 
Para almacenar el valor devuelto por esta función en nuestra variable $ideas, usamos la siguiente asignación:

```
$ideas = getIdeas();
```

**Consigna:** para mejorar la estructura de nuestro archivo, movamos los componentes que implican lógica o asignación de variables a la parte superior del archivo. En el código html solamente deberían quedar la impresión de variables existentes y estructuras de control como if y foreach.

## Uso de require para la inclusión de funciones

Movamos la creación de nuestra función a un archivo en el que guardaremos todas las futuras funciones. Creemos el archivo lib/funciones.php y movamos la función getIdeas().
 
 Luego en nuestro código incluimos el archivo:
 
```
<?php
 
 require 'lib/funciones.php';
 
 // sigue código php...
 
```

Las sentencia require le indica a php que cargue y parsee el código de un archivo en particular.

Existen otras sentencias similares que se utilizan para lograr una funcionalidad similar: require; require_once; include; include_once
