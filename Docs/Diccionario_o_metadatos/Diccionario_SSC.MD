# Diccionario de datos SSC

La fuente de la Secretaría de Seguridad Ciudadana (SSC) registra hechos viales y reportes de atención que pueden complementar la información del C5. Este diccionario describe la estructura esperada para la fuente SSC con fines de análisis comparativo y limpieza de datos.

## Metadatos

| ELEMENTO | DESCRIPCIÓN |
| --- | --- |
| Fuente | Secretaría de Seguridad Ciudadana (SSC) |
| Conjunto de datos | Hechos viales y reportes de atención registrados por la SSC |
| Cobertura temporal | Variable según el periodo disponible en la fuente |
| Unidad de observación | Hecho vial o incidente reportado |
| Identificador | Folio, clave o número de atención |
| Formatos | CSV, XLSX o exportaciones institucionales |
| Licencia | Definida por la fuente pública y condiciones de uso de la CDMX |
| Actualización | Periódica, conforme a la publicación institucional |
| Cobertura geográfica | Ciudad de México |
| Fuente oficial | Portal de datos abiertos de la CDMX o sistema de la SSC |

## Diccionario de variables

| VARIABLE | DESCRIPCIÓN | TIPO DE DATO ESPERADO | UTILIDAD PARA EL PROYECTO |
| :--- | :--- | :--- | :--- |
| Folio | Identificador único del reporte o incidente | Texto | Correlacionar reportes y evitar duplicados |
| Fecha del hecho | Fecha en que ocurrió el incidente | Fecha | Analizar tendencias temporales |
| Hora del hecho | Hora en que ocurrió el incidente | Hora | Identificar horarios de mayor riesgo |
| Fecha de registro | Fecha en que se reportó el hecho | Fecha | Evaluar tiempos de respuesta y registro |
| Hora de registro | Hora de registro del hecho | Hora | Comparar momentos de recepción del reporte |
| Tipo de accidente | Clase de incidente reportado | Categoría | Clasificar eventos viales |
| Tipo de vehículo | Vehículo involucrado en el hecho | Categoría | Estimar patrones por tipo de transporte |
| Alcaldía | Alcaldía donde ocurrió el hecho | Categoría | Identificar zonas de concentración |
| Colonia | Colonia o zona de incidencia | Texto/Categoría | Análisis estadístico por área urbana |
| Calle | Nombre de la vialidad principal | Texto | Localizar el evento |
| Cruce | Intersección o punto de referencia | Texto | Mejorar la georreferenciación |
| Latitud | Coordenada geográfica de la ubicación | Numérica | Representación cartográfica |
| Longitud | Coordenada geográfica de la ubicación | Numérica | Representación cartográfica |
| Lesionados | Número de personas lesionadas | Numérica | Medir severidad del evento |
| Muertos | Número de personas fallecidas | Numérica | Evaluar gravedad del incidente |
| Estado del reporte | Situación del caso registrado | Categoría | Seguir avance del reporte |
| Resultado | Resultado de la atención o cierre del caso | Categoría | Comparar resolución y atención |
| Motivo | Causa o razón reportada del incidente | Categoría | Analizar factores asociados |
| Unidad responsable | Dependencia o área que atendió el evento | Texto/Categoría | Evaluar gestión institucional |
| Observaciones | Comentarios adicionales del reporte | Texto | Completar contexto del incidente |

## Notas de validación

- Las categorías de `Tipo de accidente`, `Motivo`, `Resultado` y `Estado del reporte` deberán validarse con el catálogo oficial para evitar interpretaciones inconsistentes.
- La variable `Tipo de vehículo` puede variar según la fuente; es recomendable normalizarla en un esquema único para el proyecto.
- En los casos en los que la geolocalización sea imprecisa, se debe revisar la calidad de las coordenadas antes de hacer análisis espaciales.

## Recomendación para el proyecto

Para el análisis comparativo entre fuentes, se recomienda construir una tabla de trabajo con las siguientes columnas comunes:

- `folio`
- `fecha_hecho`
- `hora_hecho`
- `alcaldía`
- `colonia`
- `latitud`
- `longitud`
- `tipo_accidente`
- `num_lesionados`
- `num_muertos`
- `estado_reporte`

De esta manera se logra homogeneizar la información de la SSC con el diccionario de la fuente C5 y facilitar comparaciones entre ambas bases.
