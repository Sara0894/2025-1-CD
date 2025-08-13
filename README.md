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
![image](https://github.com/Sara0894/2025-1-CD/blob/main/uno.png)
###### Se indica el tamaño del conjunto de datos (cantidad de registros y variables) y se muestran las primeras cinco filas, lo que facilita familiarizarse con el tipo de información incluida, como diagnóstico, edad, régimen, año, entre otros.

#### Información y estadísticas descriptivas:
```python
print("\nInformación de la base de datos:")
display(df_online.info()) 

print("\nEstadísticas descriptivas:")
display(df_online.describe(include='all')) 
```
![image](https://github.com/Sara0894/2025-1-CD/blob/main/dos.png)
###### Se obtiene un resumen que muestra el tipo de datos, la cantidad de valores faltantes y el número de registros por cada variable, además de incluir medidas descriptivas como frecuencias, valores máximos, mínimos y promedios.

#### Top 5 edades por diagnóstico:
```python
top_5 = df_online[['nombre_diagnostico', 'edad']].sort_values('edad', ascending=False).head(5)
print(top_5)

top_pacientes = df_online.sort_values('edad', ascending=False).head(5)
plt.figure(figsize=(10, 10))
sns.barplot(x='nombre_diagnostico', y='edad', data=top_pacientes, color='#BAD8B6')
plt.title('Top 5 edades de pacientes según su diagnóstico')
plt.xlabel('Diagnóstico')
plt.ylabel('Edad del paciente')
plt.xticks(rotation=45, ha='right')
plt.tight_layout()
plt.show()
```
![image](https://github.com/Sara0894/2025-1-CD/blob/main/tres.png)

###### Se identifican los 5 pacientes de mayor edad en la base de datos y sus respectivos diagnósticos, generando un gráfico de barras para visualizar la relación entre diagnóstico y edad.

###### **Análisis de resultados:**
###### Los datos muestran que los pacientes de mayor edad presentan diagnósticos asociados principalmente a tipos de cáncer con alta prevalencia en población adulta mayor, como cáncer de próstata, cáncer de colon y cáncer de pulmón. Esto es consistente con estudios epidemiológicos, donde el riesgo de desarrollar ciertos tipos de cáncer aumenta significativamente con la edad debido a la acumulación de mutaciones celulares y la disminución de la capacidad de reparación del ADN. Además, la presencia de pacientes de edad muy avanzada sugiere que, aunque estas enfermedades son graves, existe acceso a tratamiento y seguimiento que permite una mayor supervivencia en algunos casos. Esta información podría ser útil para orientar políticas de prevención, reforzando los programas de tamizaje en poblaciones mayores de 60 años.

#### Conteo de pacientes por régimen:
```python
Regimen_counts = df_online['regimen'].value_counts()
plt.figure(figsize=(10, 10))
Regimen_counts.plot(kind='bar', color='#CDC1FF')
plt.title('Conteo de Regímenes')
plt.xlabel('Régimen')
plt.ylabel('Conteo')
plt.xticks(rotation=45, ha='right')
plt.tight_layout()
plt.show()
```

![image](https://github.com/Sara0894/2025-1-CD/blob/main/cuatro.png)

###### Se realiza un conteo del número de pacientes por tipo de régimen (contributivo, subsidiado, etc.) y se grafica en un diagrama de barras.

###### Análisis de resultados:
###### Los resultados muestran que el régimen contributivo concentra la mayor cantidad de pacientes registrados con morbilidad por cáncer, seguido por el régimen subsidiado y, en menor medida, otros regímenes especiales o no clasificados. Esto sugiere que gran parte de los casos corresponden a personas con empleo formal o afiliadas al sistema por cotización, lo que podría indicar mayor acceso a diagnósticos y registro de la enfermedad en este grupo. Sin embargo, el número considerable de pacientes en el régimen subsidiado también resalta la presencia de la enfermedad en poblaciones con menores recursos económicos, donde las barreras de acceso a diagnóstico y tratamiento pueden ser más altas. Esta distribución refleja la necesidad de estrategias de detección temprana y tratamiento equitativo en todos los regímenes, especialmente en el subsidiado, para reducir desigualdades en salud.

#### Top 5 pacientes por edad y diagnóstico:
```python
top_pacientes = df_online[['nombre_diagnostico', 'edad']]

top_5 = top_pacientes.sort_values('edad', ascending=False).head(5)
print("Top 5 pacientes (diagnóstico y edad) de mayor a menor:")
print(top_5)
```
![image](https://github.com/Sara0894/2025-1-CD/blob/main/cinco.png)

###### En este paso se seleccionan únicamente las columnas nombre_diagnostico y edad para enfocarse en la relación entre ambas. Luego, se ordena la información de forma descendente según la edad, de manera que los pacientes de mayor edad aparezcan primero. Finalmente, se extraen las 5 primeras filas con head(5), que corresponden a los 5 pacientes más longevos de la base de datos junto con su diagnóstico, y se muestran en pantalla.
###### Análisis de resultados:
###### Por su prevalencia en edades avanzadas, reflejan la vulnerabilidad propia de este grupo poblacional, donde las comorbilidades y el deterioro del estado general pueden influir en la evolución de la enfermedad; este hallazgo subraya la importancia de implementar estrategias específicas de prevención, detección temprana y seguimiento para adultos mayores, así como la necesidad de adaptar los tratamientos oncológicos a sus condiciones particulares para mejorar su calidad de vida y pronóstico.

#### Top 10 pacientes con diagnóstico de "Tumor maligno del ciego"
```python
df_filtrado = df_online[df_online['nombre_diagnostico'] == 'TUMOR MALIGNO DEL CIEGO']


top_10_filtrado = df_filtrado.sort_values('edad', ascending=False).head(10)
print("\nTop 10 pacientes con diagnóstico TUMOR MALIGNO DEL CIEGO:")
print(top_10_filtrado[['nombre_diagnostico', 'edad']])


plt.figure(figsize=(10, 10))
sns.barplot(x=top_10_filtrado.index, y='edad', data=top_10_filtrado, color='#9EC6F3')
plt.title('Top 10 edades de pacientes con diagnóstico de Tumor maligno  del ciego')
plt.xlabel('Índice del paciente')
plt.ylabel('Edad del paciente')
plt.xticks(rotation=45, ha='right')
plt.tight_layout()
plt.show()
```
![image](https://github.com/Sara0894/2025-1-CD/blob/main/seis.png)

###### Se filtra la base de datos para conservar únicamente los registros cuyo diagnóstico sea "Tumor maligno del ciego". Posteriormente, se ordenan estos casos de forma descendente según la edad y se seleccionan los 10 pacientes más longevos, mostrando sus edades y diagnóstico. Para facilitar la interpretación visual, se genera un gráfico de barras donde el eje X representa el índice del paciente en el DataFrame y el eje Y su edad, lo que permite comparar rápidamente las edades de los casos más relevantes dentro de este diagnóstico.

###### Análisis de resultados:

###### El análisis revela que los pacientes con tumor maligno del ciego en el grupo de mayor edad presentan un rango etario elevado, lo que coincide con la tendencia epidemiológica de que la mayoría de los cánceres colorrectales se diagnostican en personas mayores, especialmente después de los 60 años. Esta información sugiere que el diagnóstico y la vigilancia en adultos mayores son cruciales para la detección temprana, dado que la edad avanzada es un factor de riesgo significativo. Además, este patrón resalta la importancia de promover campañas de tamizaje y control en la población de riesgo para reducir el diagnóstico en etapas avanzadas, cuando las opciones terapéuticas suelen ser más limitadas.

#### Top 5 pacientes más jóvenes con diagnóstico de "Tumor maligno del ciego"

```python
df_filtrado = df_online[df_online['nombre_diagnostico'] == 'TUMOR MALIGNO DEL CIEGO']

top_5_filtrado = df_filtrado.sort_values('edad', ascending=True).head(5)

print("\nTop 5 pacientes con menor edad de diagnóstico TUMOR MALIGNO DEL CIEGO:")
print(top_5_filtrado[['nombre_diagnostico', 'edad']])

top_5_filtrado = top_5_filtrado.reset_index(drop=True)

plt.figure(figsize=(10, 10))
sns.barplot(x=top_5_filtrado.index, y='edad', data=top_5_filtrado, color='#E6B2BA')
plt.title('Top 10 menores edades de pacientes con diagnóstico de Tumor maligno del ciego')
plt.xlabel('Índice del paciente')
plt.ylabel('Edad del paciente')
plt.xticks(rotation=45, ha='right')
plt.tight_layout()
plt.show()
```
![image](https://github.com/Sara0894/2025-1-CD/blob/main/siete.png)

###### Se filtra la base de datos para conservar únicamente los casos con diagnóstico de "Tumor maligno del ciego", y posteriormente se ordenan de menor a mayor edad para identificar a los 5 pacientes más jóvenes que lo presentan. Esta información se imprime en pantalla y se visualiza mediante un gráfico de barras donde el eje X corresponde al índice de cada paciente y el eje Y a su edad. El uso de un color distintivo facilita resaltar estos casos particulares.

###### Análisis de resultados:

###### La presencia de pacientes jóvenes con tumor maligno del ciego resulta significativa, ya que esta neoplasia es más común en adultos mayores y su aparición en edades tempranas podría estar asociada a factores genéticos, síndromes hereditarios como el cáncer colorrectal hereditario no polipósico (HNPCC) o la poliposis adenomatosa familiar, así como a estilos de vida y hábitos alimentarios de riesgo. Este hallazgo sugiere la necesidad de fortalecer los programas de detección precoz en poblaciones con antecedentes familiares y fomentar hábitos preventivos desde edades tempranas, ya que la detección a tiempo mejora considerablemente el pronóstico y las posibilidades de tratamiento exitoso.

#### Top 3 diagnósticos más comunes

```python
conteo_diagnosticos = df_online['nombre_diagnostico'].value_counts().head(3)

df_conteo = conteo_diagnosticos.reset_index()
df_conteo.columns = ['nombre_diagnostico', 'cantidad']

plt.figure(figsize=(10, 5))
sns.barplot(x='cantidad', y='nombre_diagnostico', data=df_conteo, color='#FADA7A')
plt.title('Top 3 diagnósticos más comunes')
plt.xlabel('Cantidad de diagnósticos')
plt.ylabel('Diagnóstico')
plt.tight_layout()
plt.show()
```
![image](https://github.com/Sara0894/2025-1-CD/blob/main/ocho.png)

###### Se realiza un conteo de los diagnósticos presentes en la base de datos y se seleccionan los tres más frecuentes. Posteriormente, se reorganiza esta información en un nuevo DataFrame con dos columnas: el nombre del diagnóstico y la cantidad de casos. Finalmente, se construye un gráfico de barras horizontales donde se representa la frecuencia de cada diagnóstico, facilitando la comparación visual entre ellos.
###### Análisis de resultados:

###### Los tres diagnósticos más comunes evidencian cuáles son los tipos de cáncer con mayor prevalencia en la población analizada de la ciudad Pereira. Este patrón puede reflejar la carga epidemiológica de estas enfermedades en el país y orientar a las autoridades sanitarias sobre dónde focalizar recursos y campañas de prevención. La alta frecuencia de estos diagnósticos podría estar relacionada con factores como estilos de vida, predisposición genética o exposición ambiental, y su identificación permite priorizar estrategias de detección temprana y tratamiento oportuno para reducir la mortalidad y mejorar el pronóstico en la población afectada.

#### Distribución de edad para los 4 diagnósticos más comunes

```python
top_4_diagnosticos = df_online['nombre_diagnostico'].value_counts().head(4).index

df_top5 = df_online[df_online['nombre_diagnostico'].isin(top_4_diagnosticos)]

plt.figure(figsize=(12, 12))
sns.boxplot(x='nombre_diagnostico', y='edad', data=df_top5, color='#B5828C')

plt.title('Distribución de Edad para los 4 Diagnósticos Más Comunes')
plt.xlabel('Diagnóstico')
plt.ylabel('Edad')
plt.xticks(rotation=45, ha='right')
plt.tight_layout()
plt.show()
```
![image](https://github.com/Sara0894/2025-1-CD/blob/main/nueve.png)

###### Se obtienen los cuatro diagnósticos con mayor frecuencia en la base de datos y se filtran los registros que corresponden a ellos. A partir de esta selección, se genera un gráfico de cajas (boxplot) para analizar la distribución de las edades en cada diagnóstico. El gráfico permite visualizar la mediana, los cuartiles y los valores atípicos, mostrando cómo varía la edad de los pacientes según el tipo de cáncer.

###### Análisis de resultados:

###### El análisis revela diferencias notables en la distribución etaria entre los cuatro diagnósticos más frecuentes. Algunos muestran concentraciones de pacientes en edades avanzadas, mientras que otros presentan una dispersión más amplia, con casos tanto jóvenes como mayores. La presencia de valores atípicos indica que ciertos diagnósticos pueden darse en edades inusuales, lo que podría estar relacionado con factores genéticos, condiciones predisponentes o diagnósticos incidentales. Esta información es útil para orientar estrategias de tamizaje específicas según el grupo etario predominante en cada tipo de cáncer y para investigar las razones detrás de casos fuera del rango habitual.
