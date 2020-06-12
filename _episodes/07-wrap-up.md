---
title: "Resumen"
teaching: 30
exercises: 30
questions:
- "¿Cuál es el recurso más importante de GEE?"
- "¿Dónde se puede encontrar ayuda acerca del uso de GEE?"
objectives:
- "Recordar que hemos aprendido"
- "Discutir acerca de los recursos para un uso futuro y aprendizaje"
keypoints:
- "Google Earth Engine es una plataforma de análisis geoespacial a escala planetaria."
- "La Guía del Desarrollador tiene una amplia colección de documentos y scripts de ejemplo."
- "El Foro de Desarrolladores puede utilizarse para publicar preguntas o responder a preguntas sobre scripts de GEE."
- "El Code Editor y el sitio web de GEE contienen muchos recursos, entre ellos el catálogo de datos, la documentación de scripts y lugares para la retroalimentación de los usuarios."

---

## Reflecciones Finales

En este tutorial, aprendiste
- [1. Introducción a Google Earth Engine](https://hasencios.github.io/GEE_BASICO_SENAMHI/01-introduction/): Una descripción general básica de Google Earth Engine (GEE)
- [2. Code Editor](https://hasencios.github.io/GEE_BASICO_SENAMHI/02-code-editor/): Como navegar por el Code Editor
- [3. Accediendo al catálogo de imágenes de satélite
](https://hasencios.github.io/GEE_BASICO_SENAMHI/03-load-imagery/): Como trabajar con imágenes satelitales a escala regional
- [4. Reductores espaciales y temporales](https://hasencios.github.io/GEE_BASICO_SENAMHI/04-reducers/): Como agregar imágenes a través del tiempo y el espacio
- [5. Clasificación Supervisada de Imágenes de Satélite](https://hasencios.github.io/GEE_BASICO_SENAMHI/05-classify-imagery/): Como clasificar las imágenes para los diferentes usos de la tierra
- [6. Series de Tiempo](https://hasencios.github.io/GEE_BASICO_SENAMHI/06-time-series/): Como graficar interactivamente una serie temporal

GEE fue diseñado para el provecho de la ciencia. No dudes en buscar documentación, iniciar discusiones en el foro, sugerir bases de datos y dar retroalimentación a lo largo del camino.
<br>
<br>

## Remarcar estas Webpages
La API de JavaScript y el Code Editor en línea son la mejor manera de desarrollar algoritmos de procesamiento y obtener ayuda de los foros. El API de Python se recomienda generalmente para la implementación a nivel de producción de los algoritmos desarrollados.

Debido a esto, trabajar con GEE es más fácil con un rápido acceso a los elementos en línea. Recomendamos añadir estos marcadores a su navegador web para facilitar su uso:

- [Code Editor](https://code.earthengine.google.com/): Donde vas a escribir el script.
- [Data Catalogue](https://code.earthengine.google.com/datasets/): Detalles de las bases de datos disponibles.
- [Developers Guide](https://developers.google.com/earth-engine/): lo más parecido a un manual.
- [Developers Forum](https://groups.google.com/forum/?fromgroups#!forum/google-earth-engine-developers): Donde vas a colocar las preguntas
  - También hay un enlace al foro desde el menú desplegable "Help" en el Code Editor, pero un marcador puede ser bueno para el uso frecuente
  - El equipo de Google es muy activo en los foros y es un recurso vital. La documentación de GEE no siempre está completa, así que si estás atascado en algo, ¡pregunta!
  - **Recommendation:** Establezca su preferencia de envío de correo electrónico en "Send daily summaries". Nadie quiere recibir un correo electrónico por cada mensaje en el foro, pero revisar el resumen diario en busca de temas que necesite en el futuro es una gran manera de encontrar de forma preventiva ejemplos de scripts para su trabajo. También es probable que descubras un uso que no sabías que existía a través de los mensajes de otras personas.
  - **Consejo:** Al publicar preguntas en el foro, obtendrás la mejor ayuda si incluyes un enlace a tu script actual que otros puedan ejecutar para ayudarte a solucionar el problema. Los ejemplos ficticios pueden funcionar muy bien, y si compartes tu espacio de trabajo real, asegúrate de que cualquier Asset o información personal cargada en tu script sean compartidas públicamente.

## Recursos de aprendizaje adicional
Hay varios recursos educativos y de capacitación disponibles para seguir aprendiendo sobre GEE.

- [GEE tutorials](https://developers.google.com/earth-engine/tutorials)
- [GEE EDU page](https://developers.google.com/earth-engine/edu)
  - Recursos educativos: ofrece planes de estudio sobre sensoramiento remoto elaborados con GEE
  - Recursos de entrenamiento: Proporciona recursos para aquellos que enseñan GEE. Esto incluye una introducción general en Powerpoint y los materiales del Taller para Principiantes e Intermedios dirigido por GEE

## Para avanzar
- [Debugging Guide](https://developers.google.com/earth-engine/debugging)
  - Publicado por demanda popular. Un recurso EXCELENTE. **Debug del código de un programador, y recibirás sus mensajes en el foro para el script. Enseña a un programador a depurar, y recibirás sus mensajes en el foro de por vida.
 - [The "Under the Hood" forum thread](https://groups.google.com/forum/#!searchin/google-earth-engine-developers/benefits$20of$20python%7Csort:relevance/google-earth-engine-developers/LWHTFSH9FRk/NGxiEQ5KEQAJ)
   - Si continúa usando GEE, inevitablemente comenzará a tener preguntas acerca de cómo funciona GEE para optimizar su flujo de trabajo. A veces las operaciones se acaban o no se ejecutan. En general, el funcionamiento interno de GEE es bastante desconocido. Los típicos arreglos y enfoques que los científicos de datos usan no se aplican realmente en el marco de trabajo de GEE. Este hilo proporciona alguna información útil sobre lo que los usuarios pueden y no pueden controlar. Lectura altamente recomendada para los usuarios habituales de GEE.
- [Gorelick et al. 2017](http://www.sciencedirect.com/science/article/pii/S0034425717302900)
  - El Earth Engine Team publicó recientemente una descripción general de la plataforma GEE. También proporciona tablas de las bases de datos disponibles actualmente y las funciones.
