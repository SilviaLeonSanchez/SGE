# INDICE

# CONTENIDO

## CONFIGURACIÓN UBUNTU SERVER

### Habilitar acceso remoto

  Por seguridad no se puede acceder por ssh al usuario root, por lo que necesitamos cambiar el archivo de configuración de ssh desde proxmox:

  `$ sudo nano /etc/ssh/sshd_config`

  Dejando la siguiente linea de esta forma:

  `PermitRootLogin yes`

  Reiniciando después el servicio para que aplique los cambios:

  `$ sudo service sshd restart`

  Conectamos desde fuera de proxmox (por terminal o putty) a la ip de la maquina con:

  `$ ssh root@192.168.3.58`



## PREPARAR INSTALACIÓN ODOO

### 1. Conectar mediante ssh

  `$ ssh root@192.168.3.58`

  Conectamos con root para tener todos los permisos, y no tener que otorgarnos permisos temporales escribiendo sudo delante de cada comando.


### 2. Actualizar la lista de paquetes disponibles

  `$ apt-get update`


### 3. Instalar las depencias que vamos a necesitar para instalar Odoo

  `$ apt-get -yq install adduser postgresql-client python-dateutil python-docutils python-feedparser python-jinja2 python-ldap python-libxslt1 python-lxml python-mako python-mock python-openid python-psycopg2 python-psutil python-pybabel python-pychart python-pydot python-pyparsing python-reportlab python-simplejson python-tz python-unittest2 python-vatnumber python-vobject python-webdav python-werkzeug python-xlwt python-yaml python-zsi poppler-utils python-pip python-pypdf python-passlib python-decorator gcc python-dev libxml2-dev libxslt-dev libsasl2-dev libldap2-dev libssl-dev libpq-dev libjpeg-dev libjpeg8-dev python-setuptools python-markupsafe python-reportlab-accel python-zsi python-yaml python-argparse python-openssl python-egenix-mxdatetime python-usb python-serial lptools make python-pydot python-psutil python-paramiko poppler-utils python-pdftools antiword python-requests python-xlsxwriter python-suds python-software-properties`

![Captura de pantalla 1][img1]


### 4. Instalar el paquete *wkhtmltopdf* para realizar informes en pdf desde Odoo

  * Descargar:

  `$ wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.1/wkhtmltox-0.12.1_linux-trusty-amd64.deb`

  ![Captura de pantalla 2][img2]

  * Desempaquetar indicando que instale el paquete:

  `$ dpkg -i wkhtmltox-0.12.1_linux-trusty-amd64.deb`

  * Si hay problemas de dependencias las instalamos y volvemos a intentar la instalacion:

  `$ apt-get install fontconfig libjpeg-turbo8`

  `$ dpkg -i wkhtmltox-0.12.1_linux-trusty-amd64.deb`

  ![Captura de pantalla 3][img3]


### 5. Instalar npm para que funcione correctamente el servidor web

  * Instalar:

  `$ apt-get -yq install npm`

  ![Captura de pantalla 4][img4]

  * Crear el enlace:

  `$ ln -s /usr/bin/nodejs /usr/bin/node`

  * Con npm intalar less:

  `$ npm install -g less less-plugin-clean-css`

  ![Captura de pantalla 5][img5]


### 6. Instalar pip

  `$ apt-get install python3-pip python-pip`

  ![Captura de pantalla 6][img6]

### 7. Instalar el paquete *pillow*
Para no tener problemas con el procesamiento de imágenes al instalar datos demo instalamos este paquete de python:

  `$ pip install --no-cache-dir -I pillow`

  ![Captura de pantalla 7][img7]


  En mi caso propone actualizar pip con:

  `$ pip install --upgrade pip`

  ![Captura de pantalla 8][img8]


### 8. Instalar *git*

  `$ sudo apt-get install git`

~~~
 INSTANTÁNEA INSTALACIÓN_ODOO_MANUAL
~~~


## INSTALAR POSTGRES

  `$ apt-get install postgresql`

  ![Captura de pantalla 9][img9]


  ![Captura de pantalla 10][img10]

  Dar contraseña al usuario postgres que se ha creado durante la instalación:

  `$ passwd postgres`

  ![Captura de pantalla 11][img11]



## CREAR USUARIOS ODOO

### 1. Crear usuario odoo en la base de datos postgres

  Cambiar al usuario postgres que se acaba de crear en la instalacion:

  `$ sudo su postgres`

  Crear el usuario:

  `$ createuser -P -s -e odoo`

~~~
Argumentos:
-P Preguntar contraseña
-s Permiso para crear bases de datos
-e Mostrar resultado de la operacion
~~~

  ![Captura de pantalla 12][img12]


