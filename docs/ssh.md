-Instalacion servicio ssh-

Un servicio de importancia en los servidores, es el servicio ssh, llamado secure shell, es una shell remota por la cual el usuario que tiene cierto usuario y al que se le ha compartido la contraseña puede acceder al servidor desde su propio equipo

En esta practica se haran pruebas tanto de instalacion y configuracion en el servidor para despues crear usuarios, grupos y permisos

-Descarga ssh-

Usando el comando sudo apt install ssh se descargara el paquete ssh, esto bien pudo haberse hecho en la instalacion del S.O. con la opcion install SSH, pero para entender de mejor manera los comandos de ubuntu server y de linux en general se descargara manualmente

![descarga ssh](https://github.com/JOGU-HP/ubuntu-server-lab/blob/ccabedf638c93a006a09ff26330403e4b42fb15a/images/sshinstall/descarga%20ssh.png)

Una vez descargado el paquete, se verificara su status con sudo systemctl status ssh

![status ssh](https://github.com/JOGU-HP/ubuntu-server-lab/blob/ccabedf638c93a006a09ff26330403e4b42fb15a/images/sshinstall/status%20ssh.png)

Se observa una opcion en loaded que dice disabled, significa que el servicio no arranca automaticamente al iniciar el servidor y es una mala practica dejarlo en ese estado, con sudo systemctl enable ssh se corrige este error que, aunque no es grave no es practico dejarlo asi y habilitarlo cumple con la triada CIA (Confidencialidad, Integridad y Disponibilidad)

-sudo systemctl enable ssh (habilita el inicio automatico)

-sudo systemctl restart ssh (reinicia el servicio)

-sudo systemctl status ssh (debe mostrar la opcion de loaded en enabled)

![enable ssh](https://github.com/JOGU-HP/ubuntu-server-lab/blob/ccabedf638c93a006a09ff26330403e4b42fb15a/images/sshinstall/enable%20ssh.png)


Ahora que el servicio ssh esta ejecutandose de manera correcta es momento de preparar la maquina cliente que se conectara via remota al servidor

Para Ubuntu o cualquier distribucion de linux basada en Debian, instalar ssh es sencillo y basta con escribir el comando sudo apt install ssh

![ssh en ubuntu](https://github.com/JOGU-HP/ubuntu-server-lab/blob/ccabedf638c93a006a09ff26330403e4b42fb15a/images/sshinstall/ssh%20en%20ubuntu.png)

Para el caso de windows es diferente el proceso 

Se debe ingresar a Configuracion

-Sistema

-Caracteristicas Opcionales

-Agregar una caracteristica

-Buscar OpenSSH

-Instalar y Reiniciar el equipo

![SSH windows](https://github.com/JOGU-HP/ubuntu-server-lab/blob/ccabedf638c93a006a09ff26330403e4b42fb15a/images/sshinstall/ssh%20windows.png)

Se puede comprobar la instalacion de ssh con el simbolo de sistema escribiendo ssh y si la instalacion fue correcta se podran ver ciertos parametros para ssh

![Verificacion ssh windows](https://github.com/JOGU-HP/ubuntu-server-lab/blob/ccabedf638c93a006a09ff26330403e4b42fb15a/images/sshinstall/verificacion%20ssh%20windows.png)

Con estos pasos, la descarga de cliente ssh para diferentes S.O's esta completada
