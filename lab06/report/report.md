---
# Front matter
lang: ru-RU
title: "Отчёт по лабораторной работе №6"
subtitle: "Мандатное разграничение прав в Linux"
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

Развить навыки администрирования ОС Linux. 
Получить первое практическое знакомство с технологией SELinux.
Проверить работу SELinx на практике совместно с веб-сервером Apache.

# Выполнение лабораторной работы

Войдите в систему с полученными учётными данными и убедитесь, что
SELinux работает в режиме enforcing политики targeted с помощью команд 
getenforce и sestatus 
(fig. -@fig:001).  

Обратитесь с помощью браузера к веб-серверу, запущенному на вашем
компьютере, и убедитесь, что последний работает:  
service httpd status  
Если не работает, запустите его так же, но с параметром start (fig. -@fig:001).   

Найдите веб-сервер Apache в списке процессов, определите его контекст
безопасности и занесите эту информацию в отчёт (fig. -@fig:001). 
Например, можно использовать команду  
ps auxZ | grep httpd  

Контекст безопасности - system_u:system_r:httpd_t

![Начало работs с apache](image/1.jpg){ #fig:001 width=70% }

Посмотрите текущее состояние переключателей SELinux для Apache (fig. -@fig:002) с
помощью команды  
sestatus -b httpd

![Состояние переключателей](image/2.jpg){ #fig:002 width=70% }  

Посмотрите статистику по политике с помощью команды seinfo, также
определите множество пользователей, ролей, типов (fig. -@fig:003).  

![Статистика по политике](image/3.jpg){ #fig:003 width=70% }

Определите тип файлов и поддиректорий, находящихся в директории
/var/www (fig. -@fig:004), с помощью команды  
ls -lZ /var/www  

Определите тип файлов, находящихся в директории /var/www/html (fig. -@fig:004):  
ls -lZ /var/www/html  

Определите круг пользователей, которым разрешено создание файлов в
директории /var/www/html. Позволено только владельцу. 

![Тип файлов и поддерикторий](image/4.jpg){ #fig:004 width=70% }

Создайте от имени суперпользователя 
(так как в дистрибутиве после установки только ему разрешена запись в директорию) 
html-файл /var/www/html/test.html следующего содержания 
(fig. -@fig:005):  

![Файл test.html](image/5.jpg){ #fig:005 width=70% }

Проверьте контекст созданного вами файла.  
unconfined_u:object_r:httpd_sys_content_t - контекст,
присваиваемый по умолчанию вновь созданным файлам в директории
/var/www/html (fig. -@fig:006).   

![Проверка контеста](image/6.jpg){ #fig:006 width=70% }

Обратитесь к файлу через веб-сервер, введя в браузере адрес
http://127.0.0.1/test.html. Убедитесь, что файл был успешно отображён (fig. -@fig:007).  

![Вывод файла](image/7.jpg){ #fig:007 width=70% }

Изучите справку man httpd и выясните, какие контексты файлов определены для httpd. 
Сопоставьте их с типом файла
test.html. Контектсы совпадают.
Проверить контекст файла можно командой ls -Z (fig. -@fig:008).  
ls -Z /var/www/html/test.html  

![Справка по apache](image/8.jpg){ #fig:008 width=70% }

Измените контекст файла /var/www/html/test.html с
httpd_sys_content_t на любой другой, к которому процесс httpd не
должен иметь доступа, например, на samba_share_t (fig. -@fig:009):  
chcon -t samba_share_t /var/www/html/test.html  
ls -Z /var/www/html/test.html  
После этого проверьте, что контекст поменялся.  

![Изменение контекста файла](image/9.jpg){ #fig:009 width=70% }

Попробуйте ещё раз получить доступ к файлу через веб-сервер, введя в
браузере адрес http://127.0.0.1/test.html. Вы должны получить
сообщение об ошибке (fig. -@fig:010).  

![Ошибка доступа](image/10.jpg){ #fig:010 width=70% }

Файл не был отображён так как у httpd не было доступа к измененному контексту.
Просмотрите log-файлы веб-сервера Apache. Также просмотрите системный лог-файл (fig. -@fig:011):  
tail /var/log/messages   
Если в системе окажутся запущенными процессы setroubleshootd и
audtd, то вы также сможете увидеть ошибки, аналогичные указанным
выше, в файле /var/log/audit/audit.log (fig. -@fig:011).

![log-файлы](image/11.jpg){ #fig:011 width=70% }

Попробуйте запустить веб-сервер Apache на прослушивание ТСР-порта
81 (а не 80, как рекомендует IANA и прописано в /etc/services). Для
этого в файле /etc/httpd/httpd.conf найдите строчку Listen 80 и
замените её на Listen 81.  

Выполните перезапуск веб-сервера Apache (fig. -@fig:012). 

![Перезапуск веб-сервера Apache](image/12.jpg){ #fig:012 width=70% }

Выполните команду  
semanage port -a -t http_port_t -р tcp 81  
После этого проверьте список портов командой  
semanage port -l | grep http_port_t  
Убедитесь, что порт 81 появился в списке (fig. -@fig:013).  

Попробуйте запустить веб-сервер Apache ещё раз (fig. -@fig:013).  

Верните контекст httpd_sys_cоntent__t к файлу /var/www/html/test.html (fig. -@fig:013):  
chcon -t httpd_sys_content_t /var/www/html/test.html  

![Подготовка к запуску файла test.html](image/13.jpg){ #fig:013 width=70% }
  
После этого попробуйте получить доступ к файлу через веб-сервер, 
введя в браузере адрес http://127.0.0.1:81/test.html (fig. -@fig:014).  
Вы должны увидеть содержимое файла — слово «test»  

![Вывод файла](image/14.jpg){ #fig:014 width=70% }

Исправьте обратно конфигурационный файл apache, вернув Listen 80.  

Удалите привязку http_port_t к 81 порту:
semanage port -d -t http_port_t -p tcp 81

Удалите файл /var/www/html/test.html:
rm /var/www/html/test.html  

![Возврат к начальным настройкам](image/15.jpg){ #fig:015 width=70% }

# Выводы

Развил навыки администрирования ОС Linux. 
Получил первое практическое знакомство с технологией SELinux.
Проверил работу SELinx на практике совместно с веб-сервером Apache.
