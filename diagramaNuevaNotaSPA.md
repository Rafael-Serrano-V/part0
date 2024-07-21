sequenceDiagram

    participant user
    participant browser
    participant server

    Note over User, Browser: Navega a https://studies.cs.helsinki.fi/exampleapp/spa
    user->>browser: Ingresa al sitio

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa
    activate Server
    Server-->>Browser: HTML document
    deactivate Server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: CSS file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa.js
    activate server
    server-->>browser: JavaScript file
    deactivate Server

    Note right of Browser: El navegador comienza a ejecutar el código JavaScript que obtiene el JSON desde el sevidor

    Browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate Server
    Server-->>Browser: [{ "content": "HTML is easy", "date": "2023-1-1 }, ... ]
    deactivate Server

    Note right of browser: El navegador ejecuta la función de devolución de llamada que renderiza las notas

    Note over Browser: Interfaz de la aplicación cargada
    User->>Browser: Escribe contenido de la nota y presiona el botón 'Save'

    Browser->>Server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa
    Note over Server: Crea la nueva nota en la base de datos
    Server-->>Browser: Respuesta HTTP 201 Created

    Note over Browser: Esta vez, el servidor no solicita una redirección, el navegador permanece en la misma página y no envía más solicitudes HTTP.
    
    Browser-->User: Interfaz actualizada con la nueva nota 