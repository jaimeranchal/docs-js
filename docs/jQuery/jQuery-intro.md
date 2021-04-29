# jQuery

JQuery es una librería JavaScript que simplifica la forma de programar: _escribe menos, haz más_. Para conseguirlo proporciona métodos muy simples para ejecutar lo que en JS serían bastantes líneas de código.

Es especialmente útil para manejar **llamadas AJAX** y **manipular el DOM**. De forma general, permite:

- Manipular el DOM/HTML
- Manipular CSS
- Métodos para eventos HTML
- Efectos y animaciones
- AJAX
- Utilidades

También se puede amplicar su funcionalidad con **plugins**.

## Añadir jQuery a tu página

=== "Descarga"
    Hay dos **versiones** disponibles desde [jQuery.com](http://jquery.com/download/):

    - _Producción_: minimizada y comprimida; la recomendada.
    - _Desarrollo_: para pruebas y desarrollo (descomprimida, para poder leer el código)

    Una vez descargada, sólo hay que añadir la referencia:

    ```html
    <head>
        <script scr="./jquery-3.5.1.min.js"></script>
    </head>
    ```
=== "Enlace"
    Desde un CDN (_Content Delivery Network_), siempre y cuando no esté caído:

    ```html
    <head>
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
    </head>
    ```

    Probablemente esta última opción sea más **rápida**; mucha gente ya tiene descargada la librería por haber visitado otras páginas web.

## Sintaxis

El mecanismo básico es **seleccionar** (_query_) elementos HTML para realizar **acciones** sobre ellos:

- `$` define y da acceso a jQuery
- `selector`: cadena de búsqueda de elementos
- `action()`: el método que queremos ejecutar

```javascript
$(selector).accion();

$(this).hide()    // oculta el elemento actual
$("p").hide()     // oculta todos los elementos `p`
$(".test").hide() // oculta todos los elementos con la clase `test`
$("#test").hide() // oculta todos los elementos con la id `test`
```

### El evento _Document Ready_

Para impedir que el código jQuery se ejecute _antes_ de que el documento termine de cargarse, los métodos se insertan dentro de una función:

=== "Completa"
    ```javascript
    $(document).ready(function(){

      // ...

    });
    ```
=== "Reducida"
    ```javascript
    $(function(){

      // ...

    });
    ```
=== "Mínima"
    ```javascript
    $((){

        // ...

    })
    ```

### Selectores

Sirven para encontrar elementos HTML. 

- Se pueden usar todos los **selectores CSS**, más alguno particular de jQuery.
- Todos los selectores empiezan con el **signo del dólar** y los **paréntesis** `$()`

=== "css"
    ```javascript
    $('*')        // todos los elementos
    $('p')        // todos los <p>
    $('p', 'a')   // todos los <p> y todos los <a>
    $('p a')      // todos los <a> hijos de <p>
    $('li.clase') // todos los <li> con la clase indicada
    $('li>p')     // todos los <p> hijos directos de <li>
    $('h1+p')     // todos los <p> inmediatamente por un <h1> hermano
    $('p:has(b)') // todos los <p> que contienen un <b>
    $('.clase')   // todos los elementos con la clase x
    $('#id')      // todos los elementos con esa id
    $('p:empty')  // todos los <p> vacíos

    /* Atributos */

    $('img[alt]') // todos los <img> con atributo "alt"
    $(':button[id*=boton]') // todos los <button> cuyo "id" sea 'boton'
    $('a[href$=.pdf]') // todos los <a> cuyo "href" acabe en 'pdf'
    $('a[title^=.lr]') // todos los <a> cuyo "title" empiece por '.lr'
    ```
=== "jquery"
    ```javascript
    /* Posición */
    $('p:first')            // primer <p>
    $('p:last')             // último <p>
    $('li:first-child')     // todos los <li> primeros hijos
    $('li:only-child')      // todos los <li> hijos únicos
    $('li:nth-child(3)')    // todos los <li> terceros hijos
    $('tr:nth-child(odd)')  // todos los <tr> impares
    $('tr:nth-child(even)') // todos los <tr> pares
    $('p:odd')              // <p> impares
    $('p:eq(1)')            // segundo <p> (asumiendo que el primero es 0)
    $('p:gt(1)')            // todos los <p> a partir de la 2 posicion
    $('p:lt(1)')            // todos los <p> antes de las 2 posicion

    /* Contenido */
    $('p:contains(texto)')  // todos los <p> con 'texto'
    ```
=== "formulario"
    ```javascript
    $('input') // todos los input
    ```

    Como buscar _inputs_ es algo que se hace a menudo, jQuery incluye una notación especial reducida para seleccionar tipos de inputs:

    ```javascript
    /* Selecciona todos los input con el atributo indicado tras los dos puntos */
    $(':text')
    $(':checkbox')
    $(':button')
    
    /* Selecciona inputs por su estado */
    $(':enabled') // todos los elementos activados
    $(':disabled') // todos los elementos desactivados
    $(':checked') // ¿está seleccionado? (radiobutton + checkbox)
        $('objeto').is(':checked') //booleano
        $(':radio:checked').val() // valor del radio seleccionado
    $(':selected') // ¿está seleccionado? (option)
        $('select option:selected') // elementos selecc.
        $('select option:selected').text() // valor de la opción selecc.
        $('select option:selected').prop("value") // valor
    ```
