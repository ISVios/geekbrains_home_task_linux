# Task 3

## Создадим ключ.

### Основная машина

```bash
   ~  cat /etc/lsb-release                                                ✔ 
DISTRIB_ID=ManjaroLinux
DISTRIB_RELEASE=21.2.1
DISTRIB_CODENAME=Qonos
DISTRIB_DESCRIPTION="Manjaro Linux"

   ~  ssh-keygen -t rsa                                                1 ✘ 
Generating public/private rsa key pair.
Enter file in which to save the key (/home/****/.ssh/id_rsa): /home/****/.ssh/ubnt_cli
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/****/.ssh/ubnt_cli
Your public key has been saved in /home/****/.ssh/ubnt_cli.pub
The key fingerprint is:
SHA256:VF/Wk5l1m++b8kWWuCWW7q4JdebhgptKmyeMKH5ctpc ***@*********
The key's randomart image is:
+---[RSA 3072]----+
|          .   o.B|
|         . . o ==|
|        .   .  o.|
|       .      o o|
|        S  . O o+|
|     o    o B =+ |
|  . + +..o . =  o|
| . + o.Eo.+ +.  +|
|..o   .++o oooo+ |
+----[SHA256]-----+
    ~                                                         ✔  1m 58s  
```

### Загрузим ключ на Виртуалную машину

```bash
    ~  ssh-copy-id -i .ssh/ubnt_cli.pub virt@192.168.100.100       1 ✘ 
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: ".ssh/ubnt_cli.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
virt@192.168.100.100's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'virt@192.168.100.100'"
and check to make sure that only the key(s) you wanted were added.
```

### На вируальной машине

```bash
virt@virt-server:~$ ls .ssh/
authorized_keys
virt@virt-server:~$ 
virt@virt-server:~$ sudo vim /etc/ssh/sshd_config
virt@virt-server:~$ # chage PasswordAuthentication no
virt@virt-server:~$ # chage PubkeyAuthentication yes
virt@virt-server:~$ # chage PermitRootLogin no
[sudo] password for virt: 
virt@virt-server:~$ sudo service ssh restart 
virt@virt-server:~$ sudo service ssh status 
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabl>
     Active: active (running) since Sat 2022-01-15 20:08:31 UTC; 5s ago
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 2596 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
   Main PID: 2614 (sshd)
      Tasks: 1 (limit: 4612)
     Memory: 1.3M
     CGroup: /system.slice/ssh.service
             └─2614 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups

Jan 15 20:08:31 virt-server systemd[1]: Starting OpenBSD Secure Shell server...
Jan 15 20:08:31 virt-server sshd[2614]: Server listening on 0.0.0.0 port 22.
Jan 15 20:08:31 virt-server sshd[2614]: Server listening on :: port 22.
Jan 15 20:08:31 virt-server systemd[1]: Started OpenBSD Secure Shell server.
```

### Подключение

```bash
    ~  ssh virt@192.168.100.100                             ✔ 
virt@192.168.100.100: Permission denied (publickey).
    ~  ssh -i .ssh/ubnt_cli virt@192.168.100.100              ✔  1m 17s  
Enter passphrase for key '.ssh/ubnt_cli': 
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.4.0-94-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Sat 15 Jan 2022 08:12:35 PM UTC

  System load:  0.06               Processes:               153
  Usage of /:   44.0% of 10.09GB   Users logged in:         1
  Memory usage: 6%                 IPv4 address for enp1s0: 192.168.100.100
  Swap usage:   0%


0 updates can be applied immediately.


Last login: Sat Jan 15 20:10:46 2022 from 192.168.100.1
virt@virt-server:~$
```
