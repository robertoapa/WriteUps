Resultado de nmap.
<img src="./Images/Pasted%20image%2020241014182101.png">

Buscando información, se puede ver que la versión de nostromo (1.9.6) es vulnerable a un ataque de RCE - CVE-2019-16278.
Usare el siguiente exploit para explotar esta vulnerabilidad.
<img src="./Images/Pasted%20image%2020241014183227.png">
<img src="./Images/Pasted%20image%2020241014184031.png">
 Ejecuto una reverse shell para acceder al sistema.
<img src="./Images/Pasted%20image%2020241014184239.png">

Se accede al usuario www-data.
<img src="./Images/Pasted%20image%2020241014184426.png">

En el archivo /etc/passwd encontramos el usuario david.

Encontramos que en el directorio del usuario david existe un directorio publico donde se encuentra la clave SSH del usuario.

<img src="./Images/Pasted%20image%2020241014185736.png">

Nos lo pasamos a nuestra máquina mediante nc y extraemos los archivos donde encontramos el id_rsa.
<img src="./Images/Pasted%20image%2020241014190154.png">

Con el archivo id_rsa se puede acceder mediante ssh al usuario david.
Al intentar acceder se necesita una contraseña por lo que con lo desciframos utilizando jhon.

Se extrae el hash
<img src="./Images/Pasted%20image%2020241014190757.png">

<img src="./Images/Pasted%20image%2020241014190940.png">

<img src="./Images/Pasted%20image%2020241014191006.png">

Ya se puede acceder por ssh al usuario david.
<img src="./Images/Pasted%20image%2020241014191105.png">


## Escalada de privilegios.
El siguiente archivo ejecuta un comando utilizando sudo.

<img src="./Images/Pasted%20image%2020241014192146.png">

Al ejecutar el comando podemos ejecutar una shell mediante el uso de !/bin/bash obteniendo una shell como root.
<img src="./Images/Pasted%20image%2020241014192343.png">
