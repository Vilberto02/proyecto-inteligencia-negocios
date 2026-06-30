# Registro de prompts — Parte 1: Datamart Analítico

### Tabla de registros

| **N°** | **Objetivo del prompt**                                       | **Herramienta/Modelo** | **Resultado/Uso**                                                     | **Ajustes del equipo**                                                       |
| ------ | ------------------------------------------------------------- | ---------------------- | --------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| 3      | ETL y construcción del datamart analítico desde datos crudos  | Asistente IA + Python  | Notebook 01_datamart_etl.ipynb con limpieza, métricas y exportación   | Se ajustó la fórmula de importe (descuento como monto, no porcentaje)        |

---

### Prompt: ETL y construcción del datamart analítico

```
## Rol

Actúa como **ingeniero de datos** especializado en procesos ETL para Business Intelligence.
Trabajas con los datos sintéticos de "Botica Salud Total" generados previamente.

## Objetivo

Construir un pipeline ETL en Python (notebook Jupyter) que:
1. Cargue los datos crudos desde `data/raw/` (6 CSVs: Dim_Cliente, Dim_Producto, Dim_Tienda, Dim_Tiempo, Dim_Promocion, Fact_Ventas)
2. Reporte métricas de calidad iniciales (nulos por columna, duplicados, claves huérfanas, outliers)
3. Estandarice fechas en formato mixto (dd/mm/aaaa, aaaa-mm-dd, texto en español como "10 de mayo de 2024")
4. Normalice el texto de categorías (mayúsculas/minúsculas/espacios/tildes → nombres estandarizados)
5. Trate nulos según regla de negocio (distrito → "Sin Especificar", descuento → 0.0)
6. Elimine filas duplicadas en Fact_Ventas
7. Elimine claves huérfanas (id_producto sin referencia en Dim_Producto)
8. Corrija outliers (cantidad >100 → mediana, precio_unitario <1 o >1000 → precio_lista)
9. Derive métricas calculadas:
   - importe = (cantidad * precio_unitario) - descuento
   - costo = cantidad * costo (desde Dim_Producto)
   - margen = importe - costo
10. Exporte las 6 tablas limpias a `data/processed/` (un CSV por tabla, separador ";", UTF-8)
11. Elabore un diccionario de datos con: tabla, campo, tipo, clave (PK/FK) y descripción
12. Incluya un diagrama textual del esquema estrella

## Problemas de calidad a resolver

| Problema | Tabla | Solución |
|---|---|---|
| Fechas en 3 formatos mixtos | Fact_Ventas, Dim_Cliente | Limpiar texto español y convertir con dayfirst=True |
| Nulos en distrito (~6.44%) | Dim_Cliente | Imputar con "Sin Especificar" |
| Nulos en categoria (~6.20%) | Dim_Producto | Imputar con "Sin Categoría" |
| Nulos en descuento (~5.36%) | Fact_Ventas | Imputar con 0.0 |
| Texto sucio en categoría (35 variantes) | Dim_Producto | strip + upper + homologación |
| Duplicados (~1.5%) | Fact_Ventas | drop_duplicates() |
| Claves huérfanas (~0.5%) | Fact_Ventas | Filtrar id_producto no existentes |
| Outliers en cantidad (>100) | Fact_Ventas | Reemplazar con mediana |
| Outliers en precio_unitario (<1 o >1000) | Fact_Ventas | Reemplazar con precio_lista |

## Formato de salida

- Notebook ejecutado paso a paso con celdas Markdown explicativas
- Reportes de calidad antes y después del ETL
- Diccionario de datos exportado como CSV
- Diagrama del esquema estrella en Markdown
```
