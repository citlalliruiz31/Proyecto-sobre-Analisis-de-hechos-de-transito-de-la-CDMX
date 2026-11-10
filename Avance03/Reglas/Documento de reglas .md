# **DOCUMENTO DE REGLAS DE CALIDAD, LIMPIEZA Y PREPARACIÓN DE DATOS**

**Proyecto:** Análisis de accidentes y hechos de tránsito en la Ciudad de México  
**Institución:** Universidad Autónoma de la Ciudad de México (UACM)  
**Equipo:** A\&C  
**Asignatura:** Inteligencia de Negocios  
**Periodo:** 2026-2

---

# **1\. Propósito del documento**

El presente documento establece los criterios metodológicos que se aplicarán durante la revisión, limpieza, validación y preparación de las fuentes de información utilizadas en el proyecto: Secretaría de Seguridad Ciudadana (SSC), C5 e INEGI-ATUS.

Su propósito es definir bajo qué condiciones se conservarán, eliminarán, normalizarán, imputarán o separarán los registros, evitando decisiones arbitrarias y asegurando que cada transformación tenga una justificación técnica y estadística.

Las reglas servirán como referencia para modificar los notebooks del proyecto y desarrollar el proceso ETL del Avance 03\.

# **2\. Pregunta de investigación y alcance**

**Pregunta principal:**

¿En qué alcaldías y franjas horarias de la Ciudad de México se registra la mayor cantidad de personas lesionadas en hechos de tránsito, de acuerdo con los registros disponibles a partir de 2018?

El análisis considera:

* Las 16 alcaldías de la Ciudad de México.  
* Registros correspondientes a 2018 en adelante, según la cobertura de cada fuente.  
* Información relacionada con hechos de tránsito y personas lesionadas.  
* Variables territoriales y temporales que puedan verificarse y compararse.  
* La hora en que ocurrió el incidente como referencia principal para el análisis temporal.

La información sobre personas fallecidas podrá conservarse para análisis descriptivos complementarios, pero no se utilizará como sustituto de la variable principal de personas lesionadas.

# **3\. Reglas generales de calidad y tratamiento de datos**

Las siguientes reglas son universales y deberán aplicarse a todas las fuentes.

| Código | Regla | Criterio de aplicación |
| ----- | ----- | ----- |
| RG-01 | Integridad de los datos originales | Los archivos originales se conservarán sin modificaciones. Todo el proceso de limpieza y transformación se realizará exclusivamente sobre copias de trabajo. |
| RG-02 | Conservación de variables originales | No se sobrescribirán las columnas originales. Las variables modificadas o normalizadas se generarán en columnas auxiliares. |
| RG-03 | Identificación de valores ausentes | Se distinguirán los valores nulos, cadenas vacías, categorías como SD y valores numéricos iguales a cero. |
| RG-04 | Identificación de duplicados | Se considerará duplicado exacto únicamente cuando coincidan todos los valores de las columnas evaluadas. |
| RG-05 | Tratamiento de folios repetidos | La repetición de un folio no será motivo suficiente para eliminar registros. Se revisará la unidad de observación y las diferencias entre filas. |
| RG-06 | Respeto a la unidad de observación | Antes de contar o relacionar registros se identificará si cada fila representa un hecho, una persona, un vehículo o un reporte. |
| RG-07 | Justificación de eliminaciones | Toda eliminación deberá cumplir un criterio previamente definido, contar con evidencia y tener un motivo documentado. |
| RG-08 | Justificación de imputaciones | Ningún valor se rellenará automáticamente. La imputación deberá contar con una justificación, un método definido y una evaluación de sus posibles efectos. |
| RG-09 | Normalización controlada | Las categorías se normalizarán únicamente cuando exista evidencia de que representan el mismo concepto. Se conservará siempre el valor original. |
| RG-10 | Validación de variables | Se comprobarán los tipos de datos, rangos, fechas, horas, categorías y valores indispensables para el análisis. |
| RG-11 | Trazabilidad | Se conservará la procedencia de los registros y se documentarán las operaciones realizadas. |
| RG-12 | Reproducibilidad | Las transformaciones deberán poder ejecutarse nuevamente y producir resultados verificables. |

