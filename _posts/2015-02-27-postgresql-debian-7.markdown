---
layout:     post
title:      "Como instalar PostgreSQL en Debian 7"
subtitle:   "Tutorial para tener instalado postgresql en debian 7."
date:       2015-02-27 14:00:00
author:     "@hellfish2"
header-img: "img/postgresql.jpg"
---
Este articulo explica como instalar el servidor y un cliente de lineas de comandos de la base de datos PostgreSQL en Debian Wheezy.

PostgreSQL, es un gestor de base de datos relacional, la primera versión del código fue público el 1 de agosto de 1996, liberado bajo la licencia BSD y desarrollado por “PostgreSQL Global Development Group”.

Debian GNU/Linux, es un sistema operativo, liberado bajo la licencia GPL y desarrollado por “Proyecto Debian” una comunidad de desarrolladores y usuarios.

#### Instalación

Para este caso se instalara el servidor y un cliente de lineas de comandos PostgreSQL de la versión 9.1, ejecutando el siguiente comando:

~~~
# aptitude install postgresql-9.1
~~~

#### Configuración

Lo primero que se tiene que hacer es cambiarle la contraseña al usuario ‘postgres’ que se crea luego de haber instalado el paquete:

~~~
# passwd postgres
~~~

Acceda a la consola de administración de PostgreSQL para cambiar la contraseña del usuario ‘postgres’ con los siguientes comandos:

~~~
# su postgres
postgres@nombre_maquina:/directorio$ psql postgres
postgres=# ALTER ROLE postgres PASSWORD 'CONTRASENA_DEL_USUARIO';
~~~

Donde ‘postgres’ es el nombre del usuario al cual debe cambiar la contraseña ‘CONTRASENA_DEL_USUARIO’ por la que estableció previamente y luego salga de la sesión, ejecutando los siguientes comandos:

~~~
postgres=# \q
postgres@nombre_maquina:/directorio$ exit
~~~


#### Configuración de acceso local

Para dar acceso local, es decir, dar accesos a clientes PostgreSQL que están en el mismo servidor donde esta instalando el servidor PostgreSQL puede aplicar las siguientes configuraciones básicas:

Debe que cambiar el archivo de configuración del servidor PostgreSQL, con el siguiente comando:

~~~
# vim /etc/postgresql/9.1/main/postgresql.conf
~~~

Busque la linea listen_addresses y verifique que su valor sea el siguiente:

~~~
listen_addresses = 'localhost'
~~~

Guarde el archivo y salga del editor.

También debe modificar el archivo de configuración del cliente PostgreSQL, con el siguiente comando:

~~~
# vim /etc/postgresql/9.1/main/pg_hba.conf
~~~

En este archivo puede configurar los modos de autenticación del cliente PostgreSQL y con que usuario puede acceder a los datos almacenados en el servidor PostgreSQL.

Para este caso de configuración usted esta conectándose localmente en el mismo servidor donde esta instalado PostgreSQL por lo cual la IP local es 127.0.0.1, entonces agregue debajo de la linea “# IPv4 local connections:” la siguiente instrucción:

~~~
host  nombre_base_datos  usuario_postgresql  127.0.0.1/32  password
~~~

Donde ‘nombre_base_datos’ y ‘usuario_postgresql’ es el nombre de la base de datos y el usuario de PostgreSQL a crear respectivamente mas adelante en este articulo.

Con estas configuraciones hechas debe reiniciar el servicio de PostgreSQL, con el siguiente comando:

~~~
# service postgresql restart
~~~

#### Configuración de acceso remoto

Para dar acceso remoto a clientes PostgreSQL desde otro maquina o mascara de red distinta a la de donde esta instalado servidor PostgreSQL puede aplicar las siguientes configuraciones básicas:

Debe que cambiar el archivo de configuración del servidor PostgreSQL, con el siguiente comando:

~~~
# vim /etc/postgresql/9.1/main/postgresql.conf
~~~

Busque la linea listen_addresses = ‘localhost’ y la cambia por el siguiente:

~~~
listen_addresses = '*'
~~~

Opcionalmente usted puede simplemente unir las direcciones IP especificas a la cual da acceso de la siguiente forma:

~~~
listen_addresses='192.168.3.220 192.168.3.221'
~~~

Guarde el archivo y salga de la edición.

También debe modificar el archivo de configuración del cliente PostgreSQL, con el siguiente comando:

~~~
# vim /etc/postgresql/9.1/main/pg_hba.conf
~~~

En este archivo puede configurar desde que maquina o mascara de red puede acceder a los datos almacenados en el servidor PostgreSQL y con que usuario se puede acceder.

Para ejemplo practico que se suponga que esta en una red 192.168.1.1/16 así que quiere darle acceso a la IP 192.168.3.220, agregue debajo de la linea “# IPv4 local connections:” la siguiente instrucción:

~~~
host  nombre_base_datos  usuario_postgresql  192.168.2.3/32  md5
~~~

Donde ‘nombre_base_datos’ y ‘usuario_postgresql’ es el nombre de la base de datos y el usuario de PostgreSQL a crear respectivamente mas adelante en este articulo.

El ‘md5′ es el método de envió de la contraseña del usuario PostgreSQL por la red a comparación de la Configuración de acceso local que se define en ‘password’ la cual envía la contraseña en texto plano por la red, en la Configuración de acceso remota se configura ‘md5′ ya que envía contraseñas cifradas.

Con estas configuraciones hechas debe reiniciar el servicio del servidor PostgreSQL, con el siguiente comando:

~~~
# service postgresql restart
~~~

#### Creando usuarios

