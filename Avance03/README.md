# Avance 03 — ETL reproducible y análisis descriptivo

**Proyecto:** Análisis de hechos de tránsito en la Ciudad de México

**Equipo:** A&C — Méndez Cabral Ángel David (`23-003-1466`) y Ruiz Moreno Citlalli Viviana (`23-003-1162`)

**Institución:** Universidad Autónoma de la Ciudad de México (UACM) · Colegio de Ciencia y Tecnología · Inteligencia de Negocios · Grupo 301 · Semestre 2026-2

**Docentes:** Araceli Liliana Reyes Cabello y Manuel Soto Romero
**Repositorio:** https://github.com/citlalliruiz31/Proyecto-sobre-Analisis-de-hechos-de-transito-de-la-CDMX

---

## 1. Pregunta de negocio y decisión apoyada

> **¿En qué alcaldías y franjas horarias de la Ciudad de México se registra la mayor cantidad de personas lesionadas en hechos de tránsito, de acuerdo con los registros disponibles a partir de 2018?**

**Decisión que apoya:** identificar y priorizar las alcaldías y franjas horarias con mayor volumen de personas lesionadas registradas para orientar análisis posteriores y medidas preventivas de seguridad vial. El alcance es **descriptivo** (no inferencial ni causal), ya que no se dispone de datos de flujo vehicular o población expuesta para calcular tasas de riesgo relativo.

---

## 2. Fuentes y declaración explícita de no integración

Conforme al [Documento de reglas](Reglas/Documento%20de%20reglas%20.md):

- **No se integran (ni unen ni suman) las fuentes SSC, C5 e INEGI-ATUS entre sí**, debido a que representan unidades de observación, coberturas temporales y definiciones administrativas distintas (y ATUS carece de folio operativo de la CDMX).
- **Dentro de SSC, las cinco tablas se limpian por separado (`SSC-R06`)** para evitar multiplicación artificial de filas en relaciones `1:N`.
- **Kaggle** (*Accidentes viales en México 1997–2022*) queda excluido del ETL por haberse verificado su coincidencia exacta con INEGI-ATUS en `2018–2022` (`43,217` filas).

| Fuente | Rol en Avance 03 | Cobertura | Unidad (`1 fila =`) | Filas crudas | Delimitadas CDMX (2018+) |
|---|---|---|---|---:|---:|
| **SSC** (5 tablas) | **Principal** | 2018–2023 (*TipoPersona* 2020–2023) | Hecho / Vehículo / Persona | 759,074 | 759,069 |
| **C5** (`inViales`) | **Complementaria** | 2018–feb 2024 | Incidente vial reportado | 2,115,080 | 1,341,419 |
| **INEGI-ATUS** (`atus_anual`) | **Referencia estadística** | 2018–2025 | Accidente registrado (46 cols) | 2,883,722 | 62,424 |

