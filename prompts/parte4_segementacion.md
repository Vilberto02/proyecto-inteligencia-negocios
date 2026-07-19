# Prompts - Parte 4: Segmentación de Clientes

### Tabla de registros

| **N°** | **Objetivo del prompt**                       | **Herramienta/Modelo** | **Resultado/Uso**                                            | **Ajustes del equipo**                                                                                                                             |
| ------ | --------------------------------------------- | ---------------------- | ------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1      | Selección de variables de negocio             | Asistente IA + Python  | Selección de variables de negocio adecuadas para el negocio. | Se seleccionaron variables de negocio que sean adecuadas para una botica.                                                                          |
| 2      | Optimización y escalado para K-Means          | Asistente IA + Python  | Optimización y escalado para K-Means                         | Se optimizó y escaló para K-Means para evitar desbalance en la distancia euclidiana.                                                               |
| 3      | Discusión sobre la elección de K (k=4 vs k=6) | Asistente IA           | Discusión sobre la elección de K                             | Se discutió sobre la elección de K, considerando que el número de clientes por clúster debe ser suficiente para aplicar estrategias diferenciadas. |
| 4      | Nomenclatura y estrategias                    | Asistente IA           | Nomenclatura y estrategias de fidelización                   | Se asignaron nombres y estrategias                                                                                                                 |

## Prompt 1: Selección de variables de negocio

```
Tengo una base de ventas de una botica y tengo las variables base RFM (Recencia, Frecuencia y Monto). Sin embargo, necesito agregar variables específicas del rubro farmacéutico para perfilar mejor mis clientes. ¿Qué otras variables serían apropiadas para incluir en el apartado de segmentación de clientes considerando que tengo un catálogo de productos clasificado en categorías como: Medicamentos,Cosmética,Cuidado Personal,Accesorios y Equipos,Nutrición y Suplementos,Primeros Auxilios,Salud y Bienestar,Cuidado Infantil,Cuidado Oral?
```

## Prompt 2: Optimización y escalado para K-Means

```
Estoy a punto de aplicar el algoritmo K-Means sobre las variables RFM (Recencia, Frecuencia y Monto), Afinidad a Promociones y Afinidad a Medicamentos. He notado que los montos están en miles de soles y las afinidades son porcentajes decimales, lo que generaría un desbalance en la distancia euclidiana. ¿Cuál sería la mejor práctica de escalado en Scikit-Learn antes de entrenar el modelo y cómo genero el Método del Codo y el Coeficiente de Silueta evaluando k del 2 al 10?
```

## Prompt 3: Discusión sobre la elección de K (k=4 vs k=6)

```text
Al analizar la gráfica del método del codo y el coeficiente de silueta, noto que el valor más apropiado matemáticamente para 'k' sería 6 (ya que tiene un pico de silueta de 0.37). Sin embargo, inicialmente en la guía del proyecto pensé en usar 4 clústeres para simplificar la estrategia. ¿Cuál es el impacto de utilizar un valor de 4 en el número de clusters con respecto al valor de 6 en el número e clusters?
Además, tengo problemas en la generación de las reglas de asociación al evaluar las canastas en base a subcategorías, ya que tengo una gran cantidad de productos y no he logrado obtener reglas interesantes. ¿Cómo podría ajustar el parámetro 'min_support' para obtener reglas más significativas?
```

## Prompt 4: Nomenclatura y estrategias

```text
Luego de ejecutar K-Means con k=6, extraje los promedios de mis centroides. Por ejemplo, un clúster tiene: Alta recencia (500 días), Baja frecuencia y Bajo gasto. Otro clúster destaca por: Alta afinidad a ofertas (86%), entonces, ¿qué nomenclatura me recomiendas para asignar nombres para identificar a los segmentos automáticamente a mi DataFrame, ya que no tengo muchas ideas de nombres? Luego de identificar los segmentos, necesito que me ayudes a pulir la redacción de 2 estrategias de negocio concretas de fidelización.
```
