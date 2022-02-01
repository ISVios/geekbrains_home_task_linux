# Task 6

- Написать скрипт,
 делающий архивную копию каталога etc, и прописать задание в crontab.

Добавим права на `tar` выполнения скрипта для пользователя `daemon`

```bash
virt@virtubserver:~$ id daemon 
uid=1(daemon) gid=1(daemon) groups=1(daemon)
virt@virtubserver:~$ sudo grep "daemon" /etc/sudoers
daemon  ALL=(ALL:ALL) NOPASSWD:/usr/bin/tar,/opt/backup_etc.sh
virt@virtubserver:~$ 
``` 

Скрип

```bash
virt@virtubserver:~$ cat /opt/backup_etc.sh
#!/bin/bash

dt=$(/usr/bin/date +'%d-%m-%y')
sudo tar -czf "/var/backups/${dt}-etc.gz"  /etc/
```

Планировщик

```bash
virt@virtubserver:~$ sudo crontab -u daemon -l | tail -2
@reboot sudo /opt/backup_etc.sh 
   
virt@virtubserver:~$ 
```

Результат:

```bash
virt@virtubserver:~$ sudo ls /var/backups/*etc*
/var/backups/31-01-22-etc.gz
virt@virtubserver:~$ 
virt@virtubserver:~$ sudo mail -u daemon
"/var/mail/daemon": 1 message 1 unread
>U   1 Cron Daemon        Mon Jan 31 19:55  22/712   Cron <daemon@virtubserver> sudo /opt/backup_etc.sh 
? 
Return-Path: <daemon@virtubserver>
X-Original-To: daemon
Delivered-To: daemon@virtubserver
Received: by virtubserver (Postfix, from userid 1)
        id 315E06CD7; Mon, 31 Jan 2022 19:55:02 +0000 (UTC)
From: root@virtubserver (Cron Daemon)
To: daemon@virtubserver
Subject: Cron <daemon@virtubserver> sudo /opt/backup_etc.sh 
MIME-Version: 1.0
Content-Type: text/plain; charset=UTF-8
Content-Transfer-Encoding: 8bit
X-Cron-Env: <SHELL=/bin/sh>
X-Cron-Env: <HOME=/usr/sbin>
X-Cron-Env: <PATH=/usr/bin:/bin>
X-Cron-Env: <LOGNAME=daemon>
Message-Id: <20220131195502.315E06CD7@virtubserver>
Date: Mon, 31 Jan 2022 19:55:02 +0000 (UTC)
X-IMAPbase: 1643658738 7
Status: O
X-UID: 6

tar: Removing leading `/' from member names
?
```
