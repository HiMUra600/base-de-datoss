<?php
/*
 * This is needed for cookie based authentication to encrypt password in
 * cookie
 */
$cfg['blowfish_secret'] = 'xampp'; /* YOU SHOULD CHANGE THIS FOR A MORE SECURE COOKIE AUTH! */

/*
 * Servers configuration
 */
$i = 0;

/*
 * First server
 */
$i++;

/* Authentication type and info */
$cfg['Servers'][$i]['auth_type'] = 'config';
$cfg['Servers'][$i]['user'] = 'root';
$cfg['Servers'][$i]['password'] = '0000';
$cfg['Servers'][$i]['extension'] = 'mysqli';
$cfg['Servers'][$i]['AllowNoPassword'] = true;
$cfg['Lang'] = '';

/* Bind to the localhost ipv4 address and tcp */
$cfg['Servers'][$i]['host'] = '127.0.0.1';
$cfg['Servers'][$i]['connect_type'] = 'tcp';

/* User for advanced features */
$cfg['Servers'][$i]['controluser'] = 'pma';
$cfg['Servers'][$i]['controlpass'] = '';

/* Advanced phpMyAdmin features */
$cfg['Servers'][$i]['pmadb'] = 'phpmyadmin';
$cfg['Servers'][$i]['bookmarktable'] = 'pma__bookmark';
$cfg['Servers'][$i]['relation'] = 'pma__relation';
$cfg['Servers'][$i]['table_info'] = 'pma__table_info';
$cfg['Servers'][$i]['table_coords'] = 'pma__table_coords';
$cfg['Servers'][$i]['pdf_pages'] = 'pma__pdf_pages';
$cfg['Servers'][$i]['column_info'] = 'pma__column_info';
$cfg['Servers'][$i]['history'] = 'pma__history';
$cfg['Servers'][$i]['designer_coords'] = 'pma__designer_coords';
$cfg['Servers'][$i]['tracking'] = 'pma__tracking';
$cfg['Servers'][$i]['userconfig'] = 'pma__userconfig';
$cfg['Servers'][$i]['recent'] = 'pma__recent';
$cfg['Servers'][$i]['table_uiprefs'] = 'pma__table_uiprefs';
$cfg['Servers'][$i]['users'] = 'pma__users';
$cfg['Servers'][$i]['usergroups'] = 'pma__usergroups';
$cfg['Servers'][$i]['navigationhiding'] = 'pma__navigationhiding';
$cfg['Servers'][$i]['savedsearches'] = 'pma__savedsearches';
$cfg['Servers'][$i]['central_columns'] = 'pma__central_columns';
$cfg['Servers'][$i]['designer_settings'] = 'pma__designer_settings';
$cfg['Servers'][$i]['export_templates'] = 'pma__export_templates';
$cfg['Servers'][$i]['favorite'] = 'pma__favorite';

-- Crear la base de datos
CREATE DATABASE IF NOT EXISTS web_empresa;

-- Usar la base de datos creada
USE web_empresa;

-- Tabla para almacenar información de productos
CREATE TABLE IF NOT EXISTS productos (
id INT PRIMARY KEY,
nombre VARCHAR(255) NOT NULL,
descripcion TEXT,
precio DECIMAL(10, 2) NOT NULL,
stock INT DEFAULT 0,
fecha_creacion TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Tabla para almacenar información de servicios
CREATE TABLE IF NOT EXISTS servicios (
id INT PRIMARY KEY,
nombre VARCHAR(255) NOT NULL,
descripcion TEXT,
precio DECIMAL(10, 2) NOT NULL,
fecha_creacion TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Tabla para almacenar información de clientes
CREATE TABLE IF NOT EXISTS clientes (
id INT PRIMARY KEY,
nombre VARCHAR(255) NOT NULL,
email VARCHAR(255) NOT NULL UNIQUE,
telefono VARCHAR(20),
direccion TEXT,

fecha_registro TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Tabla para almacenar información de pedidos
CREATE TABLE IF NOT EXISTS pedidos (
id INT PRIMARY KEY,
id_cliente INT,
fecha_pedido TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
total DECIMAL(10, 2) NOT NULL,
estado ENUM(pendiente, completado, cancelado,) DEFAULT pendiente,
FOREIGN KEY (id_cliente) REFERENCES clientes(id) ON DELETE CASCADE
);

-- Tabla para almacenar los productos de cada pedido
CREATE TABLE IF NOT EXISTS pedidos_productos (
id INT PRIMARY KEY,
id_pedido INT,
id_producto INT,
cantidad INT NOT NULL,
FOREIGN KEY (id_pedido) REFERENCES pedidos(id) ON DELETE
CASCADE,
FOREIGN KEY (id_producto) REFERENCES productos(id) ON DELETE
CASCADE
);

-- Tabla para almacenar los servicios de cada pedido
CREATE TABLE IF NOT EXISTS pedidos_servicios (
id INT PRIMARY KEY,
id_pedido INT,
id_servicio INT,
cantidad INT NOT NULL,
FOREIGN KEY (id_pedido) REFERENCES pedidos(id) ON DELETE
CASCADE,

FOREIGN KEY (id_servicio) REFERENCES servicios(id) ON DELETE
CASCADE
);
/*
 * End of servers configuration
 */

?>

