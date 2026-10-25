# Bitácora — Equipo A&C

| Fecha | Fuente | Etapa | Tarea | Responsable | Evidencia | Estado |
|---|---|---|---|---|---|---|
| Por registrar | Todas | 1 | Leer crudos, perfilar y delimitar CDMX/2018+ | Equipo A&C | contrato_lectura.csv, impacto_etapa1.csv | Por ejecutar |
| Por registrar | Todas | 2 | Validar nulos, formatos, repeticiones y frecuencias | Equipo A&C | resumen_validacion.csv y perfiles | Por ejecutar |
| Por registrar | Todas | 3 | Normalizar columnas auxiliares y comparar | Equipo A&C | comparacion_y_bitacora.csv | Por ejecutar |
| Por registrar | Kaggle | 1 | Investigar desalineación de columnas | Equipo A&C | pendientes.csv | Pendiente |
| Por registrar | SSC | 3 | Confirmar granularidad antes de retirar filas idénticas | Equipo A&C | Casos revisados | Pendiente |

## Acuerdo de duplicados
La profesora Liliana nos dio la regla ya que no pudimos preguntarle al profesor Emilio. Primero identificamos folios repetidos, después comprobamos si corresponde a la misma alcaldía y finalmente comparamos las filas completas. Conservamos registros que difieren en alcaldía o contenido. Los casos idénticos se someten a revisión según su unidad de observación. No borramos automáticamente folios `SD`.

## Plantilla por transformación
**Archivo:**  
**Problema y evidencia:**  
**Regla y fundamento:**  
**Columnas afectadas:**  
**Operación aplicada:**  
**Filas antes/después:**  
**Cantidad afectada:**  
**Comprobación:**  
**Pendientes y efecto analítico:**  

El dia 13 de octubre del 2026 se hizo la correcion de funciones_calidad.py 

Esta versión conserva tus tres etapas y las funciones para SSC, C5, INEGI y Kaggle. Además, incluye las correcciones que encontramos al revisar tus datos de SSC:
- Convierte las fechas de SSC con el formato %Y-%m-%d.
- Reconoce CUAJIMALPA, MAGDALENA CONTRERAS y GUSTAVO A. MADERO como alcaldías válidas.
- Conserva los valores originales y agrega una columna auxiliar normalizada.
- Genera evidencia de los registros excluidos en la Etapa 1.
- No elimina duplicados automáticamente, porque primero debemos revisar la unidad de observación de cada archivo.