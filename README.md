# vgtp
#-------------split del var---------- 

#var era muy grande por lo que tuvimos que hacer un split split -b 90M var.tar.gz varparte

#Luego hicimos el otro push de los splits #Para volver a unirlos deberiamos hacer lo siguiente: cat varpartea* > var.tar.gz

#-------------FIREWALL--------------- 

#No podiamos subir a Git los tar teniendo el firewall activado, por lo que tuvimos que desactivar los firewall por lo tanto no esta esa configuracion.

#Para volver a tener esa configuracion deberiamos hacer lo siguiente:

#Ejecutariamos los siguientes comandos: #Si no estainstalado iptables apt-get install iptables

#Eliminamos todas las reglas iptables -F

#Establecemos por defecto DROP los INPUTS iptables -P INPUT DROP

#Permitimos solo los puertos de SSH y APACHE2 iptables -A INPUT -p tcp --dport 22 -j ACCEPT # Puerto SSH iptables -A INPUT -p tcp --dport 80 -j ACCEPT # Puerto HTTP iptables -A INPUT -p tcp --dport 3306 -j ACCEPT # Puerto MySQL iptables -A INPUT -p tcp --dport 443 -j ACCEPT # Puerto HTTPS iptables -A INPUT -p udp --dport 53 -j ACCEPT # Puerto para resolver DNS iptables -A INPUT -p tcp --dport 53 -j ACCEPT # Puerto para resolver DNS

#Primero tuvimos que hacer un mkdir /opt/tp/firewal . La carpeta tp ya la teniamos al crear lso scripts #creamos el archivo touch firewall.conf

#Guardamos la configuracion en la carpeta destino con el nombre firewall.conf iptables-save > /opt/tp/firewall/firewall.conf

#Hacemos que siempre inicie con la configuracion recien creada crontab -e

#Agregamos la siguiente linea al final. @reboot /usr/sbin/iptables-restore < /opt/tp/firewall/firewall.conf