## **3.1. Valores ausentes y ceros**

Se aplicarán las siguientes definiciones:

| Tipo de valor | Interpretación | Tratamiento |
| ----- | ----- | ----- |
| Nulo | No existe un valor reconocido por el proceso de lectura. | Se conserva como ausente. |
| Cadena vacía | El campo no contiene caracteres. | Se identifica y se trata como información ausente cuando corresponda. |
| SD o equivalente | La fuente indica que la información no está disponible o no fue especificada. | Se conserva su significado y no se convierte en cero. |
| Cero | Existe un valor numérico igual a cero. | Se conserva como valor válido cuando corresponda a la definición de la variable. |

**Regla de imputación de valores ausentes:**

No se rellenará automáticamente los valores faltantes con cero, promedios, medianas, modas u otros valores.

Antes de realizar una imputación se deberá:

1. Identificar la variable y la cantidad de valores ausentes.  
2. Determinar por qué es importante completar esa variable.  
3. Revisar la distribución y el comportamiento de los datos disponibles.  
4. Definir un método de imputación adecuado a la naturaleza de la variable.  
5. Justificar por qué el método no altera de manera importante la interpretación de los resultados.  
6. Conservar la columna original y generar una columna con los valores imputados.  
7. Registrar cuántos datos fueron completados y mediante qué procedimiento.

Cuando no exista una justificación suficiente, los valores se mantendrán como ausentes y no se utilizarán en los cálculos que requieran esa variable.

## **3.2. Duplicados y folios repetidos**

Se considerará duplicado exacto un registro cuyos valores coincidan en todas las columnas evaluadas con otro registro.

Se aplicarán los siguientes criterios:

**Duplicados exactos:**

* Se identificarán mediante una comparación de todas las columnas.  
* Se conservará una sola aparición del registro en el conjunto limpio.  
* Las copias adicionales se eliminarán del conjunto de análisis.  
* Las filas eliminadas se guardarán en un archivo independiente.  
* Se documentará el número de filas recibidas, duplicados identificados y registros conservados.

**Justificación:** mantener copias idénticas puede provocar que una misma observación se contabilice más de una vez y altere las frecuencias, totales y resultados estadísticos.

La eliminación de copias adicionales no significa destruir la evidencia: estas permanecerán en los archivos de duplicados para permitir su revisión.

**Folios repetidos:**

* Se identificarán los folios que aparezcan en más de una fila.  
* Se compararán las demás columnas para determinar si existen diferencias.  
* Si las filas representan personas, vehículos u observaciones diferentes, se conservarán.  
* Si se identifica una coincidencia parcial, se enviará a revisión.  
* No se eliminarán grupos completos únicamente por compartir un folio.

**Justificación:** un mismo hecho de tránsito puede estar relacionado con varias personas o vehículos. Por lo tanto, el folio puede funcionar como identificador de relación y no necesariamente como identificador único de cada fila.

## **3.3. Validación de edades**

Para las variables de edad se establecerá un rango de referencia de acuerdo con los datos observados y los criterios definidos por el equipo.

**Criterios establecidos:**

* Edad máxima permitida: 99 años.  
* Edad mínima de referencia: se calculará tomando la edad mínima observada en la fuente y restándole una unidad.  
* No se aceptarán edades negativas.  
* Los valores que no sean numéricos se identificarán como no válidos para el análisis de edad.  
* Las edades superiores a 99 años se marcarán como atípicas y se excluirán de los cálculos que requieran una edad válida, conservando los registros originales para revisión.

La edad mínima de referencia se calculará después de revisar la distribución de la variable y verificar que el valor mínimo observado sea numéricamente válido.

La regla se expresará de la siguiente manera:

**Rango de edad permitido:**

Edad mínima de referencia \= edad mínima observada − 1

