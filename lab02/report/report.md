---
# Front matter
lang: ru-RU
title: "Отчёт по лабораторной работе №2"
subtitle: "Дискреционное разграничение прав в Linux. Основные атрибуты."
author: "Волков Тимофей Евгеньевич"

# Formatting
toc-title: "Содержание"
toc: true # Table of contents
toc_depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4paper
documentclass: scrreprt
polyglossia-lang: russian 
polyglossia-otherlangs: english
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase
indent: true
pdf-engine: lualatex
header-includes:
  - \linepenalty=10 # the penalty added to the badness of each line within a paragraph (no associated penalty node) Increasing the value makes tex try to have fewer lines in the paragraph.
  - \interlinepenalty=0 # value of the penalty (node) added after each line of a paragraph.
  - \hyphenpenalty=50 # the penalty for line breaking at an automatically inserted hyphen
  - \exhyphenpenalty=50 # the penalty for line breaking at an explicit hyphen
  - \binoppenalty=700 # the penalty for breaking a line at a binary operator
  - \relpenalty=500 # the penalty for breaking a line at a relation
  - \clubpenalty=150 # extra penalty for breaking after first line of a paragraph
  - \widowpenalty=150 # extra penalty for breaking before last line of a paragraph
  - \displaywidowpenalty=50 # extra penalty for breaking before last line before a display math
  - \brokenpenalty=100 # extra penalty for page breaking after a hyphenated line
  - \predisplaypenalty=10000 # penalty for breaking before a display
  - \postdisplaypenalty=0 # penalty for breaking after a display
  - \floatingpenalty = 20000 # penalty for splitting an insertion (can only be split footnote in standard LaTeX)
  - \raggedbottom # or \flushbottom
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Получение практических навыков работы в консоли с атрибутами файлов, закрепление 
теоретических основ дискреционного разграничения доступа в современных системах с 
открытым кодом на базе ОС Linux.  

# Выполнение лабораторной работы

В установленной при выполнении предыдущей лабораторной работы
операционной системе создать учётную запись пользователя guest (fig. -@fig:001) 
(используя учётную запись администратора)  
*useradd guest*   
и задать пароль для пользователя guest (fig. -@fig:001)  
*passwd guest* 

