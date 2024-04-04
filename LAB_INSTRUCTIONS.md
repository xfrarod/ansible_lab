# Instrucciones del laboratorio
Una vez que tengas tu ambiente funcionando deberás crear un par de playbooks, uno para los webservers y otro para los dbservers. Los nodos son Centos7, por lo que deberás investigar los módulos que deberás utilizar para poder lograr hacer las instalaciones requeridas.

A continuación te muestro los requisitos y pasos para la instalación y configuración de cada uno de los roles, que deberás utilizar como guía para traducirlo y crear tus playbooks.

## 1. Crear un playbook para webservers
El playbook deberá instalar nginx, siguiendo los siguientes pasos:

### Step 1 — Adding the EPEL Software Repository
To add the CentOS 7 EPEL repository, first connect to your CentOS 7 machine via SSH, then use the yum command to install the extended package repository:
`$ sudo yum install epel-release`
You’ll be prompted to verify that you want to install the software. Type y then ENTER to continue.

### Step 2 — Installing Nginx
Now that the EPEL repository is installed on your server, install Nginx using the following yum command:
`$ sudo yum install nginx`
Again, answer yes to the verification prompt, then Nginx will finish installing.

### Step 3 — Starting Nginx
Nginx will not start automatically after it is installed. To get Nginx running, use the systemctl command:
`$ sudo systemctl start nginx`
You can check the status of the service with systemctl status:
`$ sudo systemctl status nginx`
```shell
[vagrant@host1 ~]$ sudo systemctl status nginx
● nginx.service - The nginx HTTP and reverse proxy server
   Loaded: loaded (/usr/lib/systemd/system/nginx.service; disabled; vendor preset: disabled)
   Active: active (running) since Thu 2024-04-04 00:11:44 UTC; 10s ago
  Process: 3542 ExecStart=/usr/sbin/nginx (code=exited, status=0/SUCCESS)
  Process: 3540 ExecStartPre=/usr/sbin/nginx -t (code=exited, status=0/SUCCESS)
  Process: 3539 ExecStartPre=/usr/bin/rm -f /run/nginx.pid (code=exited, status=0/SUCCESS)
 Main PID: 3544 (nginx)
   CGroup: /system.slice/nginx.service
           ├─3544 nginx: master process /usr/sbin/nginx
           └─3545 nginx: worker process

Apr 04 00:11:44 host1 systemd[1]: Starting The nginx HTTP and reverse proxy server...
Apr 04 00:11:44 host1 nginx[3540]: nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
Apr 04 00:11:44 host1 nginx[3540]: nginx: configuration file /etc/nginx/nginx.conf test is successful
Apr 04 00:11:44 host1 systemd[1]: Started The nginx HTTP and reverse proxy server.
```
### Step 4 — Check the URL is up and running
> http://server_domain_name_or_IP/

![nginx for CentOS](images/nginx_web.png)


## 2. Crear un playbook para dbservers



## Entrega
La entrega será a través de la plataforma de Canvas, y deberás subir cada uno de tus playbooks.