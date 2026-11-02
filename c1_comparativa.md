# C1 – Comparativa de estándares geográficos y servicios reales

**Actividad:** Ruta C – C1  
**Tema:** Repaso de estándares OGC con servicios reales.

## 1. Introducción

Los servicios geográficos permiten publicar, consultar e intercambiar información espacial a través de Internet. En esta actividad se estudian los estándares WMS, WFS y OGC API – Features, así como el servicio REST FeatureServer de Esri.

El propósito es identificar las características de cada servicio, analizar sus mecanismos de consulta y comparar la estructura de las respuestas obtenidas mediante servicios geográficos reales.

## 2. Consulta del servicio WMS del DANE

Se intentó consultar el servicio WMS del Marco Geoestadístico Nacional (MGN) 2024 del DANE mediante la operación GetCapabilities.

Durante la consulta, el servidor respondió con el código RequestNotAllowed y el mensaje "The request not allowed".

Debido a esta respuesta, no fue posible obtener directamente el documento XML de capacidades para verificar el inventario completo de capas, los sistemas de referencia y los formatos de salida admitidos por el WMS.

Se registra esta situación como una limitación de acceso al servicio, evitando presentar datos que no hayan sido comprobados directamente.

**Dirección del servicio:**

https://geoportal.dane.gov.co/mparcgis/services/MGN2024/Serv_CapasMGN_2024/MapServer/WMSServer

**Operación solicitada:** GetCapabilities.

## 3. Consulta de tres elementos mediante FeatureServer

Se utilizó el servicio FeatureServer de Esri correspondiente a las veredas del departamento de Boyacá.

La consulta se realizó mediante la operación query y los siguientes parámetros:

- where=1=1: condición de consulta.
- outFields=*: solicita todos los atributos.
- resultRecordCount=3: limita la respuesta a tres registros.
- f=geojson: establece el formato de salida.

**Dirección del servicio:**

https://services6.arcgis.com/Ex2fmFOuTOHRZtML/ArcGIS/rest/services/Veredas_Boyaca_2024/FeatureServer/0/query?where=1%3D1&outFields=*&resultRecordCount=3&f=geojson

La respuesta utiliza una estructura GeoJSON de tipo FeatureCollection. Dentro de ella se encuentra el arreglo features, que contiene los elementos consultados.

Cada elemento presenta:

- type: identifica el tipo de objeto geográfico.
- geometry: contiene la geometría de la entidad.
- properties: almacena los atributos descriptivos.
- id: identificador del elemento, cuando está incluido.

## 4. Consulta de tres elementos mediante OGC API – Features

Se utilizó la plataforma de demostración pygeoapi, específicamente la colección lakes, correspondiente a información geográfica de lagos.

La consulta se realizó mediante la ruta:

/collections/lakes/items

Se utilizó el parámetro limit=3 para solicitar un máximo de tres elementos y f=json para establecer el formato de respuesta.

**Dirección del servicio:**

https://demo.pygeoapi.io/master/collections/lakes/items?limit=3&f=json

La respuesta presenta una estructura FeatureCollection, que contiene los elementos geográficos dentro del arreglo features.

Cada elemento incluye geometría, identificador y propiedades descriptivas.

## 5. Tabla comparativa de estándares geográficos

| Estándar | Qué entrega | Cómo se filtra | Cómo se pagina |
|---|---|---|---|
| WMS | Imágenes cartográficas renderizadas. | Mediante capas, extensión espacial BBOX, estilos y dimensiones como TIME. | No pagina entidades; permite controlar la extensión y dimensiones de la imagen. |
| WFS | Entidades vectoriales con geometrías y atributos. | Mediante filtros espaciales, BBOX y filtros de atributos utilizando Filter Encoding. | Mediante count y startIndex en WFS 2.0, según las capacidades del servidor. |
| FeatureServer (Esri) | Entidades vectoriales mediante REST, JSON y GeoJSON. | Mediante parámetros where, geometry, outFields y consultas espaciales. | Mediante resultRecordCount y resultOffset. |
| OGC API – Features | Entidades geográficas mediante rutas REST y formatos como GeoJSON. | Mediante parámetros como bbox y datetime; filtros de atributos mediante extensiones compatibles. | Mediante limit y enlaces de navegación como next; offset puede estar disponible según la implementación. |

### Análisis de la comparación

WMS se orienta principalmente a la visualización de información geográfica mediante mapas renderizados, mientras que WFS permite consultar las entidades vectoriales y sus atributos.

