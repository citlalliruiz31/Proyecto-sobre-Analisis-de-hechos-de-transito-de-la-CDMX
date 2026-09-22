# Análisis de hechos de tránsito de la CDMX

## Proyecto Semestral de Inteligencia de Negocios

### Equipo A&c

**Integrantes:**

* Mendez Cabral Angel David 23-003-1466
* Ruiz Moreno Citlalli Viviana 23-003-1162

**Institución:** Universidad Autónoma de la Ciudad de México (UACM)
---

## Proyecto
### Análisis de hechos de tránsito en la Ciudad de México

El proyecto tiene como propósito analizar los hechos de tránsito registrados en la Ciudad de México para identificar los patrones de **frecuencia y severidad** de estos eventos.

El análisis se enfocará principalmente en conocer las alcaldías y horarios donde se concentra una mayor cantidad de hechos de tránsito, así como identificar aquellos periodos y zonas en los que se observa una mayor severidad registrada, considerando el número de personas lesionadas y fallecidas.
---
## Pregunta de negocio

> **¿En qué alcaldías y horarios de la CDMX se concentra la mayor frecuencia de hechos de tránsito y en cuáles se observa una mayor severidad registrada, considerando las personas lesionadas y fallecidas?**

---

## Objetivo general

Analizar los hechos de tránsito registrados en la Ciudad de México para identificar las alcaldías y horarios con mayor frecuencia de eventos y determinar en cuáles se observa una mayor severidad registrada, considerando el número de personas lesionadas y fallecidas.

---

## Decisión esperada

Identificar las alcaldías y horarios que concentran una mayor frecuencia de hechos de tránsito y distinguir aquellas zonas y periodos que presentan una mayor severidad registrada mediante el número de personas lesionadas y fallecidas.

---
## Fuente principal

La fuente principal del proyecto será la información de **hechos de tránsito de la Secretaría de Seguridad Ciudadana (SSC) de la Ciudad de México**.

Esta fuente permitirá trabajar con variables relacionadas con:

* Fecha del hecho.
* Hora del hecho.
* Alcaldía.
* Tipo de evento.
* Ubicación.
* Personas lesionadas.
* Personas fallecidas.
* Coordenadas geográficas.
La información será utilizada para realizar el análisis de frecuencia y severidad planteado en la pregunta de negocio.
---

## Fuentes complementarias

El proyecto contempla el uso y revisión de otras fuentes de información relacionadas con los hechos e incidentes de tránsito:

### C5 – Incidentes viales

Fuente de datos abiertos de la Ciudad de México que contiene registros de incidentes viales reportados al C5.

### INEGI / SINEGI

Fuente estadística que permitirá complementar y contextualizar la información relacionada con accidentes y hechos de tránsito.

### Kaggle

Se considera el dataset: **Accidentes viales en México 1997–2022**
Esta fuente será utilizada como fuente complementaria
---
## Indicadores principales

Para responder la pregunta de negocio se consideran inicialmente los siguientes indicadores:

| Indicador               | Descripción                                                      |
| ----------------------- | ---------------------------------------------------------------- |
| Frecuencia de hechos    | Número total de hechos de tránsito registrados                   |
| Frecuencia por alcaldía | Número de hechos registrados en cada alcaldía                    |
| Frecuencia por horario  | Número de hechos registrados por hora o intervalo horario        |
| Personas lesionadas     | Total de personas lesionadas registradas                         |
| Personas fallecidas     | Total de personas fallecidas registradas                         |
| Lesionados por hecho    | Promedio de personas lesionadas por hecho                        |
| Fallecidos por hecho    | Promedio de personas fallecidas por hecho                        |
| Hechos con lesionados   | Cantidad de hechos en los que se registraron personas lesionadas |
| Hechos con fallecidos   | Cantidad de hechos en los que se registraron personas fallecidas |
---
## Flujo que se tendra en Inteligencia de Negocios

El proyecto seguirá el siguiente flujo:

```text
DATOS CRUDOS
     ↓
Exploración y análisis con Python
     ↓
ETL
     ↓
PostgreSQL
     ↓
Consultas SQL
     ↓
Power BI
     ↓
Indicadores y visualizaciones
     ↓
Análisis de frecuencia y severidad
     ↓
Información para la toma de decisiones
```
---
## Organización del repositorio

El repositorio se organizará de la siguiente manera:

```text
Proyecto-sobre-Analisis-de-hechos-de-transito-de-la-CDMX
│
├── 📂 Bitacora
│   └── 📄 Bitacora_AC.md
│
├── 📂 Data
│   ├── 📦 CARPETA_DATOS.zip
│   ├── 📓 Data.ipynb
│   ├── 📄 README.md
│   └── 📂 raw
│       ├── 📂 c5
│       │   └── 📄 .gitkeep
│       ├── 📂 inegi
│       │   └── 📄 .gitkeep
│       ├── 📂 kaggle
│       │   └── 📄 .gitkeep
│       └── 📂 ssc
│           └── 📄 .gitkeep
│
├── 📂 Docs
│   │
│   ├── 📂 Diccionario_o_metadatos
│   │   ├── 📊 DiccionarioDatos_C5.xlsx
│   │   ├── 📄 Diccionario_C5.md
│   │   ├── 📄 Diccionario_INEGI_ATUS.md
│   │   ├── 📄 Diccionario_Kaggle.md
│   │   ├── 📄 Diccionario_SSC.MD
│   │   ├── 📄 Nota.md
│   │   └── 📄 diccionario_de_datos_atus_anual_1997_2025.csv
│   │
│   ├── 📄 Avance01_AyC.pdf
│   ├── 📄 Diccionario_o_metadatos.docs
│   └── 📄 Evaluacion_fuentes.pdf
│
├── 📂 Notebooks
│   │
│   ├── 📂 DatosCrudos_C5
│   │   └── 📄 Donde.md
│   │
│   ├── 📂 DatosCrudos_INEGI_ATUS
│   │   └── 📄 Donde.md
│   │
│   ├── 📂 DatosCrudos_KAGGLE
│   │   └── 📄 Donde.md
│   │
│   ├── 📂 DatosCrudos_SSC
│   │   └── 📄 Donde.md
│   └── 📄 Nota.md
│
├── 📂 Presentacion
│   └── 📄 Avance01_Presentacion.pdf
│
├── 📄 .gitignore
└── 📄 README.md
```

## Nota sobre los datos crudos

Algunos archivos de datos pueden superar el límite de tamaño permitido por GitHub. Por esta razón, los archivos originales de gran tamaño no necesariamente serán almacenados directamente en el repositorio.

En esos casos se conservará la **fuente oficial, el enlace de consulta o descarga, los metadatos, el diccionario de variables y las instrucciones necesarias para acceder a los datos crudos**.

Esto permitirá documentar la procedencia de los datos y mantener reproducible el proyecto sin exceder los límites de almacenamiento del repositorio.
---

## Repositorio

**GitHub:**
https://github.com/citlalliruiz31/Proyecto-sobre-Analisis-de-hechos-de-transito-de-la-CDMX

---

## Propósito del repositorio

Este repositorio concentra los documentos, datos disponibles, metadatos, código, notebooks, consultas, presentaciones, evidencias y demás materiales generados durante el desarrollo del Proyecto Semestral de Inteligencia de Negocios.

