---
title: "Reductores espaciales y temporales"
teaching: 5
exercises: 10
questions:
- ¿Cómo agregar las imágenes que comprenden una Image Collection sobre un periodo de tiempo?
- ¿Cómo estimar medios areales usando regiones vectoriales?
- ¿Cómo exportar una tabla de resumen?
objectives:
- Usar reducers para agregar una Image Collection con información diaria a valores anuales
- Importar información vectorial para estimar medios areales por regiones de poligonos
- Usar los productos de información climática disponibles a través de GEE
- Exportar la información tabular
keypoints:
- GEE mantiene una ámplia variedad de base de datos espaciales
- Los reducers agregan o resumen información en el espacio y tiempo
- Hay varias maneras de usar la información temporal en GEE
- Los resultados pueden ser exportados a **Google Drive** o **Google Cloud**
---

# Reductores: Descripción general


En Google Earth Engine (GEE), [reducers](https://developers.google.com/earth-engine/reducers_intro) se utilizan para agregar datos en el tiempo, el espacio y otras estructuras de datos. Pertenecen a la clase `ee.Reducer` e incluyen estadísticas de resumen, histogramas y regresión lineal, entre otros. Aquí se presenta una demostración visual que muestra un reductor aplicado a una `ImageCollection`:

<br>
<img src="../fig/04_reducers.png" border = "10">
<br><br>

Las reducciones también pueden ocurrir en el espacio, sobre las bandas dentro de una imagen, o sobre los atributos de una `FeatureCollection`. Ver el [Reducer Overview](https://developers.google.com/earth-engine/reducers_intro) en la Guía del Desarrollador de Google para más información.

En el Módulo 03: Accediendo al Catálogo de Imágenes de Satélite, usamos un límite vectorial y un rango de fechas para filtrar una colección de imágenes, aplicamos un algoritmo (NDVI) sobre esa colección, y luego la redujimos a una imagen en la que cada valor de píxel era su máximo NDVI. Aquí seguimos el mismo flujo de trabajo, pero en su lugar reduciremos usando `imageCollection.sum()` para calcular la precipitación anual total para cada píxel en los EE.UU. (reductores temporales). Luego daremos un paso más y usaremos el reductor espacial 'reduceRegions' para calcular la precipitación anual total para cada condado de los EE.UU.

# Ejercicio: Obtener datos climáticos desde GEE
Aquí demostraremos cómo aplicar un reductor temporal y espacial para obtener datos de precipitación anual por condado para los EE.UU.

### El catálogo de datos de GEE
Un objetivo secundario de este ejercicio es utilizar GEE para acceder a bases de datos comunes almacenados en archivo que puedan resultar atractivos para quienes no estén directamente relacionados con el sensoramiento remoto. Como se describe en la [Introducción](https://hasencios.github.io/GEE_BASICO_SENAMHI/01-introduction/), GEE provee diferentes bases de datos pertinentes para los análisis de los sistemas terrestres. El archivo completo puede ser consultado [here](https://code.earthengine.google.com/datasets/). En este ejercicio, usaremos el [GRIDMET Meteorological Dataset](https://code.earthengine.google.com/dataset/IDAHO_EPSCOR/GRIDMET) para obtener precipitaciones. GRIDMET combina PRISM y NLDAS para producir una base de datos climáticos diarios, en grillas de 4 km, para los Estados Unidos desde 1979 hasta el presente.

### Temporal Reducer: Generar un Image Statistics en el tiempo
Tal como se discutió en el [módulo Accediendo al catálogo de imágenes de satélite
](https://hasencios.github.io/GEE_BASICO_SENAMHI/03-load-imagery/), una `ImageCollection` es una pila o serie temporal de imágenes. Los reductores se usan para derivar una sola `Image` basada en la `ImageCollection`. Las operaciones ocurren en por píxeles. Seguiremos este flujo de trabajo:

  * "Load" los datos de la GRIDMET como una `ImageCollection`
  * Filtrar la banda de datos de precipitaciones y las fechas deseadas
  * **Reduce** 365 imágenes "raster" de precipitaciones diarias en una imagen "raster" de totales de precipitaciones anuales (suma de rasters por píxel)
  * Visualizar el resultado

#### Cargar y filtrar una ImageCollection
Primero, necesitamos identificar el **ImageCollection ID** para el producto de datos GRIDMET y el **band name** para los datos de precipitación (y comprobar cualquier metadato relevante). Esto se puede encontrar en el [data catalog](https://code.earthengine.google.com/datasets/) o directamente en el [GEE Code Editor](https://code.earthengine.google.com/) en la parte superior del panel central.

Para la [GRIDMET description](https://code.earthengine.google.com/dataset/IDAHO_EPSCOR/GRIDMET), sabemos que el ID de ImageCollection = 'IDAHO_EPSCOR/GRIDMET' y el nombre de la banda de precipitación es 'pr'. Específicamente `select` esta banda solamente.

{% highlight javascript %}

// carga datos de precipitación (mm/día): 365 imágenes por año
var precipCollection = ee.ImageCollection('IDAHO_EPSCOR/GRIDMET')
                    .select('pr')   // select  precip band only
                    .filterDate('2017-01-01', '2017-12-31');
print(precipCollection, 'precipCollection');

{% endhighlight %}

Al imprimir la colección resultante en la consola, podemos ver que hemos accedido a 365 imágenes, cada una con una banda llamada 'pr'.

#### Aplicar un Sum Reducer y visualizar los resultados
El operador `imageCollection.reduce()` permite aplicar cualquier función de la clase `ee.Reducer()` a todas las imágenes de la colección. Si tu `ImageCollection` tenía múltiples bandas, el reductor se aplica por separado a todas las bandas (a menos que el reductor utilice múltiples bandas como entradas, en cuyo caso el número de bandas de la colección de imágenes debe coincidir con el número de entradas que requiere el reductor). Puede encontrar los reductores disponibles y sus descripciones en la referencia de la API que se puede buscar en la pestaña **Docs** en el panel superior izquierdo del Code Editor.

<br>
<img src="../fig/04_reducerMenu.PNG" border = "10">
<br><br>

Algunos reductores comúnmente usados tienen una sintaxis abreviada, como `imageCollection.mean()`, `imageCollection.min()`, y convenientemente, `imageCollection.sum()`. Ambas sintaxis se demuestran en el siguiente fragmento de código.

{% highlight javascript %}

// carga datos de precipitación (mm/día): 365 imágenes por año
var precipCollection = ee.ImageCollection('IDAHO_EPSCOR/GRIDMET')
                    .select('pr')   // select  precip band only
                    .filterDate('2017-01-01', '2017-12-31');
print(precipCollection);  

// reducir la colección de imágenes a una sola imagen sumando los 365 patrones diarios
var annualPrecip = precipCollection.reduce(ee.Reducer.sum());
print(annualPrecip);

// sintaxis equivalente
var annualPrecip2 = precipCollection.sum();

// visualizar la precipitación anual
var precipPal = ['white','blue'] // store palette as variable               
Map.addLayer(annualPrecip, {min: 60, max: 3000, palette: precipPal}, 'precip');

{% endhighlight %}

Al imprimir la imagen resultante en la consola, podemos ver que ahora tenemos una imagen con una banda llamada 'pr_sum'. Esto es lo que parece:

<br>
<img src="../fig/04_annualPrecipMap.PNG" border = "10">
<br><br>

### Spatial Reducer: Generar un Image Statistics por regiones
Ahora tomemos la imagen de la precipitación anual que acabamos de crear y obtengamos la precipitación media areal por condado en los Estados Unidos. Para obtener las estadísticas de la imagen para múltiples regiones, podemos usar una función [image.reduceRegions()](https://developers.google.com/earth-engine/reducers_reduce_regions). Usaremos una [FeatureCollection](https://developers.google.com/earth-engine/feature_collections) para almacenar nuestra base de datos vectorial de los condados. Tengan en cuenta que también hay un operador [image.reduceRegion()](https://developers.google.com/earth-engine/reducers_reduce_region) si quería resumir una región del polígono solamente. El resultado de la operación `reduceRegiones()` se añade a las propiedades de cada característica en la `FeatureCollection`.

  >*Una nota importante sobre el parámetro de escala**

  > GEE utiliza una evaluación de su código que sólo ejecuta las partes de su script necesarias para los resultados esperados - en el caso del entorno de la API de JavaScript. *GEE ejecutará sus cálculos con la resolución de su vista actual del mapa en el Code Editor, a menos que usted le diga lo contrario*. Siempre que sea posible, establezca explícitamente los argumentos de escala para forzar a GEE a trabajar en una escala que tenga sentido para sus imágenes/análisis. Lea el wiki [modifiable areal unit problem](https://en.wikipedia.org/wiki/Modifiable_areal_unit_problem) o el [Developers Docs](https://developers.google.com/earth-engine/scale) para observar porque esto es importante.

#### Cargar los límites de países (Data Vectorial)

Hay tres maneras de obtener datos de vectores en GEE, como se examina en el [módulo 03 Accediendo al catálogo de imágenes de satélite
](https://hasencios.github.io/GEE_BASICO_SENAMHI/03-load-imagery/). Aquí usaremos un [existing public fusion table of county boundaries](https://fusiontables.google.com/data?docid=1xdysxZ94uUFIit9eXmnw1fYc6VcQiXhceFd_CVKa#map:id=2) de la Oficina del Censo de los Estados Unidos.

Este base de datos incluye entidades fuera de los Estados Unidos como Alaska, Puerto Rico y Samoa Americana. Las eliminaremos basándonos en sus ID en un atributo de propiedad que contiene códigos FIPS "state" para demostrar el filtrado de vectores.

{% highlight javascript %}
// cargar regiones: condados de una tabla de fusión pública, eliminando los estados que no nos interesan
// usando un filtro personalizado
var nonCONUS = [2,15,60,66,69,72,78] // state FIPS codes that we don't want
var counties = ee.FeatureCollection('ft:1ZMnPbFshUI3qbk9XE0H7t1N5CjsEGyl8lZfWfVn4')
        .filter(ee.Filter.inList('STATEFP',nonCONUS).not());
print(counties, 'counties');

// visualizar
Map.addLayer(counties,{},'counties');  
{% endhighlight %}

Al imprimir el featureCollection, vemos que hay 3108 polígonos de condado y 11 columnas de datos de atributos.

<br>
<img src="../fig/04_countyMap.png" border = "10">
<br><br>

#### Aplicar el spatial reducer

{% highlight javascript %}
// obtener los valores medios de precipitación por polígono de condado
var countyPrecip = annualPrecip.reduceRegions({
  collection: counties,
  reducer: ee.Reducer.mean(),
  scale: 4000 // the resolution of the GRIDMET dataset
});
print(countyPrecip);
{% endhighlight %}

Al imprimir la featureCollection countyPrecip, vemos que hay 3108 polígonos de condado y ahora 12 columnas de datos de atributos, con la adición de la columna "mean".

### Acondicionar los resultados para exportarlos
GEE puede exportar tablas en CSV (default), GeoJSON, KML o KMZ. Aquí, hacemos un pequeño formateo para preparar nuestra FeatureCollection para exportar como CSV.

El formato incluye:

* Eliminar la columna .geo para un conjunto de datos más ordenado (esta columna puede ser bastante grande cuando los polígonos son muy detallados, pero no hay razón para que tengas que hacer este paso)
* Añadir un atributo de columna para el año de los datos del precipitación para demostrar la manipulación de los atributos. Esto sólo se puede hacer con las Features, por lo que asignamos una función para hacer esto sobre las Features dentro de la  Feature Collection

{% highlight javascript %}

// Dejar caer la columna .geo (no es necesario si el objetivo son los datos tabulares)
var polyOut = countyPrecip.select(['.*'],null,false);

// añadir una nueva columna de año a cada característica de la feature collection
polyOut = polyOut.map(function(feature){
return feature.set('Year',2017);
});

// Ejemplo para exportar tablas

Export.table.toDrive({
  collection: polyOut,
  description: 'GRIDMET_annual_precip_by_county',
  folder: 'GEE_SENAMHI',
  fileFormat: 'CSV'
});   

// Y PULSE 'RUN' EN LA PESTAÑA DE TAREAS EN EL PANEL SUPERIOR DERECHO
{% endhighlight %}

Nota sobre el nombre de la carpeta: si esta carpeta existe dentro de su unidad de Google, GEE la encontrará y exportará aquí independientemente de la ruta completa de su archivo. Si la carpeta no existe, GEE la creará al momento de la exportación.

### Comenzar a Exportar

Para poder exportar realmente tus datos, tienes que pulsar explícitamente el botón "Run" bajo la pestaña "Task" en el panel superior derecho del Code Editor. La exportación debería tomar 20-30 segundos, dependiendo de las cargas de los usuarios de GEE.

Se ha añadido una nueva y útil función en la que se puede mantener el ratón sobre el lado derecho de la tarea completada y hacer clic en el signo de interrogación para abrir una ventana con los detalles de la tarea como en el diagrama siguiente.

<br>
<img src="../fig/04_runTask.png" border = "10" width="50%" height="50%">
<br><br>

Enlace a una versión estática del script completo usado en este módulo:
[https://code.earthengine.google.com/89436bb293b0dc412ed813499a820fe1](https://code.earthengine.google.com/89436bb293b0dc412ed813499a820fe1)
