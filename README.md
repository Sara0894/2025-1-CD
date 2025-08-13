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
