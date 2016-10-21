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

## Vuelta a funciones

Ponemos la lectura del archivo en un función

## Include/require

Empezamos a organizar el código