Edad máxima \= 99 años.

**Justificación:** el límite superior permite establecer un criterio uniforme para identificar edades atípicas. El límite inferior se determinará con base en la edad mínima observada en la fuente, incorporando un margen de una unidad para la validación.

Los valores fuera del rango no se corregirán mediante suposiciones ni se sustituirán por otra edad.

Se conservarán:

* La columna de edad original.  
* La columna de edad convertida a formato numérico.  
* Una marca de validación.  
* El motivo de revisión o exclusión, cuando corresponda.

## **3.4. Delimitación territorial**

El proyecto se concentra en las 16 alcaldías de la Ciudad de México.

Se aplicarán los siguientes criterios:

1. Conservar el nombre territorial original.  
2. Crear una columna auxiliar para normalizar espacios, mayúsculas y variantes confirmadas.  
3. Verificar que las categorías correspondan a las alcaldías de la Ciudad de México.  
4. Aplicar equivalencias únicamente cuando exista documentación que las respalde.  
5. Identificar los registros con información territorial ausente o contradictoria.  
6. Separar los registros que no puedan verificarse del conjunto principal cuando su ubicación sea indispensable para el análisis.

**Justificación:** una clasificación territorial incorrecta puede asignar un incidente a una alcaldía equivocada y alterar la distribución espacial de los resultados.

No se asignará una alcaldía utilizando únicamente suposiciones o coincidencias parciales.

## **3.5. Delimitación temporal y tratamiento de las horas**

El análisis principal considerará registros desde 2018, de acuerdo con la cobertura de cada fuente.

Se conservarán los campos originales de fecha y hora y se crearán columnas auxiliares cuando sea necesario convertirlos.

**Regla principal: hora de ocurrencia del incidente.**

Para el análisis por franjas horarias se utilizará prioritariamente la hora en que ocurrió el incidente.

No se utilizará automáticamente la hora de creación del reporte ni la hora de cierre como si fueran la hora del accidente.

**Regla complementaria: comparación entre ocurrencia y registro.**

Cuando se disponga de la fecha y hora de ocurrencia y de la fecha y hora de registro, se podrá calcular el tiempo transcurrido entre ambos momentos.

Este cálculo permitirá identificar cuánto tiempo pasó entre el incidente y su registro en el sistema.

Se deberá:

* Conservar por separado la hora de ocurrencia y la hora de registro.  
* Verificar que ambas correspondan al mismo incidente.  
* Comprobar que las fechas y horas sean interpretables.  
* Calcular el tiempo transcurrido únicamente cuando existan ambos datos.  
* Identificar los resultados negativos o inconsistentes para revisión.  
* No sustituir la hora de ocurrencia por la hora de registro cuando la primera esté ausente.

La hora de cierre se conservará como una variable independiente y no se interpretará como hora del incidente.

**Franjas horarias definidas por el equipo:**

| Franja | Horario |
| ----- | ----- |
| Madrugada | 00:00 a 05:59 |
| Mañana | 06:00 a 11:59 |
| Tarde | 12:00 a 17:59 |
| Noche | 18:00 a 23:59 |

Estas categorías son una clasificación elaborada por el equipo para facilitar el análisis. No representan necesariamente categorías originales de las fuentes.

Cuando no exista información de la hora de ocurrencia, el registro no se asignará artificialmente a una franja horaria.

# **4\. Reglas específicas por fuente**

## **4.1. Secretaría de Seguridad Ciudadana (SSC)**

**Función en el proyecto:** fuente principal para el análisis de hechos de tránsito y personas lesionadas.

**Cobertura documentada en el Avance 02:** 2018–2023.

La información SSC se encuentra distribuida en cinco tablas. Cada una tiene una unidad de observación distinta, por lo que se deberán respetar sus características antes de realizar cualquier relación.

