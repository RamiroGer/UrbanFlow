#Conclusiones del Análisis de Datos - Sprint 1
Luego de procesar el dataset speeding_fines.csv, la conclusión principal es que la base de datos presenta fallas críticas de integridad que condicionan cualquier análisis posterior, especialmente en lo que respecta al tiempo.

1. Calidad y Normalización (Punto 3)
Durante la etapa de normalización, el hallazgo más preocupante fue la falta de datos temporales confiables:

Fallas en las fechas: El 77.29% de los registros tenían fechas inválidas o ausentes. Para poder trabajar con el dataset sin que el código fallara, tuvimos que normalizarlas al valor por defecto 1932-01-01. Esto significa que casi 8 de cada 10 multas no tienen una fecha real rastreable.

Fallas en las horas: Un 40.16% de los registros no tenía hora cargada (aparecían como 00:00).

Identificación de infractores: Se limpiaron las patentes quitando símbolos y espacios. En los casos donde los datos eran directamente ilegibles, se optó por usar pd.NA para separar esos errores del resto de la muestra.

2. Limpieza y Depuración de Registros (Punto 4)
La limpieza de datos fue fundamental para quedarnos solo con la información que realmente tiene valor administrativo:

Registros descartados: Se eliminaron 1982 filas que no cumplían con los requisitos mínimos (faltaban patentes, velocidades o IDs de multa). Sin estos datos, una multa no puede ser procesada legalmente.

Inconsistencias físicas: Se detectaron 30 casos con velocidades de 0 km/h o menores. Estos registros se eliminaron por ser claramente errores de los sensores de los radares.

Filtro de infracciones reales: Se aplicó el cálculo de exceso de velocidad considerando el margen de tolerancia del 5%, descartando los registros que no llegaban a superar el límite legal.

3. Diagnóstico de Utilidad del Proyecto
A partir de estos resultados, podemos determinar el alcance real de "Urban Flow":

Utilidad actual: El dataset es valioso para identificar a los infractores más frecuentes y para calcular montos totales de deuda.

Limitaciones: No es posible realizar análisis de estacionalidad (saber qué mes hay más multas) o de franjas horarias de riesgo. Intentar sacar conclusiones sobre "horas pico" con un 40% de datos faltantes y un 80% de fechas inventadas nos llevaría a resultados totalmente sesgados y erróneos.

Recomendación final: Para que el proyecto sea viable a largo plazo, es urgente revisar la forma en que los sensores capturan y guardan la información. La prioridad debería ser corregir la generación de los timestamps, ya que la pérdida de casi el 80% de los datos temporales es el punto más débil del sistema actual.
