# Task 3

```bash

virt@virtubserver:~$ sudo cat /etc/ssh/sshd_config | grep PasswordAuthentication | head -1
PasswordAuthentication yes
virt@virtubserver:~$ sudo vim /etc/ssh/sshd_config
virt@virtubserver:~$ sudo cat /etc/ssh/sshd_config | grep PasswordAuthentication | head -1
PasswordAuthentication no
virt@virtubserver:~$ sudo service sshd status
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)
     Active: active (running) since Fri 2022-01-21 21:29:23 UTC; 2min 59s ago
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 13917 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
   Main PID: 13931 (sshd)
      Tasks: 1 (limit: 2273)
     Memory: 1.3M
     CGroup: /system.slice/ssh.service
             └─13931 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups

Jan 21 21:29:23 virtubserver systemd[1]: Starting OpenBSD Secure Shell server...
Jan 21 21:29:23 virtubserver sshd[13931]: Server listening on 0.0.0.0 port 22.
Jan 21 21:29:23 virtubserver sshd[13931]: Server listening on :: port 22.
Jan 21 21:29:23 virtubserver systemd[1]: Started OpenBSD Secure Shell server.
virt@virtubserver:~$ 
virt@virtubserver:~$ sudo service sshd status
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)
     Active: active (running) since Fri 2022-01-21 21:29:23 UTC; 3min 32s ago
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 13917 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
    Process: 13999 ExecReload=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
    Process: 14000 ExecReload=/bin/kill -HUP $MAINPID (code=exited, status=0/SUCCESS)
   Main PID: 13931 (sshd)
      Tasks: 1 (limit: 2273)
     Memory: 1.7M
     CGroup: /system.slice/ssh.service
             └─13931 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups

Jan 21 21:29:23 virtubserver systemd[1]: Starting OpenBSD Secure Shell server...
Jan 21 21:29:23 virtubserver sshd[13931]: Server listening on 0.0.0.0 port 22.
Jan 21 21:29:23 virtubserver sshd[13931]: Server listening on :: port 22.
Jan 21 21:29:23 virtubserver systemd[1]: Started OpenBSD Secure Shell server.
Jan 21 21:32:53 virtubserver systemd[1]: Reloading OpenBSD Secure Shell server.
Jan 21 21:32:53 virtubserver sshd[13931]: Received SIGHUP; restarting.
Jan 21 21:32:53 virtubserver systemd[1]: Reloaded OpenBSD Secure Shell server.
Jan 21 21:32:53 virtubserver sshd[13931]: Server listening on 0.0.0.0 port 22.
Jan 21 21:32:53 virtubserver sshd[13931]: Server listening on :: port 22.
virt@virtubserver:~$ 
virt@virtubserver:~$ sudo service sshd status
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)
     Active: active (running) since Fri 2022-01-21 21:33:22 UTC; 2s ago
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 14019 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
   Main PID: 14035 (sshd)
      Tasks: 1 (limit: 2273)
     Memory: 1.2M
     CGroup: /system.slice/ssh.service
             └─14035 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups

Jan 21 21:33:22 virtubserver systemd[1]: Starting OpenBSD Secure Shell server...
Jan 21 21:33:22 virtubserver sshd[14035]: Server listening on 0.0.0.0 port 22.
Jan 21 21:33:22 virtubserver sshd[14035]: Server listening on :: port 22.
Jan 21 21:33:22 virtubserver systemd[1]: Started OpenBSD Secure Shell server.
virt@virtubserver:~$ 
```

   Различие между действиями `restart` и `reload` тем,
что `reload` перегружает только параметры сервиса,
а `reload`перегружет весь процесс -> происходит смена `pid`
(в данном случаии `13931` на `14035`)

## Создайте файл при помощи команды cat > file_name

```bash
virt@virtubserver:~$ cat > cat_file
some cat text
virt@virtubserver:~$ cat cat_file 
some cat text
virt@virtubserver:~$ 
```

Для завершения записи в файл через используем ctr + d (^d)
что равносильно EOF(END OF FILE)

