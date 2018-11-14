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

  #### 1. Conectamos con la máquina mediante ssh:  

  `$ ssh root@192.168.3.58`

    Conectamos con root para tener todos los permisos,
    y no tener que otorgarnos permisos temporales
    escribiendo sudo delante de cada comando.


![Captura de pantalla 1](https://github.com/SilviaLeonSanchez/SGE/blob/master/Ud_2/Actividades_para_entregar/CAPTURAS/CAPTURA_1.png)
