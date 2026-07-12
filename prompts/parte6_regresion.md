# Registro de prompts — Parte 6: Regresión / Pronóstico de Demanda

### Tabla de registros

| **N°** | **Objetivo del prompt**                                                                 | **Herramienta/Modelo** | **Resultado/Uso**                                     | **Ajustes del equipo**                                                                      |
| ------ | --------------------------------------------------------------------------------------- | ---------------------- | ----------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| 4      | Notebook de pronóstico de ventas diarias con 3 modelos, interpretación y exportación a CSV | Asistente IA + Python  | Notebook 06_regresion.ipynb completo con 7 pasos ejecutados | Se reemplazó feature importance por permutation importance; se corrigió discusión 6.4 |

---

### Prompt: Pronóstico de ventas diarias (Regresión)

```markdown
## Rol

Actúa como **científico de datos** especializado en modelos de regresión y pronóstico de demanda para retail. Trabajas con el datamart analítico de "Botica Salud Total" ubicado en `data/processed/`.

## Objetivo

Crear y ejecutar un notebook Jupyter (`06_regresion.ipynb`) que implemente los 7 pasos de la Parte 6 del proyecto para pronosticar ventas diarias. El notebook debe:

1. **Cargar datos:** Leer `Fact_Ventas.csv` y `Dim_Tiempo.csv` desde `data/processed/`.
2. **Definir variable objetivo:** Agregar `importe` por día (ventas diarias).
3. **Construir predictores:** `dia_sem_num`, `mes`, `trimestre`, `es_feriado`, `pct_promo`, `lag_1` (venta día anterior), `lag_7` (venta misma semana anterior), `rolling_7` (promedio móvil 7 días), `tendencia` (días desde inicio). No usar `transacciones` ni `cantidad` como predictores. No convertir categóricas a dummies.
4. **Split temporal 80/20:** Ordenar por fecha, primeros 80% para entrenar, últimos 20% para test.
5. **Entrenar 3 modelos:** Regresión Lineal, Random Forest (n_estimators=100), Gradient Boosting (parámetros por defecto).
6. **Evaluar:** Para cada modelo calcular MAE, RMSE, MAPE y R² en el conjunto de test. Identificar el mejor modelo.
7. **Interpretar:**
   - Mostrar gráfico comparativo real vs pronóstico del mejor modelo en test.
   - Mostrar importancia de predictores usando **permutation importance** (NO coeficientes crudos, porque las escalas de las variables son dispares).
   - Pronosticar la próxima semana (7 días siguientes al último día del histórico).
8. **Exportar:** Guardar `data/processed/real_vs_pronostico.csv` con columnas `fecha`, `real`, `pronostico_rl` (145 filas del conjunto de test).

## Problemas conocidos a evitar

| Problema | Solución aplicada |
|---|---|
| Coeficientes de RL no comparables por escalas dispares (tendencia está en 0-730, pct_promo en 0-1, etc.) | Usar `permutation_importance` de `sklearn.inspection` en lugar de `np.abs(rl.coef_)` |
| Gradient Boosting con parámetros por defecto produce R² negativo (~ -2.4) | Mantenerlo en la comparación pero no usarlo para el pronóstico; el modelo principal es Regresión Lineal |
| La discusión 6.4 debe reflejar los resultados reales del modelo | Asegurar que números (pronóstico semanal, MAPE, R²) coincidan con la salida del notebook |

## Formato de salida

- Notebook ejecutado paso a paso (27 celdas, 7 pasos numerados)
- Celdas Markdown explicativas al inicio de cada paso
- Gráficos: distribución de ventas, comparación real vs pronóstico, importancia de predictores, pronóstico semanal
- CSV: `data/processed/real_vs_pronostico.csv` con separador `";"` y UTF-8
- Diccionario del CSV exportado incluido en la celda final
```
