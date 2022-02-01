# Task 3

- Использовать команду AWK на вывод длинного списка каталога,
 чтобы отобразить только права доступа к файлам.
  Затем отправить в конвейере этот вывод на sort и uniq,
  чтобы отфильтровать все повторяющиеся строки.

```bash
virt@virtubserver:~$ ls -la /etc/ | head -10 # очень много файлов/папок/ссылок
total 876
drwxr-xr-x 103 root root       4096 Jan 28 20:20 .
drwxr-xr-x  20 root root       4096 Jan 18 21:00 ..
-rw-r--r--   1 root root       3028 Aug 24 08:42 adduser.conf
drwxr-xr-x   2 root root       4096 Jan 19 20:18 alternatives
drwxr-xr-x   3 root root       4096 Aug 24 08:47 apparmor
drwxr-xr-x   7 root root       4096 Jan 11 21:46 apparmor.d
drwxr-xr-x   3 root root       4096 Jan 11 21:34 apport
drwxr-xr-x   7 root root       4096 Jan 11 21:27 apt
-rw-r-----   1 root daemon      144 Nov 12  2018 at.deny
virt@virtubserver:~$ ls -l /etc/ | awk '/^-/{print $1}' # только права файлов
-rw-r--r--
-rw-r-----
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r-----
-rw-r-----
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-r--r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r-----
-rw-r-----
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-r--r-----
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rwxrwxrwx
-rw-r--r--
-rw-r--r--
-rw-r--r--
-rw-r--r--
virt@virtubserver:~$ ls -l /etc/ | awk '/^-/{print $1}' | sort | uniq
-r--r-----
-r--r--r--
-rw-r-----
-rw-r--r--
-rwxrwxrwx
virt@virtubserver:~$ 
```

