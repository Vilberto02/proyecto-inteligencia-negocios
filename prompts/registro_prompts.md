# Registro de prompts

### Tabla de registros

| **N°** | **Objetivo del prompt**                           | **Herramienta/Modelo** | **Resultado/Uso**                     | **Ajustes del equipo**                       |
| ------ | ------------------------------------------------- | ---------------------- | ------------------------------------- | -------------------------------------------- |
| 1      | Diseñar el esquema dimensional del caso           | Asistente IA           | Borrador del modelo estrella revisado | Se ajustó el grano y se añadió Dim_Promocion |
| 2      | Generar datos sintéticos con problemas de calidad | Asistente IA + Python  | Script de generación reproducible     | Se calibraron volúmenes y % de nulos         |

### Registro de prompts

##### B.1 Prompt para diseñar el caso y el modelo dimensional.

```markdown
Actúa como arquitecto de Business Intelligence. Diseña el modelo dimensional
(esquema estrella) para una cadena ficticia de retail omnicanal en Perú llamada
"AndesMarket S.A.C." que opera supermercados físicos y un canal online, con un
programa de fidelización. El modelo debe permitir analizar ventas, predecir
abandono de clientes, segmentar clientes, descubrir reglas de asociación y
pronosticar la demanda.
Entrega:

1. El proceso de negocio y el grano de la tabla de hechos.
2. Las dimensiones (Cliente, Producto, Tienda, Tiempo, Promoción) con sus campos.
3. La tabla de hechos Fact_Ventas con sus métricas (cantidad, precio, descuento,
   importe, costo, margen).
4. Un diagrama textual del esquema estrella y un diccionario de datos.
```


# Prompt: Generador de Datos Sintéticos – Botica

## Rol

Actúa como **ingeniero de datos**. Genera un script de Python (usando `pandas`, `numpy` y `faker`, con locale `"es_ES"`) que cree datos sintéticos **REPRODUCIBLES** para una empresa ficticia que es una botica. Fija la semilla **42** en `numpy` y `faker`.

---

## Volúmenes (referenciales)

| Tabla | Filas aprox. | Columnas |
|---|---|---|
| `Dim_Cliente` | ~5,000 | `id_cliente`, `nombre`, `sexo`, `fecha_nacimiento`, `distrito`, `fecha_alta`, `segmento_programa` |
| `Dim_Producto` | ~500 | `id_producto`, `nombre`, `categoria`, `subcategoria`, `marca`, `precio_lista`, `costo` |
| `Dim_Tienda` | ~15 | `id_tienda`, `nombre`, `canal` [`fisico`/`online`], `region`, `ciudad` |
| `Dim_Tiempo` | ~730 (2 años) | `fecha`, `dia`, `mes`, `trimestre`, `anio`, `dia_semana`, `es_feriado` |
| `Dim_Promocion` | ~40 | `id_promocion`, `nombre`, `tipo`, `descuento_pct`, `fecha_inicio`, `fecha_fin` |
| `Fact_Ventas` | 60,000 líneas | `id_venta`, `fecha`, `id_cliente`, `id_producto`, `id_tienda`, `id_promocion`, `cantidad`, `precio_unitario`, `descuento` |

---

## Reglas de realismo

- **Estacionalidad:** mayor volumen de ventas en julio y diciembre; menor en meses bajos.
- **Concentración tipo Pareto:** ~20% de productos genera ~80% de las ventas; pocos clientes muy frecuentes y muchos esporádicos.
- **Precio:** `precio_unitario` varía +/- alrededor de `precio_lista`; el descuento aplica solo si la venta cae dentro de una promoción vigente.
- **Afinidad de canasta:** algunas categorías tienden a comprarse juntas, de modo que existan reglas de asociación con `lift > 1`.
- **Abandono (churn):** ~20-25% de clientes deja de comprar luego de cierto periodo; agregar una columna/lógica que permita etiquetar el abandono para clasificación.

---

## Problemas de calidad a introducir (en los archivos `data/raw`)

- Fechas en formatos **mixtos**: `dd/mm/aaaa`, `aaaa-mm-dd`, y algunas como texto.
- Valores faltantes (~3-8%) en `descuento`, `distrito` y `categoria`.
- Duplicar ~1-2% de las líneas de venta.
- Texto inconsistente en `categoria`: mayúsculas/minúsculas y espacios sobrantes.
- Errores de tipeo: variantes como `"Ibuprofeno"` / `"IBUPROFENO"`, incluso respecto a tildes.
- Outliers: algunas cantidades y precios extremos poco realistas.
- ~0.5% de `id_producto` en `Fact_Ventas` que **NO** existen en `Dim_Producto` (claves huérfanas).

---

## Salida esperada

- Guardar cada tabla como CSV separado por `;` y codificación UTF-8 en `data/raw/` (versión con problemas).
- Dejar las tablas `Dim_*` limpias en `data/processed/` cuando aplique.
- Imprimir un resumen: número de filas por tabla, % de nulos por columna, número de duplicados y de claves huérfanas, para evidenciar el estado inicial de calidad.