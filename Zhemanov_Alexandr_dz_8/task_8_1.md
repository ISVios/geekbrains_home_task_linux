# Tasks 1 and 2

## Task 1

- Запустить контейнер с Ubuntu.

```bash
virt@virtubserver:~$ sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common -y
[sudo] password for virt: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
ca-certificates is already the newest version (20210119~20.04.2).
ca-certificates set to manually installed.
curl is already the newest version (7.68.0-1ubuntu2.7).
curl set to manually installed.
software-properties-common is already the newest version (0.99.9.8).
software-properties-common set to manually installed.
The following packages were automatically installed and are no longer required:
  linux-headers-5.4.0-94 linux-headers-5.4.0-94-generic linux-image-5.4.0-94-generic linux-modules-5.4.0-94-generic
  linux-modules-extra-5.4.0-94-generic
Use 'sudo apt autoremove' to remove them.
The following NEW packages will be installed:
  apt-transport-https gnupg-agent
0 upgraded, 2 newly installed, 0 to remove and 5 not upgraded.
Need to get 9,912 B of archives.
After this operation, 208 kB of additional disk space will be used.
Get:1 http://ru.archive.ubuntu.com/ubuntu focal-updates/universe amd64 apt-transport-https all 2.0.6 [4,680 B]
Get:2 http://ru.archive.ubuntu.com/ubuntu focal-updates/universe amd64 gnupg-agent all 2.2.19-3ubuntu2.1 [5,232 B]
Fetched 9,912 B in 5s (1,939 B/s) 
Selecting previously unselected package apt-transport-https.
(Reading database ... 153346 files and directories currently installed.)
Preparing to unpack .../apt-transport-https_2.0.6_all.deb ...
Unpacking apt-transport-https (2.0.6) ...
Selecting previously unselected package gnupg-agent.
Preparing to unpack .../gnupg-agent_2.2.19-3ubuntu2.1_all.deb ...
Unpacking gnupg-agent (2.2.19-3ubuntu2.1) ...
Setting up apt-transport-https (2.0.6) ...
Setting up gnupg-agent (2.2.19-3ubuntu2.1) ...
virt@virtubserver:~$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
E: This command can only be used by root.
(23) Failed writing body
virt@virtubserver:~$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
OK
virt@virtubserver:~$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
Hit:1 http://ru.archive.ubuntu.com/ubuntu focal InRelease
Get:2 http://ru.archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]                   
Get:3 http://ru.archive.ubuntu.com/ubuntu focal-backports InRelease [108 kB]                                          
Get:4 http://ru.archive.ubuntu.com/ubuntu focal-security InRelease [114 kB]                                           
Get:5 https://download.docker.com/linux/ubuntu focal InRelease [57.7 kB]                         
Hit:6 https://nginx.org/packages/ubuntu focal InRelease                      
Get:7 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 Packages [1,550 kB]
Get:8 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages [13.5 kB]
Get:9 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 c-n-f Metadata [14.7 kB]
Get:10 http://ru.archive.ubuntu.com/ubuntu focal-updates/universe amd64 Packages [896 kB]
Get:11 http://ru.archive.ubuntu.com/ubuntu focal-updates/universe amd64 c-n-f Metadata [20.0 kB]
Get:12 http://ru.archive.ubuntu.com/ubuntu focal-security/main amd64 Packages [1,210 kB]
Get:13 http://ru.archive.ubuntu.com/ubuntu focal-security/main amd64 c-n-f Metadata [9,136 B]
Get:14 http://ru.archive.ubuntu.com/ubuntu focal-security/universe amd64 Packages [676 kB]
Get:15 http://ru.archive.ubuntu.com/ubuntu focal-security/universe amd64 c-n-f Metadata [13.0 kB]
Fetched 4,796 kB in 2s (2,853 kB/s)                                
Reading package lists... Done
virt@virtubserver:~$ sudo apt install docker docker-compose
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  linux-headers-5.4.0-94 linux-headers-5.4.0-94-generic linux-image-5.4.0-94-generic linux-modules-5.4.0-94-generic
  linux-modules-extra-5.4.0-94-generic
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  bridge-utils containerd docker.io pigz python3-cached-property python3-docker python3-dockerpty python3-docopt
  python3-texttable python3-websocket runc ubuntu-fan wmdocker
Suggested packages:
  ifupdown aufs-tools cgroupfs-mount | cgroup-lite debootstrap docker-doc rinse zfs-fuse | zfsutils
The following NEW packages will be installed:
  bridge-utils containerd docker docker-compose docker.io pigz python3-cached-property python3-docker
  python3-dockerpty python3-docopt python3-texttable python3-websocket runc ubuntu-fan wmdocker
0 upgraded, 15 newly installed, 0 to remove and 6 not upgraded.
Need to get 74.4 MB of archives.
After this operation, 362 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 pigz amd64 2.4-1 [57.4 kB]
Get:2 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 bridge-utils amd64 1.6-2ubuntu1 [30.5 kB]
Get:3 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 runc amd64 1.0.1-0ubuntu2~20.04.1 [4,155 kB]
Get:4 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 containerd amd64 1.5.5-0ubuntu3~20.04.1 [33.0 MB]
Get:5 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 wmdocker amd64 1.5-2 [13.0 kB]                         
Get:6 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 docker all 1.5-2 [1,316 B]                             
Get:7 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 python3-cached-property all 1.5.1-4 [10.9 kB]          
Get:8 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 python3-websocket all 0.53.0-2ubuntu1 [32.3 kB]        
Get:9 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 python3-docker all 4.1.0-1 [83.8 kB]                   
Get:10 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 python3-dockerpty all 0.4.1-2 [11.1 kB]               
Get:11 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 python3-docopt all 0.6.2-2.2ubuntu1 [19.7 kB]         
Get:12 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 python3-texttable all 1.6.2-2 [11.0 kB]               
Get:13 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 docker-compose all 1.25.0-1 [92.7 kB]                 
Get:14 http://ru.archive.ubuntu.com/ubuntu focal-updates/universe amd64 docker.io amd64 20.10.7-0ubuntu5~20.04.2 [36.9 MB]
Get:15 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 ubuntu-fan all 0.12.13 [34.5 kB]                          
Fetched 74.4 MB in 23s (3,300 kB/s)                                                                                   
Preconfiguring packages ...
Selecting previously unselected package pigz.
(Reading database ... 153354 files and directories currently installed.)
Preparing to unpack .../00-pigz_2.4-1_amd64.deb ...
Unpacking pigz (2.4-1) ...
Selecting previously unselected package bridge-utils.
Preparing to unpack .../01-bridge-utils_1.6-2ubuntu1_amd64.deb ...
Unpacking bridge-utils (1.6-2ubuntu1) ...
Selecting previously unselected package runc.
Preparing to unpack .../02-runc_1.0.1-0ubuntu2~20.04.1_amd64.deb ...
Unpacking runc (1.0.1-0ubuntu2~20.04.1) ...
Selecting previously unselected package containerd.
Preparing to unpack .../03-containerd_1.5.5-0ubuntu3~20.04.1_amd64.deb ...
Unpacking containerd (1.5.5-0ubuntu3~20.04.1) ...
Selecting previously unselected package wmdocker.
Preparing to unpack .../04-wmdocker_1.5-2_amd64.deb ...
Unpacking wmdocker (1.5-2) ...
Selecting previously unselected package docker.
Preparing to unpack .../05-docker_1.5-2_all.deb ...
Unpacking docker (1.5-2) ...
Selecting previously unselected package python3-cached-property.
Preparing to unpack .../06-python3-cached-property_1.5.1-4_all.deb ...
Unpacking python3-cached-property (1.5.1-4) ...
Selecting previously unselected package python3-websocket.
Preparing to unpack .../07-python3-websocket_0.53.0-2ubuntu1_all.deb ...
Unpacking python3-websocket (0.53.0-2ubuntu1) ...
Selecting previously unselected package python3-docker.
Preparing to unpack .../08-python3-docker_4.1.0-1_all.deb ...
Unpacking python3-docker (4.1.0-1) ...
Selecting previously unselected package python3-dockerpty.
Preparing to unpack .../09-python3-dockerpty_0.4.1-2_all.deb ...
Unpacking python3-dockerpty (0.4.1-2) ...
Selecting previously unselected package python3-docopt.
Preparing to unpack .../10-python3-docopt_0.6.2-2.2ubuntu1_all.deb ...
Unpacking python3-docopt (0.6.2-2.2ubuntu1) ...
Selecting previously unselected package python3-texttable.
Preparing to unpack .../11-python3-texttable_1.6.2-2_all.deb ...
Unpacking python3-texttable (1.6.2-2) ...
Selecting previously unselected package docker-compose.
Preparing to unpack .../12-docker-compose_1.25.0-1_all.deb ...
Unpacking docker-compose (1.25.0-1) ...
Selecting previously unselected package docker.io.
Preparing to unpack .../13-docker.io_20.10.7-0ubuntu5~20.04.2_amd64.deb ...
Unpacking docker.io (20.10.7-0ubuntu5~20.04.2) ...
Selecting previously unselected package ubuntu-fan.
Preparing to unpack .../14-ubuntu-fan_0.12.13_all.deb ...
Unpacking ubuntu-fan (0.12.13) ...
Setting up python3-cached-property (1.5.1-4) ...
Setting up python3-texttable (1.6.2-2) ...
Setting up python3-docopt (0.6.2-2.2ubuntu1) ...
Setting up wmdocker (1.5-2) ...
Setting up runc (1.0.1-0ubuntu2~20.04.1) ...
Setting up bridge-utils (1.6-2ubuntu1) ...
Setting up pigz (2.4-1) ...
Setting up containerd (1.5.5-0ubuntu3~20.04.1) ...
Created symlink /etc/systemd/system/multi-user.target.wants/containerd.service → /lib/systemd/system/containerd.service.
Setting up python3-websocket (0.53.0-2ubuntu1) ...
update-alternatives: using /usr/bin/python3-wsdump to provide /usr/bin/wsdump (wsdump) in auto mode
Setting up python3-dockerpty (0.4.1-2) ...
Setting up docker (1.5-2) ...
Setting up ubuntu-fan (0.12.13) ...
Created symlink /etc/systemd/system/multi-user.target.wants/ubuntu-fan.service → /lib/systemd/system/ubuntu-fan.service.
Setting up python3-docker (4.1.0-1) ...
Setting up docker.io (20.10.7-0ubuntu5~20.04.2) ...
Adding group `docker' (GID 123) ...
Done.
Created symlink /etc/systemd/system/multi-user.target.wants/docker.service → /lib/systemd/system/docker.service.
Created symlink /etc/systemd/system/sockets.target.wants/docker.socket → /lib/systemd/system/docker.socket.
Setting up docker-compose (1.25.0-1) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for systemd (245.4-4ubuntu3.15) ...
virt@virtubserver:~$ 
```

Утанавливаем/Запускаем контейнер "ubuntu"


```bash
virt@virtubserver:~$ sudo docker run -it ubuntu
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
08c01a0ec47e: Pull complete 
Digest: sha256:669e010b58baf5beb2836b253c1fd5768333f0d1dbcb834f7c07a4dc93f474be
Status: Downloaded newer image for ubuntu:latest
root@ed32d522fb86:/# uname -a
Linux ed32d522fb86 5.4.0-97-generic #110-Ubuntu SMP Thu Jan 13 18:22:13 UTC 2022 x86_64 x86_64 x86_64 GNU/Linux
root@ed32d522fb86:/# cat /etc/lsb-release 
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=20.04
DISTRIB_CODENAME=focal
DISTRIB_DESCRIPTION="Ubuntu 20.04.3 LTS"
root@ed32d522fb86:/# exit
virt@virtubserver:~$ 
```

## Task 2

- Используя Dockerfile, собрать связку nginx + PHP-FPM в одном контейнере.


```dockerfile
FROM ubuntu:latest
MAINTAINER Zhemanov Alex

