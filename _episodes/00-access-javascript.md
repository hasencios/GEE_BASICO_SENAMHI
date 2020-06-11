---
title: "Acceso a GEE y tips JavaScript"
teaching: 0
exercises: 0
questions:
- ¿Cómo obtener una cuenta?
- ¿Qué es lo básico que se debe de saber acerca de JavaScript?
objectives:
- Acceder a Google Earth Engine
- Generar líneas de código JavaScript
keypoints:
- "Cualquiera puede registrarse para usar Google Earth Engine."
- "El Code Editor es un punto de acceso fácil de GEE que utiliza el IDE de JavaScript."
- "JavaScript es un lenguaje de programación que también se utiliza en desarrollo web."
---
# Pre-requisitos

Por favor, complete este el procedimiento antes de tomar las lecciones. Siga los pasos que se indican a continuación para registrarse en una cuenta de Google Earth Engine y únase a nuestro repositorio compartido.

### 1. Registering for a Google Earth Engine account

  - Ir a la [página web de GEE sign up](https://signup.earthengine.google.com/#!/) e ingresar > el correo electrónico que deseas usar para tu cuenta GEE. Una cuenta gmail es mejor la mejor opción.
  - Introduzca su correo electrónico, su afiliación y su región/país. Cuando le pregunte qué desea lograr, mencione que labora en una institución del estado peruano (SENAMHI).
  - Revise los términos, verifique su identificación de no-robot y haga clic en 'Submit'.
  - Revise su correo electrónico, incluida la carpeta de spam, para ver si hay un enlace del equipo de desarrolladores de Google. El correo electrónico de confirmación tendrá instrucciones sobre cómo acceder al Code Editor.

¿No estás seguro de tener acceso? Utilice [este link](https://code.earthengine.google.com/) para verificar. Si no ha conseguido acceso, recibirá mensale indicándole error de autorización, que significa que su cuenta no está registrada. Si tiene acceso, el enlace abrirá el IDE de Javascript. Este enlace constituye su portal permanente de acceso a GEE.

### 2. Unirse a nuestro repositorio compartido de GEE

GEE nos permite tener carpetas de grupo compartidas/repositorios para los scripts que vayamos desarrollando. Se ha organizado el código presentado en estas lecciones de la siguiente manera. En lugar de añadir cada uno de vuestros correos electrónicos uno a uno (¡lo cual es muy tedioso!), se unirá a un grupo de Google que nos permitirá acceder al repositorio de código compartido. Por favor, sigua estos pasos:

<!-- 
  - Únase al grupo de Google Earth Engine SENAMHI haciendo clic en este enlace. <a href="https://goo.gl/JsnWZH" target="_blank">https://goo.gl/JsnWZH</a> . No se preocupe por los permisos de publicación.
 -->
  - Aceptar el repositorio compartido haciendo clic en este enlace:
  <a href="https://code.earthengine.google.com/?accept_repo=users/hasencios/GEE_BASICO_SENAMHI
" target="_blank">https://code.earthengine.google.com/?accept_repo=users/hasencios/GEE_BASICO_SENAMHI</a>
  - En el Code Editor, vaya al **Scripts tab** en el panel superior izquierdo, desplácese hacia abajo y amplíe la sección "Reader". Un directorio llamado *users/hasencios/GEE_BASICO_SENAMHI* debe aparecer con versiones de sólo lectura de los scripts completos de cada lección.


### 3. Tips de Javascript 

JavaScript, que no debe confundirse con Java, es un lenguaje de programación ampliamente utilizado en el desarrollo web junto con HTML y CSS. Puede aprender JavaScript usando cualquier tutoriales en línea, como los que ofrece <a href="https://www.w3schools.com/js/" target="_blank">w3schools</a> .


At geohackweek, we access Google Earth Engine by entering JavaScript commands into an online integrated development environment (IDE) called the Code Editor. It is not necessary to formally learn JavaScript to work with Google Earth Engine. Below we provide examples and resources for getting started.  

A lo largo de las lecciones, accederemos a Google Earth Engine introduciendo comandos de JavaScript en un entorno de desarrollo integrado (IDE) en línea denominado Code Editor. No es necesario aprender formalmente JavaScript para trabajar con Google Earth Engine. A continuación te proporcionamos ejemplos y recursos para empezar.  

#### JavaScript básico para GEE
 Aquí hay algunas herramientas útiles para GEE, reproducidos de la. <a href="https://docs.google.com/document/d/1ZxRKMie8dfTvBmUNOO0TFMkd7ELGWf3WjX0JvESZdOE/edit" target="_blank">Earth Engine 101 Beginner's Curriculum</a>.



{% highlight javascript %}
// Line comments start with two forward slashes. Like this line.

/* Multi-line comments start with a forward slash and a star,
and end with a star and a forward slash. */
{% endhighlight %}

Las variables se usan para almacenar objetos y se definen usando la palabra clave **var**.
{% highlight javascript %}
var theAnswer = 42;

// string objects start and end with a single quote
var myVariable = 'I am a string';

// string objects can also use double quotes, but don't mix and match
var myOtherVariable = "I am also a string";
{% endhighlight %}

Las declaraciones deben terminar en punto y coma, o de lo contrario le aparecerá un aviso.
{% highlight javascript %}
var test = 'I feel incomplete...'
var test2 = 'I feel complete!';
{% endhighlight %}

Aplicar los parámetros de la función y utilizar las listas.
{% highlight javascript %}
// Parentheses are used to pass parameters to functions
print('This string will print in the Console tab.');

/* Square brackets are used for items in a list.
The zero index refers to the first item in a list*/
var myList = ['eggplant','apple','wheat'];
print(myList[0]); // would print 'eggplant'
{% endhighlight %}

Usando diccionarios.
{% highlight javascript %}
// Curly brackets (or braces) can be used to define dictionaries (key:value pairs).
var myDict = {'food':'bread', 'color':'red', 'number':42};

// Square brackets can be used to access dictionary items by key.
print(myDict['color']);

//Or you can use the dot notation to get the same result.
print(myDict.color);
{% endhighlight %}

Las funciones pueden definirse como una forma de reutilizar el código y facilitar su lectura.
{% highlight javascript %}
var myHelloFunction = function(string) {
  return 'Hello ' + string + '!';
};
print(myHelloFunction('world'));
{% endhighlight %}


#### Otros recursos JavaScript
El JavaScript usa camelCase. JavaScript (según la academia W3) es fácil de aprender. Como otros lenguajes de programación, puedes usar guías de estilo para aprender a escribir código estándar y reproducirlo.

Para una orientación a la industria, Google publica su propia guía <a href="http://google.github.io/styleguide/jsguide.html" target="_blank">Guía de estilos JavaScript</a>.

Dana Tomlin también ha creado <a href="https://drive.google.com/file/d/0B3H1GYZLzLKCckwwVjZfVmdPNDA/view)" target="_blank">JavaScript Quick Start Guide</a> que sólo toma unos pocos minutos de trabajo, pero que tiene algunos aspectos básicos. Puedes encontrarlo haciendo clic en ese enlace o yendo a la página principal de GEE, haciendo clic en la pestaña EDU en la parte superior izquierda, y bajando a la sección de Ejercicios de Diseño de Software Geoespacial.


<br>
<img src="../fig/00_spaceland.png" border = "10">
<br><br>
