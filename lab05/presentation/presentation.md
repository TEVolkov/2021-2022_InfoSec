---
# Front matter
lang: ru-RU
title: "Лабораторная работа № 5. Дискреционное разграничение прав в Linux. Исследованиевлияния дополнительных атрибутов"
author: "Волков Тимофей Евгеньевич  НПИбд-01-18"


## Formatting
toc: false
slide_level: 2
theme: metropolis
header-includes: 
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
 - '\makeatletter'
 - '\beamer@ignorenonframefalse'
 - '\makeatother'
aspectratio: 43
section-titles: true
---

## Цель работы

Изучение механизмов изменения идентификаторов, применения
SetUID- и Sticky-битов. Получение практических навыков работы в консоли с дополнительными атрибутами. Рассмотрение работы механизма
смены идентификатора процессов пользователей, а также влияние бита
Sticky на запись и удаление файлов.

## Изучение SetUID- SetGID-бита 

![Программа simpleid2.c](image/3.jpg){ #fig:003 width=70% }

## Изучение SetUID- SetGID-бита 

![Установка SetUID-бита](image/5.jpg){ #fig:005 width=70% }

## Изучение SetUID- SetGID-бита 

![Установка SetGID-бита](image/6.jpg){ #fig:006 width=70% }

## Изучение SetUID- SetGID-бита 

![Программа readfile.c](image/7.jpg){ #fig:007 width=70% }

## Изучение SetUID- SetGID-бита 

![Проверка работы программы readfile](image/8.jpg){ #fig:008 width=70% }

##  Исследование Sticky-бита

![Исследование Sticky-бита](image/9.jpg){ #fig:009 width=70% }

