---
layout:     post
title:      "Pentaho Data integrator 4/5"
subtitle:   "Primera Transformación."
date:       2015-03-03 01:48:00
author:     "@hellfish2"
header-img: "img/pentaho.png"
---

#### Creando nuestra primera Transformación

Supongamos que tenemos una tabla en PostgreSQL, la cual queremos exportar una columna especifica hacia un archivo de texto, entonces partiendo de esa premisa hariamos algo como esto:

Seleccionamos en la carpeta input la opción, Table input y la arrastramos hacia la pantalla vacia para empezar a trabajar, ese icono al darle doble click o editar hay que configurarlo para que lea una Tabla especifica de nuestra BD en mi caso leera la tabla noticias, luego de haber cargado las opciones de conexion procedemos a testear la conexion haciendo un preview del mismo y el nos traera todo lo que contenga la tabla, es como si hicieramos un SELECT * FROM noticias.

<p class="centerImage">
<a href="#">
<img src="{{ site.baseurl }}/img/pentaho_5.png" alt="Pentaho tutorial">
</a>
<span class="caption text-muted">Conectando a BD.</span>
</p>

Al haber hecho lo anterior procedemos a seleccionar el step anterior y boton derecho encima de el, seleccionamos la opción preview

<p class="centerImage">
<a href="#">
<img src="{{ site.baseurl }}/img/pentaho_7.png" alt="Pentaho tutorial">
</a>
<span class="caption text-muted">Preview de step input table.</span>
</p>

Ahora al ver nuestro resultado sin problemas, procedemos a realizar unas modificaciones de la columna descripcion, para colocar el cotenido de este campo en mayuscula, para esto usamos un paso en la seccion transformacion > Operaciones de String, y luego unimos el paso anterior con este paso (recordemos la aplicacion PDI en su mayoria es DRAG AND DROP por lo cual es muy intuitivo su uso)

<p class="centerImage">
<a href="#">
<img src="{{ site.baseurl }}/img/pentaho_8.png" alt="Pentaho tutorial">
</a>
<span class="caption text-muted">Preview de step Operaciones de String.</span>
</p>

Como podemos observar en la seccion preview de las metricas de el contenido observamos que nuestra columna ahora muestra informacion en mayuscula, ahora debemos escoger un output (salida) de esta columna, y como nuestro cometido inicial seria exportar nuestra columna a un archivo de texto usamos el paso ubicado en la carpeta output > text file (archivo de texto), lo configuramos y colocamos la ruta donde enviara nuestro archivo.

<p class="centerImage">
<a href="#">
<img src="{{ site.baseurl }}/img/pentaho_9.png" alt="Pentaho tutorial">
</a>
<span class="caption text-muted">Preview de step output textfile.</span>
</p>

Luego veremos que la ruta que colocamos como el output estara con el archivo y la columna en mi caso descripcion con el texto en mayuscula.

En conclusion podemos observar como Pentaho Data Integrator, influye en el flujo de datos de nuestro esquema, podemos conectarnos a multiples origenes, hacer transformaciones y mejoras del flujo de datos e inyectarlos o insertarlos a multiples salidas, dependiendo de como lo requeramos.
