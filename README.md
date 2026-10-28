# SistemaSoporte

Aplicación web para gestionar tickets de soporte, clientes y equipos de atención. Permite seguir cada caso, registrar comentarios y archivos adjuntos, y controlar sus costos y estado de facturación.

## Funcionalidades

- Inicio de sesión y acceso según los roles de administrador, agente y supervisor.
- Creación, asignación y seguimiento de tickets por estado y tipo de caso.
- Comentarios, archivos adjuntos e historial de cambios en los casos.
- Gestión de clientes, usuarios y tipos de caso.
- Registro de costos, moneda, estado de facturación y medio de pago.
- Panel de indicadores y gráficos, impresión y exportación de tickets y clientes a PDF y Excel.

## Tecnologías

PHP · MySQL/MariaDB · PDO · Composer · Bootstrap 5 · Chart.js · FPDF · PhpSpreadsheet

## Instalación y configuración

Requiere **PHP 8.1 o superior**, **Composer** y **MySQL o MariaDB**. Habilita `pdo_mysql` y las extensiones necesarias para PhpSpreadsheet, como `mbstring`, `gd`, `zip` y XML. Composer comprueba los requisitos al instalar.

```bash
git clone https://github.com/thoonidev/SistemaSoporte.git
cd SistemaSoporte
composer install
```

1. Crea una base de datos llamada `soporte_db` e importa `soporte_db.sql` mediante phpMyAdmin o tu cliente SQL. Utiliza una base vacía; el script incluye estructura y datos de ejemplo.
2. Crea la carpeta `config/` y el archivo `config/database.php` con tus credenciales:

```php
<?php
$pdo = new PDO(
    'mysql:host=localhost;dbname=soporte_db;charset=utf8mb4',
    'tu_usuario',
    'tu_password',
    [
        PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
        PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
    ]
);
```

Este archivo está excluido de Git. La aplicación crea archivos en `uploads/`; el servidor debe tener permisos de escritura en esa carpeta.

## Ejecución local

Desde la raíz del proyecto:

```bash
php -S localhost:8000
```

Abre `http://localhost:8000/crear_usuario.php` y crea una cuenta con el rol **Administrador**. Después, ingresa en `http://localhost:8000/public/login.php` con el correo y la contraseña que elegiste.

El script `crear_usuario.php` es una utilidad inicial sin control de acceso: retíralo del servidor después de crear la cuenta. Los siguientes usuarios pueden administrarse desde el panel.

## Notas de configuración

- Los nombres de las tablas del script están en minúsculas, mientras que algunas consultas usan mayúsculas. En servidores donde MySQL distingue entre ambas, debes unificar los nombres antes de ejecutar la aplicación.
- Bootstrap, sus iconos y Chart.js se cargan desde CDN y requieren conexión a Internet.
- Las cuentas del SQL contienen contraseñas cifradas; crea tu cuenta local en lugar de asumir una contraseña para los usuarios de ejemplo.