| Tabla | Unidad de observación | Tratamiento |
| ----- | ----- | ----- |
| Hechos de tránsito | Hecho | Se utilizará para identificar las características del incidente. |
| Personas por edad | Persona | Se conservarán las observaciones individuales de las personas. |
| Personas por sexo | Persona | Se mantendrá separada y se revisará su cobertura. |
| Tipo de persona | Persona | Se considerará su cobertura disponible, documentada desde 2020\. |
| Vehículos involucrados | Vehículo | Se conservarán las observaciones correspondientes a cada vehículo. |

### **SSC-R01. Duplicados exactos**

Se identificarán las filas que coincidan en todas las columnas de cada tabla.

Se conservará una sola aparición y las copias adicionales se eliminarán del conjunto limpio y se exportarán a un archivo de duplicados.

**Justificación:** una copia idéntica no aporta una observación diferente y puede provocar doble conteo.

En la tabla de personas por edad se reportaron 3,498 repeticiones adicionales en el Avance 02\. Este resultado deberá comprobarse nuevamente con la ejecución del proceso de limpieza antes de utilizarlo como resultado definitivo.

### **SSC-R02. Folios sin identificador válido**

En el perfilamiento del Avance 02 se identificaron 7,288 folios con valores SD o equivalentes en la tabla de hechos.

Estos valores no se considerarán identificadores válidos para relacionar registros.

Se conservarán los datos originales, pero no se utilizarán esos valores como llaves de unión.

**Justificación:** un marcador de información no disponible no identifica de manera única un hecho y podría generar relaciones incorrectas.

### **SSC-R03. Folios repetidos**

Los folios repetidos se identificarán y revisarán sin eliminarlos automáticamente.

Se compararán las demás variables para determinar si las observaciones corresponden a personas, vehículos o registros diferentes.

**Justificación:** la tabla de hechos, la tabla de personas y la tabla de vehículos tienen distintas unidades de observación.

### **SSC-R04. Validación de edades**

Se aplicará el rango general establecido en el apartado 3.3:

* Máximo: 99 años.  
* Mínimo: edad mínima observada menos una unidad, sin aceptar edades negativas.

En el perfilamiento anterior se identificaron 14 edades superiores a 120 años. Estos registros deberán marcarse para revisión y evaluarse con el nuevo criterio.

No se sustituirán por una edad estimada ni se eliminarán sin conservar la evidencia.

**Justificación:** las edades atípicas pueden alterar los análisis descriptivos y las distribuciones por grupos de edad.

### **SSC-R05. Valores de personas lesionadas y fallecidas**

Se comprobará que las variables numéricas:

* Sean convertibles a valores numéricos.  
* No presenten cantidades negativas.  
* Distingan los ceros de los valores ausentes.  
* Mantengan identificados los valores no disponibles.

Los valores no numéricos o negativos se enviarán a revisión. No se convertirán automáticamente en cero.

**Justificación:** las cantidades de personas deben representar valores numéricos válidos y no deben confundirse con información desconocida.

### **SSC-R06. Relación entre tablas**

Las cinco tablas permanecerán separadas durante la limpieza.

Cualquier unión deberá contar previamente con:

1. Identificación de la llave de relación.  
2. Verificación de los valores válidos de dicha llave.  
3. Identificación de la unidad de observación de cada tabla.  
4. Comprobación de la cardinalidad de la relación.  
5. Comparación del número de filas antes y después de la unión.

**Justificación:** unir tablas con diferentes unidades de observación sin comprobar su relación puede multiplicar los registros y producir conteos incorrectos.

### **SSC-R07. Cobertura temporal**

Se documentará la cobertura de cada tabla por separado.

No se asumirá que todas las tablas contienen información para los mismos años.

**Justificación:** las diferencias de cobertura pueden producir comparaciones incompletas o sesgadas.

**Decisión del equipo SSC:** eliminar las copias exactas adicionales del conjunto limpio, conservar los folios repetidos cuando representen observaciones diferentes, validar las edades mediante el rango establecido y mantener separadas las tablas hasta comprobar sus relaciones.

## **4.2. Centro de Comando, Control, Cómputo, Comunicaciones y Contacto Ciudadano (C5)**

