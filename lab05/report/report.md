---
# Front matter
lang: ru-RU
title: "Отчёт по лабораторной работе №5"
subtitle: "Дискреционное разграничение прав в Linux. Исследованиевлияния дополнительных атрибутов"
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

Изучение механизмов изменения идентификаторов, применения
SetUID- и Sticky-битов. Получение практических навыков работы в консоли с дополнительными атрибутами. Рассмотрение работы механизма
смены идентификатора процессов пользователей, а также влияние бита
Sticky на запись и удаление файлов.

# Выполнение лабораторной работы

Войдите в систему от имени пользователя guest.  
Создайте программу simpleid.c (fig. -@fig:001).  

![Программа simpleid.c](image/1.jpg){ #fig:001 width=70% }

Скомплилируйте программу (fig. -@fig:002):  
gcc simpleid.c -o simpleid  

Выполните программу simpleid (fig. -@fig:002):  
./simpleid  

Выполните системную программу id (fig. -@fig:002):  
id  

Программа и команда id выводят одинаковый uid и gid.    

![Сравнение программы simpleid и команды id](image/2.jpg){ #fig:002 width=70% }

Усложните программу, добавив вывод действительных идентификаторов (fig. -@fig:003).
Получившуюся программу назовите simpleid2.c.  

![Усложнение программы](image/3.jpg){ #fig:003 width=70% }

Скомпилируйте и запустите simpleid2.c (fig. -@fig:004):  
gcc simpleid2.c -o simpleid2  
./simpleid2   

![Запуск программы simpleid2.c](image/4.jpg){ #fig:004 width=70% }

От имени суперпользователя выполните команды (fig. -@fig:005):  
chown root:guest /home/guest/simpleid2  
chmod u+s /home/guest/simpleid2  

Выполните проверку правильности установки новых атрибутов и смены  
владельца файла simpleid2(fig. -@fig:005):  
ls -l simpleid2  

Запустите simpleid2 и id (fig. -@fig:005):  
./simpleid2  
id  

simpleid2 и id выводят одинаковые uid и gid, но отличающиеся от результатов предыдущих пунктов.

![Установка SetUID-бита](image/5.jpg){ #fig:005 width=70% }

Проделайте тоже самое относительно SetGID-бита (fig. -@fig:006).

![Установка SetGID-бита](image/6.jpg){ #fig:006 width=70% }

Создайте программу readfile.c (fig. -@fig:007).

![Программа readfile.c](image/7.jpg){ #fig:007 width=70% }

Смените владельца у файла readfile.c  и измените права так, чтобы только суперпользователь
(root) мог прочитать его, a guest не мог (fig. -@fig:008).  
Проверьте, что пользователь guest не может прочитать файл readfile.c (fig. -@fig:008).  
Смените у программы readfile владельца и установите SetUID-бит (fig. -@fig:008).  
Программа readfile может прочитать файл readfile.c и файл /etc/shadow.  

![Проверка работы программы readfile](image/8.jpg){ #fig:008 width=70% }

Выясните, установлен ли атрибут Sticky на директории /tmp (fig. -@fig:009), для чего
выполните команду  
ls -l / | grep tmp  

От имени пользователя guest создайте файл file01.txt в директории /tmp
со словом test (fig. -@fig:009):  
echo "test" > /tmp/file01.txt  

Просмотрите атрибуты у только что созданного файла и разрешите чтение и запись для 
категории пользователей «все остальные» (fig. -@fig:009):  
ls -l /tmp/file01.txt  
chmod o+rw /tmp/file01.txt  
ls -l /tmp/file01.txt  

От пользователя guest2 (не являющегося владельцем) попробуйте прочитать файл /tmp/file01.txt (fig. -@fig:009):  
cat /tmp/file01.txt   

От пользователя guest2 попробуйте дозаписать в файл  
/tmp/file01.txt слово test2 (fig. -@fig:009) командой  
echo "test2" > /tmp/file01.txt  

Дозапись прошла успешно.  

Проверьте содержимое файла командой  
cat /tmp/file01.txt  

От пользователя guest2 попробуйте записать в файл /tmp/file01.txt
слово test3, стерев при этом всю имеющуюся в файле информацию командой  
echo "test3" > /tmp/file01.txt  

Запись прошла успешно.  

Проверьте содержимое файла (fig. -@fig:009) командой  
cat /tmp/file01.txt  

От пользователя guest2 попробуйте удалить файл /tmp/file01.txt (fig. -@fig:009) командой  
rm /tmp/fileOl.txt  

Удалить файл не удалось.  

Повысьте свои права до суперпользователя (fig. -@fig:009) следующей командой  
su -  

и выполните после этого команду, снимающую атрибут t (Sticky-бит) с
директории /tmp (fig. -@fig:009):  
chmod -t /tmp  

Покиньте режим суперпользователя (fig. -@fig:009) командой  
exit  

От пользователя guest2 проверьте, что атрибута t у директории /tmp
нет(fig. -@fig:009) :  
ls -l / | grep tmp  

Повторите предыдущие шаги (fig. -@fig:009).  
Возможно выполнить все команды из предыдущих шагов.  

Повысьте свои права до суперпользователя и верните атрибут t на директорию /tmp (fig. -@fig:009):  
su -  
chmod +t /tmp  
exit  

![Исследование Sticky-бита](image/9.jpg){ #fig:009 width=70% }

# Выводы

Изучил механизмы изменения идентификаторов, применение
SetUID- и Sticky-битов. Получил практические навыки работы в консоли с дополнительными атрибутами. Рассмотрел работу механизма
смены идентификатора процессов пользователей, а также влияние бита
Sticky на запись и удаление файлов.