EXPOSE 80 80

VOLUME "/var/www/html" 

RUN apt update #&& apt upgrade -y
RUN apt-get install nginx php7.4 php7.4-cli php7.4-fpm php7.4-json php7.4-pdo php7.4-mysql php7.4-zip php7.4-gd php7.4-mbstring php7.4-curl php7.4-xml php-pear php7.4-bcmath -y

RUN service php7.4-fpm stop
RUN service nginx stop

COPY docker.d/index.php /var/www/html/

COPY docker.d/.docker-config.sh /

CMD chmod +x /.docker-config.sh && /.docker-config.sh
```

Файл `docker.d/.docker-config.sh`:

```bash
#!/bin/bash


if [[ ! -f .build ]] ; then

  echo "build flag dont del" >>  .build

  cp /etc/php/7.4/fpm/pool.d/www.conf /etc/php/7.4/fpm/pool.d/www.conf.back
  cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default.back

  sed -i 's/\;cgi.fix_pathinfo=[0-9]/cgi.fix_pathinfo=0/' /etc/php/7.4/fpm/php.ini
  service php7.4-fpm restart

  sed -i "s/index index.html index.htm index.nginx-debian.html\;/index index.php index.html index.htm index.nginx-debian.htmli\; /" /etc/nginx/sites-available/default
  sed -i "s/#location\s~\s[\].php[$]\s{/location ~ \.php { include snippets\/fastcgi-php.conf\; fastcgi_pass unix\:\/run\/php\/php7.4-fpm.sock\; \}/" /etc/nginx/sites-available/default

