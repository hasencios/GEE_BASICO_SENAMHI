---
title: "Introducción a Google Earth Engine"
teaching: 60
exercises: 60
questions:
- "¿Qué es Google Earth Engine?"
- "¿Cuáles son las ventajas y limitaciones de esta plataforma?"
objectives:
- Comprender el poder de Google Earth Engine
- Adquirir conocimientos básicos de las estructura de la plataforma y su filosofía
keypoints:
- " Google Earth Engine es una poderosa herramienta para realizar actividades de sensoramiento remoto."
- " El catálogo de datos de GEE mantiene una extensa variedad de información observada de la tierra."
- " GEE está cambiando la manera de entender el funcionamiento de los sistemas terrestres."

---

## ¿Qué es Google Earth Engine?

Gorelick et al. (2017) sugieren en su articulo publicado en la revista *<a href="http://www.sciencedirect.com/science/article/pii/S0034425717302900" target="_blank">Remote Sensing of the Environment</a>*:

> Google Earth Engine es una plataforma basada en la nube para trabajos a escala planetaria
> que presenta capacidades para realizar análisis geoespacial 
> y proporciona el poder computacional de Google.
> Provee de capacidades para incidir en una variedad de cuestiones sociales de gran impacto
> incluyendo la deforestación, las inundaciones, la sequía, los desastres naturales, las enfermedades y la > seguridad alimentaria, la gestión del agua, el monitoreo climático y la protección ambiental.

## ¿Por qué usar Google Earth Engine?

Google Earth Engine permite a los usuarios manejar petabytes de datos sobre la marcha sin tener que navegar por las complejidades de la paralelización basada en la nube. La mejora del acceso inclusivo ha estimulado el crecimiento de la observación de la Tierra a escalas antes inimaginables.


#### Razón # 1: Ciencia a escala planetaria

Desde que GEE entró en línea, han surgido varios estudios innovadores que demuestran el poder de la computación a gran escala para incidir en los problemas ambientales y sociales. Los siguientes tres ejemplos muestran la base de datos, las publicaciones de alto impacto y los exploradores web que se han generado a partir de las investigaciones realizadas en esta plataforma.

***
> **Caso 1: Monitoreo global de bósques**

Lanzado en el año 2013, <a href="http://www.globalforestwatch.org/" target="_blank">Global Forest Watch</a> fundamentalmente cambió nuestra comprensión de la pérdida de bosques a escala planetaria. Esta herramienta de monitoreo y conservación de los bosques muestra interactivamente la ganancia y la pérdida de los bosques a escala mundial. La base de datos subyacente de la deforestación de Hansen está disponible en Google Earth Engine y aprovecha más de 3 millones de imágenes de Landsat para trazar un mapa de la dinámica mundial de los bosques.



Obtenga más información aquí:

  - <a href="http://science.sciencemag.org/content/342/6160/850" target="_blank">High-Resolution Global Maps of 21st-Century Forest Cover Change</a> es la publicación original de Hansen, et al (2013).

  - <a href="https://developers.google.com/earth-engine/tutorial_forest_01" target="_blank">Hansen Tutorial for GEE</a> consituye una serie de tutoriales para aprender GEE, orientados a principiantes.

<img src="https://3c1703fe8d.site.internapcdn.net/newman/gfx/news/hires/2013/76fuygfd.gif" width="100%" height="100%" />
<sub>*Forest loss in Sumatra's Riau province, Indonesia, 2000-2012. Credit: Hansen, Potapov, Moore, Hancher et al., 2013*</sub>


***
> **Caso 2: Variabilidad espacial, a escala global, de los cuerpos de agua superficial**

