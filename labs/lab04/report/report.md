---
## Front matter
title: "Отчёт по лабораторной работе №4"
subtitle: "Архитектура компьютера"
author: "Рогожина Надежда Александровна"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Целью работы является освоение процедуры оформления отчетов с помощью легковесного языка разметки Markdown.

# Задание

1. В соответствующем каталоге сделайте отчёт по лабораторной работе №3 в формате Markdown. В качестве отчёта необходимо предоставить отчёты в 3 форматах: pdf, docx и md.
2. Загрузите файлы на github.

# Теоретическое введение
## Базовые сведения о Markdown

Чтобы создать заголовок, используйте знак #, например:

# This is heading 1
## This is heading 2
### This is heading 3
#### This is heading 4

Чтобы задать для текста полужирное начертание, заключите его в двойные звездочки: 

This text is **bold**.

Чтобы задать для текста курсивное начертание, заключите его в одинарные звездочки:

This text is *italic*

Чтобы задать для текста полужирное и курсивное начертание, заключите его в тройные звездочки:

This is text is both ***bold and italic***.

Блоки цитирования создаются с помощью символа >:

> The drought had lasted now for ten million years, and the reign of the terrible lizards had long since ended. Here on the Equator, in the continent which would one day be known as Africa, the battle for existence had reached a new climax of ferocity, and the victor was not yet in sight. In this barren and desiccated land, only the small or the swift or the fierce could flourish, or even hope to survive.

Упорядоченный список можно отформатировать с помощью соответствующих цифр:

1. First instruction
1. Sub-instruction
1. Second instruction
            
Неупорядоченный (маркированный) список можно отформатировать с помощью звездочек или тире:

* List item 1
* List item 2
* List item 3

Синтаксис Markdown для встроенной ссылки состоит из части [link text], представляющей текст гиперссылки, и части (file-name.md) – URL-адреса или имени файла, на который дается ссылка:

```[link text](file-name.md)
или
[link text](http://example.com/ "Необязательная подсказка")
```

Markdown поддерживает как встраивание фрагментов кода в предложение, так и их размещение между предложениями в виде отдельных огражденных блоков. Огражденные блоки кода — это простой способ выделить синтаксис для фрагментов кода. Общий формат огражденных блоков кода:

``` language
your code goes in here
```

## Оформление формул в Markdown

Внутритекстовые формулы делаются аналогично формулам LaTeX. Например, формула ОТТ запишется как
$\sin^2 (x) + \cos^2 (x) = 1$.

## Оформление изображений в Markdown

В Markdown вставить изображение в документ можно с помощью непосредственного указания адреса изображения. Синтаксис данной команды выглядит следующим образом: 

```
![Подпись к рисунку](/путь/к/изображению.jpg "Необязательная 
↪ подсказка"){ #fig:fig1 width=70% } 
```

Здесь: 

* в квадратных скобках указывается подпись к изображению; 

* в круглых скобках указывается URL-адрес или относительный путь изображения, а также (необязательно) всплывающую подсказку, заключённую в двойные или одиночные кавычки;