fi

service php7.4-fpm restart

nginx -t

php-fpm7.4 -t

nginx -g "daemon off;"
```

Файл `docker.d/index.php`:

```php
<?php echo "<h1> NGINX + FMP </h1><br><h2>OK</h2>" ?>

```

Результат:

```bash
virt@virtubserver:~/nginx_fpm$ docker build -t dz:latest .
Sending build context to Docker daemon   5.12kB
Step 1/11 : FROM ubuntu:latest
 ---> 54c9d81cbb44
Step 2/11 : MAINTAINER Zhemanov Alex
 ---> Using cache
 ---> 707fe1b428d3
Step 3/11 : EXPOSE 80 80
 ---> Using cache
 ---> c9e1b576ba09
Step 4/11 : VOLUME "/var/www/html"
 ---> Using cache
 ---> f660bdedd5f6
Step 5/11 : RUN apt update #&& apt upgrade -y
 ---> Using cache
 ---> 322bcc95dd90
Step 6/11 : RUN apt-get install nginx php7.4 php7.4-cli php7.4-fpm php7.4-json php7.4-pdo php7.4-mysql php7.4-zip php7.4-gd php7.4-mbstring php7.4-curl php7.4-xml php-pear php7.4-bcmath -y
 ---> Using cache
 ---> cd3feb8cd45e
Step 7/11 : RUN service php7.4-fpm stop
 ---> Using cache
 ---> 704ea35d771e
Step 8/11 : RUN service nginx stop
 ---> Using cache
 ---> f04ebfe04134
Step 9/11 : COPY docker.d/index.php /var/www/html/
 ---> Using cache
 ---> 21cce803e2c3
Step 10/11 : COPY docker.d/.docker-config.sh /
 ---> Using cache
 ---> 4d2b6db78b05
Step 11/11 : CMD chmod +x /.docker-config.sh && /.docker-config.sh
 ---> Using cache
 ---> b75127735a52
Successfully built b75127735a52
Successfully tagged dz:latest
virt@virtubserver:~/nginx_fpm$ docker run   -p 80:80   dz:latest #/bin/bashu
```

![result](./result.png)

