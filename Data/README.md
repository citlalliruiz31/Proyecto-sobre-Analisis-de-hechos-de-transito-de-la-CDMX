# Notebooks de limpieza y validación de datos

## Proyecto: Análisis de hechos de tránsito en la Ciudad de México

**Equipo:** A&C  
**Materia:** Inteligencia de Negocios  
**Periodo de análisis:** 2018 en adelante

## 1. Descripción

En esta carpeta organizamos los notebooks que utilizamos para realizar la limpieza, validación y preparación de los datos de nuestro proyecto de Inteligencia de Negocios.

Nuestro objetivo es analizar la frecuencia y severidad registrada de los hechos de tránsito en las alcaldías de la Ciudad de México, considerando los horarios, las personas lesionadas y las personas fallecidas.

Trabajamos con cuatro fuentes de información:

- Secretaría de Seguridad Ciudadana (SSC).
- Incidentes viales C5.
- INEGI, estadísticas ATUS.
- Kaggle, accidentes viales en México.

Para mantener un proceso ordenado y reproducible, dividimos nuestro trabajo en **tres etapas por fuente**, obteniendo un total de **12 notebooks**.

## 2. Estructura de carpetas

```text
notebooks/
│
├── SSC/
│   ├── 01_etapa1_delimitacion.ipynb
│   ├── 02_etapa2_validacion.ipynb
│   └── 03_etapa3_reglas_duplicados.ipynb
│
├── C5/
│   ├── 01_etapa1_delimitacion.ipynb
│   ├── 02_etapa2_validacion.ipynb
│   └── 03_etapa3_reglas_duplicados.ipynb
│
├── INEGI_ATUS/
│   ├── 01_etapa1_delimitacion.ipynb
│   ├── 02_etapa2_validacion.ipynb
│   └── 03_etapa3_reglas_duplicados.ipynb
│
└── Kaggle/
    ├── 01_etapa1_delimitacion.ipynb
    ├── 02_etapa2_validacion.ipynb
    └── 03_etapa3_reglas_duplicados.ipynb
```

Cada carpeta corresponde a una fuente de información y contiene los notebooks necesarios para trabajar sus archivos CSV de manera independiente.

## 3. Descripción de las etapas

| Etapa | Actividades | Resultado esperado |
|---|---|---|
| **1. Delimitación** | Filtrar registros correspondientes a las alcaldías de CDMX y fechas desde 2018. | CSV de primera limpieza. |
| **2. Validación** | Revisar valores nulos, tipos de datos, formatos, folios `SD`, registros repetidos y coincidencias. | Reportes de calidad y validación. |
| **3. Reglas de duplicados** | Revisar registros candidatos aplicando el criterio comunicado por la profesora Liliana. | Identificación de duplicados y bitácora de decisiones. |

### Etapa 1. Delimitación geográfica y temporal

En esta primera etapa trabajamos únicamente con los registros que corresponden a nuestro proyecto.

Realizamos las siguientes actividades:

1. Cargamos los archivos CSV originales.
2. Identificamos las columnas que contienen información geográfica y temporal.
3. Filtramos los registros correspondientes a las 16 alcaldías de la Ciudad de México.
4. Conservamos únicamente los registros con fechas del año 2018 en adelante.
5. Guardamos los resultados en nuevos archivos CSV.

Durante esta etapa **no eliminamos registros duplicados ni modificamos los valores faltantes**, ya que primero necesitamos revisar y documentar su calidad.

Los archivos originales se conservan sin modificaciones.

### Etapa 2. Validación y perfilamiento

En esta etapa revisamos la calidad de los datos obtenidos después de la delimitación.

Analizamos:

- Cantidad de filas y columnas.
- Tipos de datos.
- Formatos de fechas y horas.
- Valores faltantes o nulos.
- Valores desconocidos, como `SD`.
- Folios repetidos.
- Coincidencias entre folio y alcaldía.
- Filas completamente idénticas.
- Inconsistencias en nombres y categorías.

Los problemas encontrados se registran para justificar las decisiones posteriores.

En esta etapa identificamos los registros que requieren revisión, pero todavía no los eliminamos.

### Etapa 3. Aplicación de reglas para duplicados

Para esta etapa tomamos en cuenta la indicación que nos comunicó la **profesora Liliana**, correspondiente al criterio del **profesor Emilio**.

