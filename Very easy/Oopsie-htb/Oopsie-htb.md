**Task1: Proxy**

**Task2: /cdn-cgi/login**
Utilizando ctrl+u se puede encontrar en la ruta del login
![[Pasted image 20240523000936.png]]

**Task3: cookie**

**Task4: 34322**
Cambiando el id del usuario por 1 obtenemos acceso al usuario admin
![[Pasted image 20240523001429.png]]
![[Pasted image 20240523001444.png]]
**Task5: /uploads**

**Task6: db.php**
Para subir archivos se debe tener permisos de admin, sabiendo el id de admin cambiamos las cookies en inspeccionar>Storage>cookies y añadimos el valor de admin en el usuario 

![[Pasted image 20240523003626.png]]

![[Pasted image 20240523003641.png]]
Subimos un reverse-shell en php y lo buscamos en http://ip/reverse.php mientras escuchamos con netcat para obtener acceso a la maquina.

Para obtener una tty ejecutamos en el siguiente comando:

python3 -c ‘import pty; pty.spawn(“/bin/bash”)’

Encontramos el archivo que contiene la contraseña del usuario robert en la ruta "/var/www/html/cdn-cgi/login/db.php" 

![[Pasted image 20240523005238.png]]


**Task7: find**

**Task8:root**
Encuentro el binario bugtracker mediante el comando locate y con ls -l veo el propietario y permisos del archivo.

![[Pasted image 20240523010110.png]]


**Task9: set owner user id**

**Task10: cat** 

**User Flag: f2c74ee8db7983851ab2a96a44eb7981**

**root Flag: af13b0bee69f8a877c3faf667f7beacf**
Para escalar privilegios creamos un archivo llamado cat con el siguiente texto: "/bin/bash" y le damos privilegios de ejecucion con chmod.
luego ejecutamos:
export PATH=rutaArchivoCat:$PATH

y al ejecutar bugtracker obtendremos una bash con el usuario root.

			![[Pasted image 20240523014628.png]]
			
 por ultimo con less vemos el contenido del archivo /root/root.txt
			 ![[Pasted image 20240523014749.png]]


