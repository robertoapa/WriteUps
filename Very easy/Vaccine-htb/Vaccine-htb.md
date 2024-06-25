![[Pasted image 20240524141429.png]]
Task1: ftp

Task2: anonymous

Task3: backup.zip
Entrando al servicio ftp con el usuario anonymous vemos el archivo bakcup.zip
![[Pasted image 20240524142603.png]]

Task4: zip2john

Task5: qwerty789
el usuario del admin se encuentra en el archivo php del zip, el cual se extrae usando zip2john y john para obtener al contraseña y descomprimir el archivo
![[Pasted image 20240524142836.png]]
Abriendo el archivo se encuentra la contraseña con cifrado md5.
![[Pasted image 20240524142951.png]]
Task6: --os-shell
utilizando el parámetro  --os-shell podemos ejecutar comandos obteniendo una reverse shell.
![[Pasted image 20240524145414.png]]

User flag: ec9b13ca4d6229cd5cc1e09980965bf7
![[Pasted image 20240524145915.png]]


Root flag: dd6e058e814260bc70e9bbdef2715849
![[Pasted image 20240524150352.png]]

![[Pasted image 20240524150950.png]]
vemos que podemos ejecutar como root el binario /bin/vi en un archivo
ejecutamos:
```
:set shell=/bin/sh
:shell
```

![[Pasted image 20240524151140.png]]


![[Pasted image 20240524151225.png]]