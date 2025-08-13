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

#### Top 5 edades por diagnóstico:
```python
top_5 = df_online[['nombre_diagnostico', 'edad']].sort_values('edad', ascending=False).head(5)
print(top_5)

top_pacientes = df_online.sort_values('edad', ascending=False).head(5)
plt.figure(figsize=(10, 7))
sns.barplot(x='nombre_diagnostico', y='edad', data=top_pacientes, color='#BAD8B6')
plt.title('Top 5 edades de pacientes según su diagnóstico')
plt.xlabel('Diagnóstico')
plt.ylabel('Edad del paciente')
plt.xticks(rotation=45, ha='right')
plt.tight_layout()
plt.show()
```

###### Se identifican los 5 pacientes de mayor edad en la base de datos y sus respectivos diagnósticos, generando un gráfico de barras para visualizar la relación entre diagnóstico y edad.

###### **Análisis de resultados:**
###### Los datos muestran que los pacientes de mayor edad presentan diagnósticos asociados principalmente a tipos de cáncer con alta prevalencia en población adulta mayor, como cáncer de próstata, cáncer de colon y cáncer de pulmón. Esto es consistente con estudios epidemiológicos, donde el riesgo de desarrollar ciertos tipos de cáncer aumenta significativamente con la edad debido a la acumulación de mutaciones celulares y la disminución de la capacidad de reparación del ADN. Además, la presencia de pacientes de edad muy avanzada sugiere que, aunque estas enfermedades son graves, existe acceso a tratamiento y seguimiento que permite una mayor supervivencia en algunos casos. Esta información podría ser útil para orientar políticas de prevención, reforzando los programas de tamizaje en poblaciones mayores de 60 años.

#### Conteo de pacientes por régimen:
```python
Regimen_counts = df_online['regimen'].value_counts()
plt.figure(figsize=(10, 7))
Regimen_counts.plot(kind='bar', color='#CDC1FF')
plt.title('Conteo de Regímenes')
plt.xlabel('Régimen')
plt.ylabel('Conteo')
plt.xticks(rotation=45, ha='right')
plt.tight_layout()
plt.show()
```
###### Se realiza un conteo del número de pacientes por tipo de régimen (contributivo, subsidiado, etc.) y se grafica en un diagrama de barras.

###### Análisis de resultados:
###### Los resultados muestran que el régimen contributivo concentra la mayor cantidad de pacientes registrados con morbilidad por cáncer, seguido por el régimen subsidiado y, en menor medida, otros regímenes especiales o no clasificados. Esto sugiere que gran parte de los casos corresponden a personas con empleo formal o afiliadas al sistema por cotización, lo que podría indicar mayor acceso a diagnósticos y registro de la enfermedad en este grupo. Sin embargo, el número considerable de pacientes en el régimen subsidiado también resalta la presencia de la enfermedad en poblaciones con menores recursos económicos, donde las barreras de acceso a diagnóstico y tratamiento pueden ser más altas. Esta distribución refleja la necesidad de estrategias de detección temprana y tratamiento equitativo en todos los regímenes, especialmente en el subsidiado, para reducir desigualdades en salud.
