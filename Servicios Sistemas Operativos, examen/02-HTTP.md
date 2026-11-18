Cambiar Título 
sudo systemctl status httpd

sudo dnf install -y httpd (en caso de que no este instalado)

sudo systemctl start httpd

sudo systemctl enable httpd

sudo systemctl status httpd

sudo firewall-cmd --permanent --add-service=http  

sudo firewall-cmd --reload

sudo firewall-cmd --list-all

sudo cp /usr/share/testpage/index.html /usr/share/testpage/index.html.backup

ls -l /usr/share/testpage/index.html

sudo nano /usr/share/testpage/index.html

**Buscar la línea: "<h1>"HTTP Server Test Page</h1>"
ahi se puede cambiar el título de la página.

#En caso de no tener el símbolo "<", buscar la línea "/html", ésta se encuentra cerca de la línea que estamos buscando.

#Luego de modificar la línea, realizar los comandos "ctrl+O", "enter", "ctrl+X"

sudo systemctl restart httpd



## COLOCAR IMAGEN:
la palabra "ucuencatec.png" va a depender del nombre con el que se haya guardado a la imagen y el formato
sudo cp /ruta/de/la/imagen/ucuencatec.png /usr/share/testpage/
sudo chmod 644 /usr/share/testpage/ucuencatec.png
sudo restorecon -v /usr/share/testpage/ucuencatec.png


sudo nano /usr/share/testpage/index.html

Modifica la línea de <a class="navbar-brand"...> o más sencillo buscar "<a class "

EL FINAL DE LA LINEA SE TIENE QUE VER ASÍ 
img src="data:image/svg+xml;base64,..." alt="CentOS" /><img src="ucuencatec.png" alt="UCUENCATEC" style="height: 35px; margin-left: 15px;" /"signo de mayor que "</a"signo de mayor que"

sudo systemctl restart httpd
