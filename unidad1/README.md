###Requisitos

- Instalar XAMPP (PHP > 5.5)
- Editor de texto (Notepad++ para Win)

###Setup
1. Descargar código del repositorio: https://github.com/diasgab/curso-php
2. Copiar contenido del proyecto en C://xampp/htdocs/curso-php
3. Ingresar a http://localhost/curso-php/clase1/index.php

##1. Hola Mundo

Para escribir código PHP debemos comenzar siempre con la misma etiqueta: `<?php`. Esta etiqueta indica que ya no estamos escribiendo código HTML, sino que vamos a escribir código PHP. Empecemos imprimiendo un mensaje con la sentencia `echo`. Deberás terminar la linea con un punto y coma `;` y luego escribir la etiqueta de cierre `?>`. Estos últimos dos caracteres nos sacan del modo PHP y nos devuelven al HTML. El `<?php` y `?>` son exactamente opuestos y siempre se usan a la
par:

```
<!-- index.php -->
...
<div class="jumbotron">
      <div class="container">
        <h1><?php echo 'Hola mundo!'; ?></h1>
        ...
      </div>
</div>
...
```

Recarga la página y veras el nuevo texto.

La función de la sentencia `echo` es imprimir una cadena de texto o string. Los strings se engloban siempre en comillas simples (también se puede hacer con comillas dobles).

**Explicación de web pretición web:** El cliente inicia la acción de solicitar una página. Se envía el request al servidor. El servidor utiliza el intérprete de php para evaluar el resultado de index.php luego de ejecutar el código php contenido en el mismo. El resultado final será enviado como respuesta al cliente (ningún código PHP será incluido en la respuesta). Es decir, solamente se envía texto como respuesta.