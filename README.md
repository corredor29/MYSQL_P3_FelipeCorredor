# 📒 Guía rápida de SQL: Gestión de bases de datos y tablas

## 📚 Índice

- [Crear y seleccionar base de datos](#crear-y-seleccionar-base-de-datos)
- [Gestión de tablas](#gestión-de-tablas)
- [Manipulación y consulta de datos](#manipulación-y-consulta-de-datos)
- [Consultas avanzadas y relaciones](#consultas-avanzadas-y-relaciones)
- [Administración y buenas prácticas](#administración-y-buenas-prácticas)
- [Referencias útiles](#referencias-útiles)

---

## Crear y seleccionar base de datos

CREATE DATABASE IF NOT EXISTS tienda CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
USE tienda;

text
**Crea la base `tienda` si no existe y la selecciona como contexto para operaciones posteriores.**  
*Se recomienda `utf8mb4` para compatibilidad global y uso de emojis.*

---

## Gestión de tablas

### Crear tabla

CREATE TABLE productos (
id INT AUTO_INCREMENT PRIMARY KEY,
nombre VARCHAR(50) NOT NULL,
precio DECIMAL(10,2) NOT NULL,
stock INT DEFAULT 0,
categoria_id INT,
descripcion TEXT
);

text
**Tabla productos:** Clave primaria, datos básicos y columna de relación.

### Modificar tabla

ALTER TABLE productos ADD COLUMN fecha_creacion DATETIME DEFAULT CURRENT_TIMESTAMP AFTER stock;

text
*Agrega una columna para registrar la fecha de creación del producto.*

### Eliminar tabla

DROP TABLE IF EXISTS productos;

text
*Evita errores si la tabla ya no existe.*

---

## Manipulación y consulta de datos

### Insertar registros

INSERT INTO productos (nombre, precio, stock) VALUES ('Laptop',1200.50,15);

text

### Consultar productos en stock y ordenados

SELECT nombre, precio FROM productos WHERE stock > 0 ORDER BY precio DESC;

text

### Actualizar productos

UPDATE productos SET stock = stock - 1 WHERE id = 3;

text

### Eliminar registros puntuales

DELETE FROM productos WHERE id = 3;

text
**¡Precaución!** Eliminar sin WHERE borra todos los registros.

---

## Consultas avanzadas y relaciones

### Join entre productos y categorías

SELECT p.nombre, c.nombre AS categoria
FROM productos p
JOIN categorias c ON p.categoria_id = c.id;

text

### Agrupaciones y agregados

SELECT categoria_id, COUNT(*) AS cantidad FROM productos GROUP BY categoria_id HAVING cantidad > 5;

text
*Consulta cuántos productos hay por categoría, solo mostrando categorías con más de 5 productos.*

### Limitar resultados

SELECT nombre FROM productos LIMIT 10;

text
*Solo muestra los 10 primeros productos.*

---

## Administración y buenas prácticas

- Usa nombres descriptivos y consistentes (minúsculas, guion bajo).
- Aplica restricciones (`NOT NULL`, `UNIQUE`, `FOREIGN KEY`).
- Verifica las estructuras:

DESCRIBE productos;
SHOW TABLES;
SHOW DATABASES;

text

### Ejemplo de clave foránea

ALTER TABLE productos
ADD CONSTRAINT fk_categoria
FOREIGN KEY (categoria_id) REFERENCES categorias(id);

text

### Consejos de normalización

- Evita la redundancia de datos.
- Cada columna debe contener solo un valor (atómico).
- Usa claves primarias y foráneas para relaciones seguras.

---

## Referencias útiles

- [w3schools SQL](https://www.w3schools.com/sql/)
- [MySQL Reference Manual](https://dev.mysql.com/doc/)
- [Campuslands SQL Practice](https://camper.campuslands.com/)

---

> **Nota:** Esta guía está orientada a principiantes y sirve como referencia rápida para operaciones comunes en bases de datos relacionales.
