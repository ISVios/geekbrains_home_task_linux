# Task 2

## Отображение содерижимого в каталоге

Для отображения содержимого в каталоге используется команда `ls`.

По умолчанию отображает содержимое текущего католога `pwd`

```bash
virt@virt-server:/$ ls
bin   dev  home  lib32  libx32      media  opt   root  sbin  srv       sys  usr
boot  etc  lib   lib64  lost+found  mnt    proc  run   snap  swap.img  tmp  var
virt@virt-server:/$
```

При использование комады c путем отображает его содержимое

```bash
virt@virt-server:/$ ls /tmp/
snap.lxd
systemd-private-586051682a04499aa0a5dcc14e83ce92-systemd-logind.service-mDt94h
systemd-private-586051682a04499aa0a5dcc14e83ce92-systemd-resolved.service-RBTrQf
systemd-private-586051682a04499aa0a5dcc14e83ce92-systemd-timesyncd.service-yy0Zzi
virt@virt-server:/$ 
```

## Создание файлов c помощью команды

- ### touch

Создаёт пустой файл.

```bash
virt@virt-server:~$ touch touch_file
virt@virt-server:~$ 
virt@virt-server:~$ ls
touch_file
virt@virt-server:~$ cat touch_file 
virt@virt-server:~$ 
```

- ### echo

Команда используется для выввода текста в консоль

```bash
virt@virt-server:~$ echo some text
some text
virt@virt-server:~$
```

Но можно вывод перенаправить в файл

```bash
virt@virt-server:~$ echo some text > echo_file
virt@virt-server:~$ 
virt@virt-server:~$ ls
echo_file  touch_file
virt@virt-server:~$ 
virt@virt-server:~$ cat echo_file 
some text
virt@virt-server:~$ 
```

- ### cat

Используется для отображения содержимого файла

```bash
virt@virt-server:~$ cat echo_file 
some text
virt@virt-server:~$ 
```

Но его также можно перенаправить в файл

``` bash
virt@virt-server:~$ cat > cat_file
some cat text
```

Для выхода спользуем комбинацию `^d (ctr + d)`

Проверяем:

```bash
virt@virt-server:~$ ls
cat_file  echo_file  touch_file
virt@virt-server:~$ 
virt@virt-server:~$ cat cat_file 
some cat text
virt@virt-server:~$ 
```

- ### vim

Является текстовым редактором

```bash
virt@virt-server:~$ vim

~                                                                                   
~                                                                                   
~                                VIM - Vi IMproved                                  
~                                                                                   
~                                 version 8.1.2269                                  
~                             by Bram Moolenaar et al.                              
~                     Modified by team+vim@tracker.debian.org                       
~                   Vim is open source and freely distributable                     
~                                                                                   
~                          Help poor children in Uganda!                            
~                  type  :help iccf<Enter>       for information                    
~                                                                                   
~                  type  :q<Enter>               to exit                            
~                  type  :help<Enter>  or  <F1>  for on-line help                   
~                  type  :help version8<Enter>   for version info                   
~                                                                                   
~                                                                                   
~                                                                                   
                                                                  0,0-1         All

```

Перейдем в режим вставки:

нажмем `i`

```bash
~                                                                                   
~                                                                                   
~                                VIM - Vi IMproved                                  
~                                                                                   
~                                 version 8.1.2269                                  
~                             by Bram Moolenaar et al.                              
~                     Modified by team+vim@tracker.debian.org                       
~                   Vim is open source and freely distributable                     
~                                                                                   
~                          Help poor children in Uganda!                            
~                  type  :help iccf<Enter>       for information                    
~                                                                                   
~                  type  :q<Enter>               to exit                            
~                  type  :help<Enter>  or  <F1>  for on-line help                   
~                  type  :help version8<Enter>   for version info                   
~                                                                                   
~                                                                                   
~                                                                                   
-- INSERT --                                                      0,1           All

```
Введем текст и выйдем из режима редактирования `ESC`

```bash
some vim text
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
                                                                  1,14          All
```

Сохраним этот файл как `vim_file` с помощью режима ввода команд `:`

```bash
some vime text
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
:w vim_file
```

Выйдем из редактора используя `:q`

```bash
some vime text
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
~                                                                                   
:q
```

Результат

```bash
virt@virt-server:~$ ls
cat_file  echo_file  touch_file  vim_file
virt@virt-server:~$ 
virt@virt-server:~$ cat vim_file 
some vime text
virt@virt-server:~$
```

- ### nano

Является текстовым редактором

```bash
virt@virt-server:~$ nano

  GNU nano 4.8                         New Buffer                                   

















^G Get Help   ^O Write Out  ^W Where Is   ^K Cut Text   ^J Justify    ^C Cur Pos
^X Exit       ^R Read File  ^\ Replace    ^U Paste Text ^T To Spell   ^_ Go To Line
```

