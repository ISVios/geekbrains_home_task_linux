# Home Tasks

## На виртуальной машине

```bash
virt@virtubserver:~$ 
```

Создать пользователя в ручном режиме.

 1. дописать файл `/etc/group`
 1. дописать файл `/etc/passwd`
 1. дописать файл `/etc/shadow`
 1. скопировать в `/etc/skel` в `/home/$USER`
 1. установить права на корневую папку

|group name|guests|
|:--:|:--:|
|GID|2123|

- Группа `guests`

```bash
root@virtubserver:/home/virt# echo "guests:x:2123:" >> /etc/group
root@virtubserver:/home/virt# tail -1 /etc/group
guests:x:2123:
root@virtubserver:/home/virt# 
```

|user name| guest01|
|:--:|:--:|
|UID|2123|
|GID|2123|
|info|for guests|
|~|`\home\guests\guest01`|
|shell|`\bin\bash`|

- Пользователь `guest01`

```bash
root@virtubserver:/home/virt# echo "guest01:x:2123:2123:for guests:/home/guests/guest01:/bin/bash" >> /etc/passwd
root@virtubserver:/home/virt# tail -1 /etc/passwd
guest01:x:2123:2123:for guests:/home/guests/guest01:/bin/bash
root@virtubserver:/home/virt# mkdir -p /home/guests/guest01
root@virtubserver:/home/virt# ls -la /home/
total 16
drwxr-xr-x  4 root root 4096 Jan 18 21:00 .
drwxr-xr-x 20 root root 4096 Jan 18 21:00 ..
drwxr-xr-x  3 root root 4096 Jan 18 21:00 guests
drwxr-xr-x  8 virt virt 4096 Jan 18 20:43 virt
root@virtubserver:/home/virt# cp /etc/skel/.bashrc /home/guests/guest01/
root@virtubserver:/home/virt# cp /etc/skel/.bash_logout /home/guests/guest01/
root@virtubserver:/home/virt# cp /etc/skel/.profile /home/guests/guest01/
root@virtubserver:/home/virt# chown -R guest01:guests /home/guests/
root@virtubserver:/home/virt# ls -la /home/
total 16
drwxr-xr-x  4 root    root   4096 Jan 18 21:00 .
drwxr-xr-x 20 root    root   4096 Jan 18 21:00 ..
drwxr-xr-x  3 guest01 guests 4096 Jan 18 21:00 guests
drwxr-xr-x  8 virt    virt   4096 Jan 18 20:43 virt
root@virtubserver:/home/virt# echo "guest01:!:2123:0:99999:7:::" >> /etc/shadow
root@virtubserver:/home/virt# tail -1 /etc/shadow
guest01:!:19005:0:99999:7:::
root@virtubserver:/home/virt#
```

## Результат

```bash
virt@virtubserver:~$ su guest01
Password: 
su: Authentication failure
virt@virtubserver:~$ 
virt@virtubserver:~$ sudo tail -1 /etc/shadow
virt@virtubserver:~$ sudo tail -1 /etc/shadow
guest01:*:19005:0:99999:7:::
virt@virtubserver:~$ 
virt@virtubserver:~$ su guest01
Password: 
su: Authentication failure
virt@virtubserver:~$ sudo tail -1 /etc/shadow
guest01::19005:0:99999:7:::
virt@virtubserver:~$ su guest01
guest01@virtubserver:/home/virt$ passwd 
New password: 
Retype new password: 
passwd: password updated successfully
guest01@virtubserver:/home/virt$ # ^d
virt@virtubserver:~$ sudo tail -1 /etc/shadow
guest01:$6$ofeFtyj0c/A3ctoV$FESBZ6I1NU5fhVZvVtgRCuOfgQZToVcU1H9cQBLxbUNmd5JMTSThScD0T0ceBNkSHyOmarNvKxlRnBKpMRxgu/:19010:0:99999:7:::
virt@virtubserver:~$ su - guest01
Password: 
guest01@virtubserver:~$ pwd
/home/guests/guest01
guest01@virtubserver:~$ id
uid=2123(guest01) gid=2123(guests) groups=2123(guests)
guest01@virtubserver:~$ 
```