### 2. Crear usuario odoo en el sistema

  `$ su root`

  `$ sudo adduser odoo`

  ![Captura de pantalla 13][img13]



## INSTALAR ODOO

### 1. Descargar el repositorio de Odoo

  `$ su odoo`

  `cd ~`

  `$ git clone https://github.com/Odoo/odoo.git --depth 1 --branch 10.0 --single-branch odoo`

~~~
¡OJO! Se indica la rama 10 y se tendrá que clonar SIEMPRE esta rama, si no descarga la ultima por defecto.
~~~

  ![Captura de pantalla 14][img14]


### 2. Instalar requisitos de python

  `$ su root`

  `$ pip install -r /home/odoo/odoo/requirements.txt`

  ![Captura de pantalla 15][img15]


~~~
INSTANTÁNEA PRE-CONFIGURACION
~~~

### 3. Crear el archivo de configuración

Para que lea los parametros que necesita al ejecutarse sin que tengamos que pasarlos nosotros.

  `$ su odoo`

  `$ nano ~/odoo-server.conf`

    La ruta del archivo debe ser /home/odoo/odoo-server.conf

Rellenamos el archivo con la siguiente informacion:

~~~
[options]
admin_passwd = admin
xmlrpc = True
xmlrpc_port = 8069
db_host = 127.0.0.1
db_port = 5432
db_user = odoo
db_password = odoo
logfile=/home/odoo/odoo-server.log
addons_path = /home/odoo/odoo/addons
~~~

  ![Captura de pantalla 16][img16]


### 4. Configurar Odoo para que arranque al inicio

 * Crear el archivo:

  `$ su root`

  `$ nano /etc/systemd/system/odoo10.service`

 * Para indicarle el archivo que tiene que ejecutar y el usuario con que lo hace:

~~~
[Unit]
Description=Odoo
[Service]
Type=simple
User=odoo
ExecStart=/home/odoo/odoo/odoo-bin -c /home/odoo/odoo-server.conf
[Install]
WantedBy=default.target
~~~

 Todos los servicios se tienen que crear desde root para que tengan permiso de ejecución, aunque el servicio una vez arrancado se indica que sea propiedad de el usuario odoo.

  ![Captura de pantalla 17][img17]


 * Habilitar el servicio para que se arranque al inicio:

  `$ sudo systemctl enable odoo10.service`

  ![Captura de pantalla 18][img18]


 * Probamos a arrancar y parar el servicio manualmente:

  `$ sudo systemctl start odoo10.service`

  `$ sudo systemctl stop odoo10.service`

~~~
INSTANTANEA TERMINADA
~~~

### 5. Iniciar Odoo

Reiniciando la máquina el servicio se inicia solo, puedo cerrar el terminal y trabajar desde el navegador en la direccion de mi Odoo:

    http://192.168.3.58:8069

Si quisieramos simplemente iniciar Odoo como proceso y no como servicio ejecutamos el comando:

  `$ /home/odoo/odoo/odoo-bin -c /home/odoo/odoo-server.conf`


## CONFIGURAR ODOO

### 1. Cambiar codificación de la base de datos

Conectar con el usuario postgres y arrancar la base de datos:

  `$ su postgres`

  `$ psql postgres`

  Ejecutamos los comandos:

  `update pg_database set datallowconn = TRUE where datname = 'template0';`

  `\c template0`

  `update pg_database set datistemplate = FALSE where datname = 'template1';`

  `drop database template1;`

  `create database template1 with template = template0 encoding = 'UTF8';`

  `update pg_database set datistemplate = TRUE where datname = 'template1';`

  `\c template1`

  `update pg_database set datallowconn = FALSE where datname = 'template0';`

  ~~~
  \q Salir de psql
  ~~~

 ![Captura 19][img19]

### 2. Crear base de datos con datos de prueba

En psql comprobamos las bases de datos que existen:

  `\l`

  ![Captura 20][img20]

~~~
\c bbdd Cambiar a la base de datos
\dt     Listar las tablas de la base de datos
~~~

### 3. Instalar internacialización de Odoo al castellano

Los modulos de internacionalizacion siempre empiezan por l10n, en este caso el que necesitamos se encuentra en www.github.com/oca.

