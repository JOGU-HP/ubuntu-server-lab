-Configuracion de servicios-

Antes de crear usuarios, grupos, permisos y administradores, es necesario realizar configuraciones con el objetivo de asemejarse lo mas posible a las configuraciones reales a un servidor

-DHCP-

El servicio DHCP es un protocolo que asigna IP's, mascaras de subred, puertas de enlace y configuraciones a los host de una red, basicamente cada equipo que se conecte al servidor se le asignara una IP diferente para su identificacion

El entorno en el que se esta trabajando, sera aislado de una red Wi-Fi personal, asi que a nivel hardware se dispone de:

1 router
2 cables ethernet con conectores RJ45
2 Laptops (1 para el servidor virtualizado y 1 para practicar con conexiones SSH)

Una vez identificadas las herramientas de hardware, se realizan ciertas configuraciones para no tener complicaciones con la descarga de paquetes para el servidor

-Configuracion de VirtualBox-

VirtualBox permite usar mas de una red fisica para las virtualizaciones, por lo que se pueden tener 2 redes a la vez, que para este caso una sera para internet y otra para que el servicio DHCP funcione correctamente

Se debe conectar el router sin salida a internet al equipo donde se esta virtualizando el servidor

Y para conocer el cable fisico del router sin salida a internet, en Windows basta con escribir en el buscador Network para entrar en la opcion View Network Connections e identificar la conexion Ethernet

