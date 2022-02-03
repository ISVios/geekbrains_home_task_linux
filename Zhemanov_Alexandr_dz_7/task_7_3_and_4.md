# Tasks 3 and 4

## Task 3

- Настроить iptables: разрешить подключения только на 22-й и 80-й порты.

Текущие настроки:

```bash
virt@virtubserver:~$ sudo iptables -L
Chain INPUT (policy ACCEPT)
target     prot opt source               destination         

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination         

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination         
virt@virtubserver:~$ 
```

Добавляем правила

```bash
virt@virtubserver:~$ sudo iptables -A INPUT -p tcp --dport 22  -j ACCEPT
virt@virtubserver:~$ sudo iptables -A INPUT -p tcp --dport 80  -j ACCEPT
virt@virtubserver:~$ sudo iptables -P INPUT  DROP
virt@virtubserver:~$ sudo iptables -L
sudo: unable to resolve host virtubserver: Temporary failure in name resolution
Chain INPUT (policy DROP)
target     prot opt source               destination         
ACCEPT     tcp  --  anywhere             anywhere             tcp dpt:ssh
ACCEPT     tcp  --  anywhere             anywhere             tcp dpt:http

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination         

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination         
virt@virtubserver:~$ 
```

### Проверим спомощью `nc` (netcat)

Виртуальная машина

```bash
virt@virtubserver:~$ sudo nc -lp 80

```

Основная

```bash
    ~  nc 192.168.100.171 -p 80
 hi 
```

Виртуальная машина

```bash
virt@virtubserver:~$ sudo nc -lp 80
hi
```

### Другой порт 87

Виртуальная машина

```bash
virt@virtubserver:~$ sudo nc -lp 87

```

Основная

```bash
    ~  nc 192.168.100.171 -p 87
 hi
 hi
 hi
 hi 
```

Виртуальная машина

```bash
virt@virtubserver:~$ sudo nc -lp 87

```

## Task 4

- Настроить проброс портов локально с порта 80 на порт 8080.

Включить переадресацию трафика:

```bash
virt@virtubserver:~$ sudo sysctl -w net.ipv4.ip_forward=1
sudo: unable to resolve host virtubserver: Temporary failure in name resolution
net.ipv4.ip_forward = 1
virt@virtubserver:~$ 
```

Убедиться, что политика по умолчанию для транзитного трафика: ACCEPT

```bash
virt@virtubserver:~$ sudo iptables -L FORWARD
sudo: unable to resolve host virtubserver: Temporary failure in name resolution
Chain FORWARD (policy ACCEPT)
target     prot opt source               destination         
virt@virtubserver:~$
```

Перадресация с 80 на 8080 (локально)

```bash
virt@virtubserver:~$ sudo iptables -A PREROUTING -t nat -i lo -p tcp --dport 80 -j REDIRECT --to-port 8080
sudo: unable to resolve host virtubserver: Temporary failure in name resolution
virt@virtubserver:~$
```

Уберем ошибку (sudo: unable to resolve host virtubserver:
 Temporary failure in name resolution), добавив `127.0.0.1 <$(hostname)>` в `/etc/hosts`


```bash
virt@virtubserver:~$ sudo vim /etc/hosts
virt@virtubserver:~$ sudo grep "$(hostname)" /etc/hosts
127.0.0.1 virtubserver
virt@virtubserver:~$ sudo systemctl restart network-manager.service 
virt@virtubserver:~$ sudo iptables -L # команда работет быстрее и ошибки нет
Chain INPUT (policy DROP)
target     prot opt source               destination         
ACCEPT     tcp  --  anywhere             anywhere             tcp dpt:ssh
ACCEPT     tcp  --  anywhere             anywhere             tcp dpt:http

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination         

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination         
virt@virtubserver:~$ 
```

Добавим доступ 8080 локально:

```bash
sudo iptables -t nat  -A INPUT -i lo -p tcp --dport 8080  -j ACCEPT
```

Результат:

Виртуальная машина

```bash
virt@virtubserver:~$ sudo nc -lp 8080

```

Основная

```bash
    ~  nc 192.168.100.171 -p 80
 hi 
```

Виртуальная машина

```bash
virt@virtubserver:~$ sudo nc -lp 8080
hi
```

### Доступ к 8080 извне

Виртуальная машина

```bash
virt@virtubserver:~$ sudo nc -lp 8080

```

Основная

```bash
    ~  nc 192.168.100.171 -p 8080
 hi
 hi
 hi
 hi 
```

Виртуальная машина

```bash
virt@virtubserver:~$ sudo nc -lp 8080

```