## Создадим пользователя через `useradd`

|user name| guest02|
|:--:|:--:|
|UID|2111|
|GID|2111 and 2123|
|info|for guests|
|~|`\home\guests\guest02`|
|shell|`\bin\bash`|


```bash
virt@virtubserver:~$ sudo useradd -c "for guests" -d /home/guests/guest02/  -G guests -m guest02 -u 2111 -s /bin/bash 
virt@virtubserver:~$ tail -1 /etc/passwd
guest02:x:2111:2111:for guests:/home/guests/guest02/:/bin/bash
virt@virtubserver:~$ tail -2 /etc/group
guests:x:2123:guest0
guest02:x:2111:
virt@virtubserver:~$ sudo tail -1 /etc/shadow
guest02::19011:0:99999:7:::
virt@virtubserver:~$ su - guest02
Password: 
guest02@virtubserver:~$ pwd
/home/guests/guest02/
guest02@virtubserver:~$ id
uid=2111(guest02) gid=2111(guest02) groups=2111(guest02),2123(guests)
guest02@virtubserver:~$ logout
virt@virtubserver:~$ 

```

## Создадим группу через `groupadd` и `addgroup`

|group name|spotguest|
|:--:|:--:|
|GID|5555|

```bash
virt@virtubserver:~$ sudo groupadd -g 5555 spotguest
virt@virtubserver:~$ tail -1 /etc/group
spotguest:x:5555:
virt@virtubserver:~$
```

|group name|blockguest|
|:--:|:--:|
|GID|4444|

```bash
virt@virtubserver:~$ sudo addgroup --gid 4444  blockguest
Adding group `devguest' (GID 4444) ...
Done.
virt@virtubserver:~$ sudo tail -1 /etc/group
devguest:x:4444:
virt@virtubserver:~$ # 
```

```bash
virt@virtubserver:~$ sudo adduser guest03
Adding user `guest03' ...
Adding new group `guest03' (1001) ...
Adding new user `guest03' (1001) with group `guest03' ...
Creating home directory `/home/guest03' ...
Copying files from `/etc/skel' ...
New password: 
Retype new password: 
passwd: password updated successfully
Changing the user information for guest03
Enter the new value, or press ENTER for the default
        Full Name []: Some
        Room Number []: 
        Work Phone []: 
        Home Phone []: 
        Other []: 
Is the information correct? [Y/n] Y
virt@virtubserver:~$ sudo tail -1 /etc/passwd
guest03:x:1001:1001:Some,,,:/home/guest03:/bin/bash
virt@virtubserver:~$ 
```

## Назначим впользователю `guest01` группу `devguest` как основную

```bash
virt@virtubserver:~$ sudo usermod -G devguest guest01
virt@virtubserver:~$ groups guest01
guest01 : devguest
virt@virtubserver:~$
```

## Удалим группу `guests` у пользователя `guest02`

```bash
virt@virtubserver:~$ groups guest02
guest02 : guest02 guests
virt@virtubserver:~$ sudo deluser guest02 guests
Removing user `guest02' from group `guests' ...
Done.
virt@virtubserver:~$ groups guest02
guest02 : guest02
virt@virtubserver:~$ 
```

## Добавим пользователя `guest03` в группу `guests`

```bash
virt@virtubserver:~$ groups guest03
guest03 : guest03
virt@virtubserver:~$ sudo usermod -aG guests guest03
virt@virtubserver:~$ groups guest03
guest03 : guest03 guests
virt@virtubserver:~$
```

## Дадим пользователя `guest02` права на `sudo`

```sudoers
guest01 ALL (ALL:ALL) NOPASSWD:ALL
```

## Дадим пользователю `guest02` право на `reboot`

```sudoers
guest02 ALL (ALL:ALL) NOPASSWD:/usr/sbin/reboot, /usr/sbin/init 6
```

## Дадим право группе  `devguest` на `apt`

```sudoers
%devguest ALL=(ALL) NOPASSWD:/usr/bin/apt update
```

