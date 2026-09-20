Diccionario de datos C5

La fuente del C5 registra incidentes viales reportados desde 2014\. El portal oficial señala que cada incidente genera un folio y publica un diccionario en formato XLSX. 

**METADATOS** 

| ELEMENTO   | DESCRIPCIÓN |
| ----- | ----- |
| Fuente  | Centro de Comando, Control, Cómputo, Comunicaciones y Contacto Ciudadano (C5) |
| Conjunto de datos  | Incidentes viales reportados por el C5 |
| Cobertura temporal  | Desde 2014 |
| Unidad de observación  | Incidente vial registrado  |
| Identificador  | Folio del incidente |
| Formatos  | CSV y XLSX |
| Licencia  | Creative Commons Attribution 4.0  |
| Actualización  | Mensual para las bases que se mantienen activas  |
| Cobertura geográfica  | Ciudad de México  |
| Fuente oficial  | Portal de Datos Abiertos de la CDMX |

 

**DICCIONARIO** 

| VARIABLE  | DESCRIPCIÓN | TIPO DE DATO ESPERADO  | UTILIDAD PARA EL PROYECTO  |
| :---- | :---- | :---- | :---- |
| Folio  | Identificador único del incidente  | Texto  | Identificar y contar incidentes  |
| Fecha de creación  | Fecha en que se creo el reporte  | Fecha | Analizar incidentes por día, mes y año  |
| Hora de creación  | Hora en que se creo el reporte  | Hora  | Identificar horarios con mayor cantidad de incidentes  |
| Dia de la semana  | Dia correspondiente a la fecha de creación  | Categoría  | Compara días de mayor incidencia  |
| Fecha de cierre | Fecha en que se cerró el reporte  | Fecha  | Analizar atención de los incidentes  |
| Hora cierre  | Hora de cierre del reporte  | Hora  | Analizar tiempos de atención  |
| Motivo  | Motivo o tipo de emergencia reportada  | Categoría  | Clasificar los incidentes  |
| Alcaldía del incidente  | Alcaldía donde ocurrió el incidente  | Categoría  | Identificar zonas con mayor concentración  |
| Latitud  | Coordenada geográfica norte-sur  | Numérica  | Representación cartográfica  |
| Longitud  | Coordenada geográfica este-oeste  | Numérica  | Representación cartográfica  |
| Código de cierre  | Código que indica el resultado del reporte  | Categórica  | Agrupar y comparar incidentes  |
| Origen  | Tipo/Origen mediante el cual se recibió el incidente  | Categoría  | Analizan procedencia de los reportes  |
| Clasificación del incidente  | Clasificación asignada al incidente  | Categoría  | Agrupar y comparar incidentes  |
| Alcaldía de resolución  | Alcaldía donde se dio resolución al incidente  | Categoría  | Analizar ubicación de la atención  |

**Diccionario de datos de las fuentes** 

| VARIABLE | DESCRIPCIÓN | TIPO APARENTE | ESTADO |
| ----- | ----- | ----- | ----- |
| Folio  | Identificador del incidente registrado  | Texto  | Conocida  |
| Fecha de creación  | Fecha de creación del reporte  | Fecha  | Conocida  |
| Hora de creación  | Hora de creación del reporte  | Hora  | Conocida  |
| Dia de la semana  | Dia de la semana correspondiente al reporte  | Categoría  | Conocida  |
| Fecha de cierre  | Fecha en que se cerró el reporte  | Fecha | Conocida  |
| Hora de cierre  | Hora en que se cerró el reporte  | Hora  | Conocida  |
| Motivo  | Motivo del incidente de acuerdo con el tipo de emergencia  | Categoría  | Parcial  |
| Alcaldía  | Alcaldía donde sucedió el incidente  | Categoría  | Conocida  |
| Latitud  | Coordenada geográfica del incidente  | Numérica  | Conocida  |
| Longitud  | Coordenada geográfica del incidente  | Numérica  | Conocida  |
| Código de cierre  | Código que identifica el resultado del incidente  | Categoría  | Conocida  |
| Clasificación  | Clasificación asignada al incidente  | Categoría  | Parcial  |
| Origen  | Origen del incidente por tipo | Categoría  | Parcial  |
| Alcaldía resolución  | Alcaldía en la que se dio la resolución al incidente | Categoría  | Conocida  |

**NOTA:** ***“PARCIAL”*** significa que conocemos el nombre general del campo, pero todavía falta confirmar completamente el significado de sus categorías. 

**Código de cierre del C5** 

Esta parte si está definida oficialmente, por lo que podemos incluirla en el diccionario:

| Código  | Significado  |
| :---- | :---- |
| A | Afirmativo  |
| N | Negativo  |
| I | Informativo  |
| F | Falso  |
| D | Duplicado  |

El C5 señala que, para contabilizar incidentes confirmados como reales, se deben utilizar los registros con código Afirmativo (A); para contabilizar todos los reportes recibidos se consideran todos los códigos

Variables que todavía requieren revisión 

En C5 no debemos inventar las categorías internas de: 

* Motivo   
* Clasificación   
* Origen 

Por lo tanto, en el avance puede escribir: 

	***Pendiente de confirmación:*** Se deberá revisar el catálogo de valores de variables Motivo, Clasificación y Origen para determinar el significado de cada categoría o código antes de realizar transformaciones o agrupaciones.