---
# Front matter
lang: ru-RU
title: "Лабораторная работа № 2. Дискреционное разграничение прав в Linux. Основные атрибуты"
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

Получение практических навыков работы в консоли с атрибутами файлов, закрепление 
теоретических основ дискреционного разграничения доступа в современных системах с 
открытым кодом на базе ОС Linux.   

## Создание учётной записи пользователя guest

![Вход в систему пользователем guest](image/2.jpg){ #fig:001 width=70% }

## Просмотр информации о пользователе

![Информация о пользователе](image/4.jpg){ #fig:002 width=70% }

## Создание поддиректории dir1

![Права доступа и расширенные атрибуты 
директории dir1](image/8.jpg){ #fig:003 width=70% }

## Изменение прав доступа

![Попытка создания в директории dir1 файла file1](image/10.jpg){ #fig:04 width=70% }

## Установленные права и разрешённые действия

![Установленные права и разрешённые действия (часть 1)](image/211.jpg){ #fig:05 width=70% }

## Установленные права и разрешённые действия

![Установленные права и разрешённые действия (часть 2)](image/212.jpg){ #fig:06 width=70% }

## Минимально необходимые права для выполнения операций

![Минимальные права для совершения операций](image/221.jpg){ #fig:07 width=70% }
