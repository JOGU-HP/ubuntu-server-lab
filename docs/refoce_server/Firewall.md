Un firewall es una medida de seguridad de suma importancia, puesto que monitorea, controla y filtra el trafico que hay en una red, tanto de entrada y salida

Las funciones Clave de un Firewall:

Filtrado de Paquetes: Inspecciona los paquetes de datos basándose en la dirección IP de origen/destino, protocolo y puertos.

Inspección con Estado (Stateful): Realiza un seguimiento de las conexiones activas para determinar si un paquete es parte de una sesión 
legítima.

Control de Acceso: Decide qué tráfico está autorizado a pasar y cuál debe ser bloqueado, ya sea tráfico entrante o saliente.

Protección de Perímetro: Protege las redes privadas de las amenazas externas.

En esta documentacion, se mostrara como se configuro el firewall paso a paso para poder evidenciar las capacidades a la hora de configurar el firewall en una red en Ubuntu server


*Verificacion del firewall

Para conocer si el firewall esta instalado, se utiliza el comando which ufw, debe de mostrar una ruta donde se supone que el firewall esta instalado

![ruta ufw](https://github.com/JOGU-HP/ubuntu-server-lab/blob/493a4f0cb7ade604e8b2fda05bd87f7e7c57e57f/images/firewall/ruta%20ufw.png)

Muestra la ruta, por lo cual verificamos el estado con el comando sudo ufw status

![status](https://github.com/JOGU-HP/ubuntu-server-lab/blob/493a4f0cb7ade604e8b2fda05bd87f7e7c57e57f/images/firewall/status.png)

Por ahora, no se activara hasta escribir las politicas del firewall

*Implementacion de politicas

Las politicas del firewall son las reglas que el firewall sigue por defecto, pueden ser configurables a las necesidades del servidor, pero por ahora se implementaran las mas basicas, a fines de aprendizaje

Para denegar todo lo que entra, se usa el comando sudo ufw default deny incoming y usando sudo ufw default allow outgoing se permite todo lo que el servidor quiere enviar fuera

![entrada y salida](https://github.com/JOGU-HP/ubuntu-server-lab/blob/493a4f0cb7ade604e8b2fda05bd87f7e7c57e57f/images/firewall/entrada%20y%20salida.png)

Ahora, se deben crear excepciones, son aquellas que el servidor abre por que son necesarias, como los puertos ssh, dhcp, dns, http

Para los puertos SSH

Se usa el comando sudo ufw allow 22/tcp y sudo ufw allow OpenSSH

![ssh conf](https://github.com/JOGU-HP/ubuntu-server-lab/blob/493a4f0cb7ade604e8b2fda05bd87f7e7c57e57f/images/firewall/ssh%20conf.png)

Para el servicio DHCP sudo ufw allow 67/udp

![dhcp conf](https://github.com/JOGU-HP/ubuntu-server-lab/blob/493a4f0cb7ade604e8b2fda05bd87f7e7c57e57f/images/firewall/dchp%20conf.png)

DNS sudo ufw allow 53/udp

![udp conf](https://github.com/JOGU-HP/ubuntu-server-lab/blob/2b3262eeaa8e9508ee6a68cb4afb160dc9b7ba22/images/firewall/udp%20conf.png)

Y por ultimo para HTTP, sudo ufw allow 80/tcp y sudo ufw allow 'www' 

![http conf](https://github.com/JOGU-HP/ubuntu-server-lab/blob/493a4f0cb7ade604e8b2fda05bd87f7e7c57e57f/images/firewall/HTTP%20conf.png)

*Proteccion adicional

Como parte de mi aprendizaje en pentesting, encuentro ataques de fuerza bruta con ssh e hydra, asi que se puede usar una herramienta para limitar conexiones contra estos ataques, usando el comando

sudo ufw limit ssh

![ssh limit](https://github.com/JOGU-HP/ubuntu-server-lab/blob/493a4f0cb7ade604e8b2fda05bd87f7e7c57e57f/images/firewall/limit%20ssh.png)

*Activacion y verificacion

Usando el comando sudo ufw show added, se podran observar las reglas ya añadidas

![show added](https://github.com/JOGU-HP/ubuntu-server-lab/blob/493a4f0cb7ade604e8b2fda05bd87f7e7c57e57f/images/firewall/show%20added.png)

Una vez verificadas las reglas que se van a integrar, procederemos a usar sudo ufw enable para aplicar e iniciar el firewall

![enable](https://github.com/JOGU-HP/ubuntu-server-lab/blob/493a4f0cb7ade604e8b2fda05bd87f7e7c57e57f/images/firewall/emable.png)

Ahora, podemos ejecutar sudo ufw status numbered para observar los servicios activados

![numbered](https://github.com/JOGU-HP/ubuntu-server-lab/blob/493a4f0cb7ade604e8b2fda05bd87f7e7c57e57f/images/firewall/numbered.png)

Con estas reglas aplicadas, podremos tener mas seguridad en el servidor

