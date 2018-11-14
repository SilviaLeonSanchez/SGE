# UNIDAD 2

## CONFIGURACIÓN UBUNTU SERVER

### HABILITAR ACCESO REMOTO

  Por seguridad no se puede acceder por ssh al usuario root, por lo que necesitamos cambiar el archivo de configuración de ssh desde proxmox:

  `$ sudo nano /etc/ssh/sshd_config`

  Dejando la siguiente linea de esta forma:

  `PermitRootLogin yes`

  Reiniciando después el servicio para que aplique los cambios:

  `$ sudo service sshd restart`

  Conectamos desde fuera de proxmox (por terminal o putty) a la ip de la maquina con:

  `$ ssh root@192.168.3.58`

---

### INSTALACION DE ODOO

1. Conectamos con la máquina mediante ssh:  

  `$ ssh root@192.168.3.58`

  Conectamos con root para tener todos los permisos, y no tener que otorgarnos permisos temporales escribiendo sudo delante de cada comando.


2. Actualizamos la lista de paquetes disponibles:

  `$ apt-get update`


3. Instalamos las depencias que vamos a necesitar para instalar Odoo con:

  `$ apt-get -yq install adduser postgresql-client python-dateutil python-docutils python-feedparser python-jinja2 python-ldap python-libxslt1 python-lxml python-mako python-mock python-openid python-psycopg2 python-psutil python-pybabel python-pychart python-pydot python-pyparsing python-reportlab python-simplejson python-tz python-unittest2 python-vatnumber python-vobject python-webdav python-werkzeug python-xlwt python-yaml python-zsi poppler-utils python-pip python-pypdf python-passlib python-decorator gcc python-dev libxml2-dev libxslt-dev libsasl2-dev libldap2-dev libssl-dev libpq-dev libjpeg-dev libjpeg8-dev python-setuptools python-markupsafe python-reportlab-accel python-zsi python-yaml python-argparse python-openssl python-egenix-mxdatetime python-usb python-serial lptools make python-pydot python-psutil python-paramiko poppler-utils python-pdftools antiword python-requests python-xlsxwriter python-suds python-software-properties`

![Captura de pantalla 1][img1]


4. Instalamos el siguiente paquete para realizar informes en pdf desde Odoo con:

  * Descargamos:

  `$ wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.1/wkhtmltox-0.12.1_linux-trusty-amd64.deb`

  ![Captura de pantalla 2][img2]

  * Desempaquetamos e indicamos que instale el paquete:

  `$ dpkg -i wkhtmltox-0.12.1_linux-trusty-amd64.deb`

  * Si hay problemas de dependencias las instalamos y volvemos a intentar la instalacion:

  `$ apt-get install fontconfig libjpeg-turbo8`

  `$ dpkg -i wkhtmltox-0.12.1_linux-trusty-amd64.deb`

  ![Captura de pantalla 3][img3]

5. Instalar npm para que funcione correctamente el servidor web:

  `$ apt-get -yq install npm`

  ![Captura de pantalla 4][img4]

  Creamos el enlace:

  `$ ln -s /usr/bin/nodejs /usr/bin/node`

  Desde npm intalamos less:

  `$ npm install -g less less-plugin-clean-css`

  ![Captura de pantalla 5][img5]

6. Instalamos pip:

  `$ apt-get install python3-pip python-pip`

  ![Captura de pantalla 6][img6]

7. Instalamos el paquete python de Pillow para no tener problemas con el procesamiento de imágenes al instalar datos demo:

  `$ pip install --no-cache-dir -I pillow`

  ![Captura de pantalla 7][img7]

  En mi caso propone actualizar pip con:

  `$ pip install --upgrade pip`

  ![Captura de pantalla 8][img8]
























[img1]: https://github.com/SilviaLeonSanchez/SGE/blob/master/Ud_2/Actividades_para_entregar/CAPTURAS/CAPTURA_1.png

[img2]: https://github.com/SilviaLeonSanchez/SGE/blob/master/Ud_2/Actividades_para_entregar/CAPTURAS/CAPTURA_2.png

[img3]: https://github.com/SilviaLeonSanchez/SGE/blob/master/Ud_2/Actividades_para_entregar/CAPTURAS/CAPTURA_3.png

[img4]: https://github.com/SilviaLeonSanchez/SGE/blob/master/Ud_2/Actividades_para_entregar/CAPTURAS/CAPTURA_4.png

[img5]: https://github.com/SilviaLeonSanchez/SGE/blob/master/Ud_2/Actividades_para_entregar/CAPTURAS/CAPTURA_5.png

[img5]: https://github.com/SilviaLeonSanchez/SGE/blob/master/Ud_2/Actividades_para_entregar/CAPTURAS/CAPTURA_5.png

[img6]: https://github.com/SilviaLeonSanchez/SGE/blob/master/Ud_2/Actividades_para_entregar/CAPTURAS/CAPTURA_6.png

[img7]: https://github.com/SilviaLeonSanchez/SGE/blob/master/Ud_2/Actividades_para_entregar/CAPTURAS/CAPTURA_7.png

[img8]: https://github.com/SilviaLeonSanchez/SGE/blob/master/Ud_2/Actividades_para_entregar/CAPTURAS/CAPTURA_8.png

[img9]: https://github.com/SilviaLeonSanchez/SGE/blob/master/Ud_2/Actividades_para_entregar/CAPTURAS/CAPTURA_9.png

[img10]: https://github.com/SilviaLeonSanchez/SGE/blob/master/Ud_2/Actividades_para_entregar/CAPTURAS/CAPTURA_10.png

[img11]: https://github.com/SilviaLeonSanchez/SGE/blob/master/Ud_2/Actividades_para_entregar/CAPTURAS/CAPTURA_11.png

[img12]: https://github.com/SilviaLeonSanchez/SGE/blob/master/Ud_2/Actividades_para_entregar/CAPTURAS/CAPTURA_12.png

[img13]: https://github.com/SilviaLeonSanchez/SGE/blob/master/Ud_2/Actividades_para_entregar/CAPTURAS/CAPTURA_13.png

[img14]: https://github.com/SilviaLeonSanchez/SGE/blob/master/Ud_2/Actividades_para_entregar/CAPTURAS/CAPTURA_14.png

[img15]: https://github.com/SilviaLeonSanchez/SGE/blob/master/Ud_2/Actividades_para_entregar/CAPTURAS/CAPTURA_15.png

[img16]: https://github.com/SilviaLeonSanchez/SGE/blob/master/Ud_2/Actividades_para_entregar/CAPTURAS/CAPTURA_16.png

[img17]: https://github.com/SilviaLeonSanchez/SGE/blob/master/Ud_2/Actividades_para_entregar/CAPTURAS/CAPTURA_17.png

[img18]: https://github.com/SilviaLeonSanchez/SGE/blob/master/Ud_2/Actividades_para_entregar/CAPTURAS/CAPTURA_18.png

[img19]: https://github.com/SilviaLeonSanchez/SGE/blob/master/Ud_2/Actividades_para_entregar/CAPTURAS/CAPTURA_19.png

[img20]: https://github.com/SilviaLeonSanchez/SGE/blob/master/Ud_2/Actividades_para_entregar/CAPTURAS/CAPTURA_20.png

[img21]: https://github.com/SilviaLeonSanchez/SGE/blob/master/Ud_2/Actividades_para_entregar/CAPTURAS/CAPTURA_21.png
