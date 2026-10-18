# sql-select-fundamentals
consultas_basicas.sql
Readme

## 1. ¿Por qué es mala práctica usar `SELECT *` en producción?

Utilizar `SELECT *` en entornos productivos genera inconvenientes críticos:

- **Rendimiento y Red:** Obliga al motor de base de datos a procesar y transferir todas las columnas de la tabla (incluso aquellas con textos pesados o datos que la aplicación no va a utilizar), saturando el ancho de banda y la memoria RAM del servidor.
- **Mantenibilidad y Fragilidad:** Si la estructura de la tabla cambia en el futuro (por ejemplo, agregando columnas con datos sensibles o internos), una consulta con `SELECT *` los incluirá automáticamente, lo que puede romper la aplicación o comprometer información.
- **Incompatibilidad con Índices:** Impide el uso eficiente de índices de cobertura (*covering indexes*), forzando a la base de datos a realizar búsquedas más lentas (*table scans*).

---

## 2. Importancia de los alias para stakeholders no técnicos

Los alias (`AS`) son herramientas esenciales de comunicación, ya que permiten transformar nombres técnicos de columnas en lenguaje de negocio claro y accesible para usuarios que no pertenecen al área de sistemas.

### Ejemplo concreto:
Si se ejecuta una consulta sin alias:
```sql
SELECT total_amount FROM sales;
