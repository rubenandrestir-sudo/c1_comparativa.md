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

## 5. Tabla comparativa de servicios

| Estándar o servicio | Qué entrega | Cómo se filtra | Cómo se pagina |
|---|---|---|---|
| WMS | Imágenes cartográficas | BBOX, capas y estilos | No pagina entidades |
| WFS | Geometrías y atributos vectoriales | Filtros espaciales y de atributos | startIndex y count, según versión |
| FeatureServer | Entidades vectoriales mediante REST y JSON | where, geometry y outFields | resultOffset y resultRecordCount |
| OGC API – Features | Entidades geográficas mediante REST y JSON | bbox, datetime y filtros compatibles | limit y enlaces de navegación |

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

