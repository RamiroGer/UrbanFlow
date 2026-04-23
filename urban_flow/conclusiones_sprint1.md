# Conclusiones del Análisis de Datos - Sprint 1

Después de trabajar con el dataset `speeding_fines.csv`, la conclusión principal es que la base de datos está bastante "herida" en términos de calidad.

Lo más preocupante que encontré fue que el 77.29% de las fechas tuvieron que ser normalizadas a 1932-01-01. Esto no es un detalle menor: significa que casi 8 de cada 10 multas no tienen una fecha real confiable. Lo mismo pasa con las horas, donde el 40.16% estaban vacías.

¿Para qué sirve el dataset entonces?
- Todavía es muy útil para ver quiénes son los infractores más frecuentes (por patente).
- Sirve para entender qué tipo de multas son las más comunes y de qué montos estamos hablando.

¿Para qué NO sirve?
- No podemos usar esto para saber en qué horario hay más infracciones o en qué mes del año la gente corre más, porque el sesgo que introducen los datos normalizados es demasiado grande.

Para que "Urban Flow" sea un proyecto serio en el futuro, habría que arreglar el sistema de captura de datos de las cámaras o los sensores, porque hoy estamos trabajando con un margen de error temporal altísimo.
