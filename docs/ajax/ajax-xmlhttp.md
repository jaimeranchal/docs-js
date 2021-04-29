# Conexión con _XMLHttpRequest_

Ejemplo de conexión asíncrona con el objeto XMLHttpRequest:

=== "Conexión"
    !!! note "Modularizar"
        Es más práctico tener una función para conectarse a la base de datos en un archivo separado, junto con las librerías.

    === "lib/connect.js"
        ```javascript
        function crearConexion() {
            let objeto;

            if (window.XMLHttpRequest) {
                objeto = new XMLHttpRequest();
            } else if (window.ActiveXObject) {
                try {
                    objeto = new ActiveXObject("MSXML2.XMLHTTP");
                } catch(e) {
                    objeto = new ActiveXObject("Microsoft.XMLHTTP");
                }
            }

            return objeto;
        }
        ```
    === "main.js"
        ```javascript
        let xmlHttp;

        // cargamos con la página
        $(()=>{
            // crear objeto xmlHttp
            xmlHttp = crearConexion();

            if (xmlHttp!=undefined) {
                // seguimos
                $("#boton").on('click', mostrarMensaje);
            } else {
                swal.fire("El navegador no soporta AJAX"+
                        " La página no tendrá funcionalidad");
            }
        })
        ```
=== "Peticiones"
    === "GET"
        === "Simple"
            ```javascript
            function mensajeGet() {
                // crear un objeto XMLHttpRequest
                let xmlHttp = crearConexion();

                // abrir la conexión sin parámetros
                xmlHttp.open("GET", "origen.php", true); 

                // preparar la respuesta
                xmlHttp.onreadystatechange = () => {
                    if (xmlHttp.readyState == 4 &&
                        xmlHttp.status == 200) {

                        $("#mensaje").text(xmlHttp.responseText);
                    }
                }

                // iniciar la conexión
                xmlHttp.send();
            }
            ```
        === "Con parámetros"
            ```javascript
            function mensajeGet() {
                // crear un objeto XMLHttpRequest
                let xmlHttp = crearConexion();

                // abrir la conexión con parámetros
                xmlHttp.open("GET", "origen.php?valor=GET&param=valor", true); 

                // preparar la respuesta
                xmlHttp.onreadystatechange = () => {
                    if (xmlHttp.readyState == 4 &&
                        xmlHttp.status == 200) {

                        $("#mensaje").text(xmlHttp.responseText);
                    }
                }

                // iniciar la conexión
                xmlHttp.send();
            }
            ```
    === "POST"
        ```javascript
        function mensajePost() {
            // crear un objeto XMLHttpRequest
            let xmlHttp = crearConexion();

            // abrir la conexión
            xmlHttp.open("POST", "origen.php", true); 
            // enviar la cabecera
            xmlHttp.setRequestHeader(
                "Content-Type",
                "application/x-www-form-urlencoded",
            );

            // preparar la respuesta
            xmlHttp.onreadystatechange = () => {
                if (xmlHttp.readyState == 4 &&
                    xmlHttp.status == 200) {

                    $("#mensaje").text(xmlHttp.responseText);
                }
            }

            // iniciar la conexión con los parámetros
            xmlHttp.send("valor=POST&param=valor");
        }
        ```

    !!! note "GET vs POST"
        Si se usa el método `POST` hay que cambiar **dos cosas**:

        1. **enviar la cabecera** HTTP explícitamente después de abrir la conexión
        2. pasar los **parámetros** en el método `send()` y no en `open()`

## Tipos de respuesta

El servidor puede mandar los datos en diferentes formatos, y se manejan de modo distinto. Son **tres tipos**:

- **xml**: con `responseXML`
- **texto plano**: con `responseText`
- **json**: con `JSON.parse(xmlHttp.responseText)`

=== "responseXML"
    ```javascript
    let datos = xmlHttp.responseXML;
    // cadena en blanco
    let mensaje = "";
    // busca y añade los datos al mensaje
    $(datos).find("selector").each((ind,ele) => {
        if (ind == 1) {
            // búsca dentro de ese elemento
            $(ele).find("selector").each((index,mod)=>{
                mensaje+=$(mod).text();
            })

            // ...
        }
    })
    // muestra los datos
    $("selector").html(mensaje);
    
    ```
=== "responseText"
    ```javascript
    /* Texto plano */
    let respuesta = xmlHttp.responseText;
    /* Json */
    let datos = JSON.parse(xmlHttp.responseText);
    $(datos.data).each((ind,ele)=>{
        // ...
    });
    ```

## El objeto XMLHttpRequest

=== "Propiedades"
    ```javascript
    /** Estado del objeto
     * @return 0 = sin inicializar
     * @return 1 = abierto
     * @return 2 = cabeceras recibidas
     * @return 3 = cargando
     * @return 4 = completado
     */
    xmlHttp.readyState;

    xmlHttp.status;     // estado (número: 404)
    xmlHttp.statusText; // estado (cadena)

    xmlHttp.responseXML;  // respuesta en XML
    xmlHttp.responseText; // respuesta como cadena (JSON etc)
    ```
=== "Métodos"
    ```javascript
    xmlHttp.abort();                   // cancela la petición en curso
    xmlHttp.getAllResponseHeaders();   // todas las cabeceras
    xmlHttp.getResponseHeader(header); // solo una cabecera
    xmlHttp.open(
        "método",    // GET o POST
        "url",       // de dónde vienen los datos
        true | false // asíncrono o no
    );
    xmlHttp.send( null | "dato=valor" ); // envía la petición
    ```
=== "Eventos"
    ```javascript
    xmlHttp.onreadystatechange; // con cada cambio de estado
    xmlHttp.onabort;            // al abortar
    xmlHttp.onload;             // al completar la carga
    xmlHttp.onloadstart;        // al comenzar la carga
    xmlHttp.onprogress;         // periódicamente con info del estado
    ```
