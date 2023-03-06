<span style="color:RoyalBlue">

# **Guía para la instalación de WordPress.**

</span>

<span style="color:Silver">

## **Guía destinada a la instalación de WordPress en Ubuntu 20.04 LTS.**

</span>

<br>

Esta es una guía acerca de cómo instalar _Wordpress_ en _Ubuntu_ 20.04 _LTS_, deseamos que la documentación aportada sea de utilidad para otros usuarios y, también, sirva para mejorar las habilidades en el uso de _Markdown_ y _GitHub_.

Reciba un cordial saludo de

El [equipo de trabajo](../src/autores.md).

<br>

---
---

<br>

<span style="color:Silver">

## **Índice de contenidos.**

</span>

<br>

1. [Introducción][apdo1]
   
2. [Instalación de LAMP][apdo2]
   
   2.1. [Introducción a LAMP][apdo21]
   
   2.2. [Primeros pasos][apdo22]
   
   2.3. [Instalación de Apache HTTP Server][apdo23]

   2.4. [Instalación de MariaDB][apdo24]

   2.5. [Instalación de PHP][apdo25]

3. [Configuración de LAMP][apdo3]
   
4. [Instalación de WordPres][apdo4]
   
5. [Configuración de WordPress][apdo5]
      
6. [Información acerca del equipo de trabajo](../src/autores.md)

<br>

---
---

<br>

<div id='id1' />

<span style="color:Silver">

## **1. Introducción.**

</span>

<br>

[apdo1]: #id1

<img src="../imgs/wordpress_intro.png" width="60%" height="60%"></img>

<br>

Millones de personas en todo el mundo utilizan este potente _CMS_ de código abierto, personalizable y conectable, para crear _blogs_ y sitios _web_ totalmente funcionales. El aprendizaje y manejo permite, incluso para quienes no tienen experiencia previa en diseño o desarrollo _web_, llevar a cabo proyectos de cierta envergadura.

Dispone una amplia variedad _themes_ y _plugins_, que te permitirán personalizar, con el aspecto que desees tu _web_.

Hay muchas formas de acceder a _WordPress_, para gestionar y modificar tus _webs_. No obstante, en algunos casos, los usuarios no informáticos &mdash;la mayoría&mdash; tienen ciertas dificultades en la instalación y configuración de este _CMS_, debido a determinados requisitos.

En esta guía te ayudaremos en la instalación y configuración de _WordPress_ en _Ubuntu_ _MATE_ 20.04 _LTS_.

<br>

---
---

<br>

<div id='id2' />

[apdo2]: #id2

<span style="color:Silver">

## **2. Instalación de LAMP.**

</span>

---

<br>

<div id='id21'/>

[apdo21]: #id21

<span style="color:DarkGray">

### **2.1. Introducción a LAMP.**

</span>

Entre estos requisitos, una vez instalado y configurado el correspondiente sistema operativo, destaca la necesidad de disponer de un _software stack_. Sucintamente, se trata de un conjunto de aplicaciones y herramientas, que “ayudan” al _CMS_ a realizar sus tareas.

En el caso de _LAMP_, se trata de un _software stack_ que comprende la instalación de los siguientes tipos de _software_:

+ **L** &nbsp;&nbsp;&nbsp;_Linux_. Sistema Operativo.
+ **A**	&nbsp;&nbsp;&nbsp;_Apache HTTP Server_. Plataforma destinada a la creación de un servidor _web_.
+ **M**	&nbsp;&nbsp;&nbsp;_MariaDB_/_MySQL_. Sistemas de gestión de bases de datos.
+ **P**	&nbsp;&nbsp;&nbsp;_PHP_. Intérprete del lenguaje de programción _php_, necesario para visualizar las _webs_ dinámicas.

**Nota.**

El usuario deberá haber instalado, previamente la distribución de _Linux_ señalada. La instalación comenzará a partir de segundo punto, es decir, con la instalación de _Apache HTTP Server_, ...

---

<br>

<div id='id22'/>

[apdo22]: #id22

<span style="color:DarkGray">

### **2.2. Primeros pasos.**

</span>

