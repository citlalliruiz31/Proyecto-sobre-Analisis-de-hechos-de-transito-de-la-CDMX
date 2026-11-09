# Avance 03

Este apartado contiene el documento del avance, las reglas de trabajo y los notebooks para procesar y analizar los datos de hechos de tránsito de la Ciudad de México.

## Contenido

- [`Docs/Avance03_AyC.pdf`](Docs/Avance03_AyC.pdf): documento del avance.
- [`Reglas/Documento de reglas .md`](Reglas/Documento%20de%20reglas%20.md): reglas y criterios del procesamiento.
- [`Notebooks/`](Notebooks/): notebooks ETL, análisis estadístico y auditoría.

## Obtener los archivos CSV

Los CSV de resultados se generan localmente al ejecutar los notebooks; no es necesario que estén incluidos en el repositorio. Antes de ejecutarlos, coloca los archivos fuente en las carpetas de entrada esperadas:

- SSC: `data/raw/`
- C5: `data/raw/C5/`
- INEGI-ATUS: `data/raw/INEGI_ATUS/`

Los notebooks de C5 e INEGI-ATUS también buscan archivos en `Datos/` y en algunas carpetas de resultados del Avance 02. Si tus fuentes están en otra ubicación, revisa las rutas de entrada configuradas en el notebook correspondiente.

Abre el proyecto en Jupyter y ejecuta las celdas de cada notebook en este orden:

1. [`01_ETL_SSC_Avance03.ipynb`](Notebooks/01_ETL_SSC_Avance03.ipynb)
2. [`02_ETL_C5_Avance03.ipynb`](Notebooks/02_ETL_C5_Avance03.ipynb)
3. [`03_ETL_INEGI_ATUS_Avance03.ipynb`](Notebooks/03_ETL_INEGI_ATUS_Avance03.ipynb)
4. [`04_Analisis_Estadistico_Avance03.ipynb`](Notebooks/04_Analisis_Estadistico_Avance03.ipynb), después del ETL de SSC.
5. [`05_Conciliacion_Bitacora_Auditoria_Avance03.ipynb`](Notebooks/05_Conciliacion_Bitacora_Auditoria_Avance03.ipynb), después de ejecutar los ETL.

En Jupyter puedes usar **Restart & Run All** para ejecutar cada notebook desde el inicio. Los resultados se guardan en carpetas con fecha y hora para no sobrescribir ejecuciones anteriores. En general, los ETL escriben sus CSV en `data/processed/<fuente>/<id_de_ejecucion>/` y las bitácoras en `bitacora/`; algunos archivos se exportan comprimidos con extensión `.csv.gz`. El análisis estadístico y la auditoría generan sus propios reportes en `data/processed/`.

La carpeta `data/` y los CSV resultantes aparecen al ejecutar los notebooks y pueden no estar presentes en el repositorio. Para reproducir los resultados se necesitan los CSV fuente. Los resultados y conteos definitivos son los que se obtengan al ejecutar los notebooks con esos datos.
