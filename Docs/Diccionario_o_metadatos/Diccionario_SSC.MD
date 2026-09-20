Diccionario de datos SSC

La Secretaría de Seguridad Ciudadana (SSC) registra hechos de tránsito desde 2018\. La fuente principal corresponde a la serie ampliada, no comparativa. El portal indica que cada fila corresponde a un hecho de tránsito e incluye fecha, tipo de evento, coordenadas, características de personas lesionadas/fallecidas y unidad médica

**METADATOS** 

| ELEMENTO   | DESCRIPCIÓN |
| ----- | ----- |
| Fuente  | Secretaria de Seguridad Ciudadana (SSC) |
| Conjunto de datos  | Hechos de tránsito registrados por la SSC  |
| Cobertura temporal  | Desde 2018 |
| Serie  | Ampliada, no comparativa  |
| Unidad de observación  | Hecho de tránsito  |
| Formatos  | CSV  |
| Licencia  | Creative Commons Attribution 4.0  |
| Actualización  | 23 de febrero de 2024  |
| Cobertura geográfica  | Ciudad de México  |
| Información complementaria  | Personas,sexo,edad,tipo de persona y vehiculos  |
| Advertencia  | No utilizar esta serie para comparaciones interanuales 2018 \- 2019 |

 

**DICCIONARIO** 

| VARIABLE  | DESCRIPCIÓN | TIPO DE DATO ESPERADO  | UTILIDAD PARA EL PROYECTO  |
| :---- | :---- | :---- | :---- |
| Fecha del evento  | Fecha en que ocurrió el hecho de tránsito  | Fecha  | Analizar evolución temporal  |
| Hora del evento  | Hora en que ocurrió el hecho  | Hora  | Identificar horarios de mayor riesgo  |
| Tipo de evento  | Tipo de hecho de tránsito registrado  | Categoria  | Comparar diferentes tipos de hechos  |
| Coordenadas  | Ubicación geográfica del hecho  | Numérica  | Crear mapas de concentración  |
| Personas lesionadas  | Total de personas lesionadas  | Numérica  | Medir afectaciones  |
| Personas fallecidas  | Total de personas fallecidas  | Numérica  | Medir gravedad  |
| Unidad médica  | Unidad médica relacionada con la atención  | Categoría  | Analizar atencion medica  |
| Sexo  | Sexo de las personas lesionadas o fallecidas  | Categoría  | Analizar características de las víctimas   |
| Edad  | Edad de las personas involucradas  | Numérica  | Analizar grupos de edad  |
| Tipo de persona  | Tipo de persona involucrada en el hecho  | Categoría  | Diferenciar peatones, conductores u otros |
| Tipo de vehículo  | tipo de vehículo involucrado  | Categoría  | Analizar vehículos asociados a los hechos  |

La SSC tambien publica recursos independientes sobre personas por sexo, edad y tipo de persona, asi como sobre vehiculos involucrados. 

**NOTA:** La fuente SSC corresponde a una serie ampliada. A partir de julio de 2018 se modificó y enriqueció la recolección de información, por lo que el propio portal señala que esta serie no debe utilizarse para realizar comparaciones interanuales entre 2018 y 2019\. Además, existen algunos registros con puntos geográficos fuera de la Ciudad de México derivados de la fuente de origen

**Diccionario de datos de las fuentes** 

| VARIABLE | DESCRIPCIÓN | TIPO APARENTE | ESTADO |
| ----- | ----- | ----- | ----- |
| Fecha del evento  | Fecha en que ocurrió el hecho de tránsito  | Fecha  | Conocida  |
| Hora del evento  | Hora en que ocurrió el hecho  | Hora  | Conocida  |
| Tipo de evento  | Clasificación del hecho de tránsito  | Categoría  | Parcial  |
| Alcaldía  | Alcaldía asociada al hecho  | Categoría  | Parcial  |
| Colonia  | Colonia o zona relacionada con el hecho  | Categoría  | Parcial  |
| Calle  | Vialidad relacionada con el hecho  | Texto  | Parcial  |
| Coordenadas X / longitud  | Ubicación geográfica del hecho  | Numérica  | Conocida  |
| Coordenadas Y / latitud  | Ubicación geográfica del hecho  | Numérica  | Conocida  |
| Personas lesionadas  | Número de personas lesionadas  | Numérica  | Conocida |
| Personas fallecidas  | Número de personas fallecidas  | Numérica  | Conocida  |
| Unidad médica  | Unidad médica relacionada con la atención  | Categoría  | Parcial  |

**NOTA:** ***“PARCIAL”*** significa que conocemos el nombre general del campo, pero todavía falta confirmar completamente el significado de sus categorías. 

**Archivo de personas** 

La SSC pública recursos adicionales relacionados con las personas involucradas. En ellos se pueden encontrar variables relacionadas con: 

| Variable  | Descripción  | Estado  |
| :---- | :---- | :---- |
| Tipo de persona  | Clasificación de la persona involucrada  | Parcial  |
| Sexo  | Sexo registrado  | Conocida  |
| Edad  | Edad registrada  | Conocida  |
| Condición de la persona  | Situación relacionada con el hecho  | Parcial  |
| Lesionado o fallecido  | Condición de afectación  | Parcial  |

**Archivo de vehiculos** 

| Variable  | Descripción  | Estado  |
| :---- | :---- | :---- |
| Tipo de vehículo  | Clasificación del vehículo involucrado  | Parcial  |
| Vehículo relacionado con el hecho  | Relacion del vehículo con el incidente  | Parcial  |
| Caracteristicas del vehiculo  | Datos adicionales disponibles sobre el vehículo  | Parcial  |

**Variables pendientes de confirmación:** aunque los nombres de algunos campos permiten identificar su tema general, todavía debe revisarse el catálogo de valores y la documentación de los archivos para confirmar el significado exacto de cada categoría, así como la forma de relacionar el archivo principal con los archivos de personas y vehículos.
