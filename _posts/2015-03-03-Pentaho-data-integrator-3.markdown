---
layout:     post
title:      "Pentaho Data integrator 3/5"
subtitle:   "Explicacion Kettle y Spoon."
date:       2015-03-03 01:48:00
author:     "@hellfish2"
header-img: "img/pentaho.png"
---

#### ¿Que es Kettle?

Es un ambiente de Extracción, Transformación, Transporte y Carga Kettle del tipo Open Source. Básicamente la herramienta Pentaho Data Integration (PDI) debe de seguir estas cuatros etapas en todas sus Transformaciones con Kettle (KTR).

#### ¿Que es Spoon?

Spoon es el entorno gráfico estándar de PDI, mediante esta Interfase Gráfica (UI) podemos diseñar todas los KTR basados en una tecnología Rapid application development (RAD). Las tareas son modeladas tipo Workflow ó flujo de trabajo para coordinar recursos, ejecución y dependencias de actividades Extract, transform and load (extracción, transformación y carga) ETL.

Existen otras herramientas para migración de data que se puede abstraer para ser utilizada con PDI pero para efectos de este manual, utilizaremos el Spoon en su forma estándar.

#### Características Generales de PDI.

1. Fácil de Usar.
2. 100% basado en meta-data.
3. Menos complejidad al no tener que generar códigos Extras.
4. Instalación Fácil, Interfase Gráfica sencilla y fácil de mantener.
5. Flexibilidad
6. Nunca obliga a tomar un camino único.
7. Arquitectura adaptable para extender funcionalidad.
8. Arquitectura basadas en estándares modernos.
9. 100% Java con amplio soporte de plataforma.
10. Mas de 70 objetos de mapeo pre-definidos (pasos y tareas).
11. Desempeño y escalabilidad empresarial.
12. Menores costos de propiedad (TCO)
13. No hay costos de Licencias.
14. Ciclos de implantación cortos.
15. Costos de mantenimiento Reducidos.

#### Plataformas soportadas

La GUI de Spoon es soportada en las siguientes plataformas:

1. M$ Window$: todas las plataformas desde Window$ 95, incluyendo Vista.
2. GNU/Linux GTK: en procesadores i386 y x86_64, trabaja mejor en Gnome.
3. OSX de Apple: trabaja en ambas máquinas, PowerPC e Intel.
4. Solaris: utilizando una interface Motif (GTK opcional).
5. AIX: utilizando una interface Motif.
6. HP-UX: utilizando una interface Motif (GTK opcional).
7. FreeBSD: soporte preliminar i386, pero aún no en x86_64.

#### Problemas conocidos

La siguiente es una lista de problemas conocidos que están asociados con Spoon:

##### GNU/Linux
Bloqueo ocasional de la JVM corriendo SuSE Linux y KDE. Corriendo bajo Gnome no presenta problemas (detectado en SUSE Linux 10.1 pero versiones anteriores también tienen el mismo problema).

##### FreeBSD
Problemas con arrastrar y soltar. Utilizar el menú contextual del clic derecho sobre el lienzo como solución.
Consultar las listas de seguimiento en http://jira.pentaho.com para encontrar información actualizada sobre los problemas recientemente descubiertos.

#### Licencia

Desde la versión 2.2.0, Kettle fue liberado al dominio público bajo la licencia LGPL. Por favor consultar el Appendix A para ver el texto completo de esta licencia.

Nota: Pentaho Data Integration es referenciado como "Kettle" en el siguiente texto

Copyright (C) 2006 Pentaho Corporation

Kettle es software libre; se puede redistribuir y/o modificar bajo los términos de la GNU Lesser General Public License publicada por la Free Software Foundation; ya sea la versión 2.1 de la Licencia, o (a elección) cualquier versión posterior.

Kettle se distribuye con la esperanza de que será útil, pero SIN NINGUNA GARANTÍA; incluso sin la garantía implícita de COMERCIALIZACIÓN o IDONEIDAD PARA UN PROPÓSITO PARTICULAR. Ver la GNU Lesser General Public License para más detalles.

Ud. debería haber recibido una copia de la GNU Lesser General Public License junto con la distribución de Kettle; si no es así, escriba a la Free Software Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA 02110-1301 USA.

#### Introduccion a Spoon

En el post anterior explicamos como instalar y correr la aplicación PDI, haremos un repaso para refrescar:

Abrimos una nueva terminal, hecho esto procedemos a ubicarnos dentro de la carpeta descomprimida de PDI, como se puede apreciar existen varios archivos en nuestra carpeta extraida, y luego tipear los siguientes comandos:

~~~
$ cd carpeta_descomprimida
$ ./spoon.sh
~~~

Si nos presenta un error al abrir referenciando "Core dumps have been disabled” error while running java" debemos agregar la instruccion a continuación, editando el archivo spoon.sh, este error se presenta por la libreria libsoup con Gnome3.+ 

~~~
OPT="-Dorg.eclipse.swt.browser.DefaultType=mozilla"
~~~

Al hacer esto nos mostrara un splash (pantalla de carga) de la aplicación, y luego continuamos a ver la aplicación corriendo.

<p class="centerImage">
<a href="#">
<img src="{{ site.baseurl }}/img/pentaho_2.png" alt="Pentaho tutorial">
</a>
<span class="caption text-muted">Ejemplo de instalacion pentaho.</span>
</p>

#### Descripción de interfaz de usuario

PDI tiene dos vistas o pestañas principales (Vista y Diseño), dentro de la pestaña Vista, podemos ver que hay dos carpetas o contenedores que serian, Transformaciones y Jobs.

<p class="centerImage">
<a href="#">
<img src="{{ site.baseurl }}/img/pentaho_3.png" alt="Pentaho tutorial">
</a>
<span class="caption text-muted">Interfaz de pentaho.</span>
</p>

Transformaciones, nos muestra todas las formas que podemos acceder a transformaciones dentro de ellas como por ejemplo entradas, modificaciones de flujo de datos, joins, salidas, entre otros.

Jobs, nos muestra un flujo el cual seria mas general por asi decirlo.

Un Job puede tener infinidades de Jobs internos y estos contienen multiples transformaciones, el concepto es un poco engorroso explicarlo pero mejor lo vemos en la practica.

Antes que nada vamos a crear una conexion a una BD PostgreSQL (debemos tener instalado postgreSQL en nuestra maquina), nos dirigimos a la barra de herramientas y seleccionamos herramientas (Tools) > Wizard > Crear una conexión BD.

<p class="centerImage">
<a href="#">
<img src="{{ site.baseurl }}/img/pentaho_4.png" alt="Pentaho tutorial">
</a>
<span class="caption text-muted">Interfaz de pentaho.</span>
</p>

Nos mostrara una pantalla para que seleccionemos el JDBC que usaremos en nuestro caso PostgreSQL, ingresamos los datos de conexion a nuestra BD y procedemos a seleccionar el boton Test, el cual nos dara el estatus de la conexion a nuestra BD, de tener todos los datos correctosnos dira que tenemos una conexion OK con nuestra BD postgreSQL.

<p class="centerImage">
<a href="#">
<img src="{{ site.baseurl }}/img/pentaho_5.png" alt="Pentaho tutorial">
</a>
<span class="caption text-muted">Interfaz de pentaho.</span>
</p>
