# PA04. Modelos de distribución de especies: diseño propio

**Asignatura:** Biogeografía (GEO-131)  
**Modalidad:** Trabajo de investigación aplicado con presentación oral

## 1. Objetivo

Modelizar la distribución potencial de una especie en un territorio determinado, utilizando registros reales de presencia y variables ambientales, y comparar los resultados de diferentes modelos de distribución de especies (*Species Distribution Models*, SDM).

La práctica se basa en un diseño propio. Cada estudiante tendrá libertad para seleccionar la especie, el territorio (todo el país o un ámbito más reducido), las fuentes de datos y las estrategias de análisis, siempre que justifique sus decisiones. No se proporciona una plantilla de análisis.

## 2. Datos y fuentes

Se deberán obtener, por cuenta propia:

- Registros georreferenciados de presencia de la especie seleccionada. Se pueden obtener de [GBIF](https://www.gbif.org/) o de otras bases de datos de ocurrencia, incluidos datos propios debidamente documentados.
- Una delimitación del área de estudio.
- **Al menos cuatro variables ambientales candidatas**, con cobertura del área de estudio y relevancia ecológica para la especie. Se podrán reunir más variables y seleccionar posteriormente las que se incorporarán a los modelos, evitando redundancia y complejidad innecesaria.

### Fuentes y variables ambientales sugeridas

| Grupo | Ejemplos de variables | Fuentes y herramientas |
|---|---|---|
| Clima | Temperatura, precipitación, estacionalidad (BIO1–BIO19) | [WorldClim](https://www.worldclim.org/), [CHELSA](https://chelsa-climate.org/) |
| Relieve | Elevación, pendiente, orientación, curvatura | [SRTM](https://www.earthdata.nasa.gov/), [Copernicus DEM](https://dataspace.copernicus.eu/), QGIS, GRASS GIS |
| Hidrología | Índice de humedad topográfica (TWI), distancia a cauces | [HydroSHEDS](https://www.hydrosheds.org/), DEM, GRASS GIS |
| Suelos | pH, textura, carbono orgánico | [SoilGrids](https://soilgrids.org/) |
| Vegetación | NDVI, EVI, altura del dosel | [Sentinel-2](https://dataspace.copernicus.eu/), [Landsat](https://www.usgs.gov/landsat-missions), [GEDI](https://gedi.umd.edu/) |
| Cobertura terrestre | Bosques, agricultura, pastizales, áreas urbanizadas | [ESA WorldCover](https://esa-worldcover.org/), [Dynamic World](https://dynamicworld.app/) |
| Factores antropogénicos | Distancia a carreteras y asentamientos | [OpenStreetMap](https://www.openstreetmap.org/) |
| Variables integradas | Estadísticas ambientales por hexágonos H3 (resoluciones 6 y 7) | [geofis/zonal-statistics](https://github.com/geofis/zonal-statistics) |

Estas fuentes son opcionales. Se podrán generar variables propias mediante [Google Earth Engine](https://earthengine.google.com/), [QGIS](https://qgis.org/), [GRASS GIS](https://grass.osgeo.org/), R o Python. No se exige utilizar el repositorio de estadísticas zonales del profesor.

## 3. Requisitos mínimos

- Plantear objetivos, preguntas de investigación e hipótesis, sustentados en una revisión básica de la literatura.
- Obtener, depurar y explorar los registros de presencia y preparar las variables ambientales, asegurando su compatibilidad espacial.
- Definir y justificar el área de calibración y la estrategia de generación de puntos de fondo o pseudoausencias, según el modelo. Los puntos de fondo no constituyen ausencias confirmadas.
- Ajustar **al menos tres modelos**, incluyendo los siguientes enfoques:

  | Modelo | Herramientas sugeridas en R | Herramientas sugeridas en Python |
  |---|---|---|
  | MaxEnt | [`maxnet`](https://cran.r-project.org/package=maxnet) | [`elapid`](https://github.com/earth-chris/elapid) |
  | Árbol de decisión (CART) | [`rpart`](https://cran.r-project.org/package=rpart) | [`scikit-learn`](https://scikit-learn.org/) |
  | Random Forest | [`ranger`](https://cran.r-project.org/package=ranger), `randomForest` | `scikit-learn` |

  Se podrán incorporar otros modelos, como GLM, GAM, SVM o Gradient Boosting. Las implementaciones indicadas son sugerencias.

- Evaluar y comparar la capacidad predictiva de los modelos mediante métricas apropiadas (por ejemplo, AUC-ROC o TSS, según los datos y el método de evaluación). Separar los datos de calibración y evaluación, preferiblemente considerando su estructura espacial.
- Generar mapas de distribución potencial o idoneidad ambiental, gráficos y tablas, e interpretar las diferencias entre los modelos desde una perspectiva biogeográfica. No interpretar automáticamente la idoneidad relativa como probabilidad absoluta de presencia.

## 4. Bitácoras de análisis y gestión de datos

El análisis deberá realizarse en R, Python o una combinación de ambos, mediante una o varias bitácoras **obligatoriamente reproducibles** (R Markdown, Quarto o Jupyter, por ejemplo). Se podrán utilizar los servidores RStudio y Jupyter del profesor o la computadora personal.

Las bitácoras deberán contener el flujo analítico completo, desde la lectura y preparación de los datos hasta la generación de los modelos, mapas, gráficos y tablas del manuscrito. Se deberán documentar las dependencias, las decisiones metodológicas y, cuando corresponda, las semillas aleatorias. Las tareas de preparación realizadas fuera de las bitácoras también deberán documentarse.

Todos los archivos necesarios deberán quedar disponibles en el repositorio de GitHub creado al aceptar la asignación. Se aplicarán las siguientes condiciones:

- No subir grandes bases de datos globales a los servidores del profesor. Filtrar los registros de ocurrencia y recortar las capas ambientales al ámbito de estudio previamente, por ejemplo, mediante QGIS en la computadora personal o Google Earth Engine.
- No incorporar a GitHub archivos individuales de más de **50 MB**, como restricción de esta práctica.
- Cuando un archivo necesario siga siendo demasiado grande después de recortarlo o filtrarlo, depositarlo en [Zenodo](https://zenodo.org/) e incluir en GitHub el enlace o DOI y las instrucciones para recuperarlo.
- Documentar las fuentes, versiones y procedimientos de preparación de los datos.

## 5. Manuscrito científico

Se elaborará un manuscrito científico utilizando cualquiera de las plantillas empleadas en las prácticas anteriores. No se proporciona una nueva plantilla. **No basta con subir un PDF:** el manuscrito deberá generarse mediante la compilación del archivo fuente de una de esas plantillas en RStudio (R Markdown o Quarto, según corresponda). Se entregarán tanto el PDF generado como todos los archivos necesarios para volver a compilarlo.

Las citas y referencias bibliográficas deberán gestionarse mediante las herramientas de citación del sistema de autoría (por ejemplo, BibTeX y Pandoc), y la numeración y las referencias cruzadas a figuras, tablas y secciones deberán generarse automáticamente mediante las herramientas propias de R Markdown o Quarto en RStudio, no escribirse manualmente.

El manuscrito deberá incluir, como mínimo: título y resumen, introducción (antecedentes, objetivos, preguntas e hipótesis), área de estudio, materiales y métodos, resultados, discusión, conclusiones y referencias bibliográficas.

Los mapas, gráficos y tablas del manuscrito deberán proceder de los análisis realizados y documentados en las bitácoras. **Las tablas deben ser tablas, no imágenes:** se deberán generar como elementos tabulares, por ejemplo, mediante `knitr::kable()` u otras herramientas compatibles con la plantilla. No se admitirán capturas de pantalla ni imágenes que hagan las veces de tablas.

## 6. Entregables

El repositorio deberá contener:

- Manuscrito científico compilado en PDF, su archivo fuente, bibliografía y demás archivos necesarios para reproducir la compilación.
- Una o varias bitácoras de análisis reproducibles.
- Datos de entrada utilizados o enlaces a los archivos depositados en Zenodo cuando su tamaño impida incorporarlos a GitHub.
- Mapas, gráficos y tablas utilizados en el manuscrito.
- Una breve descripción de la organización de los archivos y de cómo reproducir los análisis.

- Material utilizado en la presentación oral.
- Auditoría crítica del uso de inteligencia artificial.

## 7. Presentación oral

La presentación oral y defensa de la investigación son obligatorias. Cada estudiante deberá explicar y justificar sus decisiones metodológicas, los modelos empleados, su evaluación, los resultados y sus limitaciones, y responder preguntas sobre el código y los procedimientos utilizados. No basta con mostrar los productos finales: se deberá demostrar comprensión del trabajo realizado.

## 8. Auditoría crítica de inteligencia artificial

Se deberá incluir en el repositorio una auditoría crítica del uso de IA, indicando las herramientas utilizadas, las consultas relevantes, las soluciones o técnicas sugeridas, cómo se verificaron y qué se aceptó, modificó o descartó y por qué. Se deberán identificar también los errores o limitaciones detectados y explicar qué se aprendió durante el proceso. Si no se utilizó IA, se deberá declarar expresamente. La auditoría no sustituye las bitácoras de análisis ni la defensa oral.

## 9. Sugerencias para aprovechar la IA como herramienta de aprendizaje

La facilidad con la que la IA propone técnicas estadísticas y computacionales puede llevar a incorporar métodos que el estudiante todavía no comprende. Un manuscrito con muchas técnicas sofisticadas no es necesariamente mejor que uno con pocos métodos bien comprendidos y justificados.

Cuando se solicite una solución a la IA, es recomendable pedir también un **itinerario de aprendizaje acompañante**, adaptado a los conocimientos previos del estudiante, que permita comprender la solución antes de incorporarla a la investigación. Algunas sugerencias:

- Pedir una explicación de los fundamentos, supuestos, limitaciones y pertinencia ecológica de cada método, antes de solicitar el código.
- Solicitar un itinerario progresivo con conceptos previos, lecturas, ejemplos sencillos y ejercicios prácticos, avanzando después hacia los datos reales de la investigación.
- Pedir explicaciones del código por bloques, ejecutar cada bloque, modificar parámetros y examinar cómo cambian los resultados.
- Solicitar preguntas de autoevaluación y ejercicios de interpretación, intentar resolverlos sin ayuda y contrastar posteriormente las respuestas.
- Verificar las recomendaciones con documentación oficial y literatura científica; no aceptar referencias, resultados o afirmaciones sin comprobarlos.

Por ejemplo, además de pedir código para ajustar MaxEnt, se puede formular una consulta como esta:

> Ayúdame a ajustar un modelo MaxEnt con mis datos, pero diseña también un itinerario de aprendizaje que me permita comprender sus fundamentos, los puntos de fondo, la regularización, la evaluación del modelo y la interpretación de sus predicciones. Incluye ejercicios progresivos y preguntas que me permitan comprobar si realmente entiendo cada etapa. No avances a la siguiente hasta que pueda explicar la anterior.

Antes de incorporar una técnica al manuscrito, el estudiante debería poder explicar con sus propias palabras qué problema resuelve, cómo funciona, por qué la eligió y cómo interpreta sus resultados.

## 10. Consideraciones generales

Se valorará la autonomía en el diseño de la investigación, la justificación ecológica de las variables, la evaluación y comparación de los modelos, la calidad cartográfica, la reproducibilidad y la interpretación crítica de los resultados y sus limitaciones.

La inteligencia artificial podrá utilizarse como herramienta de asistencia para localizar fuentes, programar, resolver problemas y comprender métodos. **No se admite delegar los análisis en una IA para obtener directamente un manuscrito, gráficos o tablas sin ejecutar y comprender el proceso analítico.**

Las bitácoras deberán poder ejecutarse nuevamente a partir de los datos entregados y regenerar los resultados del manuscrito. **La reproducibilidad es un requisito obligatorio, no un mérito opcional.** La falta de reproducibilidad se considerará un incumplimiento fundamental de la práctica, independientemente de la calidad aparente del manuscrito. Un resultado que no pueda regenerarse mediante las bitácoras entregadas no se considerará evidencia suficiente de que el estudiante ejecutó los análisis.

**No se espera únicamente obtener mapas de distribución potencial, sino diseñar, ejecutar, comprender y explicar una investigación biogeográfica propia.**
