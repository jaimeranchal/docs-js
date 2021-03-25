# AJAX con jQuery

La librería jQuery incorpora unos cuantos métodos que facilitan trabajar con AJAX.

=== "Básicos"
    ```javascript
    /** Inicia la conexión con unos parámetros
     * @param URL
     * @param parámetros : opcional
     * @param callback : función con tres parámetros
     *      - responseText = datos leídos
     *      - statusTxt = estado de la respuesta
     *      - xhr = objeto XMLHttpRequest
     */
    $("selector").load(URL, [datos,] (responseText, statusTxt, xhr) => {
        // ...
        if (statusTxt == 'success') {
            alert("La carga ha tenido éxito");
        } else {
            alert("Error: " + xhr.status + ": " + xhr.statusTxt);
        }
    }); 
    $.get();
    $.post();
    $.getJSON();
    $.getScript(),
    ```
=== "$.ajax()"
    ```javascript
    
    ```
