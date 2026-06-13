
## Reflexión — Sprint 2

El presente sprint tuvo como objetivo vincular el dataset de multas
por exceso de velocidad procesado en el Sprint 1 con el dataset de
imágenes capturadas por los radares urbanos de Vaalserberg.

### Sobre los datos explorados

El dataset de multas contaba con 1713 registros con información de
patentes, velocidades, fechas y estado de pago (PAGADA, IMPAGA,
APELADA, ERROR). El dataset de imágenes contenía 106 archivos .jpg
divididos en dos grupos:

- **plates**: recortes directos de la zona de la patente.
- **completes**: fotografías completas del vehículo infractor.

### Sobre el proceso de vinculación

Para extraer las patentes de las imágenes se utilizó EasyOCR con
soporte para español. Dado que el OCR introduce ruido en la lectura
(espacios, corchetes, caracteres especiales), se implementó una
función de limpieza que normaliza el texto eliminando todo carácter
no alfanumérico antes de realizar la comparación.

El criterio de coincidencia utilizado fue una comparación carácter a
carácter de izquierda a derecha con un umbral mínimo del 80%, lo que
permitió tolerar errores puntuales de reconocimiento sin aceptar
coincidencias demasiado débiles.

### Resultados y limitaciones

De los 106 archivos procesados, se lograron 25 coincidencias con el
dataset de multas. Las principales limitaciones observadas fueron:

- Confusión entre caracteres visualmente similares (O/0, I/1, B/8).
- Imágenes completes con baja resolución en la zona de la patente.
- Registros del dataset sin imagen asociada, lo que indica que el
  sistema de cámaras no tiene cobertura total de las infracciones.

### Valor del cruce de datos

El subconjunto más relevante para una acción administrativa inmediata
es el de multas con estado IMPAGA que cuentan con imagen asociada,
ya que representa infracciones con evidencia visual válida y deuda
pendiente de cobro. Este cruce entre datos tabulares e imágenes
demuestra el valor del procesamiento multimodal en sistemas de
control urbano.

## Reflexión — Sprint 2

El presente sprint tuvo como objetivo vincular el dataset de multas
por exceso de velocidad procesado en el Sprint 1 con el dataset de
imágenes capturadas por los radares urbanos de Vaalserberg.

### Sobre los datos explorados

El dataset de multas contaba con 1274 registros limpios (reducidos
desde 1713 originales tras el proceso de limpieza del Sprint 1), con
información de patentes, velocidades, fechas y estado de pago
(PAGADA, IMPAGA, APELADA, ERROR). Se identificaron 66 patentes
únicas, con una frecuencia de entre 15 y 38 multas por patente.
El dataset de imágenes contenía 106 archivos .jpg divididos en:

- plates: 87 recortes directos de la zona de la patente.
- completes: 19 fotografías completas del vehículo infractor.

### Sobre el proceso de vinculación

Para extraer las patentes de las imágenes se utilizó EasyOCR con
soporte para español, logrando detectar texto en 105 de las 106
imágenes. Dado que el OCR introduce ruido en la lectura (espacios,
corchetes, caracteres especiales), se implementó una función de
limpieza que normaliza el texto eliminando todo carácter no
alfanumérico antes de realizar la comparación.

El criterio de coincidencia utilizado fue una comparación carácter a
carácter de izquierda a derecha con un umbral mínimo del 80%, lo que
permitió tolerar errores puntuales sin aceptar coincidencias débiles.

### Decisión de diseño: asignación múltiple por patente

Durante el desarrollo se tomó la decisión de asignar la imagen
matcheada a todas las filas del dataset que compartan la misma
patente, en lugar de asignarla a una sola multa.

Esta decisión se fundamenta en que el dataset contiene múltiples
multas por el mismo vehículo. Si una imagen valida visualmente una
patente, esa evidencia es válida para todas las infracciones de ese
vehículo. Ignorar las demás filas implicaría descartar evidencia
válida sin justificación.

El resultado fue pasar de 25 coincidencias (asignación única) a 491
coincidencias (asignación múltiple), lo cual refleja con mayor
fidelidad la realidad del sistema de radares.

### Resultados y limitaciones

De los 106 archivos procesados, 78 imágenes no tuvieron match con
ninguna patente del dataset. Las principales limitaciones fueron:

- Confusión entre caracteres visualmente similares (O/0, I/1, B/8).
- Imágenes completes con baja resolución en la zona de la patente.
- 783 multas sin imagen asociada, lo que indica que el sistema de
  cámaras no tiene cobertura total de las infracciones registradas.

### Valor del cruce de datos

El subconjunto más relevante para una acción administrativa inmediata
es el de las 152 multas con estado IMPAGA que cuentan con imagen
asociada, ya que representan infracciones con evidencia visual válida
y deuda pendiente de cobro. Este cruce entre datos tabulares e
imágenes demuestra el valor del procesamiento multimodal en sistemas
de control urbano.

## Reflexión — Sprint 2

El presente sprint tuvo como objetivo vincular el dataset de multas
por exceso de velocidad procesado en el Sprint 1 con el dataset de
imágenes capturadas por los radares urbanos de Vaalserberg.

### Sobre los datos explorados

