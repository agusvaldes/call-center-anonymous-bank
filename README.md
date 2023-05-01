# Dashboard Call Center Anonymous Bank

Este dashboard de Power BI muestra las operaciones del call center del banco Anonymous Bank para el año 1999.




![Logo](https://github.com/agusvaldes/call-center-anonymous-bank/blob/main/github_files/1.png?raw=true)

## Dataset

Para el presente trabajo se utilizó un dataset que fue proporcionado por Henry dentro del bootcamp de Data Science y que formó parte de la serie de proyectos integradores del módulo Data Analytics.
El mismo consta de 444.448 filas y 18 columnas. Para información acerca del contenido del dataset, atributos e información relevante se utilizó el documento denominado
"Ejercicio Call Center - Descripción del DataSet.docx"

[Diccionario de datos](https://github.com/agusvaldes/call-center-anonymous-bank/blob/main/Descripci%C3%B3n%20del%20DataSet.docx)
## Objetivo

El propósito del trabajo fue describir las operaciones del call center en función de las variables del negocio y proponer mejoras para el segmento premium de clientes.

Las consignas consistieron en investigar: 
- Meses en los que se registraron mayor cantidad de llamadas,
- Distribución de llamadas por motivo (tipo de servicio),
- Análisis de llamadas por resultado,
- Composición de la cartera de clientes,
- Detección de tiempos promedio de espera en VRU (contestador automático), en cola y en servicio para el segmento de clientes premium,
- Tipos de solicitudes para segmento premium,
- Picos de demanda de clientes premium,
- TOP 10 de clientes premium en función del número de llamadas.
## ETL - Limpieza, transformación y carga de datos 

Para realizar los procesos de ETL se utilizó la herramienta de Power BI denominada Power Query. 
Se optó por dividir el dataset en 1 tabla de transacciones y 4 tablas de dimensiones según las siguientes variables elegidas del dataset:
- Prioridad [dim_Priority]: clasificando a los clientes en 'regulares' según su id_priority sea 0 ó 1 y en 'premium' según su id_priority sea igual a 2,
- Clientes [dim_Customer]: creando un id único para cada cliente y removiendo clientes duplicados,
- Tipo de servicio [dim_Type]: clasificando el servicio en 6 categorías según las siglas indicadas en el diccionario de los datos y normalizando los valores,
- Resultado del servicio [dim_Outcome]: creando un id único para cada categoría de resultado de la llamada (llamada que se cortó, llamada atendida por el agente o aquella en la que se ignoró lo sucedido),
- Llamadas [fac_Call_Center]: tabla de transacciones que muestra por cada registro una (1) llamada con los atributos descriptos anteriormente y los tiempos de inicio y finalización de los 3 momentos de la llamada. Debido a que esta tabla no presentaba id únicos para cada registro, se procedió a crear una columna de índices a los fines de ser utilizada como clave primaria.


## Modelado de datos

Una vez efectuadas todas las transformaciones y normalizaciones en Power Query, procedimos a unir las tablas en la vista "Modelo" mediante la clave primaria de cada tabla con la tabla de transacciones creando un esquema estrella. 
A su vez creamos la tabla calendario [calendar] para poder ser utilizada en funciones de inteligencia de tiempo y mayor nivel de agregación de datos.
El modelo quedó de la siguiente forma:

[Modelo](https://github.com/agusvaldes/call-center-anonymous-bank/blob/main/github_files/5.png?raw=true)
![Logo](https://github.com/fedeandresg/call-center-anonymous-bank/blob/main/modelo.PNG?raw=true)
