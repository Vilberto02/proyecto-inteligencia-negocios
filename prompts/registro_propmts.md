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
