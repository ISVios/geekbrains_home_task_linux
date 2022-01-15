# Task 1

## Перемещение в файловой системе Linux

После авторизации:

```bash
virt@virt-server:~$
```

Где:

|virt|имя пользователя|
|:---:|:--:|
|virt-server|имя машины|
|~|текущий путь в файловой системе<br>`~` -> синоним /home/virt/|
|$|"приглашение" для ввода комманд|

Для перемешения используется команда `cd` *(change directory)*

Используем *абсолютный* путь:

```bash
virt@virt-server:~$ cd /
virt@virt-server:/$
virt@virt-server:/$ cd /home/virt
virt@virt-server:~$
virt@virt-server:~$ cd /home
virt@virt-server:/home$
```

Используем *относительный* путь:

```bash
virt@virt-server:/home$ cd ./virt
virt@virt-server:~$
```

Используем `..` для выхода из текущий папки:

```bash
virt@virt-server:~$ cd ..
virt@virt-server:/home$
```

Подтвердим что `~ == \home\virt` с помощью команды `pwd`,
которая показывает текущий путь в файловой системе:

```bash
virt@virt-server:~$ pwd
/home/virt
virt@virt-server:~$
```
