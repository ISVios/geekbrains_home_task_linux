# TAsk 4

## Запустите mc. Используя ps, найдите PID процесса, завершите процесс, передав ему сигнал 9.

```bash
virt@virtubserver:~$ mc

virt@virtubserver:~$ ps -ax | grep --color mc
   2005 pts/0    S+     0:00 mc
   2014 pts/1    S+     0:00 grep --color=auto --color mc
virt@virtubserver:~$ kill -9 2005Killed
virt@virtubserver:~$ ps -ax | grep --color mc
   2016 pts/0    S+     0:00 grep --color=auto --color mc
virt@virtubserver:~$ 
```
