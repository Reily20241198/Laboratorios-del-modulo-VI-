# Laboratorios-del-modulo-VI-
Practica 2 - IP tables - UFW/Firewall-cmd
# Práctica 2 – Manejo de Puertos con iptables y firewall-cmd en CentOS

# 1. Instalar servicios HTTP, FTP y SSH
sudo yum install httpd vsftpd openssh-server -y
→ Instala Apache (HTTP), vsftpd (FTP) y OpenSSH (SSH). El parámetro -y confirma automáticamente.

# 2. Habilitar servicios al inicio del sistema
sudo systemctl enable httpd vsftpd sshd
→ Configura los servicios para que se inicien automáticamente al arrancar CentOS.

# 3. Iniciar los servicios manualmente
sudo systemctl start httpd vsftpd sshd
→ Arranca los servicios en este momento.

# 4. Verificar que estén activos
sudo systemctl status httpd
sudo systemctl status vsftpd
sudo systemctl status sshd
→ Muestra el estado actual de cada servicio.

# 5. Bloquear puertos con iptables
sudo iptables -A INPUT -p tcp --dport 80 -j DROP
sudo iptables -A INPUT -p tcp --dport 21 -j DROP
sudo iptables -A INPUT -p tcp --dport 22 -j DROP
→ Añade reglas para bloquear tráfico TCP en los puertos 80 (HTTP), 21 (FTP) y 22 (SSH).

# 6. Ver reglas activas en iptables
sudo iptables -L -n --line-numbers
→ Lista todas las reglas activas con sus números de línea.

# 7. Eliminar reglas para permitir tráfico nuevamente
sudo iptables -D INPUT -p tcp --dport 80 -j DROP
sudo iptables -D INPUT -p tcp --dport 21 -j DROP
sudo iptables -D INPUT -p tcp --dport 22 -j DROP
→ Elimina las reglas que bloqueaban los puertos.

# 8. Verificar que se eliminaron
sudo iptables -L -n
→ Confirma que ya no hay reglas de bloqueo activas.

# 9. Bloquear puertos usando firewall-cmd
sudo firewall-cmd --permanent --remove-service=http
sudo firewall-cmd --permanent --remove-service=ftp
sudo firewall-cmd --permanent --remove-service=ssh
→ Elimina los servicios del firewall público, bloqueando el acceso.

# 10. Recargar configuración del firewall
sudo firewall-cmd --reload
→ Aplica los cambios realizados.

# 11. Ver servicios activos en el firewall
sudo firewall-cmd --list-all
→ Muestra todos los servicios y puertos permitidos actualmente.

# 12. Volver a permitir servicios en el firewall
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=ftp
sudo firewall-cmd --permanent --add-service=ssh
→ Agrega nuevamente los servicios al firewall público.

# 13. Recargar y verificar
sudo firewall-cmd --reload
sudo firewall-cmd --list-all
→ Aplica los cambios y verifica que los servicios estén permitidos.