Abrimos el terminal (_shell_); también, pulsando teclas&nbsp;&nbsp; `Alt + Ctrl + T`&nbsp; y procedemos a tomar control del sistema como superusuario (_root_), empleando los siguientes códigos; según sea la situación:

+ En el caso de conocer la contraseña del superusuario (_root_), entonces:
```
nombre_del_usuario@nombre_de_la_computadora:~$ su -

Contraseña:

root@nombre_la_computadora:~#
```
+ En el caso de desconocer la contraseña del superusuario (_root_) y sólo disponer de la contraseña del usuario, entonces:

```
nombre_del_usuario@nombre_de_la_computadora:~$ sudo -i

[sudo] contraseña para nombre_del_usuario:

root@nombre_la_computadora:~#
```

Antes de continuar, realizaremos la actualización de todo el _software_ que haya sido instalado en la computadora:

```
root@nombre_la_computadora:~# apt update
```

Una vez que termine leer la lista de posibles actualizaciones, en función del respositorios disponibles; respectivamente; procederemos a realizar dicha actualización.

```
root@nombre_la_computadora:~# apt upgrade -y
```

---

<br>

<div id='id23'/>

[apdo23]: #id23

<span style="color:DarkGray">

### **2.3. Instalación de Apache HTTP Server.**

</span>

Sin salir del terminal y con el sistema actualizado, procederemos a instalar _Apache HTTP Server_:

```
root@nombre_la_computadora:~# apt install -y apache2 apache2-utils
```

A continuación, ejecutamos la siguiente orden, de modo que, ahora nuestra computadora pueda realizar tareas como servidor:

```
root@nombre_la_computadora:~# systemctl start apache2

root@nombre_la_computadora:~# systemctl enable apache2
```

**Nota.**

Es preciso, comprobar que el servicio esté ejecutándose en todo momento, para ello escribimos:

```
root@nombre_la_computadora:~# systemctl status apache2
```
Si el servicio está ejecutándose correctamente y en todo momento, entonces, el terminal debería mostrarnos algo así:

```
● apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor prese>
     Active: active (running) since Thu 2023-02-23 09:11:17 CET; 4h 7min ago
       Docs: https://httpd.apache.org/docs/2.4/
   Main PID: 1088 (apache2)
      Tasks: 6 (limit: 9406)
     Memory: 19.0M
        CPU: 1.039s
     CGroup: /system.slice/apache2.service
             ├─1088 /usr/sbin/apache2 -k start
             ├─1118 /usr/sbin/apache2 -k start
             ├─1119 /usr/sbin/apache2 -k start
             ├─1120 /usr/sbin/apache2 -k start
             ├─1121 /usr/sbin/apache2 -k start
             └─1122 /usr/sbin/apache2 -k start

feb 23 09:11:16 nombre_de_la_computadora systemd[1]: Starting The Apache HTTP Server...
feb 23 09:11:17 nombre_de_la_computadora systemd[1]: Started The Apache HTTP Server.
```

Si abrimos un navegador, como _Mozilla Firefox_ y escribimos en la barra de búsqueda, alguna de las siguientes direcciones:

+ localhost
+ localhost:80
+ localhost:8080

Debe mostrar una página de esta guisa:

<br>

![apache_works](/imgs/apache_works.png "Apache HTTP Server")

---

<br>

<div id='id24' />

<span style="color:DarkGray">

### **2.4. Instalación de MariaDB.**

</span>

[apdo24]: #id24

Una vez instalado _Apache HTTP Server_ dispondremos de comunicación a través de un protocolo de red, entre un cliente (p. ej. un navegador) y el servidor que, en este caso, será nuestra computadora (_localhost_). Por otra parte, los contenidos creados para una _web_ o _API_ &mdash;veáse, en el caso que nos ocupa, _WordPress_&mdash; deben almacenarse en algún lugar. En este sentido, si vamos a crear nuestros propios contenidos, desde nuestra computadora, es recomendable disponer de una base de datos “_in situ_”. Para ello, disponemos de ciertos _RDBMS_ de código abierto, que se encargarán de gestionar el almacenamiento. Entre éstos destacan _MySQL_ y su bifurcación (_fork_), denominada _MariaDB_.

