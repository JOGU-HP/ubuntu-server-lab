Configuracion de Red

Para trabajar con este servidor Ubuntu, se utilizara un router que no esta conectado a internet, pero que servira para una red aislada y para mantener comunicacion con los equipos con los que se vaya a trabajar

Como se esta utilizando VirtualBox, se deben elegir las redes que se van a usar

1 para descarga de paquetes
1 como red local y comunicacion entre equipos

Configuracion de red

Se conecto el router al equipo que tiene Ubuntu Server y en el menu superior de VirtualBox, se accede a la opcion Settings

Dentro de Setting, se entro a la opcion Network, donde muestra la red donde se esta conectado actualmente, esto es para que haya internet y para que se pueda hacer actualizacion del sistema y descarga de paquetes

En la pestaña de Adapter 2, se marca la casilla Enable Network Adapter

Se selecciono la opcion Bridged Adapter y en el Adapter Type se selecciona el cable de la conexion al router

Si se desconoce este cable, se puede acceder View Network Conections

Se ubica la red que se va a usar como red local y muestra el tipo de cable que se esta utilizando como conexion hacia el equipo

![Identificacion del cable]

Cuando se haya seleccionado el cable de conexion, se aplican los cambios y se inicia el servidor nuevamente

