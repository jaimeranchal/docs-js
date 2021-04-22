# AJAX con jQuery

La librería jQuery incorpora unos cuantos métodos que facilitan trabajar con AJAX.

=== "Básicos"
    ```javascript
    /** Inicia la conexión con unos parámetros
     * @param URL
     * @param parámetros : opcional
     * @param callback(respuesta, estado, XHR)
     *      - responseText = datos leídos
     *      - statusTxt = estado de la respuesta [success, error, timeout, parsererror]
     *      - xhr = objeto XMLHttpRequest
     */
    $.load();

    // Ejemplo
    $("selector").load(URL, [datos,] (responseText, statusTxt, xhr) => {
        // ...
        if (statusTxt == 'success') {
            alert("La carga ha tenido éxito");
        } else {
            alert("Error: " + xhr.status + ": " + xhr.statusTxt);
        }
    }); 

    /**
     * Carga los datos usando una petición GET/POST
     * @param URL
     * @param datos: query string (lo que buscas)
     * @param callback(datos, estado, XHR)
     */
    $.get(url, [datos], [callback]);
    $.getJSON(url, [datos], [callback]);
    $.post(url, [datos], [callback]);

    // Ejemplo
    $.get("test.php");
    $.get("test.php", { nom: 'María', ape: 'Estévez' });
    $.get("test.php", { nom: 'María', ape: 'Estévez' }, (responseTxt, statusTxt, xhr) => {
        if (statusTxt == 'success')
            alert("Se han cargado los datos con éxito");
        if (statusTxt == 'error')
            alert("Error: " + xhr.status + ": " + xhr.statusTxt);
    });
    ```
=== "$.ajax()"
    En lugar de los anteriores se recomienda usar `$.ajax()`.

    | Opción       | Descripción                                                        | Por defecto |
    |--------------|--------------------------------------------------------------------|-------------|
    | `async`      | ¿petición asíncrona?                                               | `true`      |
    | `beforeSend` | Función que modifica el objeto XML antes de mandar la petición     |             |
    | `data`       | query string                                                       |             |
    | `datatype`   | tipo de dato: `xml`, `html`, `script`, `json`                      |             |
    | `timeout`    | Tiempo máximo de espera antes de anular la petición (milisegundos) |             |
    | `type`       | POST o GET                                                         |             |
    | `url`        | Dónde mandamos la petición                                         |             |
    | `success`    | (**deprecated**) Función cuando la petición tiene éxito            |             |
    | `error`      | (**deprecated**) Función cuando la petición falla                  |             |

    === "Normal"
        ```javascript
        // Ejemplo
        $.ajax({
            url: '/ruta/hasta/pagina.php',
            type: 'POST',
            async: true,
            data: {
                parametro1: valor1,
                parametro2: valor2,
            },
            success: procesarRespuesta,
            error: mostrarError
        });
        ```
    === "Con promises"
        ```javascript
        // Con promesas
        $.ajax({
            url: '/ruta/hasta/pagina.php',
            type: 'POST',
            async: true,
            data: {
                parametro1: valor1,
                parametro2: valor2,
            };
        });
        .done( function(response, textStatus, jqXHRs) {
            // ...
        });
        .fail( function(response, textStatus, errorThrown) {
            // ...
        });
        .always( function() {
            console.log("completado");
        });
        ```