Введем текст

```bash
  GNU nano 4.8                         New Buffer                         Modified  
some nano text















                 [ Welcome to nano.  For basic help, type Ctrl+G. ]
^G Get Help   ^O Write Out  ^W Where Is   ^K Cut Text   ^J Justify    ^C Cur Pos
^X Exit       ^R Read File  ^\ Replace    ^U Paste Text ^T To Spell   ^_ Go To Line
```

Сохраним используя `^O (ctr + shift + o)`

```bash
 GNU nano 4.8                         New Buffer                         Modified  
some nano text















File Name to Write: nano_text                                                                
^G Get Help          M-D DOS Format       M-A Append           M-B Backup File
^C Cancel            M-M Mac Format       M-P Prepend          ^T To Files
```

Выход осуществляется через комбинацию `^X (ctr + shift + x)`.

Результат:

```bash
virt@virt-server:~$ ls
cat_file  echo_file  nano_text  touch_file  vim_file
virt@virt-server:~$ cat nano_text 
some nano text
virt@virt-server:~$ 
```

## Создание каталогов

Для создание каталогов используется команда `mkdir`

```bash
virt@virt-server:~$ mkdir fld_1
virt@virt-server:~$ 
virt@virt-server:~$ ls
cat_file  echo_file  fld_1  nano_text  touch_file  vim_file
virt@virt-server:~$
```

Для создание дерева каталогов используется ключ `-p`

```bash
virt@virt-server:~$ mkdir -p fld_2/fld_3/fld_4
virt@virt-server:~$ 
virt@virt-server:~$ ls
cat_file  echo_file  fld_1  fld_2  nano_text  touch_file  vim_file
virt@virt-server:~$ ls fld_2
fld_3
virt@virt-server:~$ ls fld_2/fld_3/
fld_4
virt@virt-server:~$
```

## Копирование файлов

Для копирования используется команда `cp`(copy)

копируем `nano_text` в fld_1

```bash
virt@virt-server:~$ cp nano_text fld_1/
virt@virt-server:~$ ls fld_1/
nano_text
virt@virt-server:~$ 
```

Скопируем оставшиеся файлы

```bash
virt@virt-server:~$ cp vim_file fld_1/
virt@virt-server:~$ cp cat_file fld_1/
virt@virt-server:~$ cp touch_file fld_1/
virt@virt-server:~$ ls fld_1/
cat_file  nano_text  touch_file  vim_file
virt@virt-server:~$ 
```

Для копирования папки необходима испоьзовать ключ `-r`

```bash
virt@virt-server:~$ cp -r  fld_1/ fld_2/fld_3/fld_4/
virt@virt-server:~$ ls fld_1/
cat_file    nano_text   touch_file  vim_file    
virt@virt-server:~$ ls fld_2/fld_3/fld_4/
fld_1
virt@virt-server:~$ ls fld_2/fld_3/fld_4/fld_1/
cat_file  nano_text  touch_file  vim_file
virt@virt-server:~$ 
```

## Перемещения файлов

Для перемещение используется команда `mv`(move)

Переместим файл `touch_text` из fld_1 в fld_2

```bash
virt@virt-server:~$ ls fld_1/
cat_file  nano_text  touch_file  vim_file
virt@virt-server:~$ mv ./fld_1/touch_file ./fld_2/
virt@virt-server:~$ ls fld_1/
cat_file  nano_text  vim_file
virt@virt-server:~$ ls fld_2/
fld_3  touch_file
virt@virt-server:~$ 
```

Так же команда `mv` может переименовать файлы/каталоги

```bash
virt@virt-server:~$ mv fld_1/ texts/
virt@virt-server:~$ ls
cat_file  echo_file  fld_2  nano_text  texts  touch_file  vim_file
virt@virt-server:~$ mv touch_file empty_file
virt@virt-server:~$ ls
cat_file  echo_file  empty_file  fld_2  nano_text  texts  vim_file
virt@virt-server:~$
```

## Удаление файлов

Для удаления используется команда `rm`(remove)

```bash
virt@virt-server:~$ ls
cat_file  echo_file  empty_file  fld_2  nano_text  texts  vim_file
virt@virt-server:~$ rm nano_text 
virt@virt-server:~$ ls
cat_file  echo_file  empty_file  fld_2  texts  vim_file
virt@virt-server:~$
```

В случаи если необходимо удалить католог необходимо испоьзовать ключ `-r`

```bash
virt@virt-server:~$ rm -r fld_2/
virt@virt-server:~$ ls
cat_file  echo_file  empty_file  texts  vim_file
virt@virt-server:~$
```

