# Task 2

- Создать однострочный скрипт, который создаст директории для нескольких годов (2010–2017),
в них — поддиректории для месяцев (от 01 до 12),
и в каждый из них запишет несколько файлов с произвольными записями.
Например, 001.txt, содержащий текст «Файл 001», 002.txt с текстом «Файл 002»
и т. д.

```bash
virt@virtubserver:~$ for y in {2010..2017}; do ! [[ -d $y ]] && mkdir $y; cd $y; for d in {01..12}; do ! [[ -d $d ]] && mkdir $d; cd $d; for f in {001..010}; do  ! [[ -f $f ]] && (echo "Файл $f" > "$f.txt"); done; cd ..; done; cd ..; done;
```
Или

```bash
virt@virtubserver:~$ for y in {2010..2017}; do mkdir -p $y; cd $y; for d in {01..12}; do mkdir -p $d; cd $d; for f in {001..010}; do  ! [[ -f $f ]] && (echo "Файл $f" > "$f.txt"); done; cd ..; done; cd ..; done;
```

Или

```bash
virt@virtubserver:~$ struct=$(echo {2010..2017}/{01..12}); for path in $struct; do mkdir -p $path; for f in {001..010}; do echo "File $f" > $path/$f.txt ;done ;done
```


Результат:

```bash
virt@virtubserver:~$ ls
cls_upp_f.sh  file1
virt@virtubserver:~$ struct=$(echo {2010..2017}/{01..12}); for path in $struct; do mkdir -p $path; for f in {001..010}; do echo "File $f" > $path/$f.txt ;done ;done
virt@virtubserver:~$ tree | head -20
.
├── 2010
│   ├── 01
│   │   ├── 001.txt
│   │   ├── 002.txt
│   │   ├── 003.txt
│   │   ├── 004.txt
│   │   ├── 005.txt
│   │   ├── 006.txt
│   │   ├── 007.txt
│   │   ├── 008.txt
│   │   ├── 009.txt
│   │   └── 010.txt
│   ├── 02
│   │   ├── 001.txt
│   │   ├── 002.txt
│   │   ├── 003.txt
│   │   ├── 004.txt
│   │   ├── 005.txt
│   │   ├── 006.txt
virt@virtubserver:~$ cat 2017/04/007.txt 
File 007
virt@virtubserver:~$ 
```