### Integridad de los datos crudos (`RG-01`)
Las salidas guardadas corresponden a corridas realizadas el **9 de noviembre de 2026**. En el contenido actual de este repositorio no están `CARPETA_DATOS/`, los archivos procesados ni las bitácoras exportadas; por ello, en este entorno no se volvió a comprobar su integridad ni se recalcularon las cifras. Los archivos pesados de origen se reportan disponibles en el Release de Avance 02: [`CARPETA_DATOS.zip`](https://github.com/citlalliruiz31/Proyecto-sobre-Analisis-de-hechos-de-transito-de-la-CDMX/releases/download/avance02-datos/CARPETA_DATOS.zip).

Los notebooks `01` a `03` admiten leer salidas procesadas previas o los archivos originales en modo solo lectura. Para reproducirlos en este checkout se deben restaurar las fuentes en las rutas que reconoce cada notebook; la presencia de salidas incrustadas en un `.ipynb` no sustituye esos insumos.

---

## 3. Dependencias y entorno

- **Python:** `3.10+` (`pandas`, `numpy`; `matplotlib` y/o `Pillow` para las gráficas de los notebooks de análisis)
- **Biblioteca estándar:** `pathlib`, `datetime`, `zoneinfo`, `hashlib`, `csv`, `gzip`, `re`, `unicodedata`

---

## 4. Organización de archivos entregados

```text
Avance03/
├── README.md
├── Docs/
│   ├── Avance03_AyC.pdf
│   └── Informe_Avance03.docx
├── Notebooks/
│   ├── 01_ETL_SSC_Avance03 .ipynb
│   ├── 02_ETL_C5_Avance03 .ipynb
│   ├── 03_ETL_INEGI_ATUS_Avance03 .ipynb
│   ├── 04_Analisis_Estadistico_Avance03 .ipynb
│   ├── 04b_Analisis_Estadistico_C5_Avance03 .ipynb
│   ├── 04c_Analisis_Estadistico_INEGI_ATUS_Avance03 .ipynb
│   └── 05_Conciliacion_Bitacora_Auditoria_Avance03 .ipynb
├── Evidencias/
│   └── [exportaciones HTML de las salidas guardadas de cada notebook]
├── Presentacion/
│   └── Presentacion_Avance03.pptx
└── Reglas/
    └── Documento de reglas .md
```

En esta carpeta no están los datos crudos, los CSV procesados ni las bitácoras. Los notebooks conservan salidas de ejecuciones previas, cuyas rutas corresponden al equipo donde se generaron.

## 5. Evidencias de resultados por notebook

Cada notebook disponible conserva las salidas de sus celdas ejecutadas. Para facilitar su consulta y conservar una versión estática con tablas y gráficas, esas salidas también se exportaron a HTML en [`Evidencias/`](Evidencias/). Las exportaciones reflejan el contenido ya guardado en cada `.ipynb`; **no representan una nueva ejecución ni una validación con datos disponibles en este checkout**.

| Notebook | Evidencia HTML |
|---|---|
| ETL SSC | [01_ETL_SSC_Avance03 .html](Evidencias/01_ETL_SSC_Avance03%20.html) |
| ETL C5 | [02_ETL_C5_Avance03 .html](Evidencias/02_ETL_C5_Avance03%20.html) |
| ETL INEGI-ATUS | [03_ETL_INEGI_ATUS_Avance03 .html](Evidencias/03_ETL_INEGI_ATUS_Avance03%20.html) |
| Análisis SSC | [04_Analisis_Estadistico_Avance03 .html](Evidencias/04_Analisis_Estadistico_Avance03%20.html) |
| Análisis C5 | [04b_Analisis_Estadistico_C5_Avance03 .html](Evidencias/04b_Analisis_Estadistico_C5_Avance03%20.html) |
| Análisis INEGI-ATUS | [04c_Analisis_Estadistico_INEGI_ATUS_Avance03 .html](Evidencias/04c_Analisis_Estadistico_INEGI_ATUS_Avance03%20.html) |
| Conciliación y auditoría | [05_Conciliacion_Bitacora_Auditoria_Avance03 .html](Evidencias/05_Conciliacion_Bitacora_Auditoria_Avance03%20.html) |

El notebook 05 conserva un resultado previo que indica que SSC no tenía conciliación disponible en la ruta usada entonces. Esa salida se mantiene como evidencia histórica y **no debe interpretarse como auditoría vigente** de las corridas citadas en este README.

La presentación ejecutiva de 10 diapositivas está en [`Presentacion_Avance03.pptx`](Presentacion/Presentacion_Avance03.pptx).

---

## 6. Orden de ejecución y reproducibilidad

Para reproducir los resultados completos, primero se deben disponer las fuentes crudas o procesadas en las rutas reconocidas por los notebooks. Las salidas incrustadas no permiten recalcular los resultados sin esos archivos.

1. Abrir JupyterLab / Jupyter Notebook en esta carpeta raíz.
2. Ejecutar en orden:
   1. [`01_ETL_SSC_Avance03 .ipynb`](Notebooks/01_ETL_SSC_Avance03%20.ipynb)
   2. [`02_ETL_C5_Avance03 .ipynb`](Notebooks/02_ETL_C5_Avance03%20.ipynb)
   3. [`03_ETL_INEGI_ATUS_Avance03 .ipynb`](Notebooks/03_ETL_INEGI_ATUS_Avance03%20.ipynb)
   4. [`04_Analisis_Estadistico_Avance03 .ipynb`](Notebooks/04_Analisis_Estadistico_Avance03%20.ipynb)
   5. [`04b_Analisis_Estadistico_C5_Avance03 .ipynb`](Notebooks/04b_Analisis_Estadistico_C5_Avance03%20.ipynb)
   6. [`04c_Analisis_Estadistico_INEGI_ATUS_Avance03 .ipynb`](Notebooks/04c_Analisis_Estadistico_INEGI_ATUS_Avance03%20.ipynb)
   7. [`05_Conciliacion_Bitacora_Auditoria_Avance03 .ipynb`](Notebooks/05_Conciliacion_Bitacora_Auditoria_Avance03%20.ipynb), cuando estén disponibles las carpetas exportadas y bitácoras.

Cuando se ejecutan con sus insumos, los notebooks ETL generan salidas por `RUN_ID` (`YYYYMMDD_HHMMSS`); el notebook `05` requiere esas salidas para realizar la auditoría global.

---

## 7. Resumen de conciliación y resultados registrados

### Resultados ETL de las salidas guardadas

Las corridas ETL consignadas en las salidas de los notebooks son: **SSC `20261109_043146`**, **C5 `20261109_043243`** e **INEGI-ATUS `20261109_043449`**. Las corridas de análisis registradas son: **SSC `20261109_125058`** (documentada en el informe), **C5 `20261109_132918`** e **INEGI-ATUS `20261109_132940`**. Estos resultados no se volvieron a calcular en este checkout.

| Fuente / Tabla | Entrada delim. | Limpios (conservados) | Pendientes | Excluidos por regla | Dup. exactos | Total reconciliado |
|---|---:|---:|---:|---:|---:|---:|
| SSC · `HechosTransito` | 134,078 | 134,078 | 0 | 0 | 0 | 134,078 |
| SSC · `VehiculosInvolucrados` | 215,078 | 215,078 | 0 | 0 | 0 | 215,078 |
| SSC · `PersonasLyFporSexo` | 144,043 | 144,043 | 0 | 0 | 0 | 144,043 |
| SSC · `PersonasLyFporEdad` | 158,076 | **142,176** | **12,388** | **14** (`>99`) | **3,498** | **158,076** |
| SSC · `PersonasLyFporTipoPersona` | 107,794 | 107,794 | 0 | 0 | 0 | 107,794 |
| C5 · `incidentes_viales` | 1,341,419 | **1,265,215** | 0 | **76,204** (`C5-R03`) | 0 | **1,341,419** |
| INEGI-ATUS · CDMX (2018–2025) | 62,424 | **62,277** | **2** (`2023-12-32`) | 0 | **145** (46 cols) | **62,424** |

> Las marcas superpuestas (folios repetidos en SSC/C5 y `1,544` reportes C5 sin `hora_creacion`) se reportan por separado y no se suman como registros adicionales.

> **Alcance de la auditoría:** las salidas guardadas en el notebook `05` provienen de otra ruta de ejecución y señalan que SSC no tiene conciliación disponible. No se usan como verificación de las corridas anteriores; la auditoría debe repetirse cuando estén disponibles las exportaciones y bitácoras correspondientes.

### Hallazgos principales del análisis descriptivo

#### Fuente principal: SSC (resultados documentados en [Informe_Avance03.docx](Docs/Informe_Avance03.docx); el notebook de análisis `04` no está en esta carpeta)
- **Territorial (`alcaldia_normalizada`, `16` demarcaciones):** `155,988` personas lesionadas en `134,078` hechos (`2018–2023`). Las tres principales —**Cuauhtémoc** (`22,573`), **Iztapalapa** (`22,345`) y **Gustavo A. Madero** (`17,549` ya unificada)— concentran **`40.05%`** (`62,467`) del total; Milpa Alta registra el menor volumen (`1,127`, `0.72%`).
- **Franja horaria (`hora_evento`):** la franja **Tarde (12:00–17:59)** concentra **`47,294`** lesionados (`31.50%` con hora válida), seguida de Mañana (`42,303`), Noche (`40,943`) y Madrugada (`19,584`). `5,864` lesionados (`5,008` hechos) sin hora válida permanecen sin imputación (`RG-08`).
- **Severidad por hecho:** media = `1.1634` lesionados/hecho, mediana = `1.0`, moda = `1.0`, `DE = 0.6253`, `Q1 = Q3 = 1.0`, rango `0–25` (`1,902` hechos con `0` lesionados).
- **Perfil etario limpio (`PersonasLyFporEdad`, `N = 142,176`):** media = `33.4634` años (vs. `33.4086` pre-deduplicación en `144,144` filas), mediana = `30`, moda = `25`, `Q1 = 23`, `Q3 = 41`, `DE = 14.8870` (solo condición *lesionada*: `N = 140,050`, media `33.3957`).

#### Fuente complementaria: C5 ([notebook 04b](Notebooks/04b_Analisis_Estadistico_C5_Avance03%20.ipynb))
- **Territorial (`alcaldia_normalizada`, `N = 1,265,215` reportes limpios):** **Iztapalapa** (`217,899`, `17.22%`), **Gustavo A. Madero** (`139,217`, `11.00%`) y **Cuauhtémoc** (`126,650`, `10.01%`) concentran **`38.24%`** (`483,766`); Milpa Alta registra el mínimo (`8,389`, `0.66%`). *(Reportes operativos C5 ≠ personas lesionadas confirmadas).*
- **Franja de creación/registro (`_hora_creacion_validada`, regla `C5-R04`):** **Noche (18:00–23:59)** concentra **`457,993`** reportes (`36.24%` con hora válida), seguida de Tarde (`414,584`), Mañana (`250,991`) y Madrugada (`140,186`); `1,461` reportes limpios sin hora (`1,544` pre `C5-R03`) no se imputan ni se sustituyen por `hora_cierre`.
- **Tiempo de atención/cierre (`N = 1,263,727` pares `>= 0` min):** media = **`181.17 min`** (`DE = 2,450.43 min`) frente a mediana = **`116.83 min`**, moda = `3.0 min`, `Q1 = 15.15 min`, `Q3 = 187.88 min`; la cola extrema (`21,993` casos `> 24 h`, `1.74%`) distorsiona el promedio (`<= 24 h`, `N = 1,241,734`: media = `120.04 min`). Se separan `9` negativos y `1,479` sin marca completa.
- **Impacto `C5-R03` y composición `incidente_c4`:** retirar `76,204` contradicciones territoriales (`5.68%`) impacta más a Iztacalco (`10.33%`) e invierte los rangos #5/#6 (Benito Juárez ↔ Coyoacán) y #7/#8 (Venustiano Carranza ↔ Álvaro Obregón). Además, **`48.35%`** (`611,744`) son *Choque sin lesionados*, frente a *Choque con lesionados* (`340,451`, `26.91%`), *Atropellado* (`147,982`, `11.70%`) y *Motociclista* (`108,685`, `8.59%`).

#### Fuente de referencia: INEGI-ATUS ([notebook 04c](Notebooks/04c_Analisis_Estadistico_INEGI_ATUS_Avance03%20.ipynb))
- **Territorial (`alcaldia_normalizada`, `2018–2025`):** **`17,637`** personas heridas y `1,896` fallecidas (contexto) en `62,277` accidentes limpios. Top 3 por heridos —**Cuauhtémoc** (`3,359`), **Gustavo A. Madero** (`2,961`) e **Iztapalapa** (`1,734`)— concentran **`45.67%`** (`8,054`); Tláhuac registra el mínimo (`113`, `0.64%`).
- **Franja horaria (`ID_HORA`, `0` faltantes):** **Tarde (12:00–17:59)** concentra más heridos (`4,998`, `28.34%`), seguida de Mañana (`4,828`), Noche (`4,595`) y Madrugada (`3,216`). Aunque Mañana suma más fallecidos absolutos (`533`), **Madrugada** muestra la mayor letalidad relativa: **`4.86`** fallecidos por cada 100 accidentes (`490` en `10,078`).
- **Severidad y clase (`CLASACC`):** media = `0.2832` heridos/accidente, mediana = `0.0`, moda = `0`, `DE = 0.6803`, `Q1 = Q3 = 0.0`, máx. = `43` (`48,071` con `0` heridos = `77.19%` vs. `14,206` con `>= 1`). Desglose `CLASACC`: *Sólo daños* `46,503` (`74.67%`), *No fatal* `13,961` (`22.42%`) y *Fatal* `1,813` (`2.91%`).
- **Impacto `INEGI-R01`, serie `2018–2025` y `ID_EDAD`:** retirar `145` duplicados exactos sobre 46 columnas reduce de `62,424` a `62,277` limpios (`-15` heridos; `75/145` en Cuauhtémoc; `1` fecha `2023-12-32` retirada como copia y `2` en pendientes). En edad conocida del conductor (`1–98`, `N = 48,666`): media = `38.50`, mediana = `37`, moda = `30`, `Q1 = 28`, `Q3 = 47`, `DE = 12.93`; se separan `12,948` en `0` (`100% SEXO = 'Se fugó'`) y `663` en `99`.
