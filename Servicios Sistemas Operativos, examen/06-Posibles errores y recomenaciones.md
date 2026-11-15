# SSH
1. SSH

• No cierres tu sesión actual: Prueba el puerto nuevo (2222) en otra ventana antes de cerrar la actual para no quedarte fuera.
• Cierra el puerto 22: Cuando funcione el 2222, quita el servicio SSH antiguo del firewall (--remove-service=ssh).


# HTTP
• Usa /var/www/html/: Pon ahí tu index.html y tus imágenes en lugar de editar las rutas del sistema.
• Usa cp en vez de mv: Copia las imágenes para que hereden los permisos de SELinux, o ejecuta restorecon -Rv /var/www/html/.


# vsftpd
## Errores
• Modo Pasivo en FTP (Conexión desde Windows/MobaXterm): Al usar chroot_local_user=YES desde una máquina externa, el cliente FTP suele quedarse colgado al listar carpetas.
	• Corrección: Agrega estas líneas al final de /etc/vsftpd/vsftpd.conf y abre los puertos en el firewall:text
pasv_enable=YES
pasv_min_port=40000
pasv_max_port=40100
Usa el código con precaución.
Luego ejecuta: sudo firewall-cmd --permanent --add-port=40000-40100/tcp && sudo firewall-cmd --reload

## Recomendaciones
• Usa Modo Pasivo: Configúralo en tu cliente (FileZilla/MobaXterm) para que Windows no bloquee la lista de carpetas.
• Permisos chroot: Asegura que allow_writeable_chroot=YES esté activo para evitar errores al subir archivos.
# ntp
## Errores
Si te sigue saliendo algún error al ejecutar w32tm /resync, compárteme el mensaje exacto o el resultado de w32tm /query /status para ayudarte a resolverlo.

## Recomendaciones
• Verifica clientes: Usa sudo chronyc clients en CentOS para confirmar que Windows ya se conectó.
• Revisa el Firewall de Windows: Si falla la sincronización, permite la salida del puerto UDP 123 en Windows.

# VirtualBox
## Recomendaciones

• Realizar backups o copias: Realiza copias en especial si se va a trabajar en nano por si necesitas revertir errores rápido.
