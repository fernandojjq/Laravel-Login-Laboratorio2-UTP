# Laboratorio #2: Implementación de Login con Laravel

![PHP](https://img.shields.io/badge/PHP-8.4-777BB4?style=for-the-badge&logo=php)![Laravel](https://img.shields.io/badge/Laravel-12-FF2D20?style=for-the-badge&logo=laravel)![MySQL](https://img.shields.io/badge/MySQL-9.1-4479A1?style=for-the-badge&logo=mysql)![Vite](https://img.shields.io/badge/Vite-7.1-646CFF?style=for-the-badge&logo=vite)

Este repositorio es, más que nada, el diario de mi primer viaje real al ecosistema de Laravel. La verdad es que el objetivo iba más allá de un simple tutorial; se trataba de construir desde cero un sistema de autenticación que funcionara, con su login y su registro, y en el proceso, enfrentarme a todos los problemas que supone configurar un entorno de desarrollo moderno desde la nada.


## Arquitectura del Proyecto: Entendiendo qué es MVC

Uno de los puntos clave de este laboratorio era, sin duda, entender la famosa arquitectura **Modelo-Vista-Controlador (MVC)**. Al principio suena súper académico, pero en realidad es una forma bastante lógica de organizar el caos.

Yo lo veo como dividir un equipo de trabajo en tres especialistas, cada uno con una tarea muy clara:

*   **El Modelo (`Model`):** Este es el que sabe de datos. Su única preocupación es hablar con la base de datos, traer la información que se le pide (como los datos de un usuario) y asegurarse de que todo cumpla con las reglas. Para nosotros, la estrella aquí fue el archivo `app/Models/User.php`.

*   **La Vista (`View`):** Este es el diseñador del equipo. Le da igual de dónde vienen los datos; su trabajo es que todo se vea bien y que el usuario pueda interactuar con la página. Son básicamente los archivos HTML que ves en el navegador, como el formulario para iniciar sesión. Todos estos viven en la carpeta `resources/views`.

*   **El Controlador (`Controller`):** Este es el cerebro, el que dirige la orquesta. Cuando un usuario hace algo, como intentar iniciar sesión, el Controlador recibe esa petición. Luego, le pide al Modelo la información necesaria y finalmente le dice a la Vista cómo tiene que mostrar el resultado. Es el que conecta todo.

La siguiente captura intenta ser un pequeño mapa de esto en nuestro proyecto, mostrando dónde se pueden encontrar los `Controllers`, el `Model` y los archivos de `routes` que actúan como el GPS de la aplicación.

<img width="247" height="795" alt="image" src="https://github.com/user-attachments/assets/13b949b1-828d-48f5-9c87-46db34646982" />


## Puesta en Marcha del Proyecto

Si quieres echar a andar este proyecto en tu propia máquina, aquí te dejo los pasos.

### Prerrequisitos

Primero, lo primero. Necesitas tener todo este ecosistema montado. Esto fue lo que yo usé para que todo funcionara:

| Tecnología | Versión | Propósito |
| :--- | :--- | :--- |
| **PHP** | `8.4.0` | El lenguaje sobre el que corre todo esto. |
| **Composer** | `2.x` | El gestor de paquetes de PHP. Sin esto, no hay Laravel. |
| **WAMP Server** | `3.x` | Mi servidor local, que ya trae Apache y MySQL. |
| **MySQL** | `9.1.0` | El motor de la base de datos para guardar los usuarios. |
| **Node.js & NPM** | `20.x (LTS)` | Necesario para manejar todo el tema del frontend. |
| **Git** | `2.x` | Para el control de versiones, claro. |

### Secuencia de Instalación

1.  **Clonar el Repositorio:**
    ```bash
    git clone https://github.com/fernandojjq/Laravel-Login-Laboratorio2-UTP.git
    cd Laravel-Login-Laboratorio2-UTP
    ```

2.  **Instalar las Dependencias:**
    ```bash
    # Primero, las de PHP
    composer install

    # Y luego, las de Node.js
    npm install
    ```

3.  **Configurar el Entorno:**
    *   Haz una copia del archivo `.env.example` y renómbrala a `.env`. Este paso es clave.
    *   Abre ese nuevo archivo `.env` y ajusta los datos de tu base de datos. Debería quedar algo así:
    ```env
    DB_CONNECTION=mysql
    DB_HOST=127.0.0.1
    DB_PORT=3306
    DB_DATABASE=login_db
    DB_USERNAME=root
    DB_PASSWORD=
    ```
    *   *Obviamente, tienes que haber creado una base de datos vacía con el nombre `login_db` antes de esto.*

4.  **Generar la Clave de la Aplicación:**
    ```bash
    php artisan key:generate
    ```

5.  **Crear las Tablas en la Base de Datos:**
    ```bash
    php artisan migrate
    ```

6.  **Arrancar los Servidores:**
    *   **En una terminal,** dejas corriendo el servidor de Vite para el frontend:
        ```bash
        npm run dev
        ```
    *   **Y en una segunda terminal,** levantas el servidor de Laravel:
        ```bash
        php artisan serve
        ```

7.  **Y ya está.** Con esto, si abres `http://127.0.0.1:8000` en tu navegador, deberías ver la aplicación funcionando.

---

## Base de Datos

El tema de la base de datos fue central en este laboratorio.

*   **Entorno:** Usamos una base de datos **MySQL** que venía con **WAMP Server**. La conexión, como ya dije, se configura en el archivo `.env`. Me gusta pensar en ese archivo como la "caja de secretos" de la aplicación; ahí van todas las contraseñas y configuraciones delicadas.
*   **Migraciones:** El comando `php artisan migrate` me pareció una genialidad. En lugar de crear tablas a mano, Laravel usa unos archivos en `database/migrations` que son como recetas. El comando las lee y construye la base de datos por ti. Así, si trabajas en equipo, todos tienen la misma estructura.
*   **Respaldo (Backup):** Para asegurarnos de tener una copia de todo, generé un respaldo de la base de datos con este comando. Crea un archivo `.sql` con toda la estructura y los datos.
    ```bash
    mysqldump -u root login_db > login_db_backup.sql
    ```

La siguiente captura es la prueba del delito: la tabla `users` con un registro dentro. La confirmación de que la aplicación y la base de datos por fin se estaban comunicando.

<img width="921" height="270" alt="image" src="https://github.com/user-attachments/assets/bcc518ed-1b00-4959-8a6e-6bd8631fd5b4" />


---

## El Resultado Final

Después de toda la pelea con la configuración, el resultado fue una aplicación web que funciona, se ve bien y es moderna. No es solo un montón de código, es algo tangible.

La imagen de abajo muestra el "Dashboard". Es la página a la que llegas después de iniciar sesión, la prueba visual de que todo el sistema de autenticación está operativo.

<img width="921" height="230" alt="image" src="https://github.com/user-attachments/assets/1a147787-aeb6-4a1e-a9d5-593f12a5737c" />

---

## El Verdadero Viaje: Dificultades y Soluciones

Este laboratorio fue, en esencia, una cadena de "un paso adelante, un problema que resolver". Y aunque a ratos fue frustrante, creo que es la única forma real de aprender.

#### Dificultad 1: La terminal no me conocía de nada.
*   **Descripción:** El primer golpe de realidad. Abrí la terminal, escribí `php -v` y nada. La terminal me dijo que no tenía ni idea de qué era `php` o `composer`. Sin eso, era imposible empezar.
*   **Solución:** Resulta que Windows no es adivino. Tienes que decirle dónde están los programas que instalas. La solución fue meterme en las "Variables de Entorno" y añadir las rutas de las carpetas de PHP y Composer al `Path`. Es como darle un mapa a la terminal. Reinicié, y por fin me reconoció.

#### Dificultad 2: El misterioso error del disco "E:".
*   **Descripción:** Este fue bastante curioso. Justo al instalar Composer, el programa se detuvo con un error muy específico sobre una extensión, `xdebug`, y una ruta que apuntaba a un disco `E:`. Lo raro es que yo no tengo ningún disco `E:`.
*   **Solución:** Al principio pensé que era algo grave, pero el problema estaba en el `php.ini`. Era como una dirección antigua olvidada en una agenda. Abrí el archivo, busqué la línea de `xdebug` y le puse un punto y coma (`;`) al principio. Con eso, el programa la ignora. Guardé, volví a intentar y la instalación pasó sin problemas.

#### Dificultad 3: El "déjà vu" del comando `npm`.
*   **Descripción:** Justo cuando celebraba haber arreglado los problemas de "comandos no reconocidos", apareció otro con `npm install`. Exactamente el mismo error.
*   **Solución:** Por suerte, esta vez ya sabía qué pasaba. Si la terminal no reconocía `npm`, es que me faltaba Node.js. Fui a su web, descargué la versión LTS (la estable, para evitar más sorpresas) y la instalé. Lo bueno es que el instalador de Node.js ya se encarga de todo el tema de las variables de entorno, así que funcionó a la primera.

#### Dificultad 4: La base de datos y su "llave demasiado larga".
*   **Descripción:** Este fue el último gran reto, y el más técnico. Cuando por fin lancé `php artisan migrate:fresh`, la base de datos me devolvió un error: `Specified key was too long`.
*   **Solución:** Después de buscar, entendí la analogía: era como intentar meter una llave muy larga en una cerradura pequeña. Las versiones más viejas de MySQL tienen un límite. La solución fue ir a un archivo de configuración de Laravel, el `AppServiceProvider.php`, y decirle explícitamente que hiciera las columnas de texto un poco más cortas por defecto. Fue un cambio de una sola línea, pero fue la clave que lo arregló todo.

---

## Referencias

Para salir de todos estos líos y entender mejor los conceptos, me apoyé bastante en estas fuentes:

1.  **Documentación Oficial de Laravel 12:** La verdad es que es el primer sitio al que hay que ir. Casi todo está ahí. [https://laravel.com/docs/12.x](https://laravel.com/docs/12.x)
2.  **Documentación de Laravel Breeze:** Muy útil para entender el paquete de autenticación que usamos. [https://laravel.com/docs/12.x/starter-kits#laravel-breeze](https://laravel.com/docs/12.x/starter-kits#laravel-breeze)
3.  **Hilos de Stack Overflow y Artículos Varios:** Para el error de la "llave demasiado larga", la comunidad fue clave. Hay muchísima gente que ya se ha topado con ese problema y explica la solución del `AppServiceProvider`.

---

<div align="center">
Este laboratorio ha sido desarrollado por:
<br>
<b>Fernando Jiménez</b>
<br>
<i>Estudiante de la Universidad Tecnológica de Panamá</i>
<br>
<br>
<b>Curso:</b> Ingeniería Web
<br>
<b>Instructor del Laboratorio:</b> Ing. Irina Fong
</div>
