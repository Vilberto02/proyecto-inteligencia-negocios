# Registro de prompts — Parte 3: Clasificación en BI

### Tabla de registros

| **N°** | **Objetivo del prompt**                                                        | **Herramienta/Modelo** | **Resultado/Uso**                                                                  | **Ajustes del equipo**                                                                                          |
| ------ | -------------------------------------------------------------------------------- | ----------------------- | ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| 1      | Construcción del notebook de clasificación (feature engineering, EDA, modelos) | Asistente IA + Python   | Notebook `03_clasificacion.ipynb` con tabla analítica, EDA, 3 modelos comparados y exportación de predicciones | Se ajustó el manejo de clientes sin compras registradas (recencia = antigüedad) y se agregó `pct_compras_con_promocion` como variable adicional |
| 2      | Interpretación del modelo y definición de niveles de riesgo para Power BI       | Asistente IA             | Criterio de importancia de variables y umbrales de `nivel_riesgo` (Bajo/Medio/Alto) | Se ajustaron los umbrales de riesgo de percentiles a cortes fijos (0.33 / 0.66) para que sean más fáciles de explicar en el tablero |

---

### Prompt 1: Construcción del notebook de clasificación

```
## Rol

Actúa como **científico de datos** especializado en modelos de clasificación para
problemas de churn en retail.
Trabajas con el datamart procesado de "Botica Salud Total" (data/processed/),
resultado de la Parte 1 (ETL) del proyecto.

## Objetivo

Construir un notebook Jupyter (03_clasificacion.ipynb) que:
1. Cargue Dim_Cliente, Dim_Producto y Fact_Ventas desde data/processed/ (separador ";").
2. Use la columna `churn` de Dim_Cliente como variable objetivo (ya viene calculada
   desde la generación de datos, no se recalcula).
3. Construya una tabla analítica por cliente con variables tipo RFM y variables
   adicionales:
   - antigüedad (desde fecha_alta)
   - recencia (días desde la última compra)
   - frecuencia (número de boletas distintas)
   - monto acumulado y ticket promedio
   - número de categorías distintas compradas
   - porcentaje de compras realizadas con promoción vigente
4. Trate el caso de clientes sin ninguna compra registrada en Fact_Ventas (rellenar
   variables de comportamiento con 0 y usar la antigüedad como recencia).
5. Haga un EDA breve: balance de clases, distribución de variables clave por clase
   (recencia, frecuencia, monto), tasa de abandono por segmento del programa y
   correlación entre variables numéricas.
6. Divida los datos en entrenamiento y prueba (75/25, estratificado, semilla 42).
7. Entrene y compare Regresión Logística, Árbol de Decisión y Random Forest, todos
   con manejo de clases desbalanceadas (class_weight="balanced").
8. Evalúe cada modelo con matriz de confusión, precisión, recall, F1 y ROC-AUC, y
   presente una tabla comparativa y las curvas ROC.
9. Interprete el modelo final mediante importancia de variables.

## Formato de salida

- Notebook con celdas Markdown explicativas y celdas de código sin comentarios
  excesivos.
- Gráficos con seaborn/matplotlib, paleta consistente con los notebooks anteriores
  del proyecto (azules corporativos).
- Sin exportar imágenes a carpetas locales, solo mostrar con plt.show().
```

---

### Prompt 2: Interpretación del modelo y niveles de riesgo para Power BI

```
## Rol

Actúa como **analista de datos** encargado de traducir un modelo de clasificación
de churn en una tabla que pueda consumir Power BI.

## Objetivo

A partir del modelo Random Forest ya entrenado sobre los clientes de Botica Salud
Total:
1. Explica qué variables pesan más en la predicción de abandono y por qué tiene
   sentido de negocio (relación con la forma en que se etiquetó el churn).
2. Genera una tabla de predicciones sobre el conjunto de prueba con: id_cliente,
   churn real, probabilidad de abandono y predicción del modelo.
3. Clasifica a cada cliente en un nivel de riesgo (Bajo/Medio/Alto) a partir de su
   probabilidad de abandono, usando cortes simples y fáciles de explicar en un
   tablero gerencial.
4. Exporta la tabla resultante a data/processed/ separada por ";" para que pueda
   importarse en Power BI como base de la página "Riesgo de abandono".

## Formato de salida

- Código Python limpio, sin comentarios innecesarios.
- Explicación breve en Markdown de la relación entre las variables más importantes
  y el negocio (qué acción de retención sugiere cada una).
```