En 2016 el European Commission's Joint Research Centre publicó una base de datos denominada Global Surface Water Occurrence, que muestra la intensidad del cambio en la ocurrencia de aguas superficiales a escala global. En otras palabras, cartografiaron la pérdida y la ganancia de cuerpos de agua a escala mundial desde 1984.

  - <a href="https://www.nature.com/articles/nature20584" target="_blank">High-resolution mapping of global surface water and its long-term changes</a> - El artículo original publicado en *Nature*.

  - Tutorial en línea para revisar los datos:  <a href="https://developers.google.com/earth-engine/tutorial_global_surface_water_01" target="_blank">Global Surface Water Tutorial for GEE</a>

  - El <a href="https://global-surface-water.appspot.com/" target="_blank">Global Surface Water Data Explorer</a> que se publicó junto con la base de datos para permitir a los usuarios visualizar los cambios en los cuerpos de aguas superficiales.

  - Un <a href="https://storage.googleapis.com/global-surface-water/downloads_ancillary/DataUsersGuidev2.pdf" target="_blank">Data Users Guide</a> describiendo la base de datos en detalle.  

***
> **Caso 3: Tiempo de viaje a escala global**

El Oxford Malaria Atlas Project, el European Commission’s Joint Research Centre y la University of Twente se unieron para crear un mapa de los tiempos de viaje desde cualquier punto del mundo hasta el centro urbano más cercano. Este trabajo puede localizar áreas con poco acceso a servicios para informar los esfuerzos de salud pública y las decisiones políticas.

  - <a href="https://www.nature.com/articles/nature25181" target="_blank">A global map of travel time to cities to assess inequalities in accessibility in 2015</a> - El artículo original publicado en *Nature* que describe la distribución de los tiempos de viaje al área de densidad de población más cercana desde cualquier punto del globo.

  - La <a href="https://map.ox.ac.uk/research-project/accessibility_to_cities/" target="_blank">website</a> publicado en conjunto con el artículo.

  - Algunos ejemplos <a href="https://code.earthengine.google.com/d52c656d3098b2723b275cc0d113d05e" target="_blank">GEE scripts</a> para visualizar la información.

***

#### Razón # 2: Procesamiento gratuito en la nube usando una variedad de funciones preestablecidas

Google Earth Engine está diseñado para el análisis de datos geoespaciales utilizando cloud computing. GEE se encarga de toda la infraestructura computacional y la paralelización por el usuario. Estas operaciones se denominan "server-side".

Usando GEE, se puede llamar a un amplio conjunto de funciones que han sido desarrolladas específicamente para la computación en Earth Engine y aplicarlas sobre muchas imágenes simultáneamente usando la infraestructura computacional de Google. No más descargas y análisis de los mosaicos individuales a la vez o el estrés de su almacenamiento local.


#### Razón # 3: Archivo online de datos públicos

El catálogo GEE alberga múltiples petabytes de imágenes satelitales en la nube, incluyendo toda la misión Landsat. Otras misiones de sensoramiento remoto incluyen Sentinel-1, Sentinel-2, MODIS y otros productos. Además de las imágenes, GEE también alberga bases de datos de productos de precipitación, densidad poblacional, topografía, cobertura de suelos y el clima. Se añaden diariamente más de 6000 escenas de misiones satelitales activas.
  - La <a href="http://www.sciencedirect.com/science/article/pii/S0034425717302900" target="_blank">Tabla 1</a> in Gorelick et al. (2017) describe las bases de datos frecuentemente usadas.
  - El <a href="https://earthengine.google.com/datasets/" target="_blank">Google Earth Engine</a>
  website presenta una descripción general de la base de datos.
  - Se puede navegar directamente por la base de datos a través de la <a href="https://explorer.earthengine.google.com/#index" target="_blank">Google Earth Engine API</a>.


<br>
<img src="../fig/01_datasets.png" border = "10" width="80%" height="80%">
<br><br>

#### Razón # 4: Cargar su propio catálogo de datos

Se puede subir nuestra propia base de datos raster **y** vectorial a la plataforma. También puedes recomendar la base de datos desde la ventana del Code Editor de la API de Javascript yendo al botón *Help* en la parte superior derecha y seleccionando *Suggest a dataset*.

<br>
<img src="../fig/01_datasetsuggest.png" border = "10" width="70%" height="70%">
<br><br>

#### Razón # 5: GEE se encarga del control de versiones

