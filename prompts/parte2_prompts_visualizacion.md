# Registro de prompts — Parte 2: Visualización de Datos

### Tabla de registros

| **N°** | **Objetivo del prompt**                                       | **Herramienta/Modelo** | **Resultado/Uso**                                                                     | **Ajustes del equipo**                                                                       |
| ------ | ------------------------------------------------------------- | ---------------------- | ------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| 1      | Desarrollo de visualizaciones analíticas (Tendencia, Pareto)  | Asistente IA + Python  | Notebook `02_visualizacion.ipynb` con scripts de Pandas y Seaborn                     | Se ajustó el código para no exportar imágenes locales y mantener el separador ";" al leer.   |
| 2      | Creación de medidas DAX (Inteligencia de Tiempo y Pareto)     | Asistente IA + DAX     | Medidas implementadas en el archivo `AndesMarket.pbix` para los gráficos de la página 4 | Se ajustó el formato de moneda a Soles (S/.) y la cardinalidad en la inteligencia de tiempo. |

---

### Prompt 1: Desarrollo de visualizaciones analíticas en Python

```text
## Rol

Actúa como **analista de datos** especializado en visualización con Python (Pandas, Matplotlib, Seaborn).
Trabajas con el Datamart procesado del proyecto "Botica Los Andes".

## Objetivo

Construir un script en un notebook Jupyter (.ipynb) que:
1. Cargue los datos limpios desde `data/processed/` (Fact_Ventas, Dim_Tiempo, Dim_Producto) considerando que están separados por punto y coma (`;`).
2. Integre el modelo dimensional mediante cruces (`merge`) utilizando las claves correspondientes.
3. Genere 3 gráficos analíticos sin exportar las imágenes a carpetas locales (mostrándolos únicamente con `plt.show()`):
   - **Gráfico de líneas:** Tendencia temporal mensual de ventas (identificando estacionalidad).
   - **Diagrama de Pareto:** Ventas por categoría (gráfico de doble eje Y: barras para el monto absoluto y línea con marcadores para el porcentaje acumulado, incluyendo una línea de referencia en el 80%).
   - **Mapa de calor (Heatmap):** Concentración de ventas cruzando Categoría y Mes (mostrando los valores en miles para mayor limpieza visual).

## Formato de salida

- Código de Python comentado paso a paso.
- Estructurado en celdas intercaladas (Markdown para la documentación gerencial y Código para la ejecución).
- Paleta de colores sobria, utilizando azules corporativos y rojos tenues para resaltar líneas clave.
```

---

### Prompt 2: Creación de medidas DAX (Inteligencia de Tiempo y Pareto)

```text
## Rol

Actúa como **desarrollador de Business Intelligence** especializado en DAX para Power BI.

## Objetivo

Crear las expresiones DAX necesarias para replicar el análisis temporal y la regla de Pareto (80/20) en el dashboard interactivo.
Necesito el código para las siguientes medidas:
1. `Total Ventas`: Suma del importe neto.
2. `Ventas Mes Anterior (MoM)`: Cálculo utilizando funciones de Time Intelligence (`DATEADD` o `PREVIOUSMONTH`).
3. `% Variación Mensual`: Cálculo del porcentaje de crecimiento respecto al mes anterior manejando posibles divisiones por cero.
4. `% Acumulado Pareto Categorías`: Cálculo del porcentaje acumulado dinámico que respete el contexto de filtro actual para rankear las categorías de mayor a menor ingreso.

## Formato de salida

- Código DAX limpio, indentado y formateado.
- Comentarios breves explicando la lógica de las funciones de modificación de contexto (como `CALCULATE`, `ALL`, `ISINSCOPE`).
```