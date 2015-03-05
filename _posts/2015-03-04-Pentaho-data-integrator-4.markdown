---
layout:     post
title:      "Pentaho Data integrator 4/5"
subtitle:   "Creando nuestra primera Transformación."
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
<span class="caption text-muted">Interfaz de pentaho.</span>
</p>

Al haber hecho lo anterior procedemos a seleccionar el step anterior y boton derecho encima de el, seleccionamos la opción preview

<p class="centerImage">
<a href="#">
<img src="{{ site.baseurl }}/img/pentaho_7.png" alt="Pentaho tutorial">
</a>
<span class="caption text-muted">Preview de step input table.</span>
</p>
