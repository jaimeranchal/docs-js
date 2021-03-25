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

=== "Document.ready"
    ```javascript
    $(document).ready(function(){

      // métodos jQuery 

    });
    ```
=== "Mínimo"
    ```javascript
    $(function(){

      // métodos jQuery 

    });
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
    $('img[alt]') // todos los <img> con atributo "alt"
    $(':button[id*=boton]') // todos los <button> cuyo "id" sea 'boton'
    $('a[href$=.pdf]') // todos los <a> cuyo "href" acabe en 'pdf'
    $('a[title^=.lr]') // todos los <a> cuyo "title" empiece por '.lr'
    ```
=== "jquery"
    ```javascript
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
    $('p:contains(texto)')  // todos los <p> con 'texto'
    ```
=== "formulario"
    ```javascript
    $('input') // todos los input
    // todos los input con el atributo indicado tras los dos puntos
    $(':text')
    $(':checkbox')
    $(':button')
    ...
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

### Funciones

=== "Filtros"
    ```javascript
    $.not()              // Elementos que no cumplen los criterios
    $.filter()           // filtra o busca una selección de elementos
    $.slice(inicio, fin) // extrae una selección de elementos
    $.find()             // Busca y extrae una selección de elementos
    ```
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
=== "Eliminar"
=== "Atributos"
=== "Atributos"
=== "css"
=== "Bucles"

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

### Eventos

jQuery crea sus propios **métodos** para los eventos del DOM

```javascript
$("p").click(); // asigna un evento 'click' a un párrafo

$("p").click(){
    // acción a realizar cuando hagas click en el párrafo
};
```

#### Comunes

```javascript
// El documento ha terminado de cargar
$(document).ready()
// Click simple sobre un elemento ( igual que onclick )
on()
// Doble clic
dbclick()
// El puntero _entra_ en un elemento HTML
mouseenter()
// El puntero _sale_ de un elemento HTML
mouseleave()
// Cuando se presiona un botón del ratón, _sobre_ un elemento
mousedown()
// Cuando se libera un botón presionado del ratón, _sobre_ un elemento
mouseup()
// Ejecuta **dos funciones**: al _entrar_ en un elemento, y al _salir_
hover()
// Cuando un elemento **input** obtiene el foco
focus()
// Cuando un elemento **input** pierde el foco
blur()
```

