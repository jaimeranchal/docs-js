# API Fetch

Para no depender de jQuery ni otras librerías se ha creado una API para facilitar el trabajo: `fetch`.

!!! note "Promesas"
    Una **promesa** (_promise_) es un objeto que devuelve un resultado (valor de retorno o error) cuando finaliza una operación. Una promesa tiene tres **estados**:

    - _Pending_
    - _Fulfilled_: accesible mediante `resolve(value)`
    - _Rejected_: accesible mediante `reject(value)`

=== "Get"
    ```javascript
    // Para leer datos
    fetch('https://httpbin.org/ip')
        .then( function(response) {
            return response.json(); // o response.text
        })
        .then( function(data) {
            console.log('data =', data);
        })
        .catch( function(err) {
            console.log(err);
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
            console.log('data =', data);
        })
        .catch( function(err) {
            console.log(err);
        })
    ```
=== "datos"
    ```javascript
    // Se pueden pasar los parámetros como un objeto formData

    let datos = new formData();

    // añadir información a los datos
    datos.append("chip", "111A");
    datos.append("nombre", "ganso");
    ```