En esta guía proponemos la instalación de _MariaDB_ vía _shell_, de la siguiente manera:

```
root@nombre_la_computadora:~# apt-get install mariadb-server
```

A continuación, ejecutamos la siguiente orden, de modo que, el _RDBMS_ se conecte con los servidores y repositorios correspondientes:

```
root@nombre_la_computadora:~# systemctl start mariadb

root@nombre_la_computadora:~# systemctl enable mariadb
```

**Nota.**

Al igual, que sucedió con _Apache HTTP Server_, comporbaremos que el servicio esté ejecutándose en todo momento, para ello escribimos:

```
root@nombre_la_computadora:~# systemctl status mariadb
```
Si el servicio está ejecutándose correctamente y en todo momento, entonces, el terminal debería mostrarnos algo así:

```
● mariadb.service - MariaDB 10.6.12 database server
     Loaded: loaded (/lib/systemd/system/mariadb.service; enabled; vendor preset: enabled)
     Active: active (running) since Thu 2023-02-23 16:15:18 CET; 5h 51min ago
       Docs: man:mariadbd(8)
             https://mariadb.com/kb/en/library/systemd/
    Process: 1185 ExecStartPre=/usr/bin/install -m 755 -o mysql -g root -d /var/run/mysqld (code=exited, status=0/SUCCESS)
    Process: 1207 ExecStartPre=/bin/sh -c systemctl unset-environment _WSREP_START_POSITION (code=exited, status=0/SUCCESS)
    Process: 1212 ExecStartPre=/bin/sh -c [ ! -e /usr/bin/galera_recovery ] && VAR= ||   VAR=`cd /usr/bin/..; /usr/bin/galera_recovery`; [ $? -eq 0 ]   && systemctl set-environment _WSREP_START_POS>
    Process: 1299 ExecStartPost=/bin/sh -c systemctl unset-environment _WSREP_START_POSITION (code=exited, status=0/SUCCESS)
    Process: 1301 ExecStartPost=/etc/mysql/debian-start (code=exited, status=0/SUCCESS)
   Main PID: 1258 (mariadbd)
     Status: "Taking your SQL requests now..."
      Tasks: 8 (limit: 18848)
     Memory: 90.3M
        CPU: 3.765s
     CGroup: /system.slice/mariadb.service
             └─1258 /usr/sbin/mariadbd

feb 23 16:15:18 nombre_de_la_computadora mariadbd[1258]: Version: '10.6.12-MariaDB-0ubuntu0.22.04.1'  socket: '/run/mysqld/mysqld.sock'  port: 3306  Ubuntu 22.04
feb 23 16:15:18 nombre_de_la_computadora systemd[1]: Started MariaDB 10.6.12 database server.
feb 23 16:15:18 nombre_de_la_computadora /etc/mysql/debian-start[1303]: Upgrading MySQL tables if necessary.
feb 23 16:15:18 nombre_de_la_computadora /etc/mysql/debian-start[1306]: Looking for 'mariadb' as: /usr/bin/mariadb
feb 23 16:15:18 nombre_de_la_computadora /etc/mysql/debian-start[1306]: Looking for 'mariadb-check' as: /usr/bin/mariadb-check
```

---

<br>

<div id='id25'/>

[apdo25]: #id25

<span style="color:DarkGray">

### **2.5. Instalación de PHP.**

</span>

A pesar del título, realmente, la clave que permite que todo este proceso “tenga sentido” reside en este punto... _PHP_ es un lenguaje de programación que proporciona los mecanismos, para poder trabajar con casi cualquier base de datos y servidor _web_. La finalidad es lograr la integración de las páginas _HTML_ con _APIs_ que “corren” en el servidor, como procesos integrados en el mismo, y no como procesos independientes. Se trata de emplear el navegador como cliente, que nos permita cargar _APIs_ que requieran un intérprete de _PHP_ para poder visualizarse en el cliente.

<br>

Para una mejor comprensión de _PHP_, debemos observar lo que nos haría falta para programar en _PHP_:

+ Un editor para poder escribir los programas _PHP_. En este caso, dicho programa ya está escrito, se trata del _CMS_ _WordPress_.

