# Ejecución del Laboratorio de Laravel

**Universidad Tecnológica de Panamá** · Facultad de Ingeniería de Sistemas Computacionales
**Curso:** Desarrollo Web · **Grupo:** 1S3122
**Estudiante:** Angel Gálvez (angel.galvez2@utp.ac.pa)
**Fecha:** 22 de octubre de 2026

Repositorio: https://github.com/galvezangel074-glitch/LARAVEL.git

## Descripción

Laboratorio de introducción a Laravel: una aplicación con **registro e inicio de sesión de usuarios** (autenticación con `laravel/ui` y Bootstrap 5), conectada a una base de datos MySQL y con los estilos compilados con Vite.

## Tecnologías

| Componente | Versión / detalle |
|---|---|
| PHP | 8.3 |
| Laravel | 13.x (`laravel/framework ^13.17`) |
| Autenticación | `laravel/ui ^4.6` (vistas Blade con Bootstrap 5) |
| Base de datos | MySQL (WAMP), base `pruebaregistrolarvel` |
| Assets | Vite + Sass (`resources/sass/app.scss`) |
| Servidor local | `php artisan serve` → http://localhost:8000 |

## Qué se hizo

1. Se creó el proyecto Laravel en `C:\wamp64\www\laravel`.
2. Se configuró la conexión a MySQL en el archivo `.env` (`DB_DATABASE=pruebaregistrolarvel`, usuario `root`).
3. Se ejecutaron las migraciones, que crean las tablas `users`, `cache` y `jobs`:
   ```bash
   php artisan migrate
   ```
4. Se instaló el scaffolding de autenticación con `laravel/ui`, que genera los controladores en `app/Http/Controllers/Auth`, las vistas en `resources/views/auth` y la ruta `Auth::routes()`.
5. Se instalaron las dependencias y se compilaron los estilos:
   ```bash
   npm install
   npm run build
   ```
6. Se levantó el servidor y se probaron las pantallas de registro, login y el panel protegido:
   ```bash
   php artisan serve
   ```

## Rutas de la aplicación

| Método | URI | Descripción |
|---|---|---|
| GET | `/` | Página de bienvenida |
| GET / POST | `/login` | Inicio de sesión |
| POST | `/logout` | Cierre de sesión |
| GET / POST | `/register` | Registro de usuarios |
| GET | `/password/reset` | Solicitud de recuperación de contraseña |
| POST | `/password/email` | Envío del enlace de recuperación |
| GET / POST | `/password/reset/{token}` | Restablecer contraseña |
| GET / POST | `/password/confirm` | Confirmar contraseña |
| GET | `/home` | Panel principal (requiere sesión iniciada) |

La ruta `/home` está protegida con el middleware `auth` en `HomeController`: si no hay sesión, redirige a `/login`.

## Capturas de la ejecución

### Inicio de sesión (`/login`)
![Login](docs/capturas/02-login.png)

### Registro de usuario (`/register`)
![Registro](docs/capturas/03-registro.png)

### Recuperar contraseña (`/password/reset`)
![Recuperar contraseña](docs/capturas/04-recuperar-password.png)

### Panel principal con la sesión iniciada (`/home`)
![Home](docs/capturas/05-home-autenticado.png)

## Cómo ejecutarlo

```bash
composer install
npm install
cp .env.example .env        # en este repositorio ya se incluye el .env del laboratorio
php artisan key:generate
php artisan migrate
npm run build
php artisan serve
```

Luego abrir http://localhost:8000.

> Este repositorio incluye `vendor/`, `node_modules/` y `.env` a petición del autor, porque es un trabajo académico de uso local. El `.env` solo contiene valores de desarrollo local (MySQL `root` sin contraseña).
