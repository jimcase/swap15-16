#Prácticas Servidores Web de Altas Prestaciones
**Práctica 2**

###Prueba del funcionamiento de la herramienta rsync  
Vamos a copiar el contenido de la carpeta /var/www de la máquina M1 (192.168.1.20) a la máquina M2 (192.168.1.21).
Desde M2 ejecutamos el siguiente comando:  
**rsync -avz -e shh casso@192.168.1.20:/var/www /var/www**  
![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica2/image1.jpg)