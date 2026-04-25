# Conclusiones del Análisis de Datos - Sprint 1
Luego de procesar el dataset speeding_fines.csv y realizar una limpieza profunda, la conclusión principal es que la base de datos presenta fallas críticas de integridad, aunque el saneamiento de registros permitió obtener una visión más clara de la realidad operativa.

#1. Calidad de los Datos y Limpieza
Para este trabajo, la limpieza de datos fue fundamental. Decidimos eliminar los registros que tenían estado ERROR y aquellos donde la velocidad era 0 o negativa, porque claramente eran fallos del sensor. También borramos las filas sin radar_id, ya que una multa que no se sabe de dónde viene no tiene validez. Si no hubiéramos hecho esto, los promedios de velocidad y los gráficos finales estarían distorsionados por datos que no son reales.

#2. El problema de la hora (41.8% a las 00:00)
Como se ve en el gráfico de torta, hay un 41.8% de infracciones concentradas a las 00:00. Esto no significa que la gente corra más a medianoche. En realidad, es un problema de los radares: son multas que están bien sacadas (tienen patente y velocidad), pero que por algún error técnico perdieron la hora original. Al normalizar los datos para que el código no falle, todos esos registros sin hora se agruparon en la medianoche, creando este pico artificial.

#3. Diagnóstico del sistema Urban Flow
La conclusión principal es que los datos sirven para saber quiénes son los infractores más frecuentes y cuánto deberían pagar, pero no sirven para analizar horarios. Con casi la mitad de las multas sin una hora real, no podemos decir con seguridad cuáles son las "horas pico" de infracciones. Intentar sacar una conclusión sobre en qué momento del día hay más peligro sería adivinar, no analizar.

#4. Recomendación
Para mejorar el sistema en el futuro, no alcanza con arreglar los datos una vez que ya están en el Excel. Lo que se necesita es revisar los equipos (radares) para que graben la hora correctamente desde el principio. La prioridad debería ser asegurar que cada multa guarde su horario real, porque sin ese dato el sistema pierde gran parte de su valor para prevenir accidentes y organizar el tránsito.