El dataset de multas contaba con 1274 registros limpios (reducidos
desde 1713 originales tras el proceso de limpieza del Sprint 1), con
información de patentes, velocidades, fechas y estado de pago
(PAGADA, IMPAGA, APELADA, ERROR). Se identificaron 66 patentes
únicas, con una frecuencia de entre 15 y 38 multas por patente.
El dataset de imágenes contenía 106 archivos .jpg divididos en:

- plates: 87 recortes directos de la zona de la patente.
- completes: 19 fotografías completas del vehículo infractor.

### Sobre el proceso de vinculación

Para extraer las patentes de las imágenes se utilizó EasyOCR con
soporte para español, logrando detectar texto en 105 de las 106
imágenes. Dado que el OCR introduce ruido en la lectura (espacios,
corchetes, caracteres especiales), se implementó una función de
limpieza que normaliza el texto eliminando todo carácter no
alfanumérico antes de realizar la comparación.

El criterio de coincidencia utilizado fue una comparación carácter a
carácter de izquierda a derecha con un umbral mínimo del 80%, lo que
permitió tolerar errores puntuales sin aceptar coincidencias débiles.

### Decisión de diseño: asignación múltiple por patente

Durante el desarrollo se tomó la decisión de asignar la imagen
matcheada a todas las filas del dataset que compartan la misma
patente, en lugar de asignarla a una sola multa.

Esta decisión se fundamenta en que el dataset contiene múltiples
multas por el mismo vehículo. Si una imagen valida visualmente una
patente, esa evidencia es válida para todas las infracciones de ese
vehículo. Ignorar las demás filas implicaría descartar evidencia
válida sin justificación.

El resultado fue pasar de 25 coincidencias (asignación única) a 491
coincidencias (asignación múltiple), lo cual refleja con mayor
fidelidad la realidad del sistema de radares.

### Resultados y limitaciones

De los 106 archivos procesados, 78 imágenes no tuvieron match con
ninguna patente del dataset. Las principales limitaciones fueron:

- Confusión entre caracteres visualmente similares (O/0, I/1, B/8).
- Imágenes completes con baja resolución en la zona de la patente.
- 783 multas sin imagen asociada, lo que indica que el sistema de
  cámaras no tiene cobertura total de las infracciones registradas.

### Valor del cruce de datos

El subconjunto más relevante para una acción administrativa inmediata
es el de las 152 multas con estado IMPAGA que cuentan con imagen
asociada, ya que representan infracciones con evidencia visual válida
y deuda pendiente de cobro. Este cruce entre datos tabulares e
imágenes demuestra el valor del procesamiento multimodal en sistemas
de control urbano.

## Conclusión — Sprint 3

En este sprint se profesionalizó la solución del sistema de radares
urbanos de Vaalserberg incorporando persistencia real en base de datos.

### Sobre la migración a base de datos relacional

Los datos procesados en los sprints anteriores fueron migrados desde
archivos CSV a una base de datos SQLite estructurada mediante el ORM
de SQLAlchemy. El modelo relacional diseñado contempla cuatro
entidades: Vehiculo, Radar, Multa y Evidencia, respetando las
relaciones de uno a muchos y la opcionalidad de la evidencia visual.

### Sobre el versionado de datos con DVC

Los archivos binarios (imágenes y CSV procesado) fueron migrados de
git a DVC, lo cual es la práctica correcta para archivos de gran
tamaño o que cambian frecuentemente. Git queda reservado para el
código y la metadata, mientras que DVC gestiona los datos.

### Sobre la base de datos vectorial

Se incorporó ChromaDB con el modelo OpenCLIP para almacenar
representaciones vectoriales de las imágenes de patentes. Esto
permite buscar vehículos por similitud visual, sin depender de OCR,
lo que complementa y fortalece el sistema de identificación del
sprint anterior.

### Valor del sistema integrado

La combinación de una base relacional (consultas estructuradas) con
una base vectorial (búsqueda por similitud) representa un sistema
robusto y escalable para la gestión de infracciones de tránsito,
con capacidad de responder tanto preguntas analíticas como búsquedas
visuales aproximadas.

## Conclusión — Sprint 3

En este sprint se profesionalizó la solución del sistema de radares
urbanos de Vaalserberg incorporando persistencia real en base de datos.

### Sobre la migración a base de datos relacional

Los datos procesados en los sprints anteriores fueron migrados desde
archivos CSV a una base de datos SQLite estructurada mediante el ORM
de SQLAlchemy. El modelo relacional diseñado contempla cuatro
entidades: Vehiculo, Radar, Multa y Evidencia, respetando las
relaciones de uno a muchos y la opcionalidad de la evidencia visual.

### Sobre el versionado de datos con DVC

Los archivos binarios (imágenes y CSV procesado) fueron migrados de
git a DVC, lo cual es la práctica correcta para archivos de gran
tamaño o que cambian frecuentemente. Git queda reservado para el
código y la metadata, mientras que DVC gestiona los datos.

### Sobre la base de datos vectorial

Se incorporó ChromaDB con el modelo OpenCLIP para almacenar
representaciones vectoriales de las imágenes de patentes. Esto
permite buscar vehículos por similitud visual, sin depender de OCR,
lo que complementa y fortalece el sistema de identificación del
sprint anterior.

### Valor del sistema integrado

La combinación de una base relacional (consultas estructuradas) con
una base vectorial (búsqueda por similitud) representa un sistema
robusto y escalable para la gestión de infracciones de tránsito,
con capacidad de responder tanto preguntas analíticas como búsquedas
visuales aproximadas.
