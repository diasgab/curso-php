**Requisitos**

- Instalar XAMPP (PHP > 5.5)
- Editor de texto (Notepad++ para Win)

**Setup**
1. Descargar código del repositorio: https://github.com/diasgab/curso-php
2. Copiar contenido del proyecto en C://xampp/htdocs/curso-php
3. Ingresar a http://localhost/curso-php/clase1/index.php

**Hola Mundo**

Para escribir código PHP debemos comenzar siempre con la misma etiqueta: ```<?php```. Esta etiqueta indica que ya no estamos escribiendo código HTML, sino que vamos a escribir código PHP. Empecemos imprimiendo un mensaje con la sentencia ```echo```. Deberás terminar la linea con un punto y coma ; y luego escribe la etiqueta de cierre ?>. Estos últimos dos caracteres nos sacan del modo PHP y nos devuelven al HTML. El <?php y ?> son exactamente opuestos y siempre se usan a la
par:


Before you write PHP code, you’ll always start with the same opening tag: <?php. This is what tells PHP that we’re not writing HTML anymore - we actually want to write some PHP code. Let’s print out a cool message by using the echo statement and surrounding our message with single quotes. Finish off the line with a semicolon and then write the PHP closing tag: ?>. These last two characters get us out of PHP mode and back into HTML. The <?php and ?> tags are exact opposites and always come in a pair. One gets us into PHP mode and the other exits PHP mode:


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


