#Prácticas Servidores Web de Altas Prestaciones
**Práctica 2**

###Prueba del funcionamiento de la herramienta rsync  
Vamos a copiar el contenido de la carpeta /var/www de la máquina M1 (192.168.1.20) a la máquina M2 (192.168.1.21).
Desde M2 ejecutamos el siguiente comando:  
**rsync -avz -e shh casso@192.168.1.20:/var/www /var/www**  
![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica2/images/image1.jpg)

Ahora vamos a hacer que se sincronice automáticamente sin contraseña para mantener el contenido de M1 y M2
actualizado e idéntico, mediante ssh sin contraseña se usa autenticación con un par de claves pública-privada.
A través de ssh-keygen podemos generar esta clave.
Desde M2 ejecutamos **ssh-keygen -t dsa** para generar la clave de tipo dsa válida para el protocolo 2 de SSH.
![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica2/images/clave-ssh.jpg)
La variable **passphrase** es una contraseña privada para la comunicación entre las máquinas, pero como no queremos que haya contraseña se deja en blanco.
Una vez generada la clave, hay que copiarla a M1.
![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica2/images/claves-ssh2.jpg)
Ahora voy a probar si ha funcionado conectándome a M1 sin contraseña con el siguiente comando: **ssh-copy-id -i .ssh/id_dsa.pub casso@192.168.1.20**
![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica2/images/claves-ssh3.jpg)
Ahora para que la actualización sea autmática vamos a hacer uso del cron de linux y que ejecute este script:
![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica2/images/scriptRsync.jpg)
![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica2/images/scriptRsync2.jpg)
Editamos el archivo **/etc/crontab** para añadir este script:
![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica2/images/crontab.jpg)
Ya tenemos la tarea programada para que actualice automáticamente el directorio **/var/www**.
