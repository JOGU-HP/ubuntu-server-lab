-Simulacion de entorno de trabajo real con usuarios y permisos-

Como parte de practicar sobre usuarios, permisos y grupos, se creara la simulacion de un entorno real de trabajo

Datos relevantes:

-La empresa se llama Techsolutions S.A. 

Departamentos:
IT (Sistemas)
Desarrollo (Programadores)
Contabilidad (Finanzas)
RRHH(Recursos Humanos)

Directorios y flujo de permisos

/company/
├── it/           # Solo IT

├── desarrollo/   # Solo Desarrollo

├── contabilidad/ # Solo Contabilidad

├── rrhh/         # Solo RRHH

├── public/       # Todos pueden leer

└── proyectos/    # Colaboración entre IT y Desarrollo


(El flujo de carpetas, usuarios e ideas fueron soliictadas a la Inteligencia Artificial Deepseek) sin copiar y pegar, escribiendo cada comando para entender su funcionamiento y comportamiento)

Para comenzar, se crea la carpeta donde estaran los recursos de la empresa, como marca, usando el comando cd ~ y mkdir -p /company

![Directorio Principal]

Para crear subdirectorios se usara mkdir -p /company/{it,desarrollo,contabilidad,rrhh,public,proyectos,backups,archivos_compartidos} con el comando

sudo mkdir /company/it
sudo mkdir /company/desarrollo
sudo mkdir /company/contabilidad
sudo mkdir /company/rrhh
sudo mkdir /company/public
sudo mkdir /company/proyectos
sudo mkdir /company/backups
sudo mkdir /company/archivos_compartidos

![Subdirectorios]

Ahora que los subdirectorios estan creados, se crean subdirectorios dentro de los subdirectorios, para mantener organizacion y hacer una simulacion mas realista sobre ciertos directorios que podrian usarse en un servidor Ubuntu

Contaran con subdirectorios como informes, documentos y confidencial

Para la creacion de cada uno de los subdirectorios, se debe usar el comando cd para ingresar al subdirectorio

Despues sudo mkdir nombre del directorio

Comprobar la creacion de directorios con ls 

![Subdirectorios2]

Como toda empresa, existen grupos, donde se albergaran los usuarios y los directorios para mantener una organizacion estructurada y evitar confusiones o practicas poco eticas entre usuarios que comprometan la seguridad del sevidor

Para añadir grupos a un servidor, se usa el comando groupadd y el nombre del grupo

Y para comprobar que los grupos se crearon con exito se usa getent group | grep departamento ya que se usa el comando groupadd departamento_nombre del departamento

![Gruppos]

Los usuarios son parte importante en los servidores, pueden hacer conexiones por via ssh y para ello, deben crearse sus perfiles, algo parecido a perfiles como Facebook o WhatsApp, solo que con limitaciones en sus acciones y permisos hacia archivos y directorios

Se escribe el comando sudo useradd -m -s /bin/bash -c "Usuario- descripcion" usuario

Para realizar un cambio en la conraseña se usa echo "usuario:contrasena" | sudo chpasswd

Para que solicite la contraseña desde el primer login se usa chage -d 0 usuario

Y para agregarlo a un grupo, sudo usermod -aG departamento_it usuario

Si ahora se quiere comprobar si se agrego al grupo correctamente basta con escribir groups jperez

![Primer Usuario]

Esta serie de comandos se replican con los demas usuarios que se van a crear

Cuando hayamos terminado de agregar a los usuarios, agregaremos jefes a cada uno de los departamentos

Con sudo chown -R usuario:departamento /directorio/

![Jefes]

Procederemos a cambiar permisos a cada carpeta dentro de un directorio siguiendo:

La cambinación de valores de cada grupo de los usuarios forma un número octal, el bit x es 20 es decir 1, el bit w es 21 es decir 2, el bit r es 22 es decir 4, tenemos entonces:

r = 4
w = 2
x = 1
La combinación de bits encendidos o apagados en cada grupo da ocho posibles combinaciones de valores, es decir la suma de los bits encendidos:

- - -	= 0	no se tiene ningún permiso
- - x	= 1	solo permiso de ejecución
- w -	= 2	solo permiso de escritura
- w x	= 3	permisos de escritura y ejecución
r - -	= 4	solo permiso de lectura
r - x	= 5	permisos de lectura y ejecución
r w -	= 6	permisos de lectura y escritura
r w x	= 7	todos los permisos establecidos, lectura, escritura y ejecución

Entendiendo esto, usaremos los siguientes comandos

![Permisos]

Estos comandos seran replicados, cambiando los directorios por los demas directorios y subdirectorios existentes

![Permisos2]

Terminado el replicado de permisos con los demas directorios, se usara la herramienta tree para ver los permisos y una estructura completa

Si no se cuenta con esta herramienta basta con hacer sudo apt install tree

Y se usa el comando sudo tree /company -pug

![directorios completos]

Con esto, quedan listos los permisos y los directorios que se han creado simulando un entorno real de trabajo 
