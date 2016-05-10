#Prácticas Servidores Web de Altas Prestaciones
**Práctica 4**

###Pruebas con Apache Benchmark
Modifiqué la pagina index.html de cada maquina M1(192.168.1.30) y M2(192.168.1.29) incluyendo un script en php para que la prueba del servidor sea mas costosa.  

![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica4/images/image1.png)

Ejecutamos en la máquina anfitriona el apache benchmark para la máquina M1(192.168.1.30), para el balanceador(192.168.1.31) con nginx y otra con haproxy.
Para M1 sería: **ab -n 1000 -c 10 http://192.168.1.30/index.html**
Para el balanceador con nginx y haproxy: **ab -n 1000 -c 10 http://192.168.1.31/index.html**
Llevamos a cabo una carga de 1000 peticiones con una concurrencia de 10, es decir, de diez en diez.

![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica4/images/image2.png)
![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica4/images/image3.png)

Resultados:

![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica4/images/image5.png)
![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica4/images/image6.png)
![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica4/images/image7.png)

###Pruebas con Siege
Ejemplo de sentencia para el balanceador: **siege -b -t60S -v http://192.168.1.31/index.html**
t= tiempo de conexión, 1 minuto.
Ejemplo:

![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica4/images/image4.png)

Resultados:

![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica4/images/image8.png)
![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica4/images/image9.png)
![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica4/images/image10.png)
![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica4/images/image11.png)
![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica4/images/image12.png)
![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica4/images/image13.png)
