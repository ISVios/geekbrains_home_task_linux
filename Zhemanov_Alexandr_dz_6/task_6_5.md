# Task 5

- Создать разовое задание на перезагрузку операционной системы, используя at.

Проверка демона

```bash
virt@virtubserver:~$ service atd status
● atd.service - Deferred execution scheduler
     Loaded: loaded (/lib/systemd/system/atd.service; enabled; vendor preset: enabled)
     Active: active (running) since Fri 2022-01-28 17:02:09 UTC; 2h 25min ago
       Docs: man:atd(8)
   Main PID: 789 (atd)
      Tasks: 1 (limit: 2273)
     Memory: 644.0K
     CGroup: /system.slice/atd.service
             └─789 /usr/sbin/atd -f

Jan 28 17:02:09 virtubserver systemd[1]: Starting Deferred execution scheduler...
Jan 28 17:02:09 virtubserver systemd[1]: Started Deferred execution scheduler.
virt@virtubserver:~$
```

Выполнение:

```bash
virt@virtubserver:~$ echo "reboot" | sudo at next minute 
[sudo] password for virt: 
warning: commands will be executed using /bin/sh
job 1 at Fri Jan 28 22:32:00 2022
virt@virtubserver:~$ 
```
