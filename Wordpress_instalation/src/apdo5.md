## **5. Configuración de WordPress.**

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

---

<br>

[Regresar al índice general de contenidos](../README.md)

[Ver los autores](autores.md)

[Regresar al apartado anterior](apdo4.md)