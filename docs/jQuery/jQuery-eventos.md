# Eventos

Un evento es una **acción** o un **cambio** que afecta o está relacionado con un elemento del DOM. Se pueden asociar funciones a determinados eventos para ejecutar automáticamente determinadas cosas, como por ejemplo:

- validar el campo de un formulario
- asignar una clase css a un elemento si ocurre algo
- mostrar ventanas modales al pulsar botones

La sintaxis con jQuery es muy simple:

```javascript
$(selector).evento(funcion);
```

## El objeto _e_

Cuando se produce un evento, el navegador guarda información sobre él. Podemos acceder y manipular esa información como si fuera un objeto.

| Propiedad  | Descripción                                                        |
|------------|--------------------------------------------------------------------|
| `pageX`    | distancia (px) entre el puntero y el lado izquierdo de la ventana  |
| `pageY`    | distancia (px) entre el puntero y la parte superior de la ventana  |
| `screenX`  | distancia (px) entre el puntero y el lado izquierdo de la monitor  |
| `screenY`  | distancia (px) entre el puntero y la parte superior de la monitor  |
| `shiftKey` | Booleano. True si _Mayús_ está pulsada                             |
| `which`    | código de la tecla pulsada (para eventos _keypress_)               |
| `target`   | objeto sobre el que se produce el evento                           |
| `data`     | _Colección_ con los datos del evento para pasárselos a una función |

```javascript
/* Imprime la coordenadas del ratón al hacer click */
$(document).click( function(e){
    // por compatibilidad con antiguos navegadores
    // incluimos la opción `window.event`
    let evento = e || window.event 

    console.log(
        "x -> " + evento.pageX +
        "y -> " + evento.pageY
    )
})
```

## Detener un evento

Algunos elementos HTML ya tienen acciones predeterminadas en ciertos eventos, especialmente en los **formularios** (enviar y resetear los campos, con los inputs o botones tipo _submit_ y _reset_).

Si quieres validar los campos antes de enviar el formulario, hay que **detener** esa acción por defecto. Eso se hace con `e.preventDefault()`:

```javascript
// Impide que se escriban caracteres que no sean números
// la acción por defecto sería mostrarlos
$(':text').keypress( (e) => {
    let evento = e || window.event

    if (evento.which < 48 || evento.which > 57) {
        evento.preventDefault();
    }
})
```

## Métodos

=== "Combinados"
    === "on"
        ```javascript
        /**
         * asigna cualquier tipo de evento
         * @param eventos
         * @param selector descendientes que dispararán el evento
         * @data datos que haya que pasar al handler (parámetros)
         * @param handler función a ejecutarse
         */
        $(selector).on(eventos [, selector] [, data], handler)

        /* Ejemplos */
        $(document).on('click', ':button', () => {
            alert("Has pulsado un botón");
        })

        $(':button').on('click mouseout', () => {
            alert("Has pulsado o movido el ratón fuera de un botón");
        })
        ```
    === "hover"
        ```javascript
        /**
         * Alterna dos acciones al entrar y salir de un elemento
         * @param mouseover funcion al entrar
         * @param mouseout funcion al salir
         */
         $(selector).hover(mouseover, mouseout)

        // Oculta y muestra el color de un botón
        let colorFondo;

        $('boton').hover( 
            () => {
                colorFondo = $('boton').css('background-color')
                $('boton').css('background-color', '')
            },
            () => {
                $('boton').css('background-color', colorFondo)
            },
        )
        ```
    === "off"
        ```javascript
        /**
         * Elimina eventos
         */

        // desactiva los clicks en el div#menú
        $('#menu').off('click')

        // botón que sólo imprime el mensaje una vez
        $(':button').on('click', ()=>{
            alert("Has pulsado un botón");
            $(':button').off('click')
        })
        ```
=== "Eventos"
    ```javascript
    // El documento ha terminado de cargar
    $(document).ready()

    click() // Click simple sobre un elemento ( igual que onclick )
    dbclick()
    mouseenter()
    mouseleave()
    mousedown()
    mouseup()
    focus()
    blur()
    ```

