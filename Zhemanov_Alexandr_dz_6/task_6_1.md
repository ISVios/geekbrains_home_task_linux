# Task 1

- Написать скрипт,
который удаляет из текстового файла пустые строки
и заменяет маленькие символы на большие. Воспользуйтесь tr или SED.

```bash
virt@virtubserver:~$ vim cls_upp_f.sh
virt@virtubserver:~$ cat cls_upp_f.sh 
#!/bin/bash

if [[ $# -eq 0 ]] ; then
  echo "plese input file" 
else
  if [[ -f $1 ]] ; then 
    sed -e "/^$/d" -e "s/[a-z]/\U&/g" -i $1
  else
    echo "$1 isn't file"
  fi
fi
virt@virtubserver:~$ vim file1
virt@virtubserver:~$ cat file1 
qwerty

qwerty

qwerty

qwerty

qwerty

qwerty

qwerty

qwerty

qwerty

qwerty


virt@virtubserver:~$ chmod +x cls_upp_f.sh 
virt@virtubserver:~$ ./cls_upp_f.sh 
plese input file
virt@virtubserver:~$ ./cls_upp_f.sh file1 
virt@virtubserver:~$ cat file1 
QWERTY
QWERTY
QWERTY
QWERTY
QWERTY
QWERTY
QWERTY
QWERTY
QWERTY
QWERTY
virt@virtubserver:~$ 
```
