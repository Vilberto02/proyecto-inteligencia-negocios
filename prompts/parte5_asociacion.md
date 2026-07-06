# Prompts - Parte 5: Minería de Reglas de Asociación

### Tabla de registros

| **N°** | **Objetivo del prompt**                                                          | **Herramienta/Modelo** | **Resultado/Uso**                                                             | **Ajustes del equipo**                                     |
| ------ | -------------------------------------------------------------------------------- | ---------------------- | ----------------------------------------------------------------------------- | ---------------------------------------------------------- |
| 1      | Transformación de tickets (Generación de matriz de ventas por ticket)            | Asistente IA + Python  | Matriz de ventas por ticket (One-Hot Encoding) con Join de dimensiones        | Se ajustó código para nuestro dataset                      |
| 2      | Ajuste de parámetros del algoritmo Apriori (soporte mínimo) para catálogo grande | Asistente IA           | Recomendación matemática del valor de `min_support` según tamaño del catálogo | Se calibró el parámetro para el tamaño del catálogo        |
| 3      | Estrategias de venta cruzada (Cross-Selling) basadas en reglas de asociación     | Asistente IA           | Estrategias operativas de marketing basadas en rules mining                   | Se aplicaron las reglas generadas por el algoritmo Apriori |

## Prompt 1: Transformación de tickets (One-Hot Encoding)

```text
Necesito construir las reglas de asociación del negocio de una botica, así que debo de utilizar el algoritmo A priori para ello, por lo que deberías de implementar la solución considerando que el dataset tiene columnas como id_venta, id_cliente, fecha, producto y cantidad, necesito transformar el dataset para obtener una matriz de ventas por ticket.

En base a lo anterior, genera el código en python para obtener una matriz de ventas por ticket y aplicarle el algoritmo Apriori, considerando que el dataset sigue un esquema estrella con dimensiones como Cliente, Producto, Promocion, Tiempo, Tienda y Fact_Ventas.
```

## Prompt 2: Ajuste de soporte mínimo para inventarios grandes

```text
Estoy ejecutando el algoritmo Apriori sobre un catálogo de aproximadamente 500 productos específicos. Al usar min_support = 0.01 (1%) me devuelve un DataFrame vacío. ¿A qué valor matemático me recomendarías bajar el parámetro 'min_support' para poder capturar combinaciones reales asumiendo que tengo 31,000 transacciones?
```

## Prompt 3: Estrategias de venta cruzada (Cross-Selling)

```text
De mi CSV generado, obtuve reglas interesantes, por ejemplo: la gente que compra 'Shampoo Anticaspa' tiene un Lift de 2.03 para comprar también 'Desodorante Roll-On'. Y los que llevan 'Toallitas Húmedas' llevan 'Talco Corporal'. En base a ello, ¿qué estrategias operativas de marketing podría aplicar en la botica?
```
