
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
