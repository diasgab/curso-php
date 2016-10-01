###Requisitos

- Instalar XAMPP (PHP > 5.5)
- Editor de texto (Notepad++ para Win)

###Setup
1. Descargar código del repositorio: https://github.com/diasgab/curso-php
2. Copiar contenido del proyecto en C://xampp/htdocs/curso-php
3. Ingresar a http://localhost/curso-php/clase1/index.php

##1. Hola Mundo

Para escribir código PHP debemos comenzar siempre con la misma etiqueta: **<\?php**. Esta etiqueta indica que ya no estamos escribiendo código HTML, sino que vamos a escribir código PHP. Empecemos imprimiendo un mensaje con la sentencia ```echo```. Deberás terminar la linea con un punto y coma ; y luego escribe la etiqueta de cierre **?>**. Estos últimos dos caracteres nos sacan del modo PHP y nos devuelven al HTML. El <?php y ?> son exactamente opuestos y siempre se usan a la
par:

```
<!-- index.php -->
...
<div class="jumbotron">
      <div class="container">
        <h1><?php echo "Hola mundo!"; ?></h1>
        ...
      </div>
</div>
...
```

Recarga la página y deberías ver el nuevo texto.

La función de `echo` es imprimir una cadena de texto o string. Los strings se engloban siempre en comillas simples (tmabién se puede hacer con comillas dobles).

**Explicación de Request (ver gráfico):** El cliente inicia la acción de solicitar una página. Se envía el request al servidor. El servidor utiliza el intérprete de php para evaluar el resultado de index.php luego de ejecutar el código php que el mismo contenga. El resultado final será enviado como respuesta al cliente.


## 2. Variables

Antes de comenzar con las variables, cabe aclarar que las etiquetas **<\?php** y **?>** pueden ir en distintas líneas. Como se puede ver, si no imprimimos nada, no habrá ningún cambio en el resultado final. Ni siquiera habrá líneas vacías o espacios en blanco.
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
Para crear una variable, comienza con el signo pesos ($), escribe un nombre significativo, y sigue con el simbolo **=** para asignarle un valor. Utiliza un punto y coma para terminar la sentencia.
```
<?php
    $mensajeBienvenida = 'Bienvenido al resumen de noticias';
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
        $mensajeBienvenida = 'Bienvenido al resumen de noticias';
        
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
        $mensajeBienvenida = 'Bienvenido al resumen de noticias';
        $noticiasCount = 20;
        ?>
        <h1><?php echo $mensajeBienvenida; ?></h1>
        <p>Tienes <?php echo $noticiasCount; ?> para leer</p>
        ...
      </div>
</div>
...
```

### Haciendo enojar a PHP con errores de sintaxis


### Tipos de variables y otras consideraciones

- PHP es un lenguaje que se interpreta en tiempo de ejecución
- No es neceario especificar el tipo de variable.

```
$variable = 'Nombre'; (string)
$variable = 30;
$variable = array();
```

A pesar de no ser recomendado el uso anterior, es una posibilidad que incluye el lenguaje, lo cual lo hace versátil y a su vez dificil de controlar si no se adoptan buenas prácticas al comenzar y mantener un proyecto.

##2. Funciones

Como la mayoría de los lenguajes de programación, PHP tiene funciones, como por ejemplo `rand()`que se utiliza para obtener un número entero aleatorio.

```
<?php
    $mensajeBienvenida = 'Bienvenido al resumen de noticias';
    $noticiasCount = rand();
?>
```
>**NOTA:** Para acceder a documentación de todas las funciones de PHP, puedes hacerlo desde el sitio web oficial [http://php.net](). Para acceder directamente a una función escribe [http://php.net/NOMBRE_FUNCION](), por ejemplo [http://php.net/rand]().

Una función comienza siempre con un nombre seguido de parentesis (de apertura y cierre).

Cuando refresquemos la página veremos un número distinto cada vez.

#### Funciones con argumento

Podemos pasar un valor a la función rand(), como figura en la documentación. Este parámetro es opcional y será 0 en caso que no lo pasemos.
```
<?php
    $mensajeBienvenida = 'Bienvenido al listado de ideas';
    $noticiasCount = rand(50);
?>
```

Probemos también con `rand(50,100)`.

#### Declaración de funciones

Si quisiesemos definir una función que nos permita obtener la cantidad de noticias totales, podríamos definirla de la siguiente manera:

```
<?php
    function getCantidadNoticias() {
        $noticias = rand();
        return $noticias;
    }
    $noticiasCount = getCantidadNoticias();
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

Para iterar sobre el array $ideas, utilizaremos la sentencias `foreach`, como sigue:

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

var_dump($ideas);

### Claves y valores


### Arrays asociativos

$idea1 = array();
$idea1['nombre'] = "Aplicación móvil";
$idea1['descripcion'] = "Aplicación móvil para consultar el clima";