Para crear usuarios vuelve a entrar como root de PostgreSQL para crear usuarios para conectarse a la base de datos, en este caso usuario ‘usuario_nomina’ con su contraseña ’123456′, con el siguiente comando:

~~~
# su postgres
postgres@nombre_maquina:/directorio$ createuser -D -S -R -l usuario_nomina
~~~

Este usuario ‘usuario_nomina’ tiene permiso para no crear base de datos, no ser super usuario, no crear roles de usuario, se le permite iniciar sesión respectivamente.

Para asignar la contraseña debe conectarse al servidor PostgreSQL, con el siguiente comando:

~~~
postgres@nombre_maquina:/directorio$ psql postgres
~~~

Esta la sesión conectado altere el usuario asignando una contraseña cifrada, con el siguiente comando:

~~~
postgres=# ALTER USER usuario_nomina WITH ENCRYPTED PASSWORD '123456';
ALTER ROLE
~~~

Para comprobar que el usuario se creo con éxito, ejecute los siguientes comandos:

~~~
postgres=# SELECT usename, passwd FROM pg_shadow;
usename    |               passwd
----------------+-------------------------------------
postgres   | md53175bce1d3201d16594cebf9d7eb3f9d
usuario_nomina | md5bad743050fa6b819130855f6cbb357ee
(2 filas)
~~~

Luego salga de la sesión de base de datos, ejecutando el siguiente comando:

~~~
postgres=# \q
~~~

### Creando base de datos

Primero tiene que iniciar sesión como usuario “root” de PostgreSQL, con el siguiente comando:

~~~
# su postgres
~~~

Luego de iniciar sesión en el servidor como “root”, ahora usted puede crear una base de datos, con el siguiente comando:

~~~
postgres@nombre_maquina:/directorio$ createdb -Ttemplate0 -O usuario_nomina -EUTF-8 sistema_nomina
~~~

Esta base de datos ‘sistema_nomina’ se basa en la plantilla de base de datos llamada ‘template0′ con la cual es construida, el usuario dueño de la base de datos es el usuario ‘usuario_nomina’ previamente creado, usando el esquema de codificación de caracteres ‘UTF-8′ soportado a ser usado en esta base de datos respectivamente.

Para los privilegios del usuario ‘usuario_nomina’ en la base de datos ‘sistema_nomina’ debe conectarse al servidor PostgreSQL, ejecute el siguiente comando:

~~~
postgres@nombre_maquina:/directorio$ psql postgres
~~~

Al estar en la sesión conectado otorgue todos los privilegios al usuario ‘usuario_nomina’ en la base de datos ‘sistema_nomina’, con el siguiente comando:

~~~
postgres=# GRANT ALL PRIVILEGES ON DATABASE sistema_nomina TO usuario_nomina;
~~~

Para comprobar que la base datos esta creada, ejecute el siguiente comando:

~~~
postgres=# SELECT datname FROM pg_database;
datname
-----------------
template0
postgres
template1
sistema_nomina
(4 filas)
~~~

Luego salga de la sesión de base de datos, ejecutando el siguiente comando:

~~~
postgres=# \q
~~~

#### Cargar estructura de datos y registros

A continuación se creará una base de datos basado en un script que importa toda las sintaxis en lenguaje de definición de datos (DDL) y lenguaje de manipulación de datos (DML) en SQL para construirla, ejecute el siguiente comando:

~~~
postgres@nombre_maquina:/directorio$ psql -U postgres -f /home/macagua/script.sql
~~~

Luego salga de la sesión de usuario postgres, ejecutando el siguiente comando:

~~~
postgres@nombre_maquina:/directorio$ exit
~~~

#### Accediendo a la base de datos

Una ves realizado los pasos anteriormente descritos ahora puede conectarse con el usuario ‘usuario_nomina‘ a la base de datos ‘sistema_nomina’ y para estoy existe varias formas de acceso que se describen a continuación:

##### Acceso local a la base de datos
Se utiliza este forma de acceso a la base de datos cuando tiene hecha una configuración de acceso local y para esto se ejecuta el siguiente comando:

~~~
postgres@nombre_maquina:/directorio$ psql -d sistema_nomina -U usuario_nomina
Contraseña para usuario usuario_nomina:
psql (9.1.8)
Digite «help» para obtener ayuda.

sistema_nomina=> help
Está usando psql, la interfaz de línea de órdenes de PostgreSQL.
Digite: \copyright para ver los términos de distribución
\h para ayuda de órdenes SQL
\? para ayuda de órdenes psql
\g o punto y coma («;») para ejecutar la consulta
\q para salir
sistema_nomina=>
~~~

#### Acceso remoto a la base de datos

Se utiliza este forma de acceso a la base de datos cuando tiene hecha una configuración de acceso remoto, a diferencia del acceso local a la base de datos en este caso tiene que indicar el ‘host’ al cual se desea conectar, para hacer esto se ejecuta el siguiente comando:

~~~
postgres@nombre_maquina:/directorio$ psql -h 10.10.29.50 -U usuario_nomina -d sistema_nomina
Contraseña para usuario usuario_nomina:
psql (9.1.8)
Digite «help» para obtener ayuda.

sistema_nomina=> help
Está usando psql, la interfaz de línea de órdenes de PostgreSQL.
Digite: \copyright para ver los términos de distribución
\h para ayuda de órdenes SQL
\? para ayuda de órdenes psql
\g o punto y coma («;») para ejecutar la consulta
\q para salir
sistema_nomina=>
~~~

Y así de esta forma ¡esta listo para trabajar con la base de datos!
