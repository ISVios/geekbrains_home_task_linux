# Tasks 4 5 and 6

## Task 4

- Создать группу developer и нескольких пользователей, входящих в неё.
Создать директорию для совместной работы.
Сделать так, чтобы созданные одними пользователями файлы могли изменять
другие пользователи этой группы.

Группа:

```bash
virt@virtubserver:/tmp$ sudo addgroup developer
[sudo] password for virt: 
Adding group `developer' (GID 1002) ...
Done.
virt@virtubserver:/tmp$  
```

Пользователи:

```bash
virt@virtubserver:/tmp$ sudo useradd -c "developer" -G developer -M develop_1 -u 3000 -s /bin/bash 
virt@virtubserver:/tmp$ sudo useradd -c "developer" -G developer -M develop_2 -u 3001 -s /bin/bash 
virt@virtubserver:/tmp$ sudo useradd -c "developer" -G developer -M develop_3 -u 3002 -s /bin/bash 
virt@virtubserver:/tmp$ cat /etc/group | tail -4
developer:x:1002:develop_1,develop_2,develop_3
develop_1:x:3000:
develop_2:x:3001:
develop_3:x:3002:
virt@virtubserver:/tmp$ cat /etc/passwd | tail -3
develop_1:x:3000:3000:developer:/home/develop_1:/bin/bash
develop_2:x:3001:3001:developer:/home/develop_2:/bin/bash
develop_3:x:3002:3002:developer:/home/develop_3:/bin/bash
virt@virtubserver:/tmp$ 
```

Обший каталог

```bash
virt@virtubserver:/tmp$ cd /opt
virt@virtubserver:/opt$ sudo mkdir prj
virt@virtubserver:/opt$ ls -dl prj/
drwxr-xr-x 2 root root 4096 Jan 26 17:38 prj/
virt@virtubserver:/opt$ sudo chown root:developer prj/
virt@virtubserver:/opt$ ls -dl prj/
drwxr-xr-x 2 root developer 4096 Jan 26 17:38 prj/
virt@virtubserver:/opt$ sudo chmod g=rwxs -R prj/
virt@virtubserver:/opt$ ls -dl prj/
drwxrwsr-x 2 root developer 4096 Jan 26 17:48 prj/
virt@virtubserver:/opt$ 
```

Результат:

```bash
virt@virtubserver:/opt$ sudo su develop_1
develop_1@virtubserver:/opt$ cd prj/
develop_1@virtubserver:/opt/prj$ echo "1234" > config
develop_1@virtubserver:/opt/prj$ ls -l config 
-rw-rw-r-- 1 develop_1 developer 5 Jan 26 17:55 config
develop_1@virtubserver:/opt/prj$ exit
virt@virtubserver:/opt$ sudo su develop_2
develop_2@virtubserver:/opt$ cd prj/
develop_2@virtubserver:/opt/prj$ vim config 
develop_2@virtubserver:/opt/prj$ echo "56789" >> config 
develop_2@virtubserver:/opt/prj$ exit
virt@virtubserver:/opt$ sudo su develop_3
develop_3@virtubserver:/opt$ cd prj/
develop_3@virtubserver:/opt/prj$ mv config trash_file
develop_3@virtubserver:/opt/prj$ ls
trash_file
develop_3@virtubserver:/opt/prj$ 
```

## Task 5

- Создать в директории для совместной работы поддиректорию для обмена файлами,
но чтобы удалять файлы могли только их создатели.

```bash
virt@virtubserver:/opt/prj$ sudo mkdir public
virt@virtubserver:/opt/prj$ sudo chown root:developer public/
virt@virtubserver:/opt/prj$ sudo chmod g+rw,+t public/
virt@virtubserver:/opt/prj$ 
```

Пользователь `develop_2`:

```bash
virt@virtubserver:/opt/prj$ sudo su develop_2
develop_2@virtubserver:/opt/prj$ cd public/
develop_2@virtubserver:/opt/prj/public$ echo "some del my config file" > todo
develop_2@virtubserver:/opt/prj/public$ exit
```

Пользователь `develop_1`:

```bash
virt@virtubserver:/opt/prj$ sudo su develop_1
develop_1@virtubserver:/opt/prj$ cd public/
develop_1@virtubserver:/opt/prj/public$ rm todo 
rm: cannot remove 'todo': Operation not permitted
develop_1@virtubserver:/opt/prj/public$ mv todo .todo 
mv: cannot move 'todo' to '.todo': Operation not permitted
develop_1@virtubserver:/opt/prj/public$ cp todo correct_todo
develop_1@virtubserver:/opt/prj/public$ echo "in Bagdat is all right" >> correct_todo 
develop_1@virtubserver:/opt/prj/public$ cat correct_todo 
some del my config file
in Bagdat is all right
develop_1@virtubserver:/opt/prj/public$ exit
```

Пользователь `develop_3`:

```bash
virt@virtubserver:/opt/prj$ sudo su develop_3
develop_3@virtubserver:/opt/prj$ cd public/
develop_3@virtubserver:/opt/prj/public$ rm *
rm: cannot remove 'correct_todo': Operation not permitted
rm: cannot remove 'todo': Operation not permitted
develop_3@virtubserver:/opt/prj/public$ cp correct_todo stop_make_stupid_file
develop_3@virtubserver:/opt/prj/public$ 
```

## Task 6

- Создать директорию, в которой есть несколько файлов.
Сделать так, чтобы открыть файлы можно было, только зная имя файла,
а через ls список файлов посмотреть было нельзя.

```bash
virt@virtubserver:/opt/prj$ sudo mkdir nomal_todo
virt@virtubserver:/opt/prj$ sudo chmod ugo-r+w nomal_todo/ 
virt@virtubserver:/opt/prj$ echo "normal todo" >  nomal_todo/pass_code_todo
virt@virtubserver:/opt/prj$ ls nomal_todo/
ls: cannot open directory 'nomal_todo/': Permission denied
virt@virtubserver:/opt/prj$ vim nomal_todo/pass_code_todo
virt@virtubserver:/opt/prj$ cat nomal_todo/pass_code_todo
normal todo

1. fix problem
2. check (1)
3. don`t say file name 
virt@virtubserver:/opt/prj$ 
virt@virtubserver:/opt/prj/nomal_todo$ ls
ls: cannot open directory '.': Permission denied
virt@virtubserver:/opt/prj/nomal_todo$ touch pass_code_config
virt@virtubserver:/opt/prj/nomal_todo$ vim pass_code_config
virt@virtubserver:/opt/prj/nomal_todo$ cat pass_code_config
disable=1
enable=0
virt@virtubserver:/opt/prj/nomal_todo$  
```


