ip a

sudo nano /etc/chrony.conf

#Baja hasta el final del archivo y agrega estas dos líneas:
allow 192.168.0.100 (aqui depende de la ip de nuestro Windows)
local stratum 10

sudo systemctl restart chronyd
sudo systemctl enable chronyd 
sudo firewall-cmd --add-service=ntp --permanent
sudo firewall-cmd --reload


Conectar Windows con tu servidor CentOS

1. En tu laptop Windows, abre el menú Inicio, escribe cmd, haz clic derecho sobre Símbolo del sistema y elige Ejecutar como administrador.
2. En la ventana negra (que debe decir C:\Windows\System32>), pega esta línea reemplazando IP_DEL_CENTOS por el número que anotaste en el Paso 1:

sc config w32time start= auto & net start w32time & w32tm /config /manualpeerlist:"IP_DEL_CENTOS,0x8" /syncfromflags:manual /update & w32tm /resync /rediscover & w32tm /query /status

w32tm /resync

w32tm /query /status

En el resultado, busca la línea Origen (Source). Debe mostrar la IP de tu servidor CentOS en lugar de Local CMOS Clock o ://windows.com
