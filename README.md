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

![Logo](https://github.com/agusvaldes/call-center-anonymous-bank/blob/main/github_files/5.png?raw=true)

## Visualización

El dashboard consta de 1 portada y 2 páginas navegables a través de una botonera de navegación.

En la primer página denominada "Llamadas" se puede observar la descripción de las operaciones del call center para el año 1999 y ambos segmentos (Regular y Premium), describiendo:

- Número total de llamadas,
- Cantidad de llamadas por mes,
- Filtro de tipo de cliente según la prioridad,
- Proporción de llamadas por resultado,
- Distribución de llamadas por tipo de servicio.

![Logo](https://github.com/agusvaldes/call-center-anonymous-bank/blob/main/github_files/2.png?raw=true)

En la segunda y última página llamada "Segmento Premium" se efectuó un detalle de las operaciones para clientes de alta prioridad (Premium) indicando:

- Total de clientes premium para el período,
- Detalle de llamadas según hayan tenido o no servicio,
- Tiempos promedio de espera en VRU (contestador automático), en cola de espera y en servicio,
- TOP 10 de clientes según la cantidad de llamadas realizadas,
- Distribución de llamadas según motivo,
- Histórico (evolución) de llamadas por período, pudiendo el usuario navegar por la jerarquía de trimestre, mes y día (por defecto se muestra mensual). El gráfico de líneas presenta a su vez un detalle de la proporción de llamadas con y sin servicio para cada punto en formato de tooltip o gráfico emergente.

![Logo](https://github.com/agusvaldes/call-center-anonymous-bank/blob/main/github_files/3.png?raw=true)

[Visualización página Segmento Premium con tooltip](https://github.com/agusvaldes/call-center-anonymous-bank/blob/main/github_files/4.png?raw=true)
## Insights

A lo largo del trabajo de análisis, visualización y exploración de datos, arribamos a las siguientes conclusiones:

Para ambos segmentos:

- Podemos decir que los meses no presentan una gran variación en cantidad de llamadas entre sí para ambos segmentos, pero podemos concluir que los meses de Marzo, Mayo, Junio, Julio, Agosto, Noviembre y Diciembre presentan llamadas que superan el promedio mensual y que por ende pueden considerarse como picos en el servicio,
- La mayoría de las llamadas fueron por actividad regular o transaccional en español, seguidas de potenciales clientes y comercio de acciones. Las llamadas por motivos de actividad en internet no representaron una gran proporción (propio de la época) y las llamadas por actividad regular en inglés representaron el menor porcentaje.
- El 79% de las llamadas del año tuvo servicio, en tanto que el 20% fueron cortadas y solo en el 1% de las llamadas se ignoró lo sucedido.

Para segmento Premium:

- La empresa contó con un total de 12.910 clientes clasificados como Premium.
- Los clientes tuvieron un promedio de espera en VRU de 5,7 segundos, un tiempo promedio de espera en cola de 86,7 segundos (lo cual indica que se estaría cumpliendo con la condición de asignarles 90 segundos para avanzar en la cola) y un tiempo promedio de llamada en servicio de 179,03 segundos. Podemos concluir que los clientes premium tienen tiempos cortos de espera en promedio para cada fase, en especial los 10 más frecuentes, pero los mismos varían mes a mes.
- El segmento premium tiene llamadas en su mayoría por motivos de actividad regular en español e intercambio de acciones principalmente. 
- Solo se registraron 2 llamadas en el año por actividad en internet para dicho segmento de clientes, lo que nos permite inferir que no utilizan medios electrónicos.
- Los picos de llamadas se registraron desde Marzo hasta Agosto y en Noviembre y Diciembre. El resto de meses las llamadas disminuyeron considerablemente por lo que resulta útil para el call center reforzar la contración de agentes para los meses de alta demanda.
