# Ejemplos de AJAX

=== "XML"
    Tenemos información sobre cursos y asignaturas en un archivo XML y queremos mostrar las asignaturas de cada curso según se seleccione uno y otro:

    === "Js"
        ```javascript
        // después de abrir la conexión
        xmlHttp.onreadystatechange = () => {
            // recojo la información del servidor y la muestro
            let datos = xmlHttp.responseXML;

            // limpiar el contenedor donde voy a mostrar los datos
            $("#asignaturas option:gt(0)").remove();

            // busco en los datos usando selectores
            $(datos).find("curso").each((ind,ele) => {
                // si coincide con la opción seleccionada
                if (ind == $("#cursos").prop("selectedIndex")-1) {
                    // busca de nuevo
                    $(ele).find("asig").each((index,mod)=>{
                        // inserta texto con el valor de los datos
                        $("#asignaturas").append("<option>"+$(mod).text()+ "</option>");
                    })
                }
            })
        }
        
        ```
    === "html"
        ```html
        <html lang="es">
            <head>
                <meta charset="utf-8">
            </head>

            <body>
                <select id="cursos">
                    <option>Seleccione curso ...</option>
                    <option>1º curso</option>
                    <option>2º curso</option>
                </select>
                <select id="asignaturas">
                    <option>Asignaturas</option>
                </select>
                
                <script src="../librerias/jquery/jquery-3.5.1.min.js"></script>
                <script src="../librerias/crearConexion.js"></script>
                <script src="script.js"></script>
            </body>
        </html>
        ```
    === "xml"
        ```xml
        <?xml version="1.0" encoding="UTF-8" ?>
        <ciclo>
            <curso>
                <asig>SIM</asig>
                <asig>prog</asig>
                <asig>BD</asig>
            </curso>
            <curso>
                <asig>DEWC</asig>
                <asig>DEWS</asig>
                <asig>DIW</asig>
            </curso>
        </ciclo>
        ```
=== "JSON"
    Vamos a mostrar las capitales de provincia de la Comunidad Autónoma seleccionada:

    === "js"
        ```javascript
        xmlHttp.onreadystatechange = () => {
            if (xmlHttp.readyState == 4 &&
                xmlHttp.status == 200) {

                // recojo la información del servidor y la muestro
                // como devuelve un string hay que "reconvertirlo" a JSON
                let datos = JSON.parse(xmlHttp.responseText);

                let mensaje = "";

                $(datos).each((ind,ele) => {
                    mensaje += ele +"<br>";
                })

                $("#mostrar").html(mensaje);
            }
        }
        ```
    === "html"
        ```html
        <html lang="es">

        <head>
            <meta charset="utf-8">
        </head>

        <body>
            <select id="regiones">
                <option>Seleccione Región ...</option>
                <option>Andalucia</option>
                <option>Castilla La Mancha</option>
                <option>Extremadura</option>
            </select>
            <div id="mostrar"></div>

            <script src="../librerias/jquery/jquery-3.5.1.min.js"></script>
            <script src="../librerias/crearConexion.js"></script>
            <script src="script.js"></script>
        </body>

        </html>
        ```
    === "php"
        ```php
        <?php

        if ($_REQUEST['ca'] == 'Andalucia') {

            $capitales = array('Almeria', 'Cádiz', 'Córdoba', 'Granada', 'Huelva', 'Jaén', 'Málaga', 'Sevilla');
        }
        if ($_REQUEST['ca'] == 'Castilla La Mancha') {
            $capitales = array('Albacete', 'Ciudad Real', 'Cuenca', 'Guadalajara', 'Toledo');
        }
        if ($_REQUEST['ca'] == 'Extremadura') {
            $capitales = array('Badajoz', 'Caceres');
        }
        header('Content-type: application/json; charset=utf-8');
        echo json_encode($capitales);
        exit();
        ?>
        ```
