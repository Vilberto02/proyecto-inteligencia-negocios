# Proyecto de Inteligencia de Negocios

Solución Business Intelligence (BI) para una botica llamada Botica Los Andes.

#### Integrantes y roles

| **Integrante**            | **Roles**                                    |
| ------------------------- | -------------------------------------------- |
| Patricio Julca, Vilberto  | Líder del proyecto y editor de documentación |
| Coronel Callupe, Giovanni | Ingeniero de datos                           |
| CHavez Gave, Jose         | Arquitecto de BI                             |
| Tataje Guzman, Kenner     | Científico de datos                          |
| Cisneros Culaca, David    | Analista de negocio                          |

#### Herramientas tecnologicas

- Python
- Power BI
- GitHub
- Jupyter Notebooks
- VS Code

#### Librerías de python

- pandas
- numpy
- matplotlib
- seaborn
- plotly
- scikit-learn
- mlxtend
- faker
- statsmodels

#### Estructura del repositorio

```
proyecto-inteligencia-negocios/
├── data/
│   ├── raw/                        # Datos sintéticos crudos (con problemas de calidad)
│   └── processed/                  # Datos limpios listos para análisis y Power BI
├── notebooks/
│   ├── 00_generacion_datos.ipynb    # Generación reproducible de datos sintéticos
│   ├── 01_datamart_etl.ipynb        # Parte 1: ETL y modelo dimensional
│   ├── 02_visualizacion.ipynb       # Parte 2: visualizaciones en Python
│   ├── 03_clasificacion.ipynb       # Parte 3
│   ├── 04_segmentacion.ipynb        # Parte 4
│   ├── 05_asociacion.ipynb          # Parte 5
│   └── 06_regresion.ipynb           # Parte 6
├── powerbi/
│   └── AndesMarket.pbix              # Modelo, medidas DAX y tableros
├── prompts/
│   └── registro_prompts.md           # Bitácora de prompts (Anexo A y B)
├── informe/
│   └── Informe_PG_AndesMarket.pdf     # Informe consolidado
├── docs/
│   └── instrucciones_proyecto.pdf      # Guía de instrucciones del proyecto del curso
├── README.md                         # Descripción, integrantes, cómo ejecutar
└── requirements.txt                  # Dependencias de Python (versiones)
```
