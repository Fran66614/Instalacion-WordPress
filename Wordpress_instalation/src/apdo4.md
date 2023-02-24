## **4. Instalación de WordPress.**

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

<br>

[Regresar al índice general de contenidos](../README.md)

[Continuar...](apdo5.md)

[Regresar al apartado anterior](apdo3.md)