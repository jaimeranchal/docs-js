# Interactuar con Servidores: AJAX

Con JavaScript se pueden enviar peticiones al servidor y procesar la respuesta de forma **asíncrona**. Se suele usar para:

- Recuperar datos del servidor después de que se haya cargado la página
- Actualizar una página sin recargar
- Enviar datos al servidor en segundo plano

AJAX son las siglas de _Asynchronous JavaScript And XML_, aunque últimamente es más JSON que XML ;P.

Hay varias formas de implementar _conexiones asíncronas_ con JavaScript, pero el proceso es similar:

1. Creamos una petición (_request_) en forma de **objeto XMLHttpRequest**:
    - **Abrir** la conexión, con o sin **parámetros**
    - Definir qué vas a hacer con la **respuesta** (mostrarla, pasarla a otro método...)
2. **Enviar** la petición
3. El _servidor_:
    - procesa la petición
    - devuelve una **respuesta** (_response_)
4. El navegador recibe y **procesa la respuesta**
5. Se **actualiza** el contenido de acuerdo como necesitemos

![esquema - w3schools](../extra/img/ajax_scheme.gif)

## Implementaciones

En esta guía recojo ejemplos de conexiones asíncronas:

- con JavaScript nativo y **XMLHttpRequest**
- con **[jQuery](../jQuery/jQuery-intro.md)**
- con JavaScript y **fetch**
