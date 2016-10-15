###Requisitos

- Completar Unidad 1

## Variables

Las etiquetas `<?php` y `?>` pueden ir en distintas líneas. Como se puede ver, si no imprimimos nada, no habrá ningún cambio en el resultado final. Ni siquiera habrá líneas vacías o espacios en blanco.
```
<!-- index.php -->
...
<div class="jumbotron">
      <div class="container">
        <?php
        
        
        ?>
        <h1><?php echo "Hola mundo!"; ?></h1>
        ...
      </div>
</div>
...
```
Para crear una variable, comienza con el signo pesos ($), escribe un nombre significativo, y sigue con el simbolo `=` para asignarle un valor. Utiliza un punto y coma para terminar la sentencia. En el siguiente ejemplo se crea una variable $mensajeBienvenida de tipo string.
```
<?php
    $mensajeBienvenida = 'Bienvenido a un mundo de ideas';
?>
```

Si refrescamos la página no veremos ningún cambio, lo cual tiene sentido ya que no imprimimos nada desde PHP. Solamente estamos definiendo una variable pero no la estamos utilizando.

Reemplaza el string de `echo` con la nueva variable.

```
<!-- index.php -->
...
<div class="jumbotron">
      <div class="container">
        <?php
        $mensajeBienvenida = 'Bienvenido a un mundo de ideas';
        
        ?>
        <h1><?php echo $mensajeBienvenida; ?></h1>
        ...
      </div>
</div>
...
```

Refresca la página para ver el resultado final.
Nota: se puede abrir y cerrar la etiqueta php cuantas veces queramos.

### Desafío

- Prueba mover la asignación de la variable $mensajeBienvenida al inicio del documento, antes de la etiqueta `<!DOCTYPE html>`. ¿Notas algún cambio al refrescar la página?
- ¿Qué pasa si mueves ese fragmento al final, debajo de la etiqueta `</html>`?

### Tipos de variables

PHP es un lenguaje que se interpreta en tiempo de ejecución y no es necesario especificar el tipo de variable. El lenguaje permite que se pueda utilizar la misma variable para asignar diferentes valores de distintos tipos de datos. En el siguiente ejemplo vemos cómo a medida que `$variable` toma distintos valores también se modifica el tipo de dato de la misma, el cual se indica entre paréntesis.

```
$variable = 'Nombre'; (string)
$variable = 30; (int)
$variable = 5.13; (float)
$variable = array(); (array)
$variable = true; (boolen)
$variable = new stdClass(); (object)
```

El ejemplo no es de uso recomendado, y solamente fue utilizado para denotar la versatilidad del lenguaje. Esta característica puede ocasionar grandes dolores de cabeza si no se utiliza a conciencia.

> **NOTA:** Para ver todos los tipos de variable soportador por PHP acceder a []()http://php.net/manual/es/language.types.php 

### Juguemos un poco más

Agreguemos a nuestro ejemplo anterior una variable numérica para ver si utilización:

```
<!-- index.php -->
...
<div class="jumbotron">
      <div class="container">
        <?php
        $mensajeBienvenida = 'Bienvenido a un mundo de ideas';
        $ideasCount = 20;
        ?>
        <h1><?php echo $mensajeBienvenida; ?></h1>
        <p>Tienes <?php echo $ideasCount; ?> ideas para inspirarte</p>
        ...
      </div>
</div>
...
```

### Haciendo enojar a PHP con errores de sintaxis

```
<?php   
    $mensajeBienvenida = 'Bienvenido a un mundo de ideas'
    $ideasCount = 20;
?>
```

##2. Uso de funciones

Como la mayoría de los lenguajes de programación, PHP tiene funciones, como por ejemplo `rand()` que se utiliza para obtener un número entero aleatorio.

```
<?php
    $mensajeBienvenida = 'Bienvenido a un mundo de ideas';
    $ideasCount = rand();
?>
```
>**TIP:** Para acceder a documentación de todas las funciones de PHP, puedes hacerlo desde el sitio web oficial [http://php.net](). Para acceder directamente a una función escribe [http://php.net/NOMBRE_FUNCION](), por ejemplo [http://php.net/rand]().

Una función comienza siempre con un nombre seguido de parentesis (de apertura y cierre).

Cuando refresquemos la página veremos un número distinto cada vez.

#### Pasando argumentos

Podemos pasar un valor a la función `rand()`, como figura en la documentación. Este parámetro es opcional y será 0 en caso que no lo pasemos.
```
<?php
    $mensajeBienvenida = 'Bienvenido a un mundo de ideas';
    $ideasCount = rand(50);
?>
```

Probemos también con `rand(50,100)`.

#### Declaración de funciones

Si quisieramos definir una función que nos permita obtener la cantidad de ideas totales, podríamos definirla de la siguiente manera:

```
<?php
    function getIdeasCount() {
        return rand();
    }
    $ideasCount = getIdeasCount();
?>
```

##3. Arrays y bucles

Un array en PHP es un mapa ordenado. Un mapa es un tipo de datos que asocia valores con claves. Este tipo se optimiza para varios usos diferentes; se puede emplear como un array, lista (vector), diccionario, colección, pila, cola y posiblemente más. Ya que los valores de un array pueden ser otros arrays, también son posibles árboles y arrays multidimensionales.

Vamos a imprimir las 3 columnas con información con php en vez de html.

Preparemos el terreno de la siguiente forma en donde utilizaremos un array para definir los títulos de los encabezados. 
```
<?php
    $idea1 = 'Aplicación móvil';
    $idea2 = 'Pulsera inteligente';
    $idea3 = 'Taza que mantiente temperatura';
?>

<div class="container">
    <div class="row">
        <div class="col-md-4">
            <h2><?php echo $idea1; ?> </h2>
        </div>
        <div class="col-md-4">
            <h2><?php echo $idea2; ?> </h2>
        </div>
        <div class="col-md-4">
            <h2><?php echo $idea3; ?> </h2>
        </div>
    </div>
</div>
```

Para definir un array se hace de la siguiente manera:

```
<?php
    $idea1 = 'Aplicación móvil';
    $idea2 = 'Pulsera inteligente';
    $idea3 = 'Taza que mantiente temperatura';
    
    $ideas = array($idea1, $idea2, $idea3);
?>
```

> A partir de PHP 5.4 se puede utilizar la notación `[]`.

### Iterando el array

Para iterar sobre el array `$ideas`, utilizaremos la sentencias `foreach`, como sigue:

```
<?php
    $idea1 = 'Aplicación móvil';
    $idea2 = 'Pulsera inteligente';
    $idea3 = 'Taza que mantiente temperatura';
    
    $ideas = array($idea1, $idea2, $idea3);
?>
<div class="container">
    <div class="row">
        <?php 
            foreach($ideas as $idea) {
                echo '<div class="col-md-4">';
                echo '<h2>'. $idea .'</h2>';
                echo '</div>';
            }
        ?>
    </div>
</div>
```
> **NOTA:** para concatenar cadenas de texto se utilza "." entre ambas cadenas. Ejemplo: `$saludo = "Hola ". $nombre;` donde $nombre es una variable de tipo string.
 
La función de foreach es copiar cada elemento del array `$ideas` en la variable `$idea`. Se comienza siempre desde el primer elemento del array hasta llegar al último. Es decir que en el ejemplo anterior el bloque contenido dentro de foreach se ejecutará 3 veces. 

### Accediendo a items específicos del array

Para visualizar la estructura de un array podemos utilizar la función `var_dump()`. Otra alternativa que no incluye los tipos de datos es la función `print_r()`.
```
<?php
var_dump($ideas);
?>
```

> **TIP:** puedes utilizar la etiqueta html `<pre>` para visualizar de forma más clara el resultado de var_dump(). Ejemplo: `<pre><?php var_dump($array); ?></pre>` 

El ejemplo anterior mostrará como resultado lo siguiente:

```
array (size=3)
  0 => string 'Aplicación móvil' (length=18)
  1 => string 'Pulsera inteligente' (length=19)
  2 => string 'Taza que mantiente temperatura' (length=30)
```

### Claves y valores

En el ejemplo anterior trabajamos con la definición de un array simple. Sin embargo cuando imprimimos su contenido utilizando `var_dump()`, podemos ver claramente que la estructura del array es asociativa. Los arrays se componen de claves y valores. Para la clave `0` el valor es el string "Aplicación móvil".

Las claves de un array pueden ser un integer o un string. El valor puede ser de cualquier tipo.

Así por ejemplo podemos definir el siguiente $array:

```
<?php
$array = array(
    "foo" => "bar",
    "bar" => "foo",
    1 => "test"
    "test" => 23
    54 => 123
);
```

¿Imprime la estructura del array anterior y observa qué sucede?

Puedes también acceder a un elemento específico del array

```
<?php
echo $array[1]; //imprime "test" 
echo $array["bar"]; // ¿Qué imprime? 
?>
```

### Agregar y borrar items de un array indexado

Para agregar un item a un array creado se debe utilizar la siguiente forma:

```
$idea = array(
    'nombre' => 'Aplicación móvil',
    'descripcion' => 'Es una aplicación para conectar amigos',
);

$idea['autor] => 'Juan Perez';
``` 

Lo que sucede es que asignamos a la clave 'autor' dentro del array $idea el valor 'Juan Perez'. Podemos utilizar `var_dump($idea)` para ver la estructura final.

Para eliminar un elemento de un array se utiliza la función unset() de la siguiente forma:

`unset($idea['autor'])`

Es decir, se indica la clave del array que se desea eliminar

### Agregar elementos a un array

Además de utilizar una clave en particular para agregar un elemento a un array, también podemos agregar elementos de forma de agregar un elemento utilizando una clave en particular, también lo podemos hacer como sigue:

```
$idea1 = 'Aplicación móvil';
$idea2 = 'Pulsera inteligente';
$idea3 = 'Taza que mantiente temperatura';

$ideas = array($idea1, $idea2, $idea3);

$ideas[] = 'Ascensor intergaláctico';
```

Con la utilización de los corchetes [] estamos indicandole a PHP que se encargue de asignar una clave automáticamente al agregar el nuevo elemento.

### Arrays multidimensionales

Además del título de la idea agreguemos una pequeña descripción a cada bloque.

```
$idea1 = ['titulo' => 'Aplicación móvil', 'descripcion' => 'Es una aplicación para conectar amigos'];
$idea2 = ['titulo' => 'Pulsera inteligente', 'descripcion' => 'Sirve para medir el ritmo cardíaco'];
$idea3 = ['titulo' => 'Taza que mantiente temperatura', 'descripcion' => 'Nunca más tendrás un café frio'];

$ideas = [$idea1, $idea2, $idea3];
```

#### Desafío

Con la ayuda de los conceptos presentados y la documentación de arrays de PHP []()http://php.net/manual/es/language.types.array.php utilza la definición anterior para imprimir debajo de cada encabezado una descripción de la idea.
