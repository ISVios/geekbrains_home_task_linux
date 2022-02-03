# Task 1

- Подключить репозиторий с nginx любым удобным способом,
 установить nginx и потом удалить nginx, используя утилиту dpkg.

Добавляем репозиторий `https://nginx.org/packages/ubuntu/`:

```bash
virt@virtubserver:~$ sudo vim /etc/apt/sources.list
virt@virtubserver:~$ sudo grep "nginx" /etc/apt/sources.list
deb https://nginx.org/packages/ubuntu/ focal nginx
deb-src https://nginx.org/packages/ubuntu/ focal nginx
virt@virtubserver:~$ sudo apt update
Hit:1 http://ru.archive.ubuntu.com/ubuntu focal InRelease
Hit:2 http://ru.archive.ubuntu.com/ubuntu focal-updates InRelease
Hit:3 http://ru.archive.ubuntu.com/ubuntu focal-backports InRelease
Hit:4 http://ru.archive.ubuntu.com/ubuntu focal-security InRelease
Get:5 https://nginx.org/packages/ubuntu focal InRelease [3,584 B] 
Err:5 https://nginx.org/packages/ubuntu focal InRelease
  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY ABF5BD827BD9BF62
Reading package lists... Done
W: GPG error: https://nginx.org/packages/ubuntu focal InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY ABF5BD827BD9BF62
E: The repository 'https://nginx.org/packages/ubuntu focal InRelease' is not signed.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
virt@virtubserver:~$ sudo grep /etc/apt/sources.list nginx
grep: nginx: No such file or directory
virt@virtubserver:~$  
```

Добавим недостающий ключ:

```bash
virt@virtubserver:~$ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys ABF5BD827BD9BF62
Executing: /tmp/apt-key-gpghome.xolGeR8cEa/gpg.1.sh --keyserver keyserver.ubuntu.com --recv-keys ABF5BD827BD9BF62
gpg: key ABF5BD827BD9BF62: public key "nginx signing key <signing-key@nginx.com>" imported
gpg: Total number processed: 1
gpg:               imported: 1
virt@virtubserver:~$ 
```

```bash
virt@virtubserver:~$ sudo apt update
Hit:1 http://ru.archive.ubuntu.com/ubuntu focal InRelease
Hit:2 http://ru.archive.ubuntu.com/ubuntu focal-updates InRelease
Hit:3 http://ru.archive.ubuntu.com/ubuntu focal-backports InRelease
Hit:4 http://ru.archive.ubuntu.com/ubuntu focal-security InRelease
Get:5 https://nginx.org/packages/ubuntu focal InRelease [3,584 B]
Get:6 https://nginx.org/packages/ubuntu focal/nginx Sources [9,696 B]
Get:7 https://nginx.org/packages/ubuntu focal/nginx amd64 Packages [15.7 kB]
Fetched 29.0 kB in 1s (36.8 kB/s)     
Reading package lists... Done
Building dependency tree       
Reading state information... Done
5 packages can be upgraded. Run 'apt list --upgradable' to see them.
virt@virtubserver:~$ 
```

Скачаем пакет:

```bash
virt@virtubserver:~$ sudo apt download nginx
Get:1 https://nginx.org/packages/ubuntu focal/nginx amd64 nginx amd64 1.20.2-1~focal [879 kB]
Fetched 879 kB in 1s (895 kB/s)
W: Download is performed unsandboxed as root as file '/home/virt/nginx_1.20.2-1~focal_amd64.deb' couldn't be accessed by user '_apt'. - pkgAcquire::Run (13: Permission denied)
virt@virtubserver:~$ ls
nginx_1.20.2-1~focal_amd64.deb  snap
virt@virtubserver:~$ 
```

Установим пакет через `dpkg`:

```bash
virt@virtubserver:~$ sudo dpkg -i nginx_1.20.2-1~focal_amd64.deb 
Selecting previously unselected package nginx.
(Reading database ... 153346 files and directories currently installed.)
Preparing to unpack nginx_1.20.2-1~focal_amd64.deb ...
----------------------------------------------------------------------

Thanks for using nginx!

Please find the official documentation for nginx here:
* https://nginx.org/en/docs/

Please subscribe to nginx-announce mailing list to get
the most important news about nginx:
* https://nginx.org/en/support.html

Commercial subscriptions for nginx are available on:
* https://nginx.com/products/

----------------------------------------------------------------------
Unpacking nginx (1.20.2-1~focal) ...
Setting up nginx (1.20.2-1~focal) ...
Created symlink /etc/systemd/system/multi-user.target.wants/nginx.service → /lib/systemd/system/nginx.service.
Processing triggers for systemd (245.4-4ubuntu3.15) ...
Processing triggers for man-db (2.9.1-1) ...
virt@virtubserver:~$
```

Проверяем:

```bash
virt@virtubserver:~$ sudo apt-cache policy nginx
nginx:
  Installed: 1.20.2-1~focal
  Candidate: 1.20.2-1~focal
  Version table:
 *** 1.20.2-1~focal 500
        500 https://nginx.org/packages/ubuntu focal/nginx amd64 Packages
        100 /var/lib/dpkg/status
     1.20.1-1~focal 500
        500 https://nginx.org/packages/ubuntu focal/nginx amd64 Packages
     1.20.0-1~focal 500
        500 https://nginx.org/packages/ubuntu focal/nginx amd64 Packages
     1.18.0-2~focal 500
        500 https://nginx.org/packages/ubuntu focal/nginx amd64 Packages
     1.18.0-1~focal 500
        500 https://nginx.org/packages/ubuntu focal/nginx amd64 Packages
     1.18.0-0ubuntu1.2 500
        500 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 Packages
        500 http://ru.archive.ubuntu.com/ubuntu focal-security/main amd64 Packages
     1.17.10-0ubuntu1 500
        500 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 Packages
virt@virtubserver:~$ dpkg -l | grep nginx
ii  nginx                                1.20.2-1~focal                        amd64        high performance web server
virt@virtubserver:~$ 
```

Удаление:

```bash
virt@virtubserver:~$ sudo dpkg -P nginx
[sudo] password for virt: 
(Reading database ... 153379 files and directories currently installed.)
Removing nginx (1.20.2-1~focal) ...
Purging configuration files for nginx (1.20.2-1~focal) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for systemd (245.4-4ubuntu3.15) ...
virt@virtubserver:~$
```

Проверяем:

```bash
virt@virtubserver:~$ dpkg -l | grep nginx
virt@virtubserver:~$ sudo apt-cache policy nginx
nginx:
  Installed: (none)
  Candidate: 1.20.2-1~focal
  Version table:
     1.20.2-1~focal 500
        500 https://nginx.org/packages/ubuntu focal/nginx amd64 Packages
     1.20.1-1~focal 500
        500 https://nginx.org/packages/ubuntu focal/nginx amd64 Packages
     1.20.0-1~focal 500
        500 https://nginx.org/packages/ubuntu focal/nginx amd64 Packages
     1.18.0-2~focal 500
        500 https://nginx.org/packages/ubuntu focal/nginx amd64 Packages
     1.18.0-1~focal 500
        500 https://nginx.org/packages/ubuntu focal/nginx amd64 Packages
     1.18.0-0ubuntu1.2 500
        500 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 Packages
        500 http://ru.archive.ubuntu.com/ubuntu focal-security/main amd64 Packages
     1.17.10-0ubuntu1 500
        500 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 Packages
virt@virtubserver:~$
```

