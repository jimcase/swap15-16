#Prácticas Servidores Web de Altas Prestaciones
**Práctica 5**

###Replicación de bases de datos MySQL
Primero creamos una base de datos en la máquina M1(192.168.1.27):

![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica5/images/image2.png)

Luego guardamos los datos de la base de datos con **mysqldump contactos -u root -p > contactos.sql**
Una vez guardada, nos vamos a la máquina esclavo(192.168.1.22) y pasamos a copiar la base de datos guardada en el paso anterior

![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica5/images/image1.png)

###Replicación de BD mediante una configuración

Editamos la configuración de mysql de la máquina M1 maestro(192.168.1.27). Para ello
editamos el archivo /etc/mysql/my.cnf.

Comentamos el parámetro bind-address que sirve para que escuche a un servidor:
**#bind-address 127.0.0.1**
Le indicamos el archivo donde almacenar el log de errores:
**log_error = /var/log/mysql/error.log**
Establecemos el identificador del servidor.
**server-id = 1**
El registro binario contiene toda la información que está disponible en el registro de
actualizaciones, en un formato más eficiente y de una manera que es segura para las
transacciones:
**log_bin = /var/log/mysql/bin.log**
Guardamos el documento y reiniciamos el servicio:
**sudo /etc/init.d/mysql restart**

Después de reiniciar con éxito mysql editamos la configuración del mysql del esclavo (vamos a editar el archivo **/etc/mysql/my.cnf**)

Establecemos el identificador del servidor.
**server-id = 2**

Reiniciamos mysql:
**sudo /etc/init.d/mysql restart**

Ahora volvemos a la máquina M1 maestro(192.168.1.27) para crear un usuario y darle permisos de acceso para la replicación:

![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica5/images/image3.png)

Para finalizar con la configuración en la máquina M1 maestro(192.168.1.27), obtenemos los datos de la base de datos que vamos a replicar.

![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica5/images/image4.png)


Volvemos a la máquina esclava, entramos en mysql y le damos los datos del maestro:

![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica5/images/image5.png)


Después de introducir los datos del maestro ejecutamos los siguientes comandos:
**UNLOCK TABLES;**
**SHOW SLAVE STATUS\G;**
Nos saldrá una pantalla como la siguiente, en donde si la variable Seconds_Behind_Master es distinta de null significa que todo ha salido bien:

![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica5/images/image5.png)