* в фигурных скобках указывается идентификатор изображения (#fig:fig1) для ссылки на него по тексту и размер изображения относительно ширины страницы (width=90%);

## Обработка файлов в формате Markdown

Преобразовать файл README.md можно следующим образом: 

pandoc README.md -o README.pdf 

или так 

pandoc README.md -o README.docx 

Для компиляции отчетов по лабораторным работам предлагается использовать следующий Makefile 

FILES = $(patsubst %.md, %.docx, $(wildcard *.md)) 

FILES += $(patsubst %.md, %.pdf, $(wildcard *.md)) 

LATEX_FORMAT = 

FILTER = --filter pandoc-crossref 

%.docx: %.md -pandoc "$<" $(FILTER) -o "$@" 

%.pdf: %.md -pandoc "$<" $(LATEX_FORMAT) $(FILTER) -o "$@" 

all: $(FILES) @echo $(FILES) 

clean: -rm $(FILES) *~ 

# Выполнение лабораторной работы

Для выполнения лабораторной работы, нам необходимо установить дополнительное ПО:

1. TeX Live (https://www.tug.org/texlive/) последней версии. 
        
2. Pandoc (https://pandoc.org/) версии v2.18 
        
3. Pandoc-crossref (https://github.com/lierdakil/pandoc-crossref/releases) версии v0.3.13.0)
        
## Установка TeX Live:

![Скачивание архива с официального сайта](/home/narogozhina/Изображения/Лабораторная работа №4/1.png){ #fig:001 width=70% }

![Распаковка архива](/home/narogozhina/Изображения/Лабораторная работа №4/2.png){ #fig:002 width=70% }

![Запуск скрипта install-tl c root правами](/home/narogozhina/Изображения/Лабораторная работа №4/3.png){ #fig:003 width=70% }

![Успешное установление скрипта](/home/narogozhina/Изображения/Лабораторная работа №4/4.png){ #fig:004 width=70% }

![Добавление /usr/local/texlive/2022/bin/x86_64-linux в наш PATH для текущей и будущих сессий](/home/narogozhina/Изображения/Лабораторная работа №4/5.png){ #fig:005 width=70% }

## Установка pandoc и pandoc-crossref:

![Скачивание архива pandoc с исходными файлами](/home/narogozhina/Изображения/Лабораторная работа №4/6.png){ #fig:006 width=70% }

![Скачивание архива pandoc-crossref с исходными файлами](/home/narogozhina/Изображения/Лабораторная работа №4/7.png){ #fig:007 width=70% }

![Распаковка архивов](/home/narogozhina/Изображения/Лабораторная работа №4/8.png){ #fig:008 width=70% }

![Копирование файлов в локальный каталог](/home/narogozhina/Изображения/Лабораторная работа №4/9.png){ #fig:009 width=70% }

![Проверка выполненных действий](/home/narogozhina/Изображения/Лабораторная работа №4/10.png){ #fig:010 width=70% }

## Ход выполнения работы:

![Перейдем в каталог курса](/home/narogozhina/Изображения/Лабораторная работа №4/11.png){ #fig:011 width=70% }

![Обновим локальный репозиторий](/home/narogozhina/Изображения/Лабораторная работа №4/12.png){ #fig:012 width=70% }

![Перейдем в каталог с шаблоном отчета по лаб. pаботе №4](/home/narogozhina/Изображения/Лабораторная работа №4/13.png){ #fig:013 width=70% }

Чтобы команда make заработала, повторим последнюю команду 

export PATH=$PATH:/usr/local/texlive/2022/bin/x86_64-linux

и затем снова перейдем в нужный нам каталог и проведем компиляцию шаблона с использованием Makefile. Видим, что компиляция прошла успешно и нужные нам файлы были созданы.

![Удалим полученные файлы с использованием Makefile.](/home/narogozhina/Изображения/Лабораторная работа №4/14.png){ #fig:014 width=70% }

![Изучим структуру документа, а также оформим отчет по лабораторной работе №3 в формате Markdown](/home/narogozhina/Изображения/Лабораторная работа №4/15.png){ #fig:015 width=70% }

![Скомпилируем отчет еще в 2 форматах(командой make):](/home/narogozhina/Изображения/Лабораторная работа №4/16.png){ #fig:016 width=70% }

![Подгрузим отчеты и снимки экрана на github.com](/home/narogozhina/Изображения/Лабораторная работа №4/17.png){ #fig:017 width=70% }

![Проверим правильность выполненных действий](/home/narogozhina/Изображения/Лабораторная работа №4/18.png){ #fig:018 width=70% }

Аналогичным образом оформим отчет по лабораторной работе №4 и подгрузим его на github.com

# Выводы

В процессе выполнения работы мне удалось изучить систему работы с языком разметки markdown, а также отработать навыки написания отчета на данном языке.

1. Markdown - язык разметки.

2. Начертание шрифтов задается в коде в начале документа.

3. Упорядоченный список можно отформатировать с помощью соответствующих цифр:

 1. First instruction
  1. Sub-instruction
 1. Second instruction

Чтобы вложить один список в другой, добавьте отступ для элементов дочернего списка:

1. First instruction
 1. Second instruction
  1. Third instruction
            
Неупорядоченный (маркированный) список можно отформатировать с помощью звездочек или тире:

* List item 1
* List item 2
* List item 3

4. В Markdown вставить изображение в документ можно с помощью непосредственного указания адреса изображения. Синтаксис данной команды выглядит следующим образом: 

```
![Подпись к рисунку](/путь/к/изображению.jpg "Необязательная 
↪ подсказка"){ #fig:fig1 width=70% } 
```

Здесь: 

• в квадратных скобках указывается подпись к изображению; 

• в круглых скобках указывается URL-адрес или относительный путь изображения, а также (необязательно) всплывающую подсказку, заключённую в двойные или одиночные кавычки. 

• в фигурных скобках указывается идентификатор изображения (#fig:fig1) для ссылки на него по тексту и размер изображения относительно ширины страницы (width=90%)

5. Внутритекстовые формулы делаются аналогично формулам LaTeX. Например, формула ОТТ запишется как
$\sin^2 (x) + \cos^2 (x) = 1$.