**Función en el proyecto:** fuente complementaria para aportar información sobre los reportes de incidentes viales.

**Cobertura documentada en el Avance 02:** 2018–2024.

Los registros de C5 representan reportes de incidentes y no necesariamente hechos de tránsito confirmados bajo la misma definición de SSC.

Por lo tanto, sus cantidades no se sumarán directamente con las de SSC.

### **C5-R01. Duplicados exactos**

Se compararán todas las columnas de cada registro.

Cuando dos o más filas coincidan completamente, se conservará una sola aparición en el conjunto limpio y se eliminarán las copias adicionales.

Las copias eliminadas se guardarán en un archivo independiente.

**Justificación:** los registros completamente idénticos no representan información adicional y pueden aumentar artificialmente la frecuencia de reportes.

### **C5-R02. Folios repetidos**

Los registros con el mismo folio, pero con diferencias en otras variables, se conservarán para revisión.

En el Avance 02 se identificaron 20 registros pertenecientes a grupos de folios repetidos que no eran duplicados exactos.

Estos registros deberán volver a verificarse.

**Justificación:** la repetición del folio no demuestra que se trate del mismo registro ni que la información sea redundante.

### **C5-R03. Discrepancias territoriales**

Se identificarán los registros en los que exista una contradicción entre las alcaldías reportadas.

En el Avance 02 se identificaron 76,204 filas con discrepancias territoriales.

Se aplicará el siguiente criterio:

* Los registros que presenten una contradicción territorial comprobada se excluirán del conjunto principal.  
* Se conservarán las filas excluidas en un archivo independiente.  
* Se registrará el motivo específico de exclusión.  
* Se conservarán los valores originales de alcaldía y las coordenadas disponibles.  
* No se asignará una alcaldía mediante suposiciones.

**Justificación:** una discrepancia territorial no resuelta puede colocar un reporte en una alcaldía incorrecta y afectar el análisis espacial.

La cantidad de 76,204 corresponde al resultado documentado en el Avance 02 y deberá comprobarse nuevamente antes de considerarla definitiva.

### **C5-R04. Tratamiento de fecha y hora**

Se conservarán por separado los campos de:

* Fecha y hora de ocurrencia del incidente, cuando existan.  
* Fecha y hora de creación del reporte.  
* Fecha y hora de cierre del reporte.

Para el análisis de franjas horarias se utilizará prioritariamente la hora de ocurrencia.

Cuando se disponga de la hora de ocurrencia y de creación, se calculará el tiempo transcurrido entre ambas para estudiar el retraso de registro.

La hora de creación no sustituirá a la hora de ocurrencia.

La hora de cierre se utilizará únicamente para análisis relacionados con la atención o cierre del reporte, si resulta pertinente.

**Justificación:** estos campos representan momentos diferentes del proceso y utilizarlos como equivalentes podría distorsionar la distribución temporal de los incidentes.

### **C5-R05. Registros sin hora**

Cuando la hora de ocurrencia no esté disponible:

* No se inventará una hora.  
* No se asignará una franja horaria.  
* El registro podrá conservarse para otros análisis cuando sus demás variables sean válidas.  
* Se identificará como pendiente para análisis temporal.

**Decisión del equipo C5:** eliminar las copias exactas adicionales del conjunto limpio, conservar los folios repetidos no idénticos, excluir del análisis territorial principal las discrepancias comprobadas y utilizar la hora de ocurrencia como referencia temporal.

## **4.3. INEGI-ATUS**

**Función en el proyecto:** fuente de referencia y contraste estadístico.

**Cobertura documentada en el Avance 02:** 2018–2025.

La información de ATUS deberá tratarse respetando las definiciones estadísticas y la unidad de observación establecida por INEGI.

### **INEGI-R01. Duplicados exactos**

Se compararán las 46 columnas identificadas en el perfilamiento del Avance 02\.

