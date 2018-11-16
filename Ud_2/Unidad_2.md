# INDICE<a name="indice"/>

* [Configurar acceso remoto a Ubuntu Server](#id1)
* [Preparar instalación Odoo](#id2)
  * [Instalar las dependencias](#id2a)
  * [Instalar *wkhtmltopdf*](#id2b)
  * [Instalar *npm*](#id2c)
  * [Instalar *pip*](#id2d)
  * [Instalar el paquete *pillow*](#id2e)
  * [Instalar *git*](#id2f)
* [Instalar Postgres](#id3)
* [Crear usuarios Odoo](#id4)
  * [En la base de datos](#id4a)
  * [En el sistema](#id4b)
* [Instalar Odoo](#id5)
  * [Descargar el repositorio de Odoo](#id5a)
  * [Instalar requisitos de python](#id5b)
  * [Crear el archivo de configuración](#id5c)
  * [Configurar Odoo para que arranque al inicio](#id5d)
  * [Iniciar Odoo](#id5e)
* [Configurar Odoo](#id6)
  * [Cambiar codificación de la base de datos](#id6a)
  * [Instalar internacialización de Odoo al castellano](#id6b)
  * [Instalar el módulo de topónimos](#id6c)
  * [Instalar módulos extra](#id6d)
  * [Instalar modulos desde Odoo](#id6e)
* [Configurar servidor de correo smtp](#id7)
* [Configurar copias de seguridad](#id8)
  * [Desde Odoo](#id8a)
  * [Desde el servidor manuales](#id8b1)
  * [Desde el servidor automáticas](#id8b2)
* [Configurar master password](#id9)



***

# CONTENIDO

## CONFIGURAR ACCESO REMOTO A UBUNTU SERVER<a name="id1"/>

  Por seguridad no se puede acceder por ssh al usuario root, por lo que necesitamos cambiar el archivo de configuración de ssh desde proxmox:

  `$ sudo nano /etc/ssh/sshd_config`

  Dejando la siguiente linea de esta forma:

  `PermitRootLogin yes`

  Reiniciando después el servicio para que aplique los cambios:

  `$ sudo service sshd restart`

  Conectamos desde fuera de proxmox (por terminal o putty) a la ip de la maquina con:

  `$ ssh root@192.168.3.58`

[**INDICE**](#indice)

## PREPARAR INSTALACIÓN ODOO<a name="id2"/>

### 1. Instalar las dependencias<a name="id2a"/>

Conectar mediante ssh:

  `$ ssh root@192.168.3.58`

  Conectamos con root para tener todos los permisos, y no tener que otorgarnos permisos temporales escribiendo sudo delante de cada comando.


Actualizar la lista de paquetes disponibles:

  `$ apt-get update`

Instalar las depencias que vamos a necesitar para instalar Odoo:

  `$ apt-get -yq install adduser postgresql-client python-dateutil python-docutils python-feedparser python-jinja2 python-ldap python-libxslt1 python-lxml python-mako python-mock python-openid python-psycopg2 python-psutil python-pybabel python-pychart python-pydot python-pyparsing python-reportlab python-simplejson python-tz python-unittest2 python-vatnumber python-vobject python-webdav python-werkzeug python-xlwt python-yaml python-zsi poppler-utils python-pip python-pypdf python-passlib python-decorator gcc python-dev libxml2-dev libxslt-dev libsasl2-dev libldap2-dev libssl-dev libpq-dev libjpeg-dev libjpeg8-dev python-setuptools python-markupsafe python-reportlab-accel python-zsi python-yaml python-argparse python-openssl python-egenix-mxdatetime python-usb python-serial lptools make python-pydot python-psutil python-paramiko poppler-utils python-pdftools antiword python-requests python-xlsxwriter python-suds python-software-properties`

![Captura de pantalla 1][img1]

[**INDICE**](#indice)

### 2. Instalar el paquete *wkhtmltopdf*<a name="id2b"/>

Para realizar informes en pdf desde Odoo.

  * Descargar:

  `$ wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.1/wkhtmltox-0.12.1_linux-trusty-amd64.deb`

  ![Captura de pantalla 2][img2]

  * Desempaquetar indicando que instale el paquete:

  `$ dpkg -i wkhtmltox-0.12.1_linux-trusty-amd64.deb`

  * Si hay problemas de dependencias las instalamos y volvemos a intentar la instalacion:

  `$ apt-get install fontconfig libjpeg-turbo8`

  `$ dpkg -i wkhtmltox-0.12.1_linux-trusty-amd64.deb`

  ![Captura de pantalla 3][img3]

[**INDICE**](#indice)

### 3. Instalar *npm*<a name="id2c"/>

Para que funcione correctamente el servidor web.

  * Instalar:

  `$ apt-get -yq install npm`

  ![Captura de pantalla 4][img4]

  * Crear el enlace:

  `$ ln -s /usr/bin/nodejs /usr/bin/node`

  * Con npm intalar less:

  `$ npm install -g less less-plugin-clean-css`

  ![Captura de pantalla 5][img5]

[**INDICE**](#indice)

### 4. Instalar *pip*<a name="id2d"/>

  `$ apt-get install python3-pip python-pip`

  ![Captura de pantalla 6][img6]
  
[**INDICE**](#indice)

### 5. Instalar el paquete *pillow*<a name="id2e"/>

Para no tener problemas con el procesamiento de imágenes al instalar datos demo instalamos este paquete de python:

  `$ pip install --no-cache-dir -I pillow`

  ![Captura de pantalla 7][img7]


  En mi caso propone actualizar pip con:

  `$ pip install --upgrade pip`

  ![Captura de pantalla 8][img8]

[**INDICE**](#indice)

### 6. Instalar *git*<a name="id2f"/>

  `$ sudo apt-get install git`

~~~
 INSTANTÁNEA INSTALACIÓN_ODOO_MANUAL
~~~

[**INDICE**](#indice)

## INSTALAR POSTGRES<a name="id3"/>

  `$ apt-get install postgresql`

  ![Captura de pantalla 9][img9]


  ![Captura de pantalla 10][img10]

  Dar contraseña al usuario postgres que se ha creado durante la instalación:

  `$ passwd postgres`

  ![Captura de pantalla 11][img11]

[**INDICE**](#indice)

## CREAR USUARIOS ODOO<a name="id4"/>

### 1. Crear usuario odoo en la base de datos postgres<a name="id4a"/>

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

[**INDICE**](#indice)

### 2. Crear usuario odoo en el sistema<a name="id4b"/>

  `$ su root`

  `$ sudo adduser odoo`

  ![Captura de pantalla 13][img13]

[**INDICE**](#indice)

## INSTALAR ODOO<a name="id5"/>

### 1. Descargar el repositorio de Odoo<a name="id5a"/>

  `$ su odoo`

  `cd ~`

  `$ git clone https://github.com/Odoo/odoo.git --depth 1 --branch 10.0 --single-branch odoo`

~~~
¡OJO! Se indica la rama 10 y se tendrá que clonar SIEMPRE esta rama, si no descarga la ultima por defecto.
~~~

  ![Captura de pantalla 14][img14]

[**INDICE**](#indice)

### 2. Instalar requisitos de python<a name="id5b"/>

  `$ su root`

  `$ pip install -r /home/odoo/odoo/requirements.txt`

  ![Captura de pantalla 15][img15]


~~~
INSTANTÁNEA PRE-CONFIGURACION
~~~

[**INDICE**](#indice)

### 3. Crear el archivo de configuración<a name="id5c"/>

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

[**INDICE**](#indice)

### 4. Configurar Odoo para que arranque al inicio<a name="id5d"/>

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

[**INDICE**](#indice)

### 5. Iniciar Odoo<a name="id5e"/>

Reiniciando la máquina el servicio se inicia solo, puedo cerrar el terminal y trabajar desde el navegador en la direccion de mi Odoo:

    http://192.168.3.58:8069

Si quisieramos simplemente iniciar Odoo como proceso y no como servicio ejecutamos el comando:

  `$ /home/odoo/odoo/odoo-bin -c /home/odoo/odoo-server.conf`

[**INDICE**](#indice)

## CONFIGURAR ODOO<a name="id6"/>

### 1. Cambiar codificación de la base de datos<a name="id6a"/>

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
 
 [**INDICE**](#indice)

### 2. Crear base de datos con datos de prueba

En psql comprobamos las bases de datos que existen:

  `\l`

  ![Captura 20][img20]

~~~
\c bbdd Cambiar a la base de datos
\dt     Listar las tablas de la base de datos
~~~

[**INDICE**](#indice)

### 3. Instalar internacialización de Odoo al castellano<a name="id6b"/>

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

  En la pagina de Odoo enteramos en configuración y las encontramos en la esquina inferior derecha.

  * Actualizar lista de aplicaciones:

  Al ir a la pestaña aplicaciones deberia aparecer el la barra lateral izquierda la opción Actualizar lista de aplicaciones.

[**INDICE**](#indice)

### 4. Instalar el módulo de topónimos<a name="id6c"/>

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

  * Instalar el módulo en Odoo:

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

[**INDICE**](#indice)

### 5. Instalar módulos extra<a name="id6d"/>

#### Jasper Reports

Sirve para la generación de informes en distintos formatos.
Disponible en el siguiente enlace:

`git clone -b 10.0 https://github.com/JayVora-SerpentCS/Jasperreports_odoo.git`

#### Web Export View

Para exportar a un fichero Excel cualquier listado de la aplicación con las 
mismas columnas que estamos viendo en pantalla.
Disponible en el siguiente enlace:

`git clone -b 10.0 https://github.com/OCA/web.git`

#### Datetime Formatter

Sirve para facilitar el formateo de fechas.
Disponible en el modulo Server Tools (dependencia del modulo de toponimos).

#### Base FontAwesome

Ofrece diferentes tipos de letras para utilizarlos en Odoo.
Disponible en el modulo Server Tools (dependencia del modulo de toponimos).

[**INDICE**](#indice)

### 6. Instalar modulos desde Odoo<a name="id6e"/>

Desde Odoo es extremadamente sencillo instalar modulos que ya se encuentran en la carpeta addons. 
Solo tenemos que actualizar la lista de aplicaciones y buscar el modulo deseado en la pestaña Aplicaciones. 

Realizo la instalación de los módulos requeridos de Compras, Ventas, Inventario y TPV. 
Además instalo Contabilidad/Facturación, CRM, y RRHH entre otros.

[**INDICE**](#indice)

## CONFIGURACIÓN SERVIDOR DE CORREO SMTP<a name="id7"/>

### 1. Configurar servidor de correo saliente

  * Desde el cliente web de Odoo entramos en:

  Configuración  ->  Opciones Generales  ->  Correo electronico  ->  Configurar servidores de correo saliente

  * Creamos un servidor nuevo:

~~~
Prioridad:      Máxima 1 (enviaría el correo desde este servidor)
Servidor        smtp (si es gmail es smtp.gmail.com)
Puerto:         465
Seguridad:      SSL/TLS
Nombre usuario: El de la cuenta de correo
Contraseña:     La de la cuenta de correo
~~~


### 2. Configurar cuenta de correos

Cambiar las preferencias para permitir envío de correos desde aplicaciones inseguras.

### 3. Realizar pruebas

Se pueden enviar correos desde muchas de las aplicaciones de Odoo, elegir una y mandar un correo a una cuenta donde podamos comprobar si llega correctamente.

### 4. Instalación del módulo para campañas de correo masivo

  (OPCIONAL)

[**INDICE**](#indice)

## CONFIGURACIÓN DE COPIAS DE SEGURIDAD<a name="id8"/>

### DESDE ODOO<a name="id8a"/>

Desde la pagina principal de Odoo (antes de entrar) pinchamos en la opción Manage databases:

  * Backup:   Realizar una copia de la base de datos

    ![Captura 21][img21]<a name="backup"/>

  * Restore:  Restaurar desde una copia guardada de la base de datos

    ![Captura 22][img22]<a name="restore"/>
    
[**INDICE**](#indice)

### MANUALES DESDE EL SERVIDOR<a name="id8b1"/>

#### COPIA

1. Nos conectamos con el usuario odoo y vamos a la carpeta donde queramos guardar la copia:

  `$ su odoo`

  `$ cd ~`

2. Volcar la base de datos con el comando pg_dump (de postgres) y con > redireccionar la salida hacia el archivo indicado:

  `$ pg_dump -Fc test > test.sql`

   ![Captura 23][img23]

3. Generar el nombre del fichero con la fecha mediante el comando date:

  Primero probamos a formatear la salida para comprobar que da el resultado esperado:

  `$ date +"%m-%d-%Y_%H-%M"`

  Concatenamos con el nombre de la copia de la base de datos:

  `pg_dump -Fc test > $(date +"%m-%d-%Y_%H-%M_")test.sql`

  ~~~
  Con $(...) conseguimos que evalue primero la expresión interna y luego utiliza el resultado para evaluar el resto de la expresión.
  ~~~

   ![Captura 24][img24]
    
[**INDICE**](#indice)

#### BORRADO

  * Borrar base de datos desde la pagina de Odoo:

    ![Captura 25][img25]

    ![Captura 26][img26]
    
[**INDICE**](#indice)

#### RESTAURACIÓN

1. Reiniciar la máquina y parar Odoo:

  `$ su root`

  `$ ps aux | grep odoo`

  `$ kill -9 pid_proceso`

  ó

  `$ sudo systemctl stop odoo10.service`

   ![Captura 27][img27]

2. Crear la base de datos vacia:

  `$ su odoo`

  `$ createdb test`

3. Restaurar la copia guardada:

  `$ pg_restore -d test 11-15-2018_08-43_test.sql`

~~~
No pide password porque estamos trabajando con el usuario odoo
en el sistema y tambien hay un usuario odoo equivalente en postgres.
~~~

   ![Captura 28][img28]

4. Iniciar el servicio de Odoo de nuevo:

  `$ sudo systemctl start odoo10.service`

5. Comprobar en Odoo que la base de datos ha sido restaurada correctamente revisando la informacion (productos, pedidos, clientes... )

[**INDICE**](#indice)

### AUTOMÁTICAS DESDE EL SERVIDOR<a name="id8b2"/>

1. Guardamos el comando de copia en un script:

  `$ nano copia.sh`

   ![Captura 29][img29]

2. Le damos permiso de ejecución:

  `$ chmod +x copia.sh`

3. Planificamos la tarea en el crontab:

~~~
Cron ejecuta tareas programadas. Cada usuario tiene
un archivo de cron (crontab) y se ejecuta con ese usuario con
sus permisos en las fechas que indiquemos.
~~~

  * Comprobar si el usuario odoo tiene crontab:

  `$ crontab -l`

  * Editar el archivo:

  `$ crontab -e`

  * Añadir la tarea:

  `55 10 * * * /home/odoo/copia.sh`

  ~~~
  Los primeros parametros indican los minutos, horas, dia del mes,
  mes y dia de la semana. En este caso estoy indicando que se realice
  la copia todos los dias a las 10:55.

  ¡OJO! Si indicamos una ruta debe ser relativa.
  ~~~

   ![Captura 30][img30]

   Compruebo que realize la copia correctamente:

  ![Captura 31][img31]

4. Creo un directorio para guardar las copias:

  `$ mkdir backups`

  Cambio el script para que la guarde ahi:

   ![Captura 32][img32]

5. Creo un script para borrar las más antiguas:

  Con el comando find encuentra archivos que cumplan las condiciones que pasamos como parametros:

  `$ find /home/odoo/backups -mtime +10 -type f -delete`

  En este caso le indico que en la carpeta backups localice los archivos de antigüedad superior a 10 dias y los borre.

  Lo guardo:

  `$ nano borrado_copias.sh`

  Le doy permiso de ejecución:

  `$ chmod +x borrado_copias.sh`

  Lo añado al crontab.

   ![Captura 33][img33]

  Compruebo que funcione correctamente:

  Cambio la frecuencia de las copias de seguridad para que realice suficientes en unos minutos:

  ![Captura 34][img34]

  Una vez terminada la comprobación establezco la hora de backup (00:00 de cada dia) y pongo la hora de borrado 5 minutos despues.

   ![Captura 35][img35]

[**INDICE**](#indice)

## CONFIGURACIÓN DE LA MASTER PASSWORD<a name="id9"/>

Se puede asignar una master password desde la web de Odoo (la pagina de entrada) o desde el servidor, modificando el archivo de configuracion odoo-server.conf. 

La master password servirá para pedir confirmación de que se tienen los permisos adecuados para realizar determinados trámites. Por ejemplo [borrar](#backup) o [restaurar](#restore) la base de datos.



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
[img21]: ./CAPTURAS/CAPTURA_21.png
[img22]: ./CAPTURAS/CAPTURA_22.png
[img23]: ./CAPTURAS/CAPTURA_23.png
[img24]: ./CAPTURAS/CAPTURA_24.png
[img25]: ./CAPTURAS/CAPTURA_25.png
[img26]: ./CAPTURAS/CAPTURA_26.png
[img27]: ./CAPTURAS/CAPTURA_27.png
[img28]: ./CAPTURAS/CAPTURA_28.png
[img29]: ./CAPTURAS/CAPTURA_29.png
[img30]: ./CAPTURAS/CAPTURA_30.png
[img31]: ./CAPTURAS/CAPTURA_31.png
[img32]: ./CAPTURAS/CAPTURA_32.png
[img33]: ./CAPTURAS/CAPTURA_33.png
[img34]: ./CAPTURAS/CAPTURA_34.png
[img35]: ./CAPTURAS/CAPTURA_35.png
[img36]: ./CAPTURAS/CAPTURA_36.png
