# Task 3

- Создать два произвольных файла.
Первому присвоить права на чтение и запись для владельца и группы,
только на чтение — для всех.
Второму присвоить права на чтение и запись только для владельца.
Сделать это в численном и символьном виде.

```bash
virt@virtubserver:/tmp$ cat /dev/random | head -10 > file1
virt@virtubserver:/tmp$ cat /dev/random | head -5 > file2
virt@virtubserver:/tmp$ ls -l file*
-rw-rw-r-- 1 virt virt 3247 Jan 26 16:29 file1
-rw-rw-r-- 1 virt virt  911 Jan 26 16:29 file2
virt@virtubserver:/tmp$ 
virt@virtubserver:/tmp$ chmod ug=rw,o=r file1
virt@virtubserver:/tmp$ ls -l file1
-rw-rw-r-- 1 virt virt 3247 Jan 26 16:29 file1
virt@virtubserver:/tmp$ chmod 000 file1 # reset
virt@virtubserver:/tmp$ ls -l file1
---------- 1 virt virt 3247 Jan 26 16:29 file1
virt@virtubserver:/tmp$ chmod 000 file1; # reset
virt@virtubserver:/tmp$ chmod 664; # 4 -> r, 6 -> rw
virt@virtubserver:/tmp$ ls -l file1
-rw-rw-r-- 1 virt virt 3247 Jan 26 16:29 file1
virt@virtubserver:/tmp$  
```

Для файла `file2`

```bash
virt@virtubserver:/tmp$ ls -l file2
-rw-rw-r-- 1 virt virt 911 Jan 26 16:29 file2
virt@virtubserver:/tmp$ chmod 600 file2
virt@virtubserver:/tmp$ ls -l file2
-rw------- 1 virt virt 911 Jan 26 16:29 file2
virt@virtubserver:/tmp$ chmod u=rw,go=- file2
virt@virtubserver:/tmp$ ls -l file2
-rw------- 1 virt virt 911 Jan 26 16:29 file2
virt@virtubserver:/tmp$ 
```