Cuando dos filas coincidan en todas las columnas, se conservará una sola aparición en el conjunto limpio y las copias adicionales se eliminarán de este.

Se guardarán en un archivo independiente para mantener la evidencia.

En el Avance 02 se identificaron 145 duplicados exactos adicionales, cantidad que deberá comprobarse nuevamente.

**Justificación:** las filas idénticas no agregan información estadística y pueden incrementar artificialmente las frecuencias.

### **INEGI-R02. Fechas inválidas**

Se validarán las fechas utilizando el formato correspondiente a la fuente.

Las fechas que no puedan interpretarse correctamente se separarán del conjunto destinado al análisis temporal.

Se conservarán sus valores originales y se registrará el motivo de exclusión.

En el Avance 02 se identificaron tres fechas calendáricas inválidas.

**Justificación:** una fecha incorrecta puede asignar un registro a un año, mes, día o franja que no le corresponde.

No se corregirán fechas mediante suposiciones.

### **INEGI-R03. Delimitación territorial**

Se comprobará que los registros correspondan a la Ciudad de México y que las categorías territoriales puedan relacionarse con sus 16 alcaldías.

No se asumirá que cualquier municipio equivale automáticamente a una alcaldía.

Se conservarán los valores originales y se generarán equivalencias únicamente cuando exista documentación que las respalde.

Los registros sin correspondencia territorial comprobable se mantendrán en un archivo de pendientes o se excluirán del análisis principal cuando no sea posible identificar su ubicación.

**Justificación:** una equivalencia territorial incorrecta puede modificar la distribución geográfica de los hechos de tránsito.

### **INEGI-R04. Variables temporales**

Se utilizará la hora de ocurrencia del accidente cuando esté disponible.

Se conservarán las fechas y horas originales y se generarán variables auxiliares para el análisis por franjas.

Si existe información de registro y de ocurrencia, se podrá calcular el tiempo transcurrido entre ambos momentos, siempre que los campos representen eventos comparables.

No se utilizará una hora de registro como sustituto de la hora del accidente.

### **INEGI-R05. Unidad de observación y comparación**

Antes de calcular frecuencias se verificará qué representa cada fila y qué significan las variables de personas lesionadas.

Los resultados de INEGI-ATUS no se sumarán directamente con SSC o C5.

**Justificación:** las fuentes pueden utilizar metodologías, coberturas y unidades estadísticas diferentes.

**Decisión del equipo INEGI-ATUS:** separar los duplicados exactos, excluir las fechas inválidas de los análisis temporales, verificar la correspondencia territorial y respetar la definición estadística de la fuente.

# **5\. Resumen de decisiones por fuente**

| Fuente | Situación detectada | Decisión del equipo |
| ----- | ----- | ----- |
| SSC | Duplicados exactos | Eliminar copias adicionales del conjunto limpio y conservar evidencia. |
| SSC | Folios repetidos | Revisar sin eliminar automáticamente. |
| SSC | Edades atípicas | Aplicar rango establecido y marcar valores fuera de él. |
| SSC | Tablas de personas y vehículos | Mantener separadas hasta verificar las relaciones. |
| SSC | Diferencias de cobertura | Documentar por tabla y periodo. |
| C5 | Duplicados exactos | Eliminar copias adicionales del conjunto limpio. |
| C5 | Folios repetidos no idénticos | Conservar para revisión. |
| C5 | Discrepancias de alcaldía | Excluir del conjunto territorial principal y conservar evidencia. |
| C5 | Hora de ocurrencia y registro | Utilizar ocurrencia como variable principal y registro para comparar retrasos. |
| INEGI-ATUS | Duplicados exactos | Eliminar copias adicionales del conjunto limpio. |
| INEGI-ATUS | Fechas inválidas | Separar para revisión y excluir del análisis temporal. |
| INEGI-ATUS | Información territorial | Verificar antes de normalizar. |
| Todas | Valores ausentes | No imputar sin justificación metodológica. |

# **6\. Reglas para los archivos de salida**

Cada fuente deberá conservar sus resultados de manera independiente.

