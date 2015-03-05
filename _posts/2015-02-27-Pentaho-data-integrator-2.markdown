---
layout:     post
title:      "Pentaho Data integrator 2/5"
subtitle:   "Descarga e Instalacionso de esta herramienta para Bussiness Inteligence."
date:       2015-02-27 22:00:00
author:     "@hellfish2"
header-img: "img/pentaho.png"
---

Como había indicado en el post anterior (Introducción sobre Pentaho) existe bastante información para empezar a trabajar con Pentaho, así que tratando de ordenar esa información lo primero que haremos es descargar los archivos necesarios.

Descargar Pentaho. Empezaremos por descargar la version Data Integration Kettle de Pentaho, ó la que contiene todas las herramientas que ya habíamos indicado.Yo usare la Version Data Integration 5.0.1 CE Stable.

1. Acceder al sitio web oficial de Pentaho. Buscar la seccion de descargas y seleccionar la version que mas se adapte a nuestra maquina, en mi caso usare la version de 64bits, cabe destacar que uso Debian Jessie (Testing):

2. Ahora accedemos al enlace Business Intelligence Server y se mostrará a continuación todas las versiones existentas de Pentaho:

4. Si se elige la version Data Integration 5.0.1 Stable, comenzara la descarga.

##### Instalación.

Una vez descargado el archivo que se haya elegido, lo único que queda es descomprimirlo.

Como se puede apreciar existen varios archivos en nuestra carpeta extraida, lo que debemos hacer es abrir una nueva terminal como usuario y tipear los siguientes comandos:

~~~
$ cd carpeta_descomprimida
$ ./spoon.sh
~~~

Espero que con todo lo indicado sea más fácil tener Pentaho "instalado" en nuestra PC o servidor.

<p class="centerImage">
<a href="#">
<img src="{{ site.baseurl }}/img/pentaho.jpg" alt="Pentaho tutorial">
</a>
<span class="caption text-muted">Bienvenido a Pentaho.</span>
</p>
