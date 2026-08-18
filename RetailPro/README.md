# RetailPro — Proyecto de Análisis de Datos

Proyecto integrador del curso de Data Analytics: pipeline completo desde el modelado de base de datos hasta un dashboard ejecutivo en Power BI, sobre un caso de negocio de una distribuidora de tecnología (RetailPro / TechStore).

## Contenido del repositorio

```
RetailPro/
├── m4_consultas_negocio.sql     # Consultas SQL de negocio (resumen mensual, ranking, clientes recurrentes)
├── m5_consultas_joins.sql       # Consultas con JOINs (vista base, clientes/productos sin ventas, UNION ALL por canal)
├── m5_extension_esquema.sql     # Extensión de esquema necesaria para M5 (tabla territorios, columnas canal/segmento)
├── M6/
│   └── Pipeline_ETL_Apellido_Nombre.pbix   # Pipeline ETL en Power BI (Power Query + limpieza)
├── M8/
│   └── Apellido_Nombre_Checkpoint2.pbix    # Modelo de datos con relaciones y medidas DAX
└── README.md
```

## Herramientas utilizadas

- **PostgreSQL** — motor de base de datos (`Ventas_Tech_DB`)
- **pgAdmin 4** — cliente de administración y ejecución de consultas SQL
- **Power BI Desktop** — ETL (Power Query / lenguaje M), modelado de datos y medidas DAX
- **GitHub** — control de versiones y entrega de los checkpoints del curso

## Cómo ejecutar los scripts SQL

1. Instalar PostgreSQL y pgAdmin 4.
2. Crear la base de datos `Ventas_Tech_DB` (ver script de creación del Módulo 3).
3. Abrir pgAdmin, conectarse al servidor, y en el **Query Tool** de `Ventas_Tech_DB` ejecutar en este orden:
   - Script de creación de tablas del Módulo 3 (DDL + carga inicial de datos).
   - `m5_extension_esquema.sql` (agrega la tabla `territorios` y las columnas `canal`/`segmento` necesarias para los JOINs).
   - `m4_consultas_negocio.sql` y `m5_consultas_joins.sql` (consultas de análisis, se pueden correr en cualquier orden entre sí).

## Cómo abrir los archivos de Power BI

Abrir los `.pbix` directamente con Power BI Desktop. El archivo de M8 (`Checkpoint2`) parte del de M6 y agrega el modelo de relaciones, la tabla de calendario y las medidas DAX (`_Medidas`).

## Estado del proyecto

Checkpoints entregados: M1 (brief), M2 (modelo relacional), M3 (base de datos), M4 (consultas SQL), M5 (JOINs), M6 (pipeline ETL), M7 (boceto de dashboard), M8 (modelo de datos + DAX). En curso: dashboard final e integración completa (M11).
