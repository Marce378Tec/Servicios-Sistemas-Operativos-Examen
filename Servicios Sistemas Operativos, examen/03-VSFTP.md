sudo dnf install vsftpd -y

sudo systemctl status vsftpd

sudo systemctl start vsftpd (en caso de que este apagado)

sudo systemctl enable vsftpd

sudo firewall-cmd --permanent --add-service=ftp

sudo firewall-cmd --reload

sudo firewall-cmd --list-all




sudo setsebool -P ftpd_full_access on

sudo cp /etc/vsftpd/vsftpd.conf /etc/vsftpd/vsftpd.conf.backup

sudo nano /etc/vsftpd/vsftpd.conf

Paso 4.2 : Asegúrate de que las siguientes directivas queden configuradas así:
#Deshabilitar el acceso anónimo
anonymous_enable=NO

#Permitir el acceso a usuarios locales del sistema
local_enable=YES

#Permitir permisos de escritura (subida de archivos)
write_enable=YES

#Enjaular a los usuarios en su directorio personal (quitar el simbolo "#")
chroot_local_user=YES

#Permitir escritura en el directorio raíz de chroot (permite al usuario enjaulado, subir, modificar o crear carpetas dentro del diectorio raíz de su propio directorio. Obligatorio en caso de activarse "chroot_local_user=YES"), agregar la siguiente linea al final:
allow_writeable_chroot=YES

#Omitir la validación de shell (necesario al usar /sbin/nologin), añadir la siguiente linea al final: 
check_shell=NO

Buscar la línea que dice "#listen=NO" o "listen=NO", quitar el simbolo # y cambiarlo a YES: 
listen=YES

Buscar la linea que dice "listen_ipv6=YES" y cambiarlo a NO:
listen_ipv6=NO

Guarda los cambios.

sudo useradd -m -s /sbin/nologin usuario_ftp

sudo passwd usuario_ftp


#Revisar si el usuario_ftp esta aqui:
sudo nano /etc/vsftpd/user_list

#Si no esta hacer el siguiente paso:
sudo nano /etc/pam.d/vsftpd

#Buscar la linea que contiene la palabra pam_shell.so::
auth required pam_shell.so

#Poner un númeral al inicio para desactivarla:
#auth required pam_shell.so


sudo systemctl restart  vsftpd


## Como hacer que se pueda subir archivos de Windows a la maquina Virtual mediante vsftp
El usuario ftp no tiene acceso a todas las carpetas, esto ocurre porque al crear a marce_ftp con -s /sbin/nologin (sin entorno gráfico), Linux le crea un directorio vacío en /home/marce_ftp sin las carpetas típicas de escritorio. Además, como activaste chroot_local_user=YES, este usuario está "enjaulado" y no puede salir de su propia ruta por seguridad.
#1. Crea una carpeta de destino en tu usuario normal

mkdir -p /home/mespinoza378/Archivos_FTP


#2. Cambia la carpeta de inicio de marce_ftp

sudo usermod -d /home/mespinoza378/Archivos_FTP marce_ftp


3. Configura los permisos compartidos

• Asigna la propiedad de la carpeta a ambos usuarios:bash

sudo chown -R mespinoza378:marce_ftp /home/mespinoza378/Archivos_FTP


• Otorga permisos totales al dueño y al grupo (775) y fuerza herencia (2):bash

sudo chmod 2775 /home/mespinoza378/Archivos_FTP


• Permite el paso a través de tu directorio principal:

chmod 711 /home/mespinoza378
