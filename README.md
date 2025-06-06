# Frontend Web para Gestión de Productos, Categorías y Usuarios (con Autenticación JWT)

Este repositorio contiene el código fuente del frontend web para interactuar con una API RESTful desarrollada con FastAPI. Esta interfaz de usuario permite la gestión de productos, categorías y usuarios, e incorpora un sistema de autenticación y autorización basado en JSON Web Tokens (JWT).

## Repositorio

El código fuente completo de este proyecto se encuentra en el siguiente repositorio de GitHub:

[https://github.com/JowelBB/Actividad_5_frontend](https://github.com/JowelBB/Actividad_5_frontend)

## API del Backend Asociada

Este frontend consume una API RESTful separada. Puedes encontrar el repositorio del backend aquí:

[https://github.com/JowelBB/Actividad_5_backend](https://github.com/JowelBB/Actividad_5_backend)

## Tecnologías Utilizadas

* **HTML5:** Estructura de las páginas web.
* **CSS3:** Estilos visuales de la aplicación.
* **JavaScript:** Lógica de interacción con la API y gestión de la sesión.
* **jQuery:** (Si estás utilizando jQuery para facilitar las peticiones AJAX y manipulación del DOM).
* **Bootstrap / Materialize / Otro Framework CSS:** (Menciona si usas alguno para el diseño).

## Arquitectura

Este repositorio se enfoca exclusivamente en el **frontend (aplicación web)**:

* Desarrollado con HTML, CSS y JavaScript.
* Gestiona el proceso de registro (`signup.html`), login (`signin.html`) y el almacenamiento del token JWT en el `localStorage` del navegador.
* Envía el token JWT en los encabezados de las solicitudes a las rutas protegidas de la API.
* Proporciona funcionalidades CRUD para productos y categorías en `tables.html`.
* Incluye un botón de "Cerrar Sesión" que elimina el token del `localStorage` y redirige al usuario a la página de login, asegurando la finalización de la sesión.
* Contiene un dashboard principal (`index.html`) accesible solo para usuarios autenticados.

## Requisitos Previos

Antes de utilizar este frontend, asegúrate de que el **backend API esté en ejecución** y sea accesible desde la ubicación donde se servirá este frontend.

## Instalación y Ejecución

Al ser un proyecto de frontend estático (HTML, CSS, JavaScript), no requiere un proceso de instalación complejo como el backend.

1.  **Clona el repositorio:**
    ```bash
    git clone [https://github.com/JowelBB/Actividad_5_frontend.git](https://github.com/JowelBB/Actividad_5_frontend.git)
    cd Actividad_5_frontend
    ```

2.  **Abre los archivos HTML en tu navegador:**
    * Puedes simplemente abrir `signup.html` o `signin.html` directamente en tu navegador web.
    * **Nota:** Para entornos de producción o desarrollo local más robusto, se recomienda servir los archivos a través de un servidor web simple (ej. `python -m http.server` o un servidor Nginx/Apache). Esto es crucial para manejar correctamente las rutas y evitar problemas de CORS si el frontend y el backend están en diferentes dominios/puertos.

## Configuración de la API Base URL

* Deberás asegurarte de que las rutas de la API en tus archivos JavaScript (`script.js` o en los scripts incrustados en los HTML) apunten a la URL correcta de tu backend API.
* Busca la variable que define la URL base de la API (ej. `const API_BASE_URL = 'http://127.0.0.1:8000';`) y actualízala a la URL de tu API en producción (ej. `https://api.yourdomain.com`).

## Páginas del Frontend

* **`signup.html`**: Página para el registro de nuevos usuarios.
* **`signin.html`**: Página para el inicio de sesión de usuarios existentes.
* **`index.html`**: Dashboard principal o página de bienvenida (protegida, requiere autenticación).
* **`tables.html`**: Página para la gestión y visualización de productos y categorías (protegida, requiere autenticación).

## Consumo de la API y Gestión de Sesión

### Autenticación y Gestión de Sesión

* **Registro (`signup.html`)**: Envía los datos del nuevo usuario al endpoint `POST /users/` del backend.
* **Login (`signin.html`)**: Maneja el envío de credenciales (`username`, `password`) al endpoint `POST /token` de la API.
    * Si la autenticación es exitosa, el token JWT (`access_token` y `token_type`) recibido se almacena en el `localStorage` del navegador.
    * El usuario es redirigido a `index.html` o `tables.html`.
* **Páginas Protegidas (`index.html`, `tables.html`)**:
    * Al cargar estas páginas, se verifica la presencia del `access_token` en el `localStorage`. Si no existe, el usuario es redirigido a `signin.html`.
    * Incluyen un botón "Cerrar Sesión" que, al ser clickeado, elimina el `access_token` y `token_type` del `localStorage` y redirige al usuario a `signin.html`, cerrando la sesión.

### Acceso a Rutas Protegidas

* Para acceder a los endpoints de la API que requieren autenticación, el JavaScript del frontend debe incluir el token JWT en el encabezado `Authorization` de cada solicitud `fetch` (o `XMLHttpRequest`). El formato es `Authorization: Bearer <your_access_token>`.
* Si una solicitud a una ruta protegida devuelve un error `401 Unauthorized` (debido a un token ausente, inválido o expirado), el frontend limpiará el token del `localStorage` y redirigirá al usuario a `signin.html` para que vuelva a iniciar sesión.

### Operaciones CRUD (tables.html)

* **Listado de Productos y Categorías:** Se realizan peticiones `GET` a `/productos/` y `/categorias/` para obtener las listas iniciales. Estas peticiones pueden requerir o no el token dependiendo de la configuración de la API (en este caso, la lectura es pública).
* **Creación, Actualización y Eliminación:** Las acciones de "Crear", "Actualizar" y "Eliminar" para productos y categorías (endpoints `POST`, `PUT`, `DELETE`) requieren que el token JWT sea enviado en el encabezado `Authorization` para que la API las acepte.
* **Filtro y Controles:** La página `tables.html` incluye controles para filtrar por ID y realizar operaciones CRUD.

## Estructura del Código:

* Actividad_5_frontend/
* ├── signin.html     # Página de login
* ├── signup.html     # Página de registro
* ├── index.html      # Dashboard principal (protegido)
* ├── tables.html     # Página de tablas (productos/categorías - protegido)
