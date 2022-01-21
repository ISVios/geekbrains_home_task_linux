# Task 1

## На виртуальной машине

```bash
virt@virtubserver:~$
```

## Создадим файл, используя команду echo

```bash
virt@virtubserver:~$ ls
virt@virtubserver:~$ 
virt@virtubserver:~$ echo "" > echo_file
virt@virtubserver:~$ ls
echo_file
virt@virtubserver:~$ 
```

## Используя команду cat, прочитать содержимое каталога etc, ошибки перенаправить в отдельный файл

```bash
virt@virtubserver:~$ ls
echo_file
virt@virtubserver:~$ cat /etc/* 2> err_etc 1> ok_etc
virt@virtubserver:~$ ls
echo_file  err_etc  ok_etc
virt@virtubserver:~$ cat err_etc | head -10
cat: /etc/alternatives: Is a directory
cat: /etc/apparmor: Is a directory
cat: /etc/apparmor.d: Is a directory
cat: /etc/apport: Is a directory
cat: /etc/apt: Is a directory
cat: /etc/at.deny: Permission denied
cat: /etc/bash_completion.d: Is a directory
cat: /etc/binfmt.d: Is a directory
cat: /etc/byobu: Is a directory
cat: /etc/ca-certificates: Is a directory
virt@virtubserver:~$ cat ok_etc | head -10
# /etc/adduser.conf: `adduser' configuration.
# See adduser(8) and adduser.conf(5) for full documentation.

# The DSHELL variable specifies the default login shell on your
# system.
DSHELL=/bin/bash

# The DHOME variable specifies the directory containing users' home
# directories.
DHOME=/home
virt@virtubserver:~$ 
```