+ Un servidor de páginas web , que ejecute y muestre los programas realizados con PHP, en este caso, _Apache HTTP Server_.

+ Un _RDBMS_, donde podamos guardar y recuperar la información. Nosotros emplearemos _MariaDB_.

+ Un navegador, para visualizar las páginas generadas con _PHP_.

Cuando pedimos a nuestro servidor web una página _PHP_, que no es sino un programa _PHP_ que genera una página _HTML_, el servidor le pasa la página al interprete _PHP_ y es el resultado lo que se le envía al cliente.

<br>

Para _Ubuntu_ _MATE_ 20.04 _LTS_ se instalará la versión 7.4 de _PHP_&nbsp;&nbsp;&mdash;por cuestiones de “compatibilidad”&mdash;. También, desde el terminal como superusuario (_root_):

```
root@nombre_la_computadora:~# apt install php7.4 libapache2-mod-php7.4 php7.4-mysql

Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  libapache2-mod-php7.4 php-common php7.4 php7.4-cli php7.4-common php7.4-json php7.4-mysql php7.4-opcache php7.4-readline
Suggested packages:
  php-pear
The following NEW packages will be installed:
  libapache2-mod-php libapache2-mod-php7.4 php php-common php-mysql php7.4 php7.4-cli php7.4-common php7.4-json php7.4-mysql php7.4-opcache php7.4-readline
0 upgraded, 12 newly installed, 0 to remove and 603 not upgraded.
Need to get 4,147 kB of archives. After this operation, 18.5 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
```


Para asegurarnos un correcto funcionamiento de _WordPress_, instalaremos algunos módulos adicionales:

```
root@nombre_la_computadora:~# apt install php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip

Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  libonig5 libxmlrpc-epi0 libzip5 php7.4-curl php7.4-gd php7.4-intl php7.4-mbstring php7.4-soap php7.4-xml php7.4-xmlrpc php7.4-zip
The following NEW packages will be installed:
  libonig5 libxmlrpc-epi0 libzip5 php-curl php-gd php-intl php-mbstring php-soap php-xml php-xmlrpc php-zip php7.4-curl php7.4-gd php7.4-intl php7.4-mbstring php7.4-soap php7.4-xml php7.4-xmlrpc php7.4-zip
0 upgraded, 19 newly installed, 0 to remove and 603 not upgraded.
Need to get 1,063 kB of archives.
After this operation, 3,814 kB of additional disk space will be used.
Do you want to continue? [Y/n] Y 
```

Una vez terminada la instalación de este _software package_, reiniciamos el servicio de _Apache HTTP Server_:

```
root@nombre_la_computadora:~# a2enmod php7.4
Considering dependency mpm_prefork for php7.4:
Considering conflict mpm_event for mpm_prefork:
Considering conflict mpm_worker for mpm_prefork:
Module mpm_prefork already enabled
Considering conflict php5 for php7.4:
Module php7.4 already enabled

root@nombre_la_computadora:~# systemctl restart apache2
```

---
---

<br>

<div id='id3' />

[apdo3]: #id3

<span style="color:Silver">

## **3. Configuración de LAMP.**

</span>

---

<br>

Este apartado comprenderá una serie de pasos necesarios para que, posteriormente, funcione el _CMS_ _WordPress_.

En primer lugar, “regresamos al apartado” del _RDBMS_. Esto se debe a que se recomienda, encarecidamente, que se ejecute un programa de seguridad con objeto de eliminar la configuración predeterminada insegura y proteger las bases de datos.

```
root@nombre_la_computadora:~# mysql_secure_installation

NOTE: RUNNING ALL PARTS OF TIRIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PIOXICTION USEI PLEASE READ EA. STEP CAREFULLY!. 

In order to log into MariaDB to secure it, we'll need the current password for the root user. If you've just installed MariaDB, and you haven't set the root password yet, the password will be blank, so you should just press enter here.

Enter current password for root (enter for none):
OK, successfully used password, moving on... 

Setting the root password ensures that nobody can log into the MariaDB
root user without the proper authorisation.

Set root password? [Y/n] Y 
New password:
Re-enter new password:
```
---
**Nota.**

Preste atención.

