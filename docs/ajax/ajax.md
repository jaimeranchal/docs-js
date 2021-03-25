# Interactuar con Servidores: AJAX

- Se establece la conexión
- Los datos se pueden leer con el método `GET` o con `POST`:

=== "Conexión"
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
=== "GET"
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
=== "GET + parámetros"
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
