# Comandos SQL básicos para gestión de bases de datos y tablas

## Crear una base de datos

CREATE DATABASE IF NOT EXISTS tienda CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

text
**Explicación:** Crea la base de datos `tienda` si no existe, usando un charset moderno que soporta emojis y diferentes alfabetos.

## Seleccionar una base de datos

USE tienda;

text
**Explicación:** Cambia el contexto a la base que acabas de crear, para que los siguientes comandos operen ahí.

## Crear una tabla

CREATE TABLE productos (
id INT AUTO_INCREMENT PRIMARY KEY,
nombre VARCHAR(50) NOT NULL,
precio DECIMAL(10,2) NOT NULL,
stock INT DEFAULT 0
);

text
**Explicación:** Crea la tabla `productos` con una clave primaria, columnas básicas y restricciones para datos válidos.

## Modificar una tabla

ALTER TABLE productos ADD COLUMN descripcion TEXT AFTER nombre;

text
**Explicación:** Agrega una columna `descripcion` después de `nombre`.

## Eliminar tabla o base de datos

DROP TABLE IF EXISTS productos;
DROP DATABASE IF EXISTS tienda;

text
**Explicación:** Elimina la tabla o base de datos solo si existe, evitando errores.

## Insertar datos

INSERT INTO productos (nombre, precio, stock) VALUES ('Laptop', 1200.50, 15);

text
**Explicación:** Inserta un registro especificando valores para cada columna.

## Consultar datos

SELECT nombre, precio FROM productos WHERE stock > 0 ORDER BY precio DESC;

text
**Explicación:** Devuelve productos en stock, mostrando su nombre y precio, ordenados por precio de mayor a menor.

## Actualizar registros

UPDATE productos SET stock = stock - 1 WHERE id = 3;

text
**Explicación:** Resta una unidad al stock del producto con id 3.

## Eliminar registros

DELETE FROM productos WHERE id = 3;

text
**Explicación:** Elimina el producto cuyo id es 3. ¡Mucho cuidado al usar DELETE sin WHERE!

## Consultas avanzadas (JOIN, agrupación, límites)

SELECT p.nombre, c.nombre AS categoria
FROM productos p
JOIN categorias c ON p.categoria_id = c.id;

text
**Explicación:** Une dos tablas para mostrar el nombre del producto junto con su categoría.

### Otras cláusulas útiles

- **ORDER BY:** Ordena resultados (`ORDER BY precio ASC`)
- **GROUP BY:** Agrupa para cálculos agregados (`GROUP BY categoria_id`)
- **HAVING:** Filtra después de agrupar
- **LIMIT:** Limita la cantidad de resultados (`LIMIT 10`)

---

## Buenas prácticas

- Usa nombres descriptivos y consistentes (minúsculas, guiones bajos).
- Aplica restricciones (`NOT NULL`, `UNIQUE`, `FOREIGN KEY`).
- Verifica el diseño con:

DESCRIBE productos;

text
undefined
