
<img src="./Images/Pasted%20image%2020241025181417.png">

Compruebo si el servicio ftp permite acceso mediante el usuario anonymous.

<img src="./Images/Pasted%20image%2020241025181509.png">

Consigo acceder con el usuario anonymous y se puede encontrar el directorio con nombre "Users".
Dentro de este directorio encontramos dos directorios llamados Nadine y Nathan. En el directorio Nadine se encuentra un archivo llamado Confidential.txt por lo que lo descargamos con get.
El contenido del archivo es el siguiente:

<img src="./Images/Pasted%20image%2020241025181811.png">

En el directorio "Nathan" se encuentra un archivo llamado Notes to do.txt el cual contiene lo siguiente.

<img src="./Images/Pasted%20image%2020241025182005.png">


Accedo al puerto 80 para ver el servicio web que tiene.

<img src="./Images/Pasted%20image%2020241025182917.png">

Buscando información sobre NVMS-1000 encuentro que existe una vulnerabilidad para este servicio ( CVE-2019-20085). Esta vulnerabilidad se trata de un LFI.
Con la herramienta curl lanzo una petición para intentar obtener el archivo Passwords.txt que es nombrado en los archivos anteriores.

``` bash
 curl -X GET http://10.10.10.184/../../../../../../../../../../../../../../Users/Nathan/Desktop/Passwords.txt --path-as-is
```

Esto nos devuelve las siguientes contraseñas.

<img src="./Images/Pasted%20image%2020241025183947.png">

 
Utilizo hydra para intentar acceder por fuerza bruta con una de estas contraseñas con el usuario Nathan.
```
hydra -l Nathan -P passwords.txt ssh://10.10.10.184 
```

Probando con el usuario Nathan no accedemos con ninguna de las contraseñas, pero con el usuario Nadine si.

<img src="./Images/Pasted%20image%2020241025185045.png">

Ya podemos obtener la Flag del usuario en el directorio Desktop de Nadine.

## Escalada de privilegios.
Analizando los directorios encuentro que tiene instalado NSClient++ en el directorio Program Files.
Se puede encontrar la contraseña para acceder a este servicio en el archivo nsclient.ini

<img src="./Images/Pasted%20image%2020241025190622.png">

Para la versión que se utiliza en este caso existe una vulnerabilidad que nos permite ejecución de código como administrador.
Con el siguiente comando hago un túnel con ssh para acceder al servicio desde nuestra máquina. 
`ssh -L 8443:localhost:8443 nadine@10.10.10.184`

Descargamos nc.exe en la máquina víctima y un arhivo pwn.bat que ejecutará la reverse-shell.

En NSClient creamos un nuevo script con los siguientes parámetros.

<img src="./Images/Pasted%20image%2020241025194241.png">

A continuación creamos una tarea para que ejecute el script.

<img src="./Images/Pasted%20image%2020241025194727.png">


A continuación en el apartado "Control" le damos en Reload y esperamos a la reverse-shell.

<img src="./Images/Pasted%20image%2020241025210544.png">


