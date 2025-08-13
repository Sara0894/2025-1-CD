# Análisis de morbilidad por cáncer en Colombia - Trabajo de acompañamiento
### Presentado por:  
### Valentina Cadavid Carmona
 
### Angie Rivera Ramírez

### Sara Judith Sequera Ruiz
------------
#### Este trabajo se centra en el análisis de una base de datos proveniente de Datos Abiertos Colombia, que incluye información sobre la morbilidad por cáncer en la ciudad de Pereira. Utilizando estos datos, se crearon códigos y representaciones visuales mediante el lenguaje Python, con el objetivo de simplificar su procesamiento y estudio; lo que posibilita el uso de técnicas estadísticas y de programación que facilitan la gestión de grandes cantidades de información y aseguran la exactitud de los resultados.
------------
#### Importar base de datos: 
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import requests


url_csv = "https://www.datos.gov.co/resource/utgq-6fdm.csv"
df_online = pd.read_csv(url_csv)
print(df_online.dtypes)

```

###### Se importan las bibliotecas pandas y numpy para el manejo y manipulación de datos; matplotlib y seaborn para la creación de visualizaciones; y requests para gestionar conexiones, aunque en este caso el archivo CSV se lee directamente desde una URL. La base de datos de morbilidad por cáncer, proveniente de Datos Abiertos Colombia en formato CSV, se descarga y se carga en un DataFrame usando pandas.
###### Este código tiene como propósito principal ser el punto de partida para un proceso de análisis de datos. 

#### Cambio de nombre de variable: 
```python
df_online = df_online.rename(columns={'a_o': 'año'})
```
###### Se corrige el nombre de la columna a_o para que aparezca como año, facilitando su interpretación y análisis.
#### Analisis exploratorio inicial: 
```python
# Análisis exploratorio inicial
print("BASE DE DATOS (MORBILIDAD POR CÁNCER)")
print(f"Filas: {df_online.shape[0]}, Columnas: {df_online.shape[1]}\n")
print("Primeras 5 filas:")
display(df_online.head())
```
###### Se indica el tamaño del conjunto de datos (cantidad de registros y variables) y se muestran las primeras cinco filas, lo que facilita familiarizarse con el tipo de información incluida, como diagnóstico, edad, régimen, año, entre otros.

#### Información y estadísticas descriptivas:
```python
print("\nInformación de la base de datos:")
display(df_online.info()) 

print("\nEstadísticas descriptivas:")
display(df_online.describe(include='all')) 
```
###### Se obtiene un resumen que muestra el tipo de datos, la cantidad de valores faltantes y el número de registros por cada variable, además de incluir medidas descriptivas como frecuencias, valores máximos, mínimos y promedios.