Los nombres propuestos para los archivos son:

### **SSC**

* `SSC_hechos_limpios.csv`  
* `SSC_personas_edad_limpio.csv`  
* `SSC_personas_sexo_limpio.csv`  
* `SSC_tipo_persona_limpio.csv`  
* `SSC_vehiculos_limpio.csv`  
* `SSC_duplicados_exactos.csv`  
* `SSC_folios_repetidos_revision.csv`  
* `SSC_pendientes_revision.csv`  
* `SSC_controles_validacion.csv`  
* `SSC_bitacora_limpieza.csv`

### **C5**

* `C5_datos_limpios.csv`  
* `C5_duplicados_exactos.csv`  
* `C5_folios_repetidos_revision.csv`  
* `C5_alcaldias_discrepantes_excluidos.csv`  
* `C5_pendientes_revision.csv`  
* `C5_controles_validacion.csv`  
* `C5_bitacora_limpieza.csv`

### **INEGI-ATUS**

* `INEGI_datos_limpios.csv`  
* `INEGI_duplicados_exactos.csv`  
* `INEGI_fechas_invalidas.csv`  
* `INEGI_pendientes_territorio.csv`  
* `INEGI_controles_validacion.csv`  
* `INEGI_bitacora_limpieza.csv`

Los archivos denominados limpios solamente se generarán después de aplicar y comprobar las reglas correspondientes.

# **7\. Controles de validación obligatorios**

| Código | Comprobación | Resultado esperado |
| ----- | ----- | ----- |
| CV-01 | Integridad de los datos originales | Los archivos originales permanecen intactos. |
| CV-02 | Copia de trabajo | Todas las transformaciones se realizan sobre copias. |
| CV-03 | Estructura | Los encabezados corresponden con los datos. |
| CV-04 | Unidad de observación | Se identifica qué representa cada fila. |
| CV-05 | Delimitación temporal | Se identifican los registros del periodo de estudio. |
| CV-06 | Delimitación territorial | Se verifican las 16 alcaldías. |
| CV-07 | Fechas y horas | Se validan sin inventar información. |
| CV-08 | Valores ausentes | Se distinguen nulos, vacíos, SD y ceros. |
| CV-09 | Duplicados | Se identifican, justifican y separan los duplicados exactos. |
| CV-10 | Folios repetidos | Se revisan sin eliminarlos automáticamente. |
| CV-11 | Variables numéricas | Se comprueban tipos y rangos. |
| CV-12 | Edades | Se aplica el rango definido por el equipo. |
| CV-13 | Imputaciones | Cada valor rellenado cuenta con justificación y evidencia. |
| CV-14 | Exclusiones | Los registros excluidos conservan su motivo. |
| CV-15 | Conteos | Se comprueban filas recibidas, conservadas, separadas y excluidas. |
| CV-16 | Reproducibilidad | Los notebooks pueden ejecutarse nuevamente. |
| CV-17 | Trazabilidad | Cada resultado puede relacionarse con su fuente y transformación. |
| CV-18 | Variable temporal | Se utiliza la hora de ocurrencia como referencia principal. |

# **8\. Bitácora de limpieza y transformación**

Cada notebook deberá generar una bitácora automática que registre las operaciones realizadas.

La bitácora deberá contener, como mínimo:

| Campo | Descripción |
| ----- | ----- |
| fuente | Nombre de la fuente de datos. |
| archivo | Archivo procesado. |
| fecha\_proceso | Fecha y hora de ejecución. |
| etapa | Delimitación, perfilamiento, limpieza o validación. |
| regla\_aplicada | Código de la regla utilizada. |
| operacion | Descripción de la transformación. |
| problema\_identificado | Situación que motivó la operación. |
| filas\_antes | Número de filas antes del proceso. |
| filas\_despues | Número de filas después del proceso. |
| filas\_afectadas | Cantidad de registros afectados. |
| motivo | Justificación metodológica. |
| archivo\_salida | Nombre del archivo generado. |
| observaciones | Pendientes o aclaraciones. |

