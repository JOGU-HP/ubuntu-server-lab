Reforzamiento de ssh por generacion de llaves

Objetivo
-Generar llaves ssh para reforzar la seguridad de login en el servior

-Aprender a generar llaves ssh

-Realizar configuraciones optimas para estas llaves

-Aprender los pasos necesarios para la generacion de llaves

*Primeros pasos

La generacion de llaves ssh es una medida de seguridad muy empleada en servidores, consiste en generar un "candado" y "llave" que se puede traducir como llave privada y publica, con la finalidad de realizar conexiones sin la necesidad de usar una contraseña, la llave publica se envia al servidor mientras que la privada se mantiene en la maquina que se va a logear

Para generar estas llaves, primero me centre en entender que son las llaves ssh y como funcionan a nivel servidor y cliente, con las bases ya establecidas, procedo a buscar informacion sobre como generar las llaves y los pasos necesarios, con la finalidad de comprender que se debe hacer por parte del cliente y por parte del servidor

*Generacion de las llaves

Para generar las llaves ssh, primero se debe ubicar la maquina que realizara la conexion via ssh

Se accede al cmd y se escribe el comando ssh-keygen

Se acepta la ruta donde se van a guardar las llaves a lo que tambien pedira una frase o contraseña adicional para mayor seguridad (por ahora no se usara esta caracteristica)

Y mostrara la siguiente informacion con la que muestra que se ha generado exitosamente la llave
![keygen](https://github.com/JOGU-HP/ubuntu-server-lab/blob/3e1d7e20302169959913b5311a70a90ceba6f917/images/key_ssh/keygen.png)

Despues de generar la llave, se abre un editor de texto en este caso Visual Studio Code para poder visualizar la llave generada 

Para poder encontrar la llave generada, se accede a:

Disco C-> User-> Usuario donde se genero la llave->carpeta .ssh

En esta carpeta se veran archivos pero los importantes son los archivos id
![location](https://github.com/JOGU-HP/ubuntu-server-lab/blob/3e1d7e20302169959913b5311a70a90ceba6f917/images/key_ssh/ruta_keys.png)

**Implementacion de la llave

Primero, accedo a la llave publica y copio el contenido que tiene el archivo

Me contecto via ssh con el usuario conta1 y creo una carpeta en el directorio de la siguiente manera

mkdir ~/.shh

Doy permisos con chmod 700 a la carpeta recien creada

Con nano, creo un archivo con el comando nano ~/.ssh/authorized_keys y pego la llave que he generado

Guardo con Crtl+o, Enter, Crtl+x

Una vez guardada la llave, procedo a reasignar permisos con chmod 600

Ahora salgo de la conexion con exit y vuelvo a conectarme con 

ssh conta1@IP

Y en esta ocasion, no me pide contraseña sino que directamete puedo acceder al servidor

![nopass](https://github.com/JOGU-HP/ubuntu-server-lab/blob/3e1d7e20302169959913b5311a70a90ceba6f917/images/key_ssh/nopasswd.png)