FeatureServer utiliza una arquitectura REST propia del ecosistema Esri, con parámetros específicos para realizar consultas y controlar la cantidad de registros obtenidos.

OGC API – Features proporciona una estructura moderna basada en recursos y colecciones, facilitando la consulta de entidades geográficas mediante solicitudes HTTP y respuestas JSON.

La principal diferencia entre los servicios tradicionales y los servicios REST está en la forma de realizar las solicitudes, organizar los recursos y entregar la información geográfica.

## 6. Comparación de las estructuras JSON

Los servicios FeatureServer y OGC API – Features permiten consultar información vectorial y obtener respuestas estructuradas.

En ambos casos se pueden encontrar los siguientes componentes:

| Componente | Descripción |
|---|---|
| FeatureCollection | Agrupa los elementos geográficos |
| features | Contiene el conjunto de entidades |
| geometry | Representa la geometría espacial |
| properties | Contiene los atributos de cada entidad |
| id | Identifica el elemento geográfico |

La principal diferencia está en la forma de realizar las solicitudes. FeatureServer utiliza parámetros propios de la API REST de Esri, mientras que OGC API – Features organiza sus recursos mediante colecciones y rutas específicas.

## 7. Conclusiones

El desarrollo de esta actividad permitió reconocer las diferencias entre los servicios geográficos tradicionales y las arquitecturas REST utilizadas para publicar información espacial.

Se identificó que WMS está orientado a la visualización cartográfica mediante imágenes, mientras que WFS permite consultar entidades vectoriales con sus respectivas geometrías y atributos.

Por otra parte, FeatureServer y OGC API – Features ofrecen mecanismos de consulta mediante direcciones URL y respuestas estructuradas en formatos como JSON y GeoJSON.

Se concluye que el conocimiento de estos estándares es fundamental para integrar diferentes fuentes de información geográfica en aplicaciones SIG, facilitar la interoperabilidad y desarrollar soluciones web geográficas.

## 8. Fuentes de consulta

- DANE. Marco Geoestadístico Nacional 2024. Servicio cartográfico.
- Esri. FeatureServer – Veredas de Boyacá 2024.
- pygeoapi. Demostración de OGC API – Features.
- Open Geospatial Consortium (OGC). Estándares de servicios geográficos.
## 4.1. Resultados obtenidos en la consulta pygeoapi

La consulta realizada a la colección lakes de la plataforma pygeoapi permitió obtener tres elementos geográficos en formato GeoJSON.

Los elementos identificados fueron Lake Baikal, Lake Winnipeg y Great Slave Lake, cuyos identificadores corresponden a 0, 1 y 2, respectivamente.

La respuesta presentó una estructura FeatureCollection, con tres objetos de tipo Feature. Cada entidad contiene información descriptiva en properties y geometrías de tipo Polygon.

Adicionalmente, se identificaron los campos numberMatched con un valor de 25 y numberReturned con un valor de 3, lo que indica que existen 25 elementos coincidentes en la colección y que la consulta devolvió únicamente tres.

La respuesta también incluye un enlace de navegación identificado mediante rel=next, que permite consultar los siguientes registros utilizando el parámetro offset=3.

## 4.2. Comparación de resultados

La consulta realizada mediante FeatureServer permitió obtener tres entidades correspondientes a veredas de Boyacá, mientras que la consulta de pygeoapi devolvió tres elementos de la colección lakes.

Ambos servicios presentan respuestas estructuradas mediante FeatureCollection y utilizan los componentes features, geometry y properties para representar la información geográfica.

Sin embargo, existen diferencias en sus mecanismos de consulta y paginación. FeatureServer utiliza parámetros como resultRecordCount y resultOffset, mientras que OGC API – Features utiliza limit, offset y enlaces de navegación.

Esta comparación demuestra que ambos servicios permiten acceder a información vectorial mediante solicitudes HTTP, aunque pertenecen a implementaciones tecnológicas diferentes.## Evidencias de consulta de servicios geográficos

### 1. Consulta del servicio FeatureServer

Se presenta la evidencia de consulta del servicio FeatureServer, en la cual se identifican los registros geográficos correspondientes a las tres veredas.

<img width="1360" height="690" alt="evidencia_featureserver" src="https://github.com/user-attachments/assets/3643d050-dfb7-4033-87a8-1f9f7feb5752" />


### 2. Consulta del servicio pygeoapi

Se presenta la evidencia de consulta del servicio pygeoapi, donde se visualizan los resultados correspondientes a Lake Baikal, Lake Winnipeg y Great Slave Lake.
![Uploading evidencia_pygeoapi.JPG…]()