La bitácora deberá permitir identificar qué sucedió con los registros durante cada etapa del proceso.

Por ejemplo, si se eliminan duplicados exactos, deberá mostrar cuántas filas se recibieron, cuántas copias adicionales se separaron y cuántas filas permanecieron en el conjunto limpio.

# **9\. Orden de trabajo**

La aplicación de las reglas se realizará en el siguiente orden:

1. **Respaldo y acceso a copias:** identificar los archivos originales y trabajar exclusivamente con copias.  
2. **Inventario:** registrar fuentes, archivos, periodos, columnas y unidades de observación.  
3. **Lectura:** cargar los datos y conservar sus valores originales.  
4. **Perfilamiento:** revisar dimensiones, tipos, faltantes, frecuencias, fechas, categorías y duplicados.  
5. **Identificación de problemas:** determinar qué registros requieren revisión, exclusión o transformación.  
6. **Limpieza:** aplicar las reglas generales y específicas de cada fuente.  
7. **Validación:** comprobar que los cambios cumplen los criterios definidos.  
8. **Preparación:** crear variables auxiliares y preparar los datos para el análisis.  
9. **Exportación:** generar archivos limpios, duplicados, pendientes y controles.  
10. **Bitácora:** registrar cada operación y sus resultados.  
11. **Revisión final:** comprobar la consistencia de los datos antes de iniciar los análisis.

# **10\. Consideraciones para la comparación de fuentes**

Las tres fuentes presentan diferencias de cobertura, definiciones y unidades de observación.

Por lo tanto:

* No se sumarán directamente las cantidades de registros de SSC, C5 e INEGI-ATUS.  
* No se supondrá que un reporte de C5 equivale automáticamente a un hecho confirmado en SSC.  
* No se asumirán equivalencias territoriales sin documentación.  
* Las comparaciones se realizarán únicamente cuando las variables, periodos y unidades de observación sean compatibles.  
* Se distinguirá entre personas lesionadas, hechos de tránsito y reportes de incidentes.  
* Se utilizará la hora de ocurrencia para los análisis temporales siempre que esté disponible.  
* Cuando existan datos de ocurrencia y registro, se podrá estudiar el tiempo transcurrido entre ambos.  
* Cada resultado indicará la fuente y el periodo de referencia.

# **11\. Acuerdo final del equipo**

El equipo A\&C establece que la limpieza, validación y preparación de datos se realizará mediante criterios previamente definidos y documentados.

Las decisiones de eliminar, conservar, normalizar, imputar o separar registros deberán justificarse de acuerdo con las características de cada fuente y la pregunta de investigación.

Los duplicados exactos se eliminarán del conjunto limpio para evitar el doble conteo, pero se conservarán en archivos independientes como evidencia.

Los folios repetidos no se eliminarán automáticamente, debido a que pueden representar distintas personas, vehículos o registros relacionados con un mismo incidente.

Los valores ausentes no se sustituirán por cero y cualquier imputación deberá contar con una justificación metodológica.

La hora de ocurrencia del incidente será la referencia principal para los análisis temporales. La hora de registro se utilizará como variable complementaria para estudiar el tiempo transcurrido entre el incidente y su registro cuando existan ambas marcas temporales.

Este documento será la referencia metodológica para actualizar los notebooks del Avance 02 y desarrollar el proceso ETL y los análisis correspondientes al Avance 03\.

# **12\. Referencia documental**

Equipo A\&C. (2026). *Avance 02: Evidencias y resultados del proyecto. Análisis de accidentes y hechos de tránsito en la Ciudad de México*. Universidad Autónoma de la Ciudad de México.

**Nota metodológica:** las cantidades, periodos y hallazgos de calidad mencionados en este documento corresponden a los resultados reportados en el Avance 02\. Deberán verificarse nuevamente mediante la ejecución de los notebooks y la comparación con los archivos originales antes de presentarse como resultados definitivos.