+ Cuando nos diga:

  `Enter current password for root (enter for none):`

  Presionamos:
  
  `Intro`

+ Cuando nos diga:

  `New password:`

  Insertaremos una contraseña [segura](https://randomkeygen.com/), que repetiremos:

  `Re-enter new password:`

---

A continuación, proseguirá una secuencia como esta, en la que presionaremos `Intro` después de escribir `Y`.

```
By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them. This is intended only for testing, and to make the  installation
go a bit smoother. You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n] Y
 ... Success!

Normally, root should only be allowed to connect from 'localhost'. This
ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? [Y/n] Y

By default, MariaDB comes with a database named 'test' that anyone can
access. This is also intended only for testing, and should be removed
before moving into a production environment.

Remove test database and access to it? [Y/n] Y
 - Droping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privileges tables will ensure that all changes made so for
will take effect immediately.

Reload privileges tables now? [Y/n] Y
  ... Success!

Cleaning up...

All done! If you've completed all of the above steps, your MariaDB
installation should be now be secure.

Thanks for using MariaDB!
```
---

En el caso de _PHP_ crearemos un archivo con la finalidad de comprobar si funciona correctamente el _package_ instalado:

```
root@nombre_la_computadora:~# cd /
root@nombre_la_computadora:/# cd var/www/html/
root@nombre_la_computadora:/var/www/html# nano info.php
```
<img src="../imgs/info_php.png" width="40%" height="40%"></img>

<br>

Una vez guardado (`Ctrl + S`), abrimos el navegador y en la barra de direcciones escribimos lo siguiente (ambas opciones son válidas):

+ 127.0.0.1/info.php
  
+ localhost/info.php

<br>

<img src="../imgs/php_localhost.png" width="50%" height="50%"></img>

<br>

**Nota.**

Se recomienda como medida de seguridad una vez comprobado que funciona, la eliminación del archivo `info.php`:
```
root@nombre_la_computadora:/var/www/html# rm info.php
```

---
---

<br>

<div id='id4' />

[apdo4]: #id4

<span style="color:Silver">

## **4. Instalación de WordPress.**

</span>

---

<br>

Desde el directorio `/var/www/html#` procedemos a la descarga del archivo `latest.tar.gz`:

```
root@nombre_la_computadora:/var/www/html# wget -c http://wordpress.org/latest.tar.gz
--2023-02-24 02:02:51--  http://wordpress.org/latest.tar.gz
Resolving wordpress.org (wordpress.org)... 198.143.164.252
Connecting to wordpress.org (wordpress.org)|198.143.164.252|:80... connected.
HTTP request sent, awaiting response... 301 Moved Permanently
Location: https://wordpress.org/latest.tar.gz [following]
--2023-02-24 02:02:51--  https://wordpress.org/latest.tar.gz
Connecting to wordpress.org (wordpress.org)|198.143.164.252|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 22751086 (22M) [application/octet-stream]
Saving to: ‘latest.tar.gz’

latest.tar.gz       100%[===================>]  21,70M  1,54MB/s    in 14s     

2023-02-24 02:03:06 (1,52 MB/s) - ‘latest.tar.gz’ saved [22751086/22751086]

root@nombre_la_computadora:/var/www/html# ls -l
total 22236
-rw-r--r-- 1 root root    10671 ene 31 22:30 index.html
-rw-r--r-- 1 root root 22751086 nov 15 20:04 latest.tar.gz
```
Descomprimimos el archivo `latest.tar.gz` en este directorio. Este archivo contiene una carpeta comprimida denominada `wordpress`, que creará un directorio del mismo nombre.

```
root@nombre_la_computadora:/var/www/html# tar -xzvf latest.tar.gz
```
<br>

```
root@nombre_la_computadora:/var/www/html# ls -l
total 22240
-rw-r--r-- 1 root   root       10671 ene 31 22:30 index.html
-rw-r--r-- 1 root   root    22751086 nov 15 20:04 latest.tar.gz
drwxr-xr-x 5 nobody nogroup     4096 nov 15 20:03 wordpress
```

A continuación, debemos asignar un nuevo usuario y grupo, concederle permisos recursivamente, al directorio `wordpress`.

```
root@nombre_de_la_computadora:/var/www/html# chown -R www-data:www-data wordpress/
root@nombre_de_la_computadora:/var/www/html# ls -l
total 22240
-rw-r--r-- 1 root     root        10671 ene 31 22:30 index.html
-rw-r--r-- 1 root     root           20 feb 24 01:32 info.php
-rw-r--r-- 1 root     root     22751086 nov 15 20:04 latest.tar.gz
drwxr-xr-x 5 www-data www-data     4096 nov 15 20:03 wordpress
```
---
---

<br>

<div id='id5' />

[apdo5]: #id5

<span style="color:Silver">

## **5. Configuración de WordPress.**

</span>

---

<br>

Ya falta poco...

Ahora, debemos crear la base de datos, donde almacenaremos datos “sensibles”.

```
root@nombre_de_la_computadora:/var/www/html# mysql -u root -p
Enter password:

Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 31
Server version: 10.6.12-MariaDB-0ubuntu0.22.04.1 Ubuntu 22.04

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> CREATE DATABASE nombre_de_la_nueva_base_de_datos;
Query OK, 1 row affected (0,001 sec)

MariaDB [(none)]> CREATE USER nombre_del_nuevo_usuario@localhost IDENTIFIED BY 'contraseña_segura';
Query OK, 0 rows affected (0,002 sec)

MariaDB [(none)]> GRANT ALL PRIVILEGES ON nombre_de_la_nueva_base_de_datos.* TO nombre_del_nuevo_usuario@localhost;
Query OK, 0 rows affected (0,001 sec)

MariaDB [(none)]> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0,001 sec)

MariaDB [(none)]> exit;
Bye
```
**Nota.**

Recordemos que cuando accedemos a _MariaDB_ (`mysql -u root -p`), la contraseña (`Enter password`) es la que asignamos durante la [configuración de _MariaDB_][apdo3].

A modo de que el ejemplo fuese lo más comprensivo posible, se escribió `nombre_de_la_nueva_base_de_datos` y `nombre_del_nuevo_usuario`. En vuestro caso, os sugerimos proponer nombres más adecuados, como `wordpress_db` y `usuario_wordpress`; p. ej.; respectivamente.

---

Proseguimos en el directorio anterior y ...
```
root@nombre_de_la_computadora:/var/www/html# chmod -R 777 wordpress/

root@nombre_de_la_computadora:/var/www/html# cd wordpress/

root@nombre_de_la_computadora:/var/www/html/wordpress# ls -l
total 224
-rwxrwxrwx  1 www-data www-data   405 feb  6  2020 index.php
-rwxrwxrwx  1 www-data www-data 19915 ene  1  2022 license.txt
-rwxrwxrwx  1 www-data www-data  7389 sep 17 00:27 readme.html
-rwxrwxrwx  1 www-data www-data  7205 sep 17 01:13 wp-activate.php
drwxrwxrwx  9 www-data www-data  4096 nov 15 20:03 wp-admin
-rwxrwxrwx  1 www-data www-data   351 feb  6  2020 wp-blog-header.php
-rwxrwxrwx  1 www-data www-data  2338 nov 10  2021 wp-comments-post.php
-rwxrwxrwx  1 www-data www-data  3001 dic 14  2021 wp-config-sample.php
drwxrwxrwx  4 www-data www-data  4096 nov 15 20:03 wp-content
-rwxrwxrwx  1 www-data www-data  5543 sep 20 17:44 wp-cron.php
drwxrwxrwx 27 www-data www-data 12288 nov 15 20:03 wp-includes
-rwxrwxrwx  1 www-data www-data  2494 mar 19  2022 wp-links-opml.php
-rwxrwxrwx  1 www-data www-data  3985 sep 19 10:59 wp-load.php
-rwxrwxrwx  1 www-data www-data 49135 sep 20 00:26 wp-login.php
-rwxrwxrwx  1 www-data www-data  8522 oct 17 13:06 wp-mail.php
-rwxrwxrwx  1 www-data www-data 24587 sep 26 12:17 wp-settings.php
-rwxrwxrwx  1 www-data www-data 34350 sep 17 02:35 wp-signup.php
-rwxrwxrwx  1 www-data www-data  4914 oct 17 13:22 wp-trackback.php
-rwxrwxrwx  1 www-data www-data  3236 jun  8  2020 xmlrpc.php
```

Renombramos el archivo `wp-config-sample.php` como `wp-config.php`. 

```
root@nombre_de_la_computadora:/var/www/html/wordpress# mv wp-config-sample.php wp-config.php

root@nombre_de_la_computadora:/var/www/html/wordpress# ls -l
total 224
-rwxrwxrwx  1 www-data www-data   405 feb  6  2020 index.php
-rwxrwxrwx  1 www-data www-data 19915 ene  1  2022 license.txt
-rwxrwxrwx  1 www-data www-data  7389 sep 17 00:27 readme.html
-rwxrwxrwx  1 www-data www-data  7205 sep 17 01:13 wp-activate.php
drwxrwxrwx  9 www-data www-data  4096 nov 15 20:03 wp-admin
-rwxrwxrwx  1 www-data www-data   351 feb  6  2020 wp-blog-header.php
-rwxrwxrwx  1 www-data www-data  2338 nov 10  2021 wp-comments-post.php
-rwxrwxrwx  1 www-data www-data  2999 feb 24 02:58 wp-config.php
drwxrwxrwx  4 www-data www-data  4096 feb 24 02:59 wp-content
-rwxrwxrwx  1 www-data www-data  5543 sep 20 17:44 wp-cron.php
drwxrwxrwx 27 www-data www-data 12288 nov 15 20:03 wp-includes
-rwxrwxrwx  1 www-data www-data  2494 mar 19  2022 wp-links-opml.php
-rwxrwxrwx  1 www-data www-data  3985 sep 19 10:59 wp-load.php
-rwxrwxrwx  1 www-data www-data 49135 sep 20 00:26 wp-login.php
-rwxrwxrwx  1 www-data www-data  8522 oct 17 13:06 wp-mail.php
-rwxrwxrwx  1 www-data www-data 24587 sep 26 12:17 wp-settings.php
-rwxrwxrwx  1 www-data www-data 34350 sep 17 02:35 wp-signup.php
-rwxrwxrwx  1 www-data www-data  4914 oct 17 13:22 wp-trackback.php
-rwxrwxrwx  1 www-data www-data  3236 jun  8  2020 xmlrpc.php
```
Después de comprobar que, efectivamente, hemos renombrado el susodicho archivo, procedemos a editarlo.

```
root@nombre_de_la_computadora:/var/www/html/wordpress# nano wp-config.php
```

Al abrir el archivo `wp-config.php` con el editor...

<br>

<img src="../imgs/wp_config_php.png" width="50%" height="50%"></img>

<br>

Obsérvese detenidamente.

Los huecos en blanco, que por defecto la primera vez están escritos, debemos sobreescribirlos, de este modo:

+ `define( 'DB_NAME', 'nombre_de_la_nueva_base_de_datos');`

+ `define( 'DB_USER', 'nombre_del_nuevo_usuario');`

+ `define( 'DB_PASSWORD', 'contraseña_segura');`

Es importante, también, definir la dirección a través de la cual vamos acceder al _CMS_ _WordPress_, por medio del navegador, en este caso:

`localhost/wordpress`

Una vez guardado el archivo, cerramos definitivamente el terminal y nos dirigimos al navegador, en este caso, empleamos _Mozilla Firefox_.

<br>

<img src="../imgs/wp_one.png" width="80%" height="80%"></img>

<br>

A partir de este punto, el proceso es más intuitivo.

Rellenaremos los campos tal como nos lo indica, puesto que, el propio _CMS_ nos permitirá modificarlos, posteriormente, si lo deseamos.

<br>

<img src="../imgs/wp_two.png" width="80%" height="80%"></img>

<br>

Por defecto, el campo correspondiente a la contraseña está cubierto con un ejemplo. Por supuesto, elija una similar, no la misma que le ofrece.

Finalmente...

<br>

<img src="../imgs/wordpress_intro.png" width="80%" height="80%"></img>

<br>

---

<br>

[Regresar al principio][apdo1]

[Ver los autores](../src/autores.md)



