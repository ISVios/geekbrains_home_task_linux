# Task 2

## Использовать команду cut на вывод длинного списка каталога, чтобы отобразить только права доступа к файлам. Затем отправить в конвейере этот вывод на sort и uniq, чтобы отфильтровать все повторяющиеся строки.

```bash
virt@virtubserver:~$ ll /home
total 20
drwxr-xr-x  5 root    root    4096 Jan 19 19:58 ./
drwxr-xr-x 20 root    root    4096 Jan 18 21:00 ../
drwxr-xr-x  2 guest03 guest03 4096 Jan 19 20:14 guest03/
drwxr-xr-x  4 guest01 guests  4096 Jan 19 19:10 guests/
drwxr-xr-x  7 virt    virt    4096 Jan 21 20:30 virt/
virt@virtubserver:~$
virt@virtubserver:~$ ll /home | tail +2
drwxr-xr-x  5 root    root    4096 Jan 19 19:58 ./
drwxr-xr-x 20 root    root    4096 Jan 18 21:00 ../
drwxr-xr-x  2 guest03 guest03 4096 Jan 19 20:14 guest03/
drwxr-xr-x  4 guest01 guests  4096 Jan 19 19:10 guests/
drwxr-xr-x  7 virt    virt    4096 Jan 21 20:30 virt/
virt@virtubserver:~$
virt@virtubserver:~$ ll /home | tail +2 | cut -c 15-29 
root    root   
root    root   
guest03 guest03
guest01 guests 
virt    virt   
virt@virtubserver:~$
virt@virtubserver:~$ ll /home | tail +2 | cut -c 15-29 | sort 
guest01 guests 
guest03 guest03
root    root   
root    root   
virt    virt   
virt@virtubserver:~$ ll /home | tail +2 | cut -c 15-29 | sort | uniq
guest01 guests 
guest03 guest03
root    root   
virt    virt   
virt@virtubserver:~$
```
