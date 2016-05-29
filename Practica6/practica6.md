#Prácticas Servidores Web de Altas Prestaciones
**Práctica 6**

###Configuración del RAID por sofware

Partimos de una máquina virtual ya instalada y configurada a la que, estando apagada, añadiremos dos discos del mismo tipo y capacidad.

![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica6/images/image1.png)
![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica6/images/image2.png)

Ahora arrancamos la máquina y entramos para instalar el software necesario para
configurar el RAID:
**sudo apt-get install mdadm**
Debemos buscar la información (identificación asignada por Linux) de ambos discos:
**sudo fdisk -l**

![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica6/images/image3.png)

Ahora ya podemos crear el RAID 1, usando el dispositivo /dev/md0, indicando el número de dispositivos a utilizar (2), así como su ubicación:
**sudo mdadm -C /dev/md0 --level=raid1 --raid-devices=2 /dev/sdb /dev/sdc**

![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica6/images/image4.png)

Una vez creado el dispositivo RAID, y como aún no habremos reiniciado la máquina, usaremos /dev/md0 para darle formato:
**sudo mkfs /dev/md0**
Por defecto, mkfs inicializa un dispositivo de almacenamiento con formato ext2.

![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica6/images/image5.png)

Podemos comprobar que el proceso se ha realizado adecuadamente, y también los parámetros con los que Linux ha conseguido montarlo usando la orden:
**sudo mount**
Para comprobar el estado del RAID, ejecutaremos:
**sudo mdadm --detail /dev/md0**
![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica6/images/image6.png)


Para finalizar el proceso, conviene configurar el sistema para que monte el dispositivo RAID creado al arrancar el sistema. Para ello debemos editar el archivo /etc/fstab y añadir la línea correspondiente para montar automáticamente dicho dispositivo.
Conviene utilizar el identificador único de cada dispositivo de almacenamiento en lugar de simplemente el nombre del dispositivo (aunque ambas opciones son válidas). Para obtener los UUID de todos los dispositivos de almacenamiento que tenemos, debemos ejecutar la orden:
**ls -l /dev/disk/by-uuid/**
![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica6/images/image7.png)

Anotaremos el correspondiente al dispositivo RAID que hemos creado. Ahora ya podemos añadir al final del archivo /etc/fstab la línea para que monte automáticamente el dispositivo RAID.

![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica6/images/image8.png)

Finalmente, una vez que esté funcionando el dispositivo RAID, podemos simular un
fallo en uno de los discos:
**sudo mdadm --manage --set-faulty /dev/md0 /dev/sdb**

![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica6/images/image9.png)

También podemos retirar “en caliente” el disco que está marcado como que ha fallado:
**sudo mdadm --manage --remove /dev/md0 /dev/sdb**

![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica6/images/image10.png)

Y por último, podemos añadir, también “en caliente”, un nuevo disco que vendría a
reemplazar al disco que hemos retirado:
**sudo mdadm --manage --add /dev/md0 /dev/sdb**

![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica6/images/image11.png)
