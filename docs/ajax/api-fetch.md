# API Fetch

Para no depender de jQuery ni otras librerías se ha creado una API para facilitar el trabajo: `fetch`.

!!! note "Promesas"
    Una **promesa** (_promise_) es un objeto que devuelve un resultado (valor de retorno o error) cuando finaliza una operación. Una promesa tiene tres **estados**:

    - _Pending_
    - _Fulfilled_: accesible mediante `resolve(value)`
    - _Rejected_: accesible mediante `reject(value)`

Con Fetch no es necesario abrir la conexión en un paso aparte, como con [XMLHttpRequest](./ajax-xmlhttp.md), sino que indicamos el origen y lo que hacemos con la respuesta:

=== "Get"
    === "Sintaxis extendida"
        ```javascript
        // Para leer datos
        fetch('https://httpbin.org/ip')
            .then( function(response) {
                return response.json(); // o response.text
            })
            .then( function(data) {
                // ...
            })
            .catch( function(err) {
                // ...
            })
        ```
    === "Reducida"
        ```javascript
        // Para leer datos
        fetch('https://httpbin.org/ip')
            .then(response => response.json())
            .then( (data) => {
                // ...
            })
            .catch( (err) => {
                // ...
            })
        ```
=== "Post"
    ```javascript
    // para crear nuevos datos, actualizar y borrar
    fetch('http://ejemplo.com/api/user', {
        method: 'POST',
        body: datos
    })
        .then( function(response) {
            return response.json(); // o response.text
        })
        .then( function(data) {
            // ...
        })
        .catch( function(err) {
            // ...
        })
    ```

    Los datos que necesita el método post se pueden crear con un **objeto FormData**:

    ```javascript
    // Se pueden pasar los parámetros como un objeto formData

    let datos = new formData();
    datos.append("chip", $("#chip").val());
    datos.append("nombre", $("#nombre").val())
    datos.append("raza", $("#raza").val())
    datos.append("fechaN", $("#fechaN").val())

    fetch("php/editar.php", {
            method: 'POST',
            body: datos,
        })
        .then( function(response) {
            return response.json(); // o response.text
        })
        .then( function(data) {
            // ...
        })
        .catch( function(err) {
            // ...
        })
    ```
