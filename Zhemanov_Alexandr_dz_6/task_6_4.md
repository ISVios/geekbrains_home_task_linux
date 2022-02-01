# Task 4

- Используя grep, проанализировать файл /var/log/syslog,
отобрав события на своё усмотрение.

Выведем события с 17:30:00 до 17:39:60

```bash
virt@virtubserver:~$ grep '^\w*\s*[0-9]*\s*17:3.:..' /var/log/syslog
Jan 28 17:34:59 virtubserver PackageKit: daemon quit
Jan 28 17:34:59 virtubserver systemd[1]: packagekit.service: Succeeded.
virt@virtubserver:~$
```
