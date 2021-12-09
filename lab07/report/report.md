---
# Front matter
lang: ru-RU
title: "Отчёт по лабораторной работе №7"
subtitle: "Элементы криптографии. Однократное гаммирование"
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

Освоить на практике применение режима однократного гаммирования.

# Теоретическое описание

Предложенная Г. С. Вернамом так называемая «схема однократного использования (гаммирования)» 
является простой, но надёжной схемой шифрования данных.  
Гаммирование представляет собой наложение (снятие) на открытые (зашифрованные) данные 
последовательности элементов других данных, полученной с помощью некоторого криптографического 
алгоритма, для получения зашифрованных (открытых) данных. Иными словами, наложение
гаммы — это сложение её элементов с элементами открытого (закрытого)
текста по некоторому фиксированному модулю, значение которого представляет собой известную 
часть алгоритма шифрования.  
В соответствии с теорией криптоанализа, если в методе шифрования используется однократная 
вероятностная гамма (однократное гаммирование)
той же длины, что и подлежащий сокрытию текст, то текст нельзя раскрыть.
Даже при раскрытии части последовательности гаммы нельзя получить информацию о всём 
скрываемом тексте.  
К. Шеннон доказал абсолютную стойкость шифра в случае, когда однократно используемый ключ, 
длиной, равной длине исходного сообщения,
является фрагментом истинно случайной двоичной последовательности с
равномерным законом распределения. Криптоалгоритм не даёт никакой информации об 
открытом тексте: при известном зашифрованном сообщении
C все различные ключевые последовательности K возможны и равновероятны, а значит, возможны 
и любые сообщения P.  
Необходимые и достаточные условия абсолютной стойкости шифра:
– полная случайность ключа;
– равенство длин ключа и открытого текста;
– однократное использование ключа.

# Выполнение лабораторной работы

Требуется разработать приложение, позволяющее шифровать и
дешифровать данные в режиме однократного гаммирования. 

Функции (fig. -@fig:001):   
hex_ --- перевод в шестнадцатиричную систему.  
gen_key --- генерирует рандомный ключ.  
encrypt --- шифрует текст.  
decrypt --- дешифрует тескт.  
compute_key --- создает ключ на основе текста и шифротекста.  

![Функции](image/1.jpg){ #fig:001 width=70% }

1. Определить вид шифротекста при известном ключе и известном открытом тексте (fig. -@fig:002).  

![Задание 1](image/2.jpg){ #fig:002 width=70% }  

2. Определить ключ, с помощью которого шифротекст может быть преобразован в некоторый 
фрагмент текста, представляющий собой один из возможных вариантов прочтения открытого текста (fig. -@fig:003).

![Задание 2](image/3.jpg){ #fig:003 width=70% } 

# Выводы

Освоил на практике применение режима однократного гаммирования.

# Контрольные вопросы

1. Поясните смысл однократного гаммирования.  
Гаммирование — метод симметричного шифрования, заключающийся в «наложении» последовательности, 
состоящей из случайных чисел, на открытый текст. Последовательность случайных чисел называется 
гамма-последовательностью и используется для зашифровывания и расшифровывания данных.  

2. Перечислите недостатки однократного гаммирования.  
Ключ одного размера с сообщением, на один ключ используется только один текст.  

3. Перечислите преимущества однократного гаммирования.  
Простота, криптостойкость.  

4. Почему длина открытого текста должна совпадать с длиной ключа?  
Каждый символ текста попарно складывается с символом ключа.  

5. Какая операция используется в режиме однократного гаммирования, назовите её особенности?  
Используется сложение по модулю 2.  

6. Как по открытому тексту и ключу получить шифротекст?  
Сложить по модулю 2 каждый символ открытого текста и ключа.  

7. Как по открытому тексту и шифротексту получить ключ?  
Сложить по модулю 2 каждый символ открытого текста и шифротекста.  

8. В чем заключаются необходимые и достаточные условия абсолютной
стойкости шифра?  
– полная случайность ключа;
– равенство длин ключа и открытого текста;
– однократное использование ключа.  
