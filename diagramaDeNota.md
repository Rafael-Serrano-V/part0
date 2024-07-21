sequenceDiagram

    participant User
    participant Browser
    participant Server

    Note over User, Browser: Navega a https://studies.cs.helsinki.fi/exampleapp/notes
    User->>Browser: Ingresa al sitio

    Browser->>Server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate Server
    Server-->>Browser: HTML document
    deactivate Server

    Browser->>Server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate Server
    Server-->>Browser: CSS file
    deactivate server

    Browser->>Server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate Server
    Server-->>Browser: JavaScript file
    deactivate Server

    Note right of Browser: El navegador comienza a ejecutar el código JavaScript que obtiene el JSON desde el sevidor

    Browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate Server
    Server-->>Browser: [{ "content": "HTML is easy", "date": "2023-1-1 }, ... ]
    deactivate Server

    Note right of browser: El navegador ejecuta la función de devolución de llamada que renderiza las notas

    Note over Browser: Interfaz de la aplicación cargada
    User->>Browser: Escribe contenido de la nota y presiona el botón 'Save'

    Browser->>Server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
    Note over Server: Crea la nueva nota en la base de datos
    Server-->>Browser: Respuesta HTTP 200 OK
    
    Note over Browser: Recarga de la página
    Browser-->User: Interfaz actualizada con la nueva nota 