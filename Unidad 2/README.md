###Requisitos

- Completar Unidad 1

## 2. Variables

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
Para crear una variable, comienza con el signo pesos ($), escribe un nombre significativo, y sigue con el simbolo `=` para asignarle un valor. Utiliza un punto y coma para terminar la sentencia.
```
<?php
    $mensajeBienvenida = 'Bienvenido a un mundo de ideas';
?>
```

Si refrescamos la página no veremos ningún cambio, lo cual tiene sentido ya que no imprimimos nada desde PHP.

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

### Variables enteras

Las variables pueden ser numéricas también, para lo cual no se require ninguna comilla.

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
        <p>Tienes <?php echo $ideasCount; ?> para inspirarte</p>
        ...
      </div>
</div>
...
```

> **NOTA:** Para ver todos los tipos de variable soportador por PHP acceder a []()http://php.net/manual/es/language.types.php 

### Haciendo enojar a PHP con errores de sintaxis

```
<?php   
    $mensajeBienvenida = 'Bienvenido a un mundo de ideas'
    $ideasCount = 20;
?>
```

### Tipos de variables y otras consideraciones

PHP es un lenguaje que se interpreta en tiempo de ejecución y no es neceario especificar el tipo de variable. Por lo tanto en teoría se puede utilizar la misma variable y a medida que se realice una nueva asignación se no solo cambiará el valor sino el tipo.

```
$variable = 'Nombre'; (string)
$variable = 30;
$variable = array();
$variable = true;
```

A pesar de no ser recomendado el uso anterior, es una posibilidad que incluye el lenguaje, lo cual lo hace versátil y a su vez dificil de controlar si no se adoptan buenas prácticas al comenzar y mantener un proyecto. Por esta simple razón se recomienda la utilización de un framework (ej. symfony) que brinda una estructura base para nuestra aplicación.

##2. Funciones

Como la mayoría de los lenguajes de programación, PHP tiene funciones, como por ejemplo `rand()` que se utiliza para obtener un número entero aleatorio.

```
<?php
    $mensajeBienvenida = 'Bienvenido a un mundo de ideas';
    $ideasCount = rand();
?>
```
>**NOTA:** Para acceder a documentación de todas las funciones de PHP, puedes hacerlo desde el sitio web oficial [http://php.net](). Para acceder directamente a una función escribe [http://php.net/NOMBRE_FUNCION](), por ejemplo [http://php.net/rand]().

Una función comienza siempre con un nombre seguido de parentesis (de apertura y cierre).

Cuando refresquemos la página veremos un número distinto cada vez.

#### Funciones con argumento

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

Antes de crear un array partamos de la siguiente situación, en donde tenemos 3 variables creadas que utilizaremos como títulos en vez de los encabezados. 
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
        <?php foreach($ideas a $idea): ?>
        <div class="col-md-4">
            <h2><?php echo $idea; ?> </h2>
        </div>
        <?php endforeach; ?>
    </div>
</div>
```

### Accediendo a items específicos del array

Para visualizar la estructura de un array podemos utilizar la función `var_dump`. Otra alternativa que no incluye los tipos de datos es la función `print_r()`.
```
<?php
var_dump($ideas);
?>
```
### Claves y valores

Para acceder a un elemento específico de un array:

```
<?php
echo $ideas[0];
?>
```