![Создание учётной записи пользователя guest](image/1.jpg){ #fig:001 width=70% }

Войти в систему от имени пользователя guest (fig. -@fig:002). 

![Вход в систему пользователем guest](image/2.jpg){ #fig:002 width=70% }

Определить директорию, в которой вы находитесь, командой *pwd* (fig. -@fig:004).   
Директория */home/guest* является домашней для пользователя guest.

![Командная строка guest](image/3.jpg){ #fig:003 width=70% }

Уточнить имя вашего пользователя командой *whoami*. 
Уточнить имя вашего пользователя, его группу, а также группы, 
куда входит пользователь, командой *id* (fig. -@fig:004). 
Выведенные значения uid, gid и др. запомнить.  
Команда *groups* выводит только название группы, которой принадлежит пользователь.  
*id* выводит идентификатор пользователя, группы, контекст безопасности.

![Информация о пользователе](image/4.jpg){ #fig:004 width=70% }

Имя пользователя совпабадет с именем пользователя в приглашении командной строки.  

Просмотреть файл */etc/passwd* используя программу grep в качестве фильтра 
для вывода только строк, содержащих определённые буквенные сочетания(fig. -@fig:005):  
*cat /etc/passwd | grep guest*  

Значения uid и gid пользователя совпадают с их значениями в предыдущих пунктах.

![Файл /etc/passwd](image/5.jpg){ #fig:005 width=70% }

Определить существующие в системе директории командой (fig. -@fig:006):  
*ls -l /home/*  
Вывелся список поддиректорий директории */home*.
Права к директориям имеются только у их владельца, которые могут просматривать 
директорию, создавать папки  или файлы внутри директории и переходить в директорию.

![Поддиректории директории home](image/6.jpg){ #fig:006 width=70% }

Проверить, какие расширенные атрибуты установлены на поддиректориях, 
находящихся в директории */home* (fig. -@fig:007), командой:  
*lsattr /home*  
Расширенные атрибуты для guest не установлены. Доступа к 
расширенным атрибутам tevolkov нет.

![Расширенные атрибуты](image/7.jpg){ #fig:007 width=70% }

Создать в домашней директории поддиректорию *dir1* командой  
*mkdir dir1*  
Определить командами *ls -l* и *lsattr*, какие права доступа и расширенные атрибуты 
были выставлены на директорию dir1 (fig. -@fig:008).  
К директории dir1 имеют полный доступ владелец, пользователи группы владельца, 
и у остальных пользователей нет только возможности именять файлы и поддиректории.

![Права доступа и расширенные атрибуты 
директории dir1](image/8.jpg){ #fig:008 width=70% }

Снять с директории dir1 все атрибуты командой  
*chmod 000 dir1*  
и проверить с её помощью правильность выполнения команды (fig. -@fig:009)  
*ls -l*

![Изменение прав доступа](image/9.jpg){ #fig:009 width=70% }

Попытаться создать в директории *dir1* файл *file1* (fig. -@fig:010) командой    
*echo "test" > /home/guest/dir1/file1*   
Так как у guest нет прав доступа к директории dir1 было отказано в доступе.

Оценить, как сообщение об ошибке отразилось на создании файла 
(перед этим вернул права доступа пользователю) (fig. -@fig:010).  
Проверить командой  
*ls -l /home/guest/dir1*  
file1 не находится внутри директории dir1.

![Попытка создания в директории dir1 файла file1](image/10.jpg){ #fig:010 width=70% }

Заполнить таблицу «Установленные права и разрешённые действия»
(см. табл. [-@tbl:001]), выполняя действия от имени владельца директории (файлов), 
определив опытным путём, какие операции разрешены, а какие нет.
Если операция разрешена, занести в таблицу знак «+», если не разрешена, знак «-».

Например, в табл.  приведено краткое описание стандартных каталогов Unix.

: Установленные права и разрешённые действия {#tbl:001}

| Права директории | Права файла | Создание файла | Удаление файла | Запись в файл | Чтение файла | Смена директории | Просмотр файлов в директории | Переименование файла | Смена атрибутов файла |
|------------------|-------------|----------------|----------------|---------------|--------------|------------------|------------------------------|----------------------|-----------------------|
| --- (000)        | --- (000)   | -              | -              | -             | -            | -                | -                            | -                    | -                     |
| --- (000)        | --x (100)   | -              | -              | -             | -            | -                | -                            | -                    | -                     |
| --- (000)        | -w- (200)   | -              | -              | -             | -            | -                | -                            | -                    | -                     |
| --- (000)        | -wx (300)   | -              | -              | -             | -            | -                | -                            | -                    | -                     |
| --- (000)        | r-- (400)   | -              | -              | -             | -            | -                | -                            | -                    | -                     |
| --- (000)        | r-x (500)   | -              | -              | -             | -            | -                | -                            | -                    | -                     |
| --- (000)        | rw- (600)   | -              | -              | -             | -            | -                | -                            | -                    | -                     |
| --- (000)        | rwx (700)   | -              | -              | -             | -            | -                | -                            | -                    | -                     |
| --x (100)        | --- (000)   | -              | -              | -             | -            | +                | -                            | -                    | +                     |
| --x (100)        | --x (100)   | -              | -              | -             | -            | +                | -                            | -                    | +                     |
| --x (100)        | -w- (200)   | -              | -              | +             | -            | +                | -                            | -                    | +                     |
| --x (100)        | -wx (300)   | -              | -              | +             | -            | +                | -                            | -                    | +                     |
| --x (100)        | r-- (400)   | -              | -              | -             | +            | +                | -                            | -                    | +                     |
| --x (100)        | r-x (500)   | -              | -              | -             | +            | +                | -                            | -                    | +                     |
| --x (100)        | rw- (600)   | -              | -              | +             | +            | +                | -                            | -                    | +                     |
| --x (100)        | rwx (700)   | -              | -              | +             | +            | +                | -                            | -                    | +                     |
| -w- (200)        | --- (000)   | -              | -              | -             | -            | -                | -                            | -                    | -                     |
| -w- (200)        | --x (100)   | -              | -              | -             | -            | -                | -                            | -                    | -                     |
| -w- (200)        | -w- (200)   | -              | -              | -             | -            | -                | -                            | -                    | -                     |
| -w- (200)        | -wx (300)   | -              | -              | -             | -            | -                | -                            | -                    | -                     |
| -w- (200)        | r-- (400)   | -              | -              | -             | -            | -                | -                            | -                    | -                     |
| -w- (200)        | r-x (500)   | -              | -              | -             | -            | -                | -                            | -                    | -                     |
| -w- (200)        | rw- (600)   | -              | -              | -             | -            | -                | -                            | -                    | -                     |
| -w- (200)        | rwx (700)   | -              | -              | -             | -            | -                | -                            | -                    | -                     |
| -wx (300)        | --- (000)   | +              | +              | -             | -            | +                | -                            | +                    | +                     |
| -wx (300)        | --x (100)   | +              | +              | -             | -            | +                | -                            | +                    | +                     |
| -wx (300)        | -w- (200)   | +              | +              | +             | -            | +                | -                            | +                    | +                     |
| -wx (300)        | -wx (300)   | +              | +              | +             | -            | +                | -                            | +                    | +                     |
| -wx (300)        | r-- (400)   | +              | +              | -             | +            | +                | -                            | +                    | +                     |
| -wx (300)        | r-x (500)   | +              | +              | -             | +            | +                | -                            | +                    | +                     |
| -wx (300)        | rw- (600)   | +              | +              | +             | +            | +                | -                            | +                    | +                     |
| -wx (300)        | rwx (700)   | +              | +              | +             | +            | +                | -                            | +                    | +                     |
| r-- (400)        | --- (000)   | -              | -              | -             | -            | -                | +                            | -                    | -                     |
| r-- (400)        | --x (100)   | -              | -              | -             | -            | -                | +                            | -                    | -                     |
| r-- (400)        | -w- (200)   | -              | -              | -             | -            | -                | +                            | -                    | -                     |
| r-- (400)        | -wx (300)   | -              | -              | -             | -            | -                | +                            | -                    | -                     |
| r-- (400)        | r-- (400)   | -              | -              | -             | -            | -                | +                            | -                    | -                     |
| r-- (400)        | r-x (500)   | -              | -              | -             | -            | -                | +                            | -                    | -                     |
| r-- (400)        | rw- (600)   | -              | -              | -             | -            | -                | +                            | -                    | -                     |
| r-- (400)        | rwx (700)   | -              | -              | -             | -            | -                | +                            | -                    | -                     |
| r-x (500)        | --- (000)   | -              | -              | -             | -            | +                | +                            | -                    | +                     |
| r-x (500)        | --x (100)   | -              | -              | -             | -            | +                | +                            | -                    | +                     |
| r-x (500)        | -w- (200)   | -              | -              | +             | -            | +                | +                            | -                    | +                     |
| r-x (500)        | -wx (300)   | -              | -              | +             | -            | +                | +                            | -                    | +                     |
| r-x (500)        | r-- (400)   | -              | -              | -             | +            | +                | +                            | -                    | +                     |
| r-x (500)        | r-x (500)   | -              | -              | -             | +            | +                | +                            | -                    | +                     |
| r-x (500)        | rw- (600)   | -              | -              | +             | +            | +                | +                            | -                    | +                     |
| r-x (500)        | rwx (700)   | -              | -              | +             | +            | +                | +                            | -                    | +                     |
| rw- (600)        | --- (000)   | -              | -              | -             | -            | -                | +                            | -                    | -                     |
| rw- (600)        | --x (100)   | -              | -              | -             | -            | -                | +                            | -                    | -                     |
| rw- (600)        | -w- (200)   | -              | -              | -             | -            | -                | +                            | -                    | -                     |
| rw- (600)        | -wx (300)   | -              | -              | -             | -            | -                | +                            | -                    | -                     |
| rw- (600)        | r-- (400)   | -              | -              | -             | -            | -                | +                            | -                    | -                     |
| rw- (600)        | r-x (500)   | -              | -              | -             | -            | -                | +                            | -                    | -                     |
| rw- (600)        | rw- (600)   | -              | -              | -             | -            | -                | +                            | -                    | -                     |
| rw- (600)        | rwx (700)   | -              | -              | -             | -            | -                | +                            | -                    | -                     |
| rwx (700)        | --- (000)   | +              | +              | -             | -            | +                | +                            | +                    | +                     |
| rwx (700)        | --x (100)   | +              | +              | -             | -            | +                | +                            | +                    | +                     |
| rwx (700)        | -w- (200)   | +              | +              | +             | -            | +                | +                            | +                    | +                     |
| rwx (700)        | -wx (300)   | +              | +              | +             | -            | +                | +                            | +                    | +                     |
| rwx (700)        | r-- (400)   | +              | +              | -             | +            | +                | +                            | +                    | +                     |
| rwx (700)        | r-x (500)   | +              | +              | -             | +            | +                | +                            | +                    | +                     |
| rwx (700)        | rw- (600)   | +              | +              | +             | +            | +                | +                            | +                    | +                     |
| rwx (700)        | rwx (700)   | +              | +              | +             | +            | +                | +                            | +                    | +                     |

На основании заполненной таблицы определить те или иные минимально необходимые права 
для выполнения операций внутри директории *dir1* (табл. [-@tbl:002]).

: Минимальные права для совершения операций {#tbl:002}

| Операция               | Минимальные права на директорию | Минимальные права на файл |
|------------------------|---------------------------------|---------------------------|
| Создание файла         | -wx (300)                       | --- (000)                 |
| Удаление файла         | -wx (300)                       | --- (000)                 |
| Чтение файла           | --x (100)                       | r-- (400)                 |
| Запись в файл          | --x (100)                       | -w- (200)                 |
| Переименование файла   | -wx (300)                       | --- (000)                 |
| Создание поддиректории | -wx (300)                       | --- (000)                 |
| Удаление поддиректории | -wx (300)                       | --- (000)                 |

# Выводы

Получил практические навыки работы в консоли с атрибутами файлов, закрепил
теоретические основы дискреционного разграничения доступа в современных системах с 
открытым кодом на базе ОС Linux. 