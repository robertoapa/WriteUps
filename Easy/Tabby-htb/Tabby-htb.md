<img src="./Images/Pasted%20image%2020241015181200.png">

En el puerto 8080 se puede acceder al manager webapp pero se necesitan credenciales para acceder.

<img src="./Images/Pasted%20image%2020241015184019.png">

Analizando la página, en el apartado news existe la vulnerabilidad LFI.

<img src="./Images/Pasted%20image%2020241015182226.png">

Listando el archivo de configuración /usr/share/tomcat9/etc/tomcat-users.xml se obtienen las credenciales de tomcat.

<img src="./Images/Pasted%20image%2020241015184150.png">

Buscando directorios en manager se puede ver el directorio text

<img src="./Images/Pasted%20image%2020241015184811.png">

Con el comando deploy se puede ejecutar un archivo .war de forma de remota.


Creo el payload con msfvenom

 <img src="./Images/Pasted%20image%2020241015194518.png">

Ahora con curl se puede subir el archivo para posteriormente acceder a el y obtener la reverse shell

<img src="./Images/Pasted%20image%2020241015194700.png">

<img src="./Images/Pasted%20image%2020241015194725.png">


## Movimiento lateral
en la ruta /var/www/html/files encontramos un archivo zip de backup por lo que con netcat nos lo pasamos a nuestra máquina para analizarlo.

El archivo nos pide una contraseña.

<img src="./Images/Pasted%20image%2020241015195538.png">

Se puede utilizar john para descifrar la contraseña.
1. Obtener el hash -> zip2john bakcup.zip > hash.txt
2. john --wordlist=rockyou hash.txt
3. Una vez descifrada se puede ver la contraseña -> john --show hash.txt

La contraseña del zip es: admin@it

Intento acceder al usuario ash con la contraseña encontrada accediendo satisfactoriamente al usuario.

<img src="./Images/Pasted%20image%2020241015200706.png">

El usuario pertenece al grupo lxd el cual nos puede permitir escalar privilegios como root.

Con searchsploit encontramos un exploit que nos permite elevar privilegios. Los pasos que hay que seguir son solos siguientes:

<img src="./Images/Pasted%20image%2020241015204400.png">

Una vez hecho esto ya seremos usuario root.

<img src="./Images/Pasted%20image%2020241015204439.png">
