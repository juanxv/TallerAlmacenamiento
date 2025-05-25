# Instalación
 (Para un entorno de notebook)
!pip install pyspark



# Descripción
Este proyecto realiza un análisis exploratorio de datos (EDA) y un modelo predictivo usando PySpark sobre un conjunto de datos de robos a personas en Colombia. Utiliza procesamiento distribuido para analizar la distribución de casos en el tiempo y por región, y posteriormente entrena un modelo para predecir con qué tipo de arma se llevaría a cabo un robo, basándose en variables sociodemográficas y geográficas.

# EDA

Se realiza una exploración inicial del dataset con los siguientes pasos:

Carga del dataset: Se utiliza spark.read.csv para cargar el archivo Hurto_a_personas_3_csv.csv.

Limpieza de columnas: Se renombran las columnas eliminando espacios y convirtiéndolas a minúsculas.

Consultas SQL sobre los datos para obtener:
Casos por año y mes.
Casos por municipio (Top 10).
Casos por departamento.
Casos agregados por mes (yyyy-MM).

Estas visualizaciones permiten entender la distribución espacial y temporal de los hurtos.

# Modelo

El objetivo del modelo es predecir el tipo de arma (armas_medios) que se utilizaría en un robo, dadas variables como:

Categorías: departamento, municipio, género, grupo de edad.

Numéricas: cantidad, año, mes.
Flujo del modelo:
Preprocesamiento:
Se extraen año y mes desde la columna fecha_hecho.
Se codifican las variables categóricas usando StringIndexer y OneHotEncoder.
Vectorización:
Todas las variables se combinan en una única columna de características usando VectorAssembler.

Entrenamiento:
Se utiliza un modelo RandomForestClassifier con los parámetros:
numTrees=80
maxDepth=12
seed=42

Todo se encapsula en un Pipeline de PySpark.

# Estructura del notebook

Setup y carga de datos
EDA con Spark SQL
Modelado con PySpark MLlib
Preparación de variables y entrenamiento del modelo