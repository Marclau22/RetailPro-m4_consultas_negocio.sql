
-- ============================================================
-- Consulta 1 — Vista base del proyecto (INNER JOIN)
-- Combina ventas, clientes, productos, categorías y territorios
-- en una sola fila por venta. Es la fuente de datos principal
-- que se va a conectar a Power BI en M6.
-- ============================================================
SELECT
    v.fecha_venta                      AS fecha,
    c.nombre                           AS nombre_cliente,
    c.segmento                         AS segmento,
    t.region                           AS region,
    p.nombre_producto                  AS nombre_producto,
    cat.nombre_categoria               AS categoria,
    v.cantidad                         AS cantidad,
    v.precio_unitario                  AS precio_unitario,
    v.cantidad * v.precio_unitario     AS total_venta,
    v.canal                            AS canal
FROM ventas v
INNER JOIN clientes c     ON v.id_cliente = c.id_cliente
INNER JOIN productos p    ON v.id_producto = p.id_producto
INNER JOIN categorias cat ON p.id_categoria = cat.id_categoria
INNER JOIN territorios t  ON v.id_territorio = t.id_territorio
ORDER BY v.fecha_venta;


-- ============================================================
-- Consulta 2 — Clientes sin ventas (LEFT JOIN)
-- Identifica clientes registrados que aún no realizaron
-- ninguna compra.
-- ============================================================
SELECT
    c.nombre         AS nombre_cliente,
    c.email          AS email,
    c.fecha_registro AS fecha_registro
FROM clientes c
LEFT JOIN ventas v ON c.id_cliente = v.id_cliente
WHERE v.id_venta IS NULL;


-- ============================================================
-- Consulta 3 — Productos sin ventas (LEFT JOIN)
-- Identifica productos del catálogo que no tienen ninguna
-- venta registrada.
-- ============================================================
SELECT
    p.nombre_producto    AS nombre_producto,
    cat.nombre_categoria AS categoria,
    p.precio             AS precio
FROM productos p
INNER JOIN categorias cat ON p.id_categoria = cat.id_categoria
LEFT JOIN ventas v ON p.id_producto = v.id_producto
WHERE v.id_venta IS NULL;


-- ============================================================
-- Consulta 4 — Consolidado por canal (UNION ALL)
-- Combina las ventas Online y Presencial en un solo resultado,
-- y calcula el total facturado por canal.
-- ============================================================
SELECT
    canal,
    SUM(total_venta) AS total_por_canal
FROM (
    SELECT 'Online' AS canal, cantidad * precio_unitario AS total_venta
    FROM ventas
    WHERE canal = 'Online'

    UNION ALL

    SELECT 'Presencial' AS canal, cantidad * precio_unitario AS total_venta
    FROM ventas
    WHERE canal = 'Presencial'
) consolidado
GROUP BY canal;


-- ============================================================
-- Notas de resultados (verificado contra los datos de M3/M4)
-- ============================================================
-- - Consulta 2 y Consulta 3 devuelven 0 filas con los datos actuales:
--   los 5 clientes y los 6 productos cargados en M3 ya tienen al
--   menos una venta registrada. Es el resultado correcto, no un error;
--   ambas consultas quedan listas para detectar casos apenas
--   se agreguen nuevos clientes o productos sin movimiento.
-- - Consulta 4: Online facturó $4.560 y Presencial $1.884 sobre
--   el total del período cargado.
