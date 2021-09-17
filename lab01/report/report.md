---
# Front matter
lang: ru-RU
title: "Отчёт по лабораторной работе №1"
subtitle: "Установка и конфигурация операционной системы на виртуальную машину."
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

Приобретение практических навыков установки операционной системы на виртуальную машину, настройки минимально необходимых для
дальнейшей работы сервисов.  

# Выполнение лабораторной работы

##Установка и конфигурация операционной системы на виртуальную машину

Запустить виртуальную машину (fig. -@fig:001).

![Менеджер VirtualBox](image/1.jpg){ #fig:001 width=70% }

Проверить в свойствах VirtualBox месторасположение каталога для
виртуальных машин. Для этого в VirtualBox выбрать *Файл Свойства*,
вкладка *Общие*. Моя папка для машин (fig. -@fig:002)  
*C:/Users/veg_2/VirtualBox VMs/tevolkov*

![Окно «Свойства» VirtualBox](image/2.jpg){ #fig:002 width=70% }

Создать новую виртуальную машину. Для этого в VirtualBox выбрать
*Машина Создать*.  
Указать имя виртуальной машины --- Base, тип операционной системы
--- Linux, RedHat (fig. -@fig:003). Указать размер основной памяти виртуальной
машины --- 1024 МБ (fig. -@fig:004).

![Окно «Имя машины и тип ОС»](image/3.jpg){ #fig:003 width=70% }

![Окно «Размер основной памяти»](image/4.jpg){ #fig:004 width=70% }

Задать конфигурацию жёсткого диска — загрузочный, VDI (BirtualBox
Disk Image), динамический виртуальный диск (fig. -@fig:005 – -@fig:007).

![Окно «Виртуальный жёсткий диск»](image/5.jpg){ #fig:005 width=70% }

![Окно «Мастер создания нового виртуального диска»](image/6.jpg){ #fig:006 width=70% }

![Окно «Дополнительные атрибуты виртуального диска»](image/7.jpg){ #fig:007 width=70% }

Задать размер диска — 40 ГБ, его расположение — в данном случае
*C:/Users/veg_2/VirtualBox VMs/tevolkov/Base/Base.vdi* (fig. -@fig:008).

![Окно «Расположение и размер виртуального диска»](image/8.jpg){ #fig:008 width=70% }

Выделить в окне менеджера VirtualBox виртуальную машину Base, и открыть окно Свойства . Папка для снимков виртуальной машины Base имеет путь
*C:/Users/veg_2/VirtualBox VMs/tevolkov/Base/Snapshots*. Для этого надо выбрать в VirtualBox *Свойства* виртуальной машины Base, *Общие* , вкладка
*Дополнительно* (fig. -@fig:009).

![Окно «Свойства» виртуальной машины Base](image/9.jpg){ #fig:009 width=70% }

Выбрать в VirtualBox *Свойства Носители* виртуальной машины Base.
Добавить новый привод оптических дисков и выбрать образ
CentOS-8.4.2105-x86_64-boot.iso (fig. -@fig:010 – -@fig:011).

![Окно «Носители» виртуальной машины Base:
выбор образа оптического диска](image/10.jpg){ #fig:010 width=70% }

![Окно «Носители» виртуальной машины Base](image/11.jpg){ #fig:011 width=70% }

Запустить виртуальную машину Base, выбрать установку системы на
жёсткий диск (fig. -@fig:012).

![Запуск установки системы](image/12.jpg){ #fig:012 width=70% }

Установить русский язык для интерфейса (fig. -@fig:013) и раскладки клавиатуры (fig. -@fig:014).

![Виртуальная машина Base. Установка русского языка](image/13.jpg){ #fig:013 width=70% }

![Виртуальная машина Base. Установка русского языка для
раскладки клавиатуры](image/14.jpg){ #fig:014 width=70% }

Выбрать диск (fig. -@fig:015).

![Конфигурация жёсткого диска](image/16.jpg){ #fig:015 width=70% }

В качестве сетевого имени машины указать «tevolkov.localdomain»
(fig. -@fig:016). Указать часовой пояс «Москва» (fig. -@fig:017).

![Задать сетевое имя виртуальной машины](image/17.jpg){ #fig:016 width=70% }

![Указать часовой пояс «Москва»](image/18.jpg){ #fig:017 width=70% }

![Установка пароля для root](image/19.jpg){ #fig:018 width=70% }

Установить пароль для root (fig. -@fig:018).  

Выбрать вариант установки CentOS (fig. -@fig:019).

![Варианты установки CentOS](image/21.jpg){ #fig:019 width=70% }

Добавить учетную запись (fig. -@fig:020).

![Настройка виртуальной машины: учётная запись](image/25.jpg){ #fig:020 width=70% }

Завершить установку операционной системы (fig. -@fig:021) и перезагрузить её.

![Виртуальная машина Base. Завершение установки](image/22.jpg){ #fig:021 width=70% }

Запустить виртуальную машину принять лицензию и перезапустить. (fig. -@fig:022).

![Информация о лицензии](image/24.jpg){ #fig:022 width=70% }

Подключиться к виртуальной машине с помощью созданной учётной
записи (fig. -@fig:023).

![Подключение к виртуальной машине](image/27.jpg){ #fig:023 width=70% }

Подключить образ диска дополнений гостевой ОС (fig. -@fig:024) и перезапустить машину (fig. -@fig:025).

![Подключение образа диска дополнений гостевой ОС](image/26.jpg){ #fig:024 width=70% }

![Работа виртуальной машины](image/31.jpg){ #fig:025 width=70% }
 
После установки необходимых программ (fig. -@fig:026) можно завершить работу виртуальной машины. 

![Установка mc](image/34.jpg){ #fig:026 width=70% }

# Выводы

Приобрел практические навыки установки операционной системы на виртуальную машину, настройки минимально необходимых для
дальнейшей работы сервисов.  