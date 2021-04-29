# Manipular el DOM con jQuery

Además de los selectores, jQuery incluye unas cuentas funciones para **seleccionar** y también **manipular** los elementos:

=== "Filtros"
    ```javascript
    $.not()              // Elementos que no cumplen los criterios
    $.filter()           // filtra o busca una selección de elementos
    $.slice(inicio, fin) // extrae una selección de elementos
    $.find()             // Busca y extrae una selección de elementos
    ```

    Por ejemplo:

    ```javascript
    // aplica borde rojo a los divs que no son verdes ni tienen id=azul
    $('div').not('.verde, #azul').css('border-color', 'red')
    // fondo azul a todos los e. con clase 'div1'
    $('div').filter(".div1").css('background-color', 'blue');
    // selecciona todos los <p> y filtra sólo el tercer párrafo
    $('p').slice(2,3);
    // fondo azul a todos los e. con clase 'div1'
    $('div').find(".div1").css('background-color', 'blue');
    
    ```
=== "Añadir contenido"
    ```javascript
    $.html()    // devuelve o asigna el código html de un elemento
    $.text()    // devuelve o asigna el texto de un elemento html
    $.append()  // añade contenido html al último elemento hijo
    $.prepend()  // añade contenido html como el primer elemento hijo
    $.before()  // añade un elemento fuera y antes del seleccionado
    $.after()  // añade un elemento fuera y después del seleccionado

    /* Ejemplos */
    alert($('#errores').html())
    $('#mensaje').html('<h2>Biblioteca jquery</h2>')
    $('#mensaje h2').text('Biblioteca jquery')

    $('ul').append('<li>item 4</li>')
    $('ul').prepend('<li>item 0</li>')
    $('ul').before('<h3>Lista</h3>')
    $('ul').after('<h3>Otra lista</h3>')
    ```
=== "Eliminar"
    ```javascript
    $.remove()  // elimina un elemento
    $.empty()   // elimina el contenido de un elemento

    /* Ejemplos */
    $('span.error').remove() // elimina todos los span con clase 'error'
    $('span.error').empty()  // elimina el contenido pero deja los elementos
    ```
=== "Atributos"
    ```javascript
    /* Otros atributos */
    $.attr()    // devuelve o asigna un atributo a un elemento
    $.removeAttr()    // elimina un atributo de un elemento

    $('.boton1').attr('value', 'un boton') // asignación
    $('.boton1').removeAttr('value')    // elimina el atributo
    let dato = $('.boton').attr('value') // asigna el valor a una variable
    ```
=== "Value"
    ```javascript
    /* Atributo value */
    $.val()    // devuelve o asigna el value de un elemento

    $(':text:first').val()  // valor del primer input texto
    $(':text').val('Mensaje') // asigna un value a todos los textos
    ```

=== "css"
    ```javascript
    /* CSS */
    $.addClass()    // añade una clase al elemento
    $.removeClass()    // elimina una clase del elemento
    $.toggleClass() // quita o añade una clase al elemento

    $.css() // devuelve o establece directamente las propiedades css

    /* Ejemplos */
    $('div').addClass('visible')
    $('div').removeClass('visible')
    $('div').toggleClass('visible')

    $('body').css('font-size', '200%')

    // varias a la vez
    $('#miCapa').css({
        'background-color': '#FF0000',
        'border': '2px solid #FE0037'
    })
    // guarda el color en una variable
    let bgColor = $('#main').css('background-color')
    ```
=== "Propiedades"
    ```javascript
    $.prop()    // modifica propiedades nativas de JS:
                // readonly, disabled, selected, checked, autofocus...
    $.removeProp()  // elimina una propiedad

    $(selec).prop('disabled');
    $(selec).removeProp('disabled');

    $(selec).prop('checked')    // booleano
    $('#select').prop('selectedIndex')  // devuelve el índice del elemento
    ```
=== "Bucles"
    ```javascript
    // Para ejecutar una acción en bucle sobre un elemento
    $.each()

    $('ol li').each( (indice, elemento) => {
        console.log(
            "El elemento es" + 
            $('elemento').text() +
            " el índice es " + indice
        );
    })
    ```

#### Bucles automáticos

Cuando se aplica una función jQuery a una **selección de elementos** no hace falta generar un bucle; se aplica automáticamente

```javascript
$('.misBotones').hide();
// oculta TODOS los botones con la clase ".misBotones"
```

#### Encadenar funciones

jQuery permite _apilar_ funciones una detrás de otra, que se ejecutarán en sucesión a la selección

```javascript
$('.misBotones').width(300).heigth(300).text('Hola').fadeIn(1000);
//  En este ejemplo se selecciona todos los elementos cuya clase es ‘misBotones’ y automáticamente se le aplican cuatro funciones.

// Otra forma:
$('.misBotones').width(300)
.heigth(300)
.text('Hola')
.fadeIn(1000);
```

