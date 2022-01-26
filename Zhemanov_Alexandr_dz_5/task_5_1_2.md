# Task 1 and 2

## Task 1

- Создать файл file1 и наполнить его произвольным содержимым.
Скопировать его в file2.
Создать символическую ссылку file3 на file1.
Создать жёсткую ссылку file4 на file1.
Посмотреть, какие inode у файлов. Удалить file1.
Что стало с остальными созданными файлами? Попробовать вывести их на экран.

### На виртуальной машине

```bash
virt@virtubserver:~$ cat /dev/random | head -100 > file1
virt@virtubserver:~$ ls
file1
virt@virtubserver:~$ cat file1 | wc -l
100
virt@virtubserver:~$
virt@virtubserver:~$ cat file1 > file2; # or cp file1 file2
virt@virtubserver:~$ ls
file1  file2
virt@virtubserver:~$ 
virt@virtubserver:~$ ln -s file1 file3
virt@virtubserver:~$ ln file1 file4
virt@virtubserver:~$ ls -lia file*
3285 -rw-rw-r-- 2 virt virt 23186 Jan 26 15:40 file1
3127 -rw-rw-r-- 1 virt virt 23186 Jan 26 15:43 file2
3146 lrwxrwxrwx 1 virt virt     5 Jan 26 15:44 file3 -> file1
3285 -rw-rw-r-- 2 virt virt 23186 Jan 26 15:40 file4
virt@virtubserver:~$ 
virt@virtubserver:~$ wc file3 -l
100 file3
virt@virtubserver:~$ rm file1
virt@virtubserver:~$ wc file3 -l
wc: file3: No such file or directory
virt@virtubserver:~$ wc file4 -l
100 file4
virt@virtubserver:~$ ls -lia file*
3127 -rw-rw-r-- 1 virt virt 23186 Jan 26 15:43 file2
3146 lrwxrwxrwx 1 virt virt     5 Jan 26 15:44 file3 -> file1
3285 -rw-rw-r-- 1 virt virt 23186 Jan 26 15:40 file4
virt@virtubserver:~$ 
```

## Task 2

- Дать созданным файлам другие, произвольные имена.
Создать новую символическую ссылку. Переместить ссылки в другую директорию.

```bash
virt@virtubserver:~$ cat /dev/random | head -100 > config_file
virt@virtubserver:~$ mv file2 backup
virt@virtubserver:~$ mv file4 hard_link
virt@virtubserver:~$ ln -s config_file symbol_link 
virt@virtubserver:~$ mv *_link somefolder/
virt@virtubserver:~$ cd somefolder/
virt@virtubserver:~/somefolder$ ls -la
total 32
drwxrwxr-x 2 virt virt  4096 Jan 26 16:09 .
drwxr-xr-x 9 virt virt  4096 Jan 26 16:09 ..
-rw-rw-r-- 1 virt virt 23186 Jan 26 15:40 hard_link
lrwxrwxrwx 1 virt virt    11 Jan 26 16:04 symbol_link -> config_file
virt@virtubserver:~/somefolder$ wc hard_link -l
100 hard_link
virt@virtubserver:~/somefolder$ wc symbol_link -l
wc: symbol_link: No such file or directory
virt@virtubserver:~/somefolder$ 
```

Для корректной работы символьными с
ссылками необходимо использовать `абсолютный путь`:

```bash
virt@virtubserver:~$ ln -s ${PWD}/config_file correct_symbol_link
virt@virtubserver:~$ wc correct_symbol_link -l
100 correct_symbol_link
virt@virtubserver:~$ mv correct_symbol_link somefolder/
virt@virtubserver:~$ cd somefolder/
virt@virtubserver:~/somefolder$ wc correct_symbol_link -l
100 correct_symbol_link
virt@virtubserver:~/somefolder$ ls -la correct_symbol_link 
lrwxrwxrwx 1 virt virt 22 Jan 26 16:16 correct_symbol_link -> /home/virt/config_file
virt@virtubserver:~/somefolder$ 
```

