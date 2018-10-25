		
### CONFIGURAR LA RED DEL SERVIDOR (MAQUINA VIRTUAL)

* En la maquina virtual cambiamos red NAT por Adaptador puente para poder tener IP propia y permitir las conexiones entrantes.

1º Consultar informacion de red del servidor: 

	$ sudo ifconfig:

2º Cambiar el archvo de configuracion:

	$ sudo nano /etc/network/interfaces

	* Aparece:
	
		auto enpos3
		iface enpos3 inet dhcp
		
	* Cambiar a:
	
		auto enpos3
		iface enpos3 inet static
		address 192.168.3.110 (mi ip es la 110)
		network 255.255.255.0
		gateway 192.168.3.1
		dns-nameservers 8.8.8.8

	* Cuando acabamos pulsamos control+X para guardar cambios

3º Hacemos flush a la ip actual:

	$ sudo ip addr flush enp0s3

4º Reiniciamos el servicio de red:

	$ sudo service networking restart

5º Comprobamos que tengamos asignada la nueva ip estatica con ipconfig	

* En el paso 3 podemos directamente reiniciar la maquina con:

	$ sudo reboot
	
	----------------------------------------------------------------------------------
	
### INSTALAR PAQUETE SSH

1º Actualizar e instalar paquete 

	$ sudo apt-get update
	$ sudo apt-get install openssh-server

	-----------------------------------------------------------------------------------
	
### COMPROBAR SSH

1º Comprobamos los procesos que se estan ejecutando 

	$ ps aux (salen todos)
	$ ps aux | grep ssh (filtramos lineas que incluyen 'ssh')

	* Si aparece /usr/sbin/sshd es que el proceso esta activo

	------------------------------------------------------------------------------------
	
### CONECTAR AL SERVIDOR

1º Desde cualquier ordenador (localhost si el server esta en una VM):

	$ ssh usuario@ip
	$ ssh silvia@192.168.3.110

	* Puedo conectarme desde la terminal de mi ordenador a la maquina virtual y comprobar que estoy en ella con ifconfig. 
	
	Para salir:
	
	$ exit

2º SSH trabaja en el puerto 22, tanto el cliente como el servidor lo tienen que tener instalado (linux lo tiene por defecto, para windows instalar putty)
		

	* Para ejecutar software desde el servidor y que aparezca la interfaz gráfica en local abrimos la sesion ssh con:

	$ ssh -x usuario@ip

	----------------------------------------------------------------------------------
	
### COPIAR DESDE SERVIDOR

* De servidor a ubicacion local (o donde quieras)

	$ scp [ip servidor]:[ruta origen] [ruta destino]
	$ scp 192.168.3.29:~/ubuntu.iso .

	(Desde un ordenador que tiene el mismo usuario y contraseña que la sesion del servidor)


* Para conectarse con un usuario distinto (poner usuario del servidor)

	$ usuarioServidor@192.168.3.28:/ubuntu.iso .

	----------------------------------------------------------------------------------
	
### CREAR USUARIO EN EL SERVIDOR

1º Comando:

	$ sudo adduser alumno

2º Conecta mediante ssh al servidor con el usuario alumno:

	$ ssh alumno@192.168.3.110

	----------------------------------------------------------------------------------
	
### HACER INSTANTANEA DE LA MAQUINA

1º Desde VirtualBox hacemos una instantanea para guardar el estado de la maquina y
poder utilizarla en caso de emergencia dandole a recuperar


