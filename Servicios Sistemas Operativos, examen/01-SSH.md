
sudo systemctl status sshd

sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup
 
sudo nano /etc/ssh/sshd_config


#Port 22, (Hay que quitar el numeral y cambiar el puero, luego poner ctrl+O, enter y ctrl+X)

sudo dnf install -y policycoreutils-python-utils

sudo semanage port -a -t ssh_port_t -p tcp 2222 (ejemplo de número de puerto)



sudo firewall-cmd --permanent --add-port=2222/tcp

sudo firewall-cmd --reload o sudo systemctl reload firewalld

sudo firewall-cmd --list-ports

sudo systemctl restart sshd

sudo systemctl status sshd
