#Prácticas Servidores Web de Altas Prestaciones
**Práctica 3**

### nginx 
En la siguinte imagen se muestra la instalación de nginx en la tercera máquina M3 que actúa como balanceador:  

![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica3/images/image1.png)

Modificamos el fichero de configuración **/etc/nginx/conf.d/default.conf** de nginx, añadiendo la IP de M1 y M2:


![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica3/images/image2.png)

Una vez realizada la configuración reiniciciamos el servicio nginx:


![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica3/images/image3.png)

Después vamos a realizar peticiones desde la máquina anfitriona (donde tenemos instalado el virtulbox con M1, M2 y M3) al balanceador M3.
Antes modificamos el archivo **index.html** del directorio html de las máquinas M1 y M2, para visualizar mejor cada página, tras realizar las dos peticiones obtenemos las dos páginas web:


![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica3/images/image4.png)

### haproxy 
Cambiamos de software para el balanceador e instalamos **haproxy** en M3:


![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica3/images/image5.png)

Cambiamos la configuración **/etc/haproxy/haproxy.cfg** ya que la que viene por defececto no nos vale:


![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica3/images/image6.png)

Después de guardar la configuración detenemos el servicio de nginx con **service nginx stop** e iniciamos el servicio de haproxy:


![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica3/images/image7.png)

Volvemos a solicitar peticiones desde la máquina anfitriona al balanceador M3.


![imagen](https://github.com/jimcase/swap15-16/blob/master/Practica3/images/image8.png)