El procedimiento consiste en:

1. Identificar los folios repetidos.
2. Comprobar si los registros repetidos corresponden a la misma alcaldía.
3. Si las alcaldías son diferentes, conservar los registros.
4. Si coinciden el folio y la alcaldía, comparar los demás campos de las filas.
5. Si existen diferencias, conservar los registros y documentar las observaciones.
6. Si los registros son completamente idénticos, revisarlos como posibles duplicados antes de decidir su eliminación.
7. Documentar las eliminaciones justificadas en nuestra bitácora.

**Importante:** compartir un folio no significa necesariamente que dos filas sean duplicadas. Además, los registros con folio `SD` necesitan una revisión independiente.

Antes de retirar filas idénticas, verificaremos la unidad de observación de cada archivo, especialmente en las tablas de personas y vehículos.

## 4. Archivos trabajados por fuente

### SSC

Trabajamos con cinco archivos CSV:

- `HechosTransito_SSC.csv`
- `PersonasLyFporEdad_SSC.csv`
- `PersonasLyFporSexo_SSC.csv`
- `PersonasLyFporTipoPersona_SSC.csv`
- `VehiculosInvolucrados_SSC.csv`

Cada archivo se revisa por separado, respetando su estructura y unidad de observación.

### C5

Trabajamos con cuatro archivos CSV originales:

- `inViales_2014_2015.csv`
- `inViales_2016_2018.csv`
- `inViales_2019_2021.csv`
- `inViales_2022_2024.csv`

Conservamos todos los archivos originales, aunque el primero no aporta registros al periodo seleccionado de 2018 en adelante.

### INEGI ATUS

Trabajamos con archivos CSV anuales, catálogos y diccionario de datos.

Para nuestro análisis seleccionamos los archivos anuales de 2018 a 2025 y filtramos los registros correspondientes a la Ciudad de México.

Los catálogos y el diccionario se conservan como documentación de referencia.

### Kaggle

Trabajamos con los archivos anuales del conjunto de datos de accidentes viales en México, además de sus catálogos y diccionario.

Nuestro periodo de interés comprende los años 2018 a 2022.

Durante la revisión detectamos un posible desplazamiento de columnas, por lo que necesitamos verificar la lectura de los archivos antes de continuar con su procesamiento.

## 5. Bitácora de limpieza

Para mantener la trazabilidad de nuestro trabajo, documentamos las operaciones realizadas durante cada etapa.

La bitácora debe registrar:

| Campo | Descripción |
|---|---|
| Fecha | Día en que realizamos la actividad. |
| Fuente | SSC, C5, INEGI o Kaggle. |
| Archivo | CSV que estamos procesando. |
| Etapa | Delimitación, validación o limpieza de duplicados. |
| Problema identificado | Situación encontrada en los datos. |
| Acción realizada | Filtro, revisión, corrección o eliminación. |
| Justificación | Motivo por el cual tomamos la decisión. |
| Registros antes | Cantidad inicial de filas. |
| Registros después | Cantidad final de filas. |
| Validación | Comprobación de los resultados. |

Nuestro propósito es poder explicar qué modificamos, por qué lo hicimos y cómo comprobamos que los resultados cumplen las reglas establecidas.

## 6. Consideraciones importantes

- Los datos originales deben conservarse sin modificaciones.
- Los notebooks están organizados por fuente y etapa.
- Cada CSV debe tener su propio registro de validación.
- No debemos asumir que los archivos de diferentes fuentes pueden unirse directamente.
- Los catálogos se conservan como archivos de referencia.
- Los registros con folio `SD` no se eliminan automáticamente.
- La tercera etapa requiere verificar las coincidencias antes de eliminar registros.
- Los resultados de cada etapa deben conservarse para mantener la trazabilidad.

## 7. Resultado esperado

Al finalizar las tres etapas buscamos obtener conjuntos de datos delimitados, validados y documentados que podamos utilizar posteriormente en nuestro proceso ETL, PostgreSQL y Power BI.

Esto nos permitirá continuar con el análisis de frecuencia y severidad registrada de los hechos de tránsito en las alcaldías de la Ciudad de México, manteniendo evidencia de las transformaciones realizadas.

---

**Equipo A&C — Proyecto de Inteligencia de Negocios**