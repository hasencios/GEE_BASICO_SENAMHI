---
title: "Series de Tiempo"
teaching: 5
exercises: 10
questions:
- "¿Cómo generar una serie de tiempo para una coordenada específica?"
- "¿Cómo graficar la serie de tiempo en Google Earth Engine?"
- "¿Cómo realizar gráficos interactivos?"
objectives:
- "Cargar una base de datos de cultivos de alta resolución."
- "Seleccionar de forma dinámica la lat/lon para crear gráficos de series de tiempo."
- "Generar una serie de tiempo de NDVI y EVI para los puntos seleccionados."
keypoints:
- "Se puede extraer series de tiempo y realizar gráficos desde Image Collections para puntos y regiones."
- "GEE ha incrementado su funcionalidad para realizar gráficos interactivos."
- "La interface de usuario puede ser modificada a través de la adición de un widget."

---

## Descripción general

Este código permite a los usuarios generar gráficos de series de tiempo a partir de puntos que son elegidos dinámicamente en un mapa. Las series temporales muestran los compuestos de 16 días del Normalized Difference Vegetation Index (NDVI) y Enhanced Vegetation Index (EVI) con una resolución de 250 m. Estos índices se derivan de MODIS.

## Definir especificaciones

Este script está estructurado para facilitar al usuario la selección de diferentes imágenes, fechas y regiones. Para este ejercicio, vamos a dejar los parámetros tal como están para establecer la extensión como área de estudio en el Medio Oeste, la Cuenca Republican River Basin

{% highlight javascript %}
// load WBD dataset & select the Republican watershed
var WBD = ee.FeatureCollection("USGS/WBD/2017/HUC06");
Map.addLayer(WBD, {}, 'watersheds');
var setExtent = WBD.filterMetadata('name', 'equals', 'Republican');

{% endhighlight %}
<br>

## Cargar una base de datos de imágenes de cultivos de alta resolución

Aquí estamos cargando tres tipos diferentes de imágenes de cultivos de alta resolución. Las dos primeras bases de datos ya están en GEE. La tercera base de datos es un Greenness Index (GI) calculado a partir de las imágenes Landsat. En lugar de calcular el GI sobre la marcha de este script, Jill previamente calculó el índice, exportó el raster y está llamandolo en la consola. Prácticas como esta pueden ayudar a acelerar su script.

1. La Cropland Data Layer (CDL) del National Agriculture Statistics Service (USDA) con una resolución de 30 metros. Esto se genera anualmente desde 2008 hasta el presente. A cada píxel se le asigna un valor que corresponde a un cultivo específico.

2. Las imágenes aéreas del National Agricultural Imagery Program (NAIP) del USDA. Estas imágenes tienen una distancia de muestreo de 1 metro (!). Este es un mapa de tres bandas usado para representar imágenes en colores naturales (RGB). Los estados son fotografiados cada 2-3 años en un ciclo rotativo.

3. Un Greenness Index derivado de las imágenes del Landsat (30 m) específicas de la zona de estudio. Este índice se calcula tomando un compuesto del píxel más verde, definido como el píxel con el NDVI más alto, durante un período de tiempo determinado.

{% highlight javascript %}
// CDL: USDA Cropland Data Layers
var cdl = ee.Image('USDA/NASS/CDL/2010').select('cropland').clip(setExtent);

// NAIP aerial photos
var StartDate = '2010-01-01';
var EndDate = '2010-12-31';

var naip = ee.ImageCollection('USDA/NAIP/DOQQ')
    .filterBounds(setExtent)
    .filterDate(StartDate, EndDate);

// Derived Landsat Composites --------------------

// annual max greenness image for background (previously exported asset)
var annualGreenest = ee.Image('users/jdeines/HPA/2010_14_Ind_001')
                    .select(['GI_max_14','EVI_max_14'])
                    .clip(setExtent);
{% endhighlight %}

## Cargar los productos derivados de MODIS: NDVI y EVI

El NDVI y el EVI son dos índices de vegetación diferentes que pueden ser calculados a partir de bandas rojas e infrarrojas cercanas. Aquí estamos usando un producto compuesto derivado de MODIS de 16 días que tiene bandas precalculadas para el NDVI y el EVI. También podrías calcularlas tú mismo usando la función `normalizedDifference`. De nuevo filtraremos la colección a las fechas, bandas y región de interés.

{% highlight javascript %}

// add satellite time series: MODIS EVI 250m 16 day -------------
var collectionModEvi = ee.ImageCollection('MODIS/006/MOD13Q1')
    .filterDate(StartDate,EndDate)
    .filterBounds(setExtent)
    .select('EVI');

// add satellite time series: MODIS NDVI 250m 16 day -------------
var collectionModNDVI = ee.ImageCollection('MODIS/006/MOD13Q1')
    .filterDate(StartDate,EndDate)
    .filterBounds(setExtent)
    .select('NDVI');
{% endhighlight %}


## Visualizar la base de datos de imágenes de alta resolución

Aquí realizaremos un mapa de los compuestos de CDL, NAIP y Annual Greenest Pixel.
 - *Consejo para ahorrar tiempo:* Si estás usando un conjunto de datos públicos, a menudo puedes encontrar  paletas tamizando los mensajes del foro. Algunas como la CDL vienen con una paleta incrustada.
 - *Consejo:* Los plugins de selección de colores de los navegadores hexadecimales son útiles para averiguar qué colores corresponden a qué códigos.
 - *Consejo:*: Usa el argumento `false` si quieres cargar una capa en el mapa pero NO la tienes activada cada vez que ejecutas el código.

 {% highlight javascript %}

// Visualize ----------------------------------------------------------------------------------
Map.centerObject(setExtent, 8);

// A nice EVI palette
var palette = [
  'FFFFFF', 'CE7E45', 'DF923D', 'F1B555', 'FCD163', '99B718',
  '74A901', '66A000', '529400', '3E8601', '207401', '056201',
  '004C00', '023B01', '012E01', '011D01', '011301'];

// greenest images
Map.addLayer(annualGreenest.clip(setExtent).select('GI_max_14'),
    {min:.75, max: 15, palette: palette}, 'GI - annual');

// cdl and naip
Map.addLayer(cdl, {}, 'cdl', false);
Map.addLayer(naip, {}, 'naip', false);
{% endhighlight %}

<br>
<img src="../fig/06_annualGreennest.png" border = "10">
<br><br>

## Crear una User Interface

Puedes alterar la client-side user interface (UI) a través del paquete ui añadiendo widgets a la interfaz del Code Editor. Puedes leer sobre el paquete ui en el [UI Overview section](https://developers.google.com/earth-engine/ui) de la Guía del Desarrollador.
La idea general es que se hace un widget, que puede ser simple (un botón) o complejo (un gráfico). Luego defines el comportamiento del widget y luego lo agregas a la pantalla. Aquí creamos un panel, definimos el contenido del panel usando etiquetas y creamos una función de respuesta al requerimiento para que el usuario pueda hacer clic en un punto y éste registre la lat/lon como un objeto llamado `points`. Puedes leer más acerca de cómo definir el panel y los diseños en el [Panels section](https://developers.google.com/earth-engine/ui_panels) de la Guía del Desarrollador.


{% highlight javascript %}

// Create User Interface portion --------------------------------------------------
// Create a panel to hold our widgets.
var panel = ui.Panel();
panel.style().set('width', '300px');

// Create an intro panel with labels.
var intro = ui.Panel([
  ui.Label({
    value: 'Two Chart Inspector',
    style: {fontSize: '20px', fontWeight: 'bold'}
  }),
  ui.Label('Click a point on the map to inspect.')
]);
panel.add(intro);

// panels to hold lon/lat values
var lon = ui.Label();
var lat = ui.Label();
panel.add(ui.Panel([lon, lat], ui.Panel.Layout.flow('horizontal')));

// Register a callback on the default map to be invoked when the map is clicked
Map.onClick(function(coords) {
  // Update the lon/lat panel with values from the click event.
  lon.setValue('lon: ' + coords.lon.toFixed(2)),
  lat.setValue('lat: ' + coords.lat.toFixed(2));
  var point = ee.Geometry.Point(coords.lon, coords.lat);
  {% endhighlight %}


## Agregar los gráficos de series de tiempo a los paneles

Ahora que hemos configurado nuestra interfaz de usuario y construido el 'call-back', podemos definir un gráfico de series de tiempo. El gráfico utiliza la lat/lon seleccionada por el usuario y construye una serie temporal para el NDVI o el EVI en ese punto. Toma el promedio del NDVI o EVI en ese punto, lo extrae y luego lo agrega a la serie de tiempo. Entonces esta serie se traza como un gráfico.


  {% highlight javascript %}

  // Create an MODIS EVI chart.
  var eviChart = ui.Chart.image.series(collectionModEvi, point, ee.Reducer.mean(), 250);
  eviChart.setOptions({
    title: 'MODIS EVI',
    vAxis: {title: 'EVI', maxValue: 9000},
    hAxis: {title: 'date', format: 'MM-yy', gridlines: {count: 7}},
  });
  panel.widgets().set(2, eviChart);

  // Create an MODIS NDVI chart.
  var ndviChart = ui.Chart.image.series(collectionModNDVI, point, ee.Reducer.mean(), 250);
  ndviChart.setOptions({
    title: 'MODIS NDVI',
    vAxis: {title: 'NDVI', maxValue: 9000},
    hAxis: {title: 'date', format: 'MM-yy', gridlines: {count: 7}},
  });
  panel.widgets().set(3, ndviChart);
});

Map.style().set('cursor', 'crosshair');

// Add the panel to the ui.root.
ui.root.insert(0, panel);
{% endhighlight %}

Deberías ver algo como esto en la parte inferior izquierda:

<br>
<img src="../fig/06_twoChart.png" border = "10" width="75%" height="75%">
<br><br>

## Explorar los gráficos NDVI y EVI para diferentes tipos de cultivos.

Activar y desactivar las capas de imágenes de Greenness, CDL y NAIP. Utiliza el inspector para hacer clic en los píxeles con diferentes niveles de verdor o diferentes tipos de cultivo y explora las diferencias en las series temporales del NDVI entre los diferentes píxeles.


## Extraer las series de tiempo para grandes regiones o puntos de interés

Si estás calculando los índices sobre la marcha, o tienes muchos puntos o áreas de interés, puedes tener la desagradable experiencia de que tu código se demora mucho. Una forma de evitarlo es exportar las series temporales como un .csv a Google Drive o Cloud Storage. Un ejemplo de cómo hacer esto se puede encontrar en
 [Episode 04: Reducers](https://geohackweek.github.io/GoogleEarthEngine/04-reducers/) de este tutorial.

Enlace a una versión estática del script completo utilizado en este módulo:
[https://code.earthengine.google.com/a47b635ed6a11a99199674364afb9944](https://code.earthengine.google.com/a47b635ed6a11a99199674364afb9944)