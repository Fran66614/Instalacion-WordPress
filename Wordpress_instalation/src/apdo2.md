## **2. Instalación de LAMP.**

---

<br>

### **Índice de contenidos de este apartado.**

<br>

2. [Instalación de LAMP][inicio2]
   
   2.1. [Introducción a LAMP][apdo21]
   
   2.2. [Primeros pasos][apdo22]
   
   2.3. [Instalación de Apache HTTP Server][apdo23]

   2.4. [Instalación de MariaDB][apdo24]

   2.5. [Instalación de PHP][apdo25]

<br>

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

<br>

[Regresar al índice general de contenidos](../README.md)

[Continuar...](apdo3.md)

[Regresar al apartado anterior](apdo1.md)


