## 2. Consulta de tres elementos mediante servicios geográficos REST

### 2.1. FeatureServer de Esri

Se realizó una consulta al servicio FeatureServer de Esri correspondiente a las veredas del departamento de Boyacá. Se utilizaron los parámetros where=1=1, outFields=*, resultRecordCount=3 y f=geojson, con el propósito de obtener tres elementos geográficos y sus respectivos atributos.

La respuesta se encuentra organizada mediante una estructura FeatureCollection, que contiene un arreglo features. Cada elemento presenta una geometría identificada mediante geometry y sus atributos descriptivos dentro de properties.

### 2.2. OGC API – Features mediante pygeoapi

Se consultó la colección lakes de la plataforma de demostración pygeoapi, utilizando la ruta /collections/lakes/items y el parámetro limit=3.

La respuesta presenta una estructura GeoJSON de tipo FeatureCollection, con elementos geográficos que contienen identificadores, atributos descriptivos y geometrías.

### 2.3. Comparación de las respuestas

Los dos servicios permiten consultar información geográfica mediante solicitudes HTTP y entregan respuestas estructuradas en JSON. Ambos utilizan los componentes features, geometry y properties para organizar los elementos espaciales.

La principal diferencia se encuentra en los mecanismos de consulta. FeatureServer utiliza parámetros propios de la API REST de Esri, mientras que OGC API – Features utiliza rutas organizadas por colecciones y parámetros como limit.

Esta estructura facilita la integración de información geográfica en aplicaciones web y sistemas de información geográfica.
