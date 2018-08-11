# comandos-open-community


* Cambiar el nombre de host a myhost.opencommunity.org 

     #hostnamectl set-hostname myhostacecinxs.opencommunity.org

* Configure su nombre de host, dirección IP, puerta de enlace y DNS.

     #nmcli connection down eth0

     #nmcli connection modify eth0 ipv4.addresses 172.24.40.41/24 ipv4.gateway 172.24.40.1 ipv4.dns 172.24.40.1
     
     #nmcli connection up eth0
     
     
* Descargue una Imagen (imagen.iso) y móntelo automáticamente bajo /media/cdrom y que surten efecto automáticamente en el arranque-inicio. 

     Se agrega el iso como device CDROM a la máquina virtual
     
     En este caso, la carpeta en la que vamos a montar se llama "iso"
     
     #mkdir /mnt/iso
     
     #echo "/dev/sr0 /mnt/iso iso9660 ro,nosuid,nodev,relatime 0 0" > /etc/fstab
     
     #cat /mnt/iso/media.repo >> /etc/yum.repos.d/local.repo
     
 * Cree dos usuarios: OpenCommunity con uid / gid igual a 8000, contraseña: password, buenestudiante con un uid / gid igual a  3333, contraseña: biendificil  y malestudiante con uid / gid igual a 6666, contraseña: refacilita. 
 
 #useradd opencommunity -u 8000 -p password
 #useradd buenestudiante -u 3333 -p biendificil
 #useradd malestudiante -u 6666 -p refacilita
 
 
 * Haga que la validez de la cuenta de malestudiante se bloque en un mes.
 
     #chage -M 30 malestudiante
 
 * Permita que buenestudiante (y solo buenestudiante) tenga acceso completo al directorio de inicio (home) de OpenCommunity.
     
     #setfacl -m u:buenestudiante:rwx /home/opencommunity/

* Crea un directorio llamado /patodos. Permita que buenestudiante, malestudiante y OpenCommunity compartan documentos en el directorio /patodos usando un grupo llamado OpenCommunityGroup. 
    
     #usermod buenestudiante -aG opencommunity
     #usermod malestudiante -aG opencommunity
     #setfacl -m g:opencommunity:rwx /patodos
     

* Todos pueden leer, escribir y eliminar documentos del otro en este directorio, pero ningún usuario que no sea miembro del grupo puede hacerlo.

     #chmod 700 /patodos
     
* Crea un catálogo en /home llamado hackaton. Se solicita a su grupo respectivo que sea el grupo de opencommuity. Los usuarios del grupo pueden leer y escribir, mientras que otros usuarios no pueden
     
     #mkdir /home/hackaton
     #chown :opencommunity /home/hackaton
     #chmod 760 /home/hackaton
     
* Busque los archivos propiedad de OpenCommunity y cópielos al catálogo: /opt/dir
     
     #find . -group opencommunity -exec cp -Rf {} /opt/dir \;



     
     
     
     
     
     
     
     
     
     
     
     
     
     
     
     
     
     
     







