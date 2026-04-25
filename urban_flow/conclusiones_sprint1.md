# Conclusiones del Análisis de Datos - Sprint 1

Luego de procesar el dataset speeding_fines.csv y realizar una limpieza profunda, la conclusión principal es que la base de datos presenta fallas críticas de integridad, aunque el saneamiento de registros permitió obtener una visión más clara de la realidad operativa.

## 1. Calidad y Normalización (Punto 3)
Durante la etapa de normalización, se confirmó una degradación importante en los datos temporales:
- **Fallas en las fechas:** El 77.29% de los registros originales carecían de fechas válidas, normalizándose a 1932-01-01. Esto indica una desconexión casi total entre el evento y su registro histórico.
- **Sesgo de Horas:** Tras eliminar los registros con estado "ERROR", el porcentaje de horas inválidas (normalizadas a 00:00) bajó del 40.16% a un **19.8%**. Esto demuestra que una gran parte de la "basura" temporal venía atada a errores de sistema que logramos depurar.
- **Normalización de Patentes:** Se estandarizaron los dominios eliminando caracteres especiales, asegurando la identificación unívoca de los infractores.

## 2. Limpieza y Depuración de Registros (Punto 4)
La limpieza fue más allá de lo básico para asegurar la calidad estadística:
- **Eliminación de Nulos:** Se descartaron filas sin patente, velocidad o ID de multa, pero también se incluyó el **radar_id** como campo crítico para garantizar la trazabilidad del origen.
- **Tratamiento de Outliers y Errores:** Se tomaron dos decisiones clave:
    1. Se eliminaron los registros con estado **"ERROR"**, ya que distorsionaban las estadísticas de tráfico.
    2. Se filtraron velocidades físicamente imposibles o incoherentes.
- **Cálculo de Infracciones:** Se aplicó el margen de tolerancia legal (5%), filtrando aquellos registros que no constituían una falta real según la normativa.

## 3. Diagnóstico de Utilidad del Proyecto
- **Utilidad actual:** El dataset saneado es altamente confiable para el ranking de infractores y la gestión de recaudación por multas válidas.
- **Limitaciones Técnicas:** Aunque la limpieza redujo el ruido, el 20% de datos temporales "por defecto" (00:00) sigue siendo un obstáculo para análisis de precisión sobre horarios pico.
- **Recomendación Estratégica:** El sistema Urban Flow es viable, pero requiere una intervención técnica en los dispositivos de captura. La prioridad debe ser estabilizar la marca de tiempo (timestamp) y reducir los registros fallidos, que representaban casi la mitad de las inconsistencias horarias.
