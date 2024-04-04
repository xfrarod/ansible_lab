# ansible_lab

Los archivos en este repositorio fueron creados con proposito educativo para el Tecmilenio. Este laboratorio es el cierre del tema "Configuration Management" utilizando Ansible.

## Prerequisitos
1. Tener instalado VirtualBox 7.0
2. Tener instalado Docker Desktop version >= 4.26.X
2. Tener instalado Hashicorp Vagrant version >= 2.4.1

## Instrucciones para levantar el ambiente
1. Levantar las maquinas virtuales de VirtualBox con Vagrant

```shell
vagrant up
```

2. Validar las direcciones IP asignadas a cada una de las máquinas virtuales para actualizar el archivo hosts utilizando el comando:

```shell
vagrant ssh host1 -c ifconfig
```

_Output:_
```
vagrant ssh host1 -c ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.0.2.15  netmask 255.255.255.0  broadcast 10.0.2.255
        inet6 fe80::5054:ff:fe4d:77d3  prefixlen 64  scopeid 0x20<link>
        ether 52:54:00:4d:77:d3  txqueuelen 1000  (Ethernet)
        RX packets 31905  bytes 45893699 (43.7 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 5985  bytes 486964 (475.5 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.100.116  netmask 255.255.255.0  broadcast 192.168.100.255
        inet6 fe80::a00:27ff:fe7f:3f03  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:7f:3f:03  txqueuelen 1000  (Ethernet)
        RX packets 128  bytes 25918 (25.3 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 30  bytes 4536 (4.4 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
```
3. Actualizar el archivo hosts con las direcciones IP correspondientes
    [webservers]
    host1 ansible_host=**192.168.100.116** ansible_user=vagrant ansible_port=22 ansible_ssh_private_key_file=./.vagrant/machines/host1/virtualbox/private_key
    
    [dbservers]
    host2 ansible_host=**192.168.100.118** ansible_user=vagrant ansible_port=22 ansible_ssh_private_key_file=./.vagrant/machines/host2/virtualbox/private_key

4. Levantar el contenedor docker de ansible utilizando docker-compose

```shell
docker-compose up -d
```

5. Dado que las llaves privadas para la conexión ssh de los servidores es un mapeo de archivos en el contenedor de docker, es necesario cambiar los permisos para que no esten muy abiertos. 
> `chmod 400 /.vagrant/machines/host1/virtualbox/private_key`
> `chmod 400 /.vagrant/machines/host2/virtualbox/private_key`

6. Validar que el ambiente esta corriendo y ansible se puede comunicar a los nodos

```shell
ansible all -m ping
```