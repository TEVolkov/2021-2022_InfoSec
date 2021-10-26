---
# Front matter
lang: ru-RU
title: "Отчёт по лабораторной работе №4"
subtitle: "Дискреционное разграничение прав в Linux. Расширенные атрибуты."
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

Получение практических навыков работы в консоли с расширенными атрибутами файлов.

# Выполнение лабораторной работы

От имени пользователя guest определите расширенные атрибуты файла
/home/guest/dir1/file1 (fig. -@fig:001) командой  
*lsattr /home/guest/dir1/file1*  
  
Установите командой
*chmod 600 file1*
на файл file1 права, разрешающие чтение и запись для владельца файла (fig. -@fig:001)  

Попробуйте установить на файл /home/guest/dir1/file1 расширенный атрибут *a* от 
имени пользователя guest (fig. -@fig:001):  
*chattr +a /home/guest/dir1/file1*  
В ответ вы должны получить отказ от выполнения операции.  

Зайдите на консоль с правами администратора.
Попробуйте установить расширенный атрибут a на файл /home/guest/dir1/file1 
от имени суперпользователя (fig. -@fig:001):  
*chattr +a /home/guest/dir1/file1*    

От пользователя guest проверьте правильность установления атрибута (fig. -@fig:001):  
*lsattr /home/guest/dir1/file1*  

![Установка расширенных прав](image/1.jpg){ #fig:001 width=70% }

Выполните дозапись в файл file1 слова «test» (fig. -@fig:002) командой  
*echo "test" /home/guest/dir1/file1*  
После этого выполните чтение файла file1 (fig. -@fig:002) командой  
*cat /home/guest/dir1/file1*  
Убедитесь, что слово test было успешно записано в file1.  

Попробуйте стереть имеющуюся в file1 информацию (fig. -@fig:002) командой  
*echo "abcd" > /home/guest/dirl/file1*  
Попробуйте переименовать файл (fig. -@fig:002)  

Попробуйте с помощью команды  
*chmod 000 file1*  
установить на файл file1 права (fig. -@fig:002), например, запрещающие чтение и запись для владельца файла.   
Успешно выполнить указанные команды кроме дозаписи и чтения файла не удалось.

Снимите расширенный атрибут *a* с файла /home/guest/dirl/file1 от
имени суперпользователя (fig. -@fig:002) командой  
*chattr -a /home/guest/dir1/file1*  

![Проверка установленных прав](image/2.jpg){ #fig:002 width=70% }

Повторите операции, которые вам ранее не удавалось выполнить (fig. -@fig:003). 
Успешно выполнились все команды.

![Повторная проверка установленных прав](image/3.jpg){ #fig:003 width=70% }

Повторите ваши действия по шагам, заменив атрибут «a» атрибутом «i» (fig. -@fig:004).    
Успешно выполнить указанные команды кроме дозаписи не удалось.   

![Установка атрибута i](image/4.jpg){ #fig:004 width=70% }

# Выводы

В результате выполнения работы повысил свои навыки использования 
интерфейса командой строки (CLI), 
познакомилcz на примерах с тем,
как используются основные и расширенные атрибуты при разграничении
доступа. Имел возможность связать теорию дискреционного разделения
доступа (дискреционная политика безопасности) с её реализацией на практике в ОС Linux. 
Составил наглядные таблицы, поясняющие какие операции возможны при тех или иных установленных 
правах. Опробовал действие на практике расширенных атрибутов «а» и «i».