![identificacion del cable](https://github.com/JOGU-HP/ubuntu-server-lab/blob/181ed39bf3027d365d4bf3d25799feb3143244cb/images/Identificacion%20del%20cable.png)

Ahora que el cable se ha identificado correctamente, en VirtualBox se selecciona la maquina que contiene el servidor y se accede a las configuraciones de la maquina

En la opcion Redes o Network, por defecto tendra la conexion con salida a internet o que tiene el equipo anfitrion y se puede verificar la informacion con la administracion de redes

Dentro de Adapter 2, se marca la casilla Enable Network Adapter, cambiando de NAT a Adaptador Puerte y dentro de las opciones de Nombre o Name seleccionar el cable conectado al router sin salida a internet y se guardan los cambios

![Configuracion 2da red](https://github.com/JOGU-HP/ubuntu-server-lab/blob/181ed39bf3027d365d4bf3d25799feb3143244cb/images/Seleccion%202da%20red.png)

Para este punto, se puede iniciar la maquina virtual sin problema para comprobar que los cambios se han efectuado correctamente

Despues de logearse, se puede escribir el comando ip a para ver las redes y se observan 3 de ellas

enp0s3 y enp0s8

Podremos corroborar los cambios efectuados con la descarga del paquete dhcp, usando el comando sudo apt install isc-dhcp-server que es el servicio dhcp, si todo esta bien hasta este punto el paquete se instalara sin problema puesto que se esta usando la conexion a internet

![descarga dhcp](https://github.com/JOGU-HP/ubuntu-server-lab/blob/181ed39bf3027d365d4bf3d25799feb3143244cb/images/descarga%20dhcp.png)

-Configuracion DHCP-

Para este punto, DHCP esta instalado exitosamente, por lo que ahora se puede configurar sin problema

Se ejecuta el comadno sudo nano /etc/netplan/TAB

(TAB se refiere a presionar la tecla TAB, para evitar complicaciones con el archivo yaml)

Dentro de netplan, se encuentra una configuracion inicial para enp0s3, pero solo marcaremos en este caso para dhcp4: false

Debajo del todo, se escribe el siguiente codigo

dhcp4: false
addresses: [IP/24]

para la identacion, es importante usar espacios y no tabulaciones

Para este caso, me han ocurrido errores que a continuacion mostrare como los solucione

-Error de escritura: El primer error que cometi, fue escribir mal la palabra addresses y escribi adresses, es importante escribir bien esta palabra por que marcara error

-dhcp4: true, al principio crei que era necesario para el servidor, sin embargo, un servidor tiene una IP fija y mantener dhcp4 en true marcara errores, el servidor debe tener una IP fija y configurada para mantenerla siempre estatica, asi que se escribe no o false para que esta permita ejecutar la tarea de mantener su IP fija

![codigo dhcp completo](https://github.com/JOGU-HP/ubuntu-server-lab/blob/181ed39bf3027d365d4bf3d25799feb3143244cb/images/codigo%20dhcp%20completo.png)

Para aplicar los cambios ejecutados, se escribe el comando sudo netplan apply y si al presionar ENTER no marca ningun error o mensaje el servicio esta completo

Ahora al escribir ip a observaremos que la red enp0s8 ahora tiene la IP que le asignamos con el archivo netplan

![new ip](https://github.com/JOGU-HP/ubuntu-server-lab/blob/181ed39bf3027d365d4bf3d25799feb3143244cb/images/new%20ip.png)

Procederemos a escirbir sudo nano /etc/default/isc-dhcp-server y dentro del archivo nano, en la opcion de INTERFACESv4:""

Dentro de las comillas, se escribe enp0s8 que es la red que acabamos de configurar, de igual manera se guardan cambios con CRTL+O y CRTL+X

![Interfaz](https://github.com/JOGU-HP/ubuntu-server-lab/blob/181ed39bf3027d365d4bf3d25799feb3143244cb/images/interfaz.png)

Ahora, se escribe el comando sudo nano /etc/dhcp.conf que nos abrira un archivo nano, y desplazandonos hasta el final del archivo se escribira el siguiente codigo

![conf dhcp](https://github.com/JOGU-HP/ubuntu-server-lab/blob/181ed39bf3027d365d4bf3d25799feb3143244cb/images/conf%20dhcp.png)

En group se puede escribir el nombre que se desee, en este caso sera red interna

Se usa una mascara de red que es 255.255.255.0

y en range se escribe la direccion IP que se asigno en el archivo yaml pero con la diferencia de que el ultimo digito se escribira un rango en el que los demas equipos que se conecten al servidor recibiran una IP

En este caso sera desde el 100 hasta el 200

De igual manera, los cambios se guardan con CRTL+O ENTER CRTL+X

Esta configuracion asigna IP's a equipos que se conecten al servidor y evita IP duplicadas 

Con todas estas configuraciones podremos ver ahora el estado del servicio con sudo systemctl status isc-dhcp-server

![error](https://github.com/JOGU-HP/ubuntu-server-lab/blob/181ed39bf3027d365d4bf3d25799feb3143244cb/images/Error%201.png)

Como veran, ha marcado error la configuracion, asi que analizo el error para saber que estoy haciendo mal

-El primer erro fue, en la configuracion de dhcp en el archivo .conf, despues de subnet, coloque la palabra IP en lugar de la direccion IP

-El segundo error, fue que despues de los rangos, debe ir al final ":"

Identificados los problemas y escrito de nuevo la configuracion correctamente, verifico el status del servicio y ahora se ejecuta correctamente

![Error Sol](https://github.com/JOGU-HP/ubuntu-server-lab/blob/181ed39bf3027d365d4bf3d25799feb3143244cb/images/Error%20Sol.png)

Ahora si, el servicio funciona correctamente y para corroborar se conecta una laptop al router

Aunque automaticamente el router da las IP's se tuvieron complicaciones con algunas configuraciones y se solucionaron

1- Es importante, que el servidor tenga la misma IP que el router tiene por defecto, aunque se puede cambiar de manera que la IP sea diferente en las mismas configuraciones del router

2- Si como yo, el router para practicar ya no sera utilizado, se puede reiniciar el router de fabrica y desactivar la opcion de DHCP para que con ello solo use el servidor como DHCP, tambien se puede cambiar la IP 

3- Para este caso, como se practica con una VM, se desactivo el firewall de windows (peligroso para ataques fuera de la practica pero funcional para la comunicacion)

Para saber si ahora si existe comunicacion con el servidor y los clientes, se realizan ping's de maquinas a cliente y de clientes a maquina

![ping a cliente](https://github.com/JOGU-HP/ubuntu-server-lab/blob/181ed39bf3027d365d4bf3d25799feb3143244cb/images/ping%20a%20cliente.png)

![ping a server](https://github.com/JOGU-HP/ubuntu-server-lab/blob/c7fdfa9ba766e7a84f76e0283289c87f0d1b1591/images/ping%20a%20server.png)

Con esto concluye la practica para la configuracion del servicio DHCP ya que ambos equipos reciben informacion de manera simultanea
