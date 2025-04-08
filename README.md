
![Clasificador de palabras](/Users/patri/Desktop/ML_Clasificacion_palabras/scr/img/clasificacion-de-datos.png)

# Clasificación automática de palabras en euskara y castellano

## Problema a resolver

El objetivo de este proyecto es desarrollar un sistema automático que clasifique palabras individuales según su idioma: **euskara** o **castellano**. 

## Dataset

Se ha construido un dataset combinando dos fuentes:

- **Euskera**: palabras extraídas mediante **web scraping** desde tres artículos de Wikipedia en euskera:
  - https://eu.wikipedia.org/wiki/Berria
  - https://eu.wikipedia.org/wiki/Euskal_Herriko_historia
  - https://eu.wikipedia.org/wiki/Euskal_Herria

- **Castellano**: archivo `.txt` con un gran número de palabras del español (`0_palabras_todas.txt`).

Las palabras se almacenan con su respectiva etiqueta de idioma y se someten a un proceso de limpieza y normalización. El dataset original estaba desbalanceado, por lo que se ha reducido la clase mayoritaria (castellano) al doble del número de palabras en euskera para evitar sesgos durante el entrenamiento.

**Tipo de dataset:** 

Combinado (público + recurso local).  

**Acceso:**  
- El scraping de Wikipedia se puede reproducir ejecutando el notebook.
- El archivo `0_palabras_todas.txt` debe estar disponible localmente.

## Solución adoptada

El pipeline completo incluye:

1. Web scraping y carga de datos.
2. Preprocesamiento y limpieza.
3. Vectorización TF-IDF.
4. Entrenamiento de modelo Random Forest.
5. Evaluación con métricas estándar.
6. Clasificación interactiva de nuevas palabras.
7. Almacenamiento de resultados en SQL.

## Ejecución

### Desde notebook

1. Ejecuta el notebook `ML_project.ipynb` desde `src/results_notebook/`.
2. Al final del notebook podrás introducir nuevas palabras para clasificarlas.
3. Las predicciones se almacenarán automáticamente en una base de datos SQL.


##  Base de datos SQL

El sistema almacena automáticamente las palabras clasificadas en la base de datos `palabras_classified.db`, organizadas en dos tablas:

- `euskara`: palabras clasificadas como euskara
- `castellano`: palabras clasificadas como castellano


**Librerías utilizadas:**

- `pandas`, `numpy`
- `scikit-learn`
- `imbalanced-learn`
- `matplotlib`, `seaborn`
- `requests`, `beautifulsoup4`
- `XGBoost`
- `re`
- `sqlite3` 
- `joblib`


## Notebooks del proyecto

Este proyecto se compone de tres notebooks principales:

- `clasificador_palabras.ipynb`: notebook exploratorio donde se comparan distintos modelos (Logistic Regression, Random Forest, XGBoost con GridSearchCV). También se aplica SMOTE para el balanceo de clases y se realiza validación cruzada. Tras la comparación, se selecciona Random Forest como modelo final.
- `ML_project.ipynb`: pipeline limpio y final con el modelo Random Forest, listo para su ejecución y reproducción.
- `Ejemplo_modelo.ipynb`: notebook interactivo que permite cargar el modelo entrenado, introducir nuevas palabras y ver cómo se clasifican automáticamente, con almacenamiento en SQLite.


## Estructura del repositorio

El proyecto sigue la siguiente organización:

```
src/
│
├── data_sample/           # Archivos de datos de muestra utilizados (pequeños CSV o TXT reproducibles)
│   ├── palabras_euskera_completo.csv
│   └── 0_palabras_todas.txt
│
├── img/(gráficas, visualizaciones, etc.)
│   └── clasificacion-de-datos.png
│
├── notebooks/             # Notebooks usados para la fase exploratoria y pruebas
│   └── clasificador_palabras.ipynb
│   └── Ejemplo_modelo.ipynb
│
├── results_notebook/      # Notebook final con el pipeline limpio y funcional
│   └── ML_project.ipynb
│
├── models/                # Modelos entrenados y vectorizador guardados
│   ├── ML project.pkl
│   └── vectorizer.pkl
│
└── utils/
  
```

También se incluye un tercer notebook:

- `Ejemplo_modelo.ipynb`: ejemplo interactivo de uso del modelo entrenado, permitiendo introducir palabras nuevas y almacenarlas en la base de datos SQLite.

## Autora

Este proyecto ha sido desarrollado como práctica de aprendizaje automático con enfoque de clasificación de palabras bilingües.

Patricia Galdos