GEE hará una copia de seguridad de tu código en un repositorio git sin que tengas que pensar en ello. Puedes compartir esos repositorios con otros usuarios y ver versiones anteriores de los scripts fácilmente desde el Code Editor.

#### Razón # 6: Acceso flexible a través de Application Programming Interface (API)

El equipo de desarrollo de GEE ha trabajado duro para hacer que la plataforma sea de fácil acceso. Se puede acceder a Google Earth Engine a través de diferentes canales, incluyendo una interfaz gráfica de usuario no programada, la API de JavaScript y la **API de Python**.


  - El <a href="https://explorer.earthengine.google.com/#workspace" target="_blank">Google Earth Engine Explorer</a> es genial para que personas sin conocimientos previos visualicen las bases de datos disponibles, pero tiene capacidades limitadas para el análisis.
  - La interfaz gráfica de JavaScript es una plataforma web en la que se puede hacer requerimientos a través de la API principal de GEE. Los desarrolladores han pasado años perfeccionando esta plataforma para facilitar a los usuarios el almacenamiento, el intercambio y la versión de los resultados del código, la ejecución de tareas y, lo que es más importante, la visualización de los resultados sobre la marcha en gráficos y mapas renderizados directamente en la ventana del navegador. También se encargan de la autenticación del usuario con sólo iniciar sesión a través de su gmail.
  - La **API de Python** requiere que los usuarios se encarguen de la autenticación y la visualización de los resultados, con el beneficio de permitir a los usuarios personalizar más plenamente los requerimientos más allá de la biblioteca de funciones disponibles de forma nativa en GEE. No hay ningún sitio web al que se acceda para realizar el análisis: el código se construye desde cero utilizando flujos de trabajo que se desarrollan de forma individual.

Para estas lecciones vamos a utilizar el JavaScript API, sin embargo el <a href="https://developers.google.com/earth-engine/python_install" target="_blank"> material de entrenamiento para acceder a GEE usando Python</a> está ahora disponible en la website de GEE. Si estás interesado en usar el Python API, segir las instrucciones mostradas en el link para la instalación y revisa los ejemplos notebooks <a href="https://github.com/renelikestacos/Google-Earth-Engine-Python-Examples/ " target="_blank">here</a>. La Javascript API ha incorporado herramientas de visualización de mapas, así que eso es lo que usaremos para aprender la plataforma inicialmente.


Si todavía no estás seguro de para qué sirve GEE, puedes revisar la siguiente presentación <a href="https://docs.google.com/presentation/d/1hT9q6kWigM1MM3p7IEcvNQlpPvkedW-lgCCrIqbNeis/edit#slide=id.gf251d1053_0_1005" target="_blank">What is Google Earth Engine?</a> disponible del equipo GEE.



***

## ¿Cómo interactuamos con la plataforma?

Usando el Code Editor, se escribe comandos que son enviados como un objeto a Google para ser procesados en paralelo en la nube (server-side). Los usuarios pueden visualizar los resultados de Google en su navegador (client-side), incluyendo objetos como mapas, gráficos o resultados estadísticos.

Utilizando una de las API, los usuarios pueden filtrar enormes colecciones de imágenes a las fechas y áreas de su interés, asignar algoritmos sobre colecciones de imágenes, aplicar algoritmos a imágenes individuales o colecciones de imágenes y estimar estadísticos a través del tiempo y el espacio sin tener que descargar una sola imágen a su computadora.

<br>
<img src="../fig/01_What is Google Earth Engine_.png" border = "10">
<br><br>


## Resumen

### ¿Cuáles son los usos comunes de GEE?

- operar en petabytes de imágenes usando los servidores en la nube de Google
- incluir los resultados en aplicaciones
- almacenar, compartir y controlar la versión de tu script
- importar y exportar sus propios datos raster y vectoriales (assets)
- compartir sus propios datos raster y vectoriales
- exportar su análisis


### ¿Para qué no ha sido diseñado GEE?

- cartografía
- grandes operaciones vectoriales
- Paralelización DIY. Como se indica en Gorelick et al. 2017, "The price of liberation from these details [of parallelization] is that the user is unable to influence them.”
