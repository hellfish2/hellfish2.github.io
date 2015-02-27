---
layout:     post
title:      "Como instalar Atom Editor en Debian Linux."
subtitle:   "IDE desarrollado por github, amado por todos los desarrolladores"
date:       2015-02-27 13:00:00
author:     "@hellfish2"
header-img: "img/atom2.png"
---

Atom Editor es el nuevo editor de texto, desarrollado por Github. Este editor está escrito con tecnologías como Node.js, CoffeeScript y LESS, es muy sencillo de usar, muy personalizable y ofrece varias herramientas para el desarrollo.

La instalación para Linux es diferente con respecto a Windows o MAC ya que en estas dos ultimas plataformas es un paquete listo para instalar, mientras tanto en Linux – Debian debemos “construir” el editor en muy pocos pasos.

#### Lo que necesitamos antes de instalar:
* Git
* Node.js v0.10.x
* npm v1.4.x
* gnome keyring dev

#### Comprobación de paquetes:

Como vemos necesitamos tener instalado Git, Node y NPM en las versiones que nos indican. Suponiendo que ya las tenemos instaladas, procederemos a revisar la versión de nuestro Node y NPM.

En caso de no tener instalado Node, podemos revisar este post para poder instalarlo.

#### Revisamos la versión de Node y npm:

Abrimos nuestro terminal o consola y escribimos lo siguiente:

~~~
# node -v
# npm -v
~~~

con esto nos dará la versión de Node que debe ser la version +0.10 (v0.10.x) y la de NPM (npm v1.4.x). En caso que ambos estén desactualizados tendremos que escribir lo siguiente:

~~~
# sudo npm cache clean -f
# sudo npm install -g n
# sudo n stable
~~~

Con esto se actualizará a la última versión de Node y NPM

#### Continuamos con la instalación

Instalamos el keyring:

~~~
# sudo apt-get install libgnome-keyring-dev
~~~

Setup python:

~~~
# sudo npm config set python /usr/bin/python2 -g
~~~

Nos dirigimos a una carpeta donde descargaremos el repositorio de Atom mediante Git y accederemos a ella:

~~~
# git clone https://github.com/atom/atom
# cd atom
~~~

Ahora vamos a compilar “Atom”, una vez dentro de la carpeta, ejecutamos:

~~~
# script/build
~~~

Con esto empezará a ejecutar tareas que será nuestro editor de texto “Atom”

Terminada la compilación, ejecutamos:

~~~
# sudo script/grunt install
~~~

Con esto ya tenemos el editor de texto “Atom” instalado

#### Luego de la instalación

En la consola ejecutamos:

~~~
# atom
~~~

Con esto ya tenemos instalado “Atom” en nuestro linux, donde lo podemos ejecutar por consola o ejecutando como aplicación (Alt + F2).