~~~
¡OJO! Instalar SIEMPRE la versión de nuestra rama, la 10.
~~~

  * Cambiar al usuario Odoo para que los archivos que decarguemos sean de su propiedad y los pueda ejecutar:

  `su odoo`

  * Borrar de la carpeta addons el modulo l10n_es:

  `$ rm -r ~/odoo/addons/l10n_es`

  * Descargar el repositorio de odoo en home del usuario odoo:

  `$ git clone --branch 10.0 https://github.com/OCA/l10n-spain.git`

  * Instalar requerimientos:

  En el archivo requirements.txt indica las dependencias de python.

  `$ su root`

  `$ pip install -r requirements.txt`

  * Al descargar el repositorio nos crea una carpeta con todos los modulos dentro, pero necesitamos una carpeta en addons por cada modulo, asique los copiamos con odoo:

  `$ su odoo`

  `$ cp -r -d l10n-spain/* /home/odoo/odoo/addons/`

  * Activar las opciones de desarrollador:

  En la pagina de odoo enteramos en configuración y las encontramos en la esquina inferior derecha.

  * Actualizar lista de aplicaciones:

  Al ir a la pestaña aplicaciones deberia aparecer el la barra lateral izquierda la opción Actualizar lista de aplicaciones.

### 4. Instalar el módulo de topónimos

  * Buscar el repositorio:

  En un navegador buscamos dentro del sitio github de Oca poniendo lo siguiente:

  `base_location_geonames_import site: www.github.com/oca`

  * Descargar:

  Clonamos el repositorio con el enlace que encontramos en el sitio de github y lo descargamos con el usuario odoo en home:

  `$ su odoo`

  `$ cd ~`

  `$ git clone --branch 10.0 https://github.com/OCA/partner-contact.git`

  ~~~
  ¡OJO! Recuerda especificar SIEMPRE la rama 10
  ~~~

  * Copiar el modulo que nos interesa a la carpeta addons:

  `$ cp -r ~/partner-contact/base_location_geonames_import /home/odoo/odoo/addons/`

  * Instalar requerimientos:

   `$ su root`

   `$ pip install -r requirements.txt`

  * Reiniciar la máquina:

   `$ su root`

   `$ reboot`

  * Instalar el módulo en el odoo:

  Ahora que esta en la carpeta de addons lo tenemos disponible para instalar, asique actualizamos el navegador y la lista de aplicaciones y buscamos l10n_es (asegurarse de tener activo el modo desarrollador).

  * Instalar dependencias del módulo:

   Si pide alguna dependencia que se encuentre en este repositorio procedemos igual que con modulo que estamos intentando instalar, es decir, movemos la carpeta correspondiente al mismo de donde lo hemos descargado a la carpeta addons.

   En este caso nos pide el módulo base_location:

   `$ su odoo`

   `mv ~/partner-contact/base_location ~/odoo/addons/`

   Una vez resueltas las dependencias necesarias reintentamos la instalación del módulo.


  * Borrar carpeta del repositorio descargado:

  Esperar siempre a tener instalado el módulo porque puede pedir alguna dependencia que este aquí.

  `$ rm -r /home/odoo/partner-contact/`

### 5. Instalar módulos extra

#### Jasper Reports

Sirve para la generación de informes en distintos formatos.
Disponible en el siguiente enlace:

`git clone -b 10.0 https://github.com/JayVora-SerpentCS/Jasperreports_odoo.git`

#### Web Export View

Disponible en el siguiente enlace:

`git clone -b 10.0 https://github.com/OCA/web.git`

#### Datetime Formatter

Sirve para facilitar el formateo de fechas.
Disponible en el modulo Server Tools (dependencia del modulo de toponimos).

#### Base FontAwesome

Ofrece diferentes tipos de letras para utilizarlos en odoo.
Disponible en el modulo Server Tools (dependencia del modulo de toponimos).














































[img1]: ./CAPTURAS/CAPTURA_1.png
[img2]: ./CAPTURAS/CAPTURA_2.png
[img3]: ./CAPTURAS/CAPTURA_3.png
[img4]: ./CAPTURAS/CAPTURA_4.png
[img5]: ./CAPTURAS/CAPTURA_5.png
[img5]: ./CAPTURAS/CAPTURA_5.png
[img6]: ./CAPTURAS/CAPTURA_6.png
[img7]: ./CAPTURAS/CAPTURA_7.png
[img8]: ./CAPTURAS/CAPTURA_8.png
[img9]: ./CAPTURAS/CAPTURA_9.png
[img10]: ./CAPTURAS/CAPTURA_10.png
[img11]: ./CAPTURAS/CAPTURA_11.png
[img12]: ./CAPTURAS/CAPTURA_12.png
[img13]: ./CAPTURAS/CAPTURA_13.png
[img14]: ./CAPTURAS/CAPTURA_14.png
[img15]: ./CAPTURAS/CAPTURA_15.png
[img16]: ./CAPTURAS/CAPTURA_16.png
[img17]: ./CAPTURAS/CAPTURA_17.png
[img18]: ./CAPTURAS/CAPTURA_18.png
[img19]: ./CAPTURAS/CAPTURA_19.png
[img20]: ./CAPTURAS/CAPTURA_20.png
