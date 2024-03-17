---
title: "Markdown_cheat_sheet"
date: 2024-03-17T16:30:12+03:00
slug: markdown_sheet
aliases:
  - markdown_sheet
weight: 10010
toc_hide: true
tags:
  - markdown
  - linux
---

Markdown — это широко используемый стандарт для распространения текстовых файлов со специальным синтаксисом, который современное программное обеспечение может легко понять и отформатировать, что устраняет необходимость написания всего HTML-кода.

Считайте это способом добавить стиль и структуру HTML к вашему текстовому документу в простой и удобочитаемой форме, чтобы люди без опыта программирования могли легко понять и запомнить.

Из-за своей простоты почти все файлы README на GitHub представляют собой файлы уценки с именем « README.md«. Широко используемый генератор статических сайтов Hugo по умолчанию также использует его для записей и страниц, а в редакторе блоков WordPress вы можете использовать его для мгновенной генерации определенных элементов.

## Как читать и записывать файлы Markdown (шпаргалка)

1. Синтаксис объявления заголовков HTML.
```
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6
```
Интерпретируется как:

# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6


2. Синтаксис оформления текста жирным шрифтом и курсивом.

```
**bold text**

*italic text*
```
Интерпретируется как:

**bold text**

*italic text*

3. Синтаксис объявления блочных кавычек и вложенных кавычек.
```
> single blockquotes

> blockquotes
>> nested blockquotes
```

Интерпретируется как:

> single blockquotes

> blockquotes
>> nested blockquotes


4. Синтаксис создания горизонтальной линии (или разделителя).

```
# The following are three hyphens to create a horizontal line.
---
lorem ipsum
```

Интерпретируется как:

# The following are three hyphens to create a horizontal line.
---
lorem ipsum

5. Синтаксис для создания упорядоченных и неупорядоченных списков.
```
# Ordered List

1. First Item
2. Second Item
3. Third Item

# Unordered List

- First Item
- Second Item
- Third Item
```

Интерпретируется как:

# Ordered List

1. First Item
2. Second Item
3. Third Item

# Unordered List

- First Item
- Second Item
- Third Item

6. Синтаксис создания блоков кода.

```
` $ echo "Linux TLDR is great site to learn about Linux." `
```
Интерпретируется как:

` $ echo "Linux TLDR is great site to learn about Linux." `

7. Синтаксис добавления (или вставки) ссылок.

```
[title](https://www.example.com)

[Linux TLDR](https://www.linuxtldr.com)
```
Интерпретируется как:

[title](https://www.example.com)

[Linux TLDR](https://www.linuxtldr.com)


8. Синтаксис добавления (или вставки) изображений.
```
![alt text](image.jpg)
```

9. Синтаксис включения ссылки в изображение.
```
[![title](image.jpg "Image Alt Text")](https://linuxtldr.com)
```

10. Синтаксис создания таблицы.
```
| No          | Person      | Age         | 
| ----------- | ----------- | ----------- |
| 01          | Chris       | 36          |
| 02          | Dennis      | 25          |
| 03          | David       | 24          |
| 04          | Thomas      | 47          |
```

Интерпретируется как:

| No          | Person      | Age         | 
| ----------- | ----------- | ----------- |
| 01          | Chris       | 36          |
| 02          | Dennis      | 25          |
| 03          | David       | 24          |
| 04          | Thomas      | 47          |

11. Синтаксис для определения изолированного (или многострочного) блока кода.

```
$ echo "This is the first sentence"
$ echo "This is the second sentence"
$ echo "This is the third sentence"
``` 

Интерпретируется как:

```
$ echo "This is the first sentence"
$ echo "This is the second sentence"
$ echo "This is the third sentence"
``` 
12. Синтаксис создания идентификатора заголовка и ссылки редиректора.

```
### Heading 01 {#ref-h1-id}

lorem ipsum

[Redirect to Heading 01](#ref-h1-id)
```

Интерпретируется как:

### Heading 01 {#ref-h1-id}

lorem ipsum

[Redirect to Heading 01](#ref-h1-id)

13. Синтаксис создания сносок.

Сноски — это способ создать заметку, а затем добавить к ней ссылку, по которой пользователи могут щелкнуть мышью и перенаправиться к созданной заметке.

```
Here's a sentence with a footnote. [^1]

lorem ipsum

[^1]: This is the footnote. 
```

Интерпретируется как:

Here's a sentence with a footnote. [^1]

lorem ipsum

[^1]: This is the footnote. 

14. Синтаксис для создания списка определений.
```
term
: definition

---

Linux TLDR
: Welcome to Linux TLDR, your ultimate destination for all things Linux! We are passionate about open-source technology and dedicated to providing you with the latest news, tutorials, tips, and resources to help you master the world of Linux and open-source software.
```
Интерпретатор как:

term
: definition

---

Linux TLDR
: Welcome to Linux TLDR, your ultimate destination for all things Linux! We are passionate about open-source technology and dedicated to providing you with the latest news, tutorials, tips, and resources to help you master the world of Linux and open-source software.

15. Синтаксис зачеркивания текста.
```
~~Cat's never bite~~
```
Интерпретатор как:

~~Cat's never bite~~

16. Синтаксис создания списка задач.

Задачи не могут работать вместе с внутренним сервером, но это хороший способ отобразить конкретный ход работы или предоставить обновление статуса.
```
- [x] Project Blueprint
- [x] Project Design
- [ ] Budget Allocation
```

Интерпретатор как:

- [x] Project Blueprint
- [x] Project Design
- [ ] Budget Allocation

17. Добавление смайлов с помощью копирования или шорткода.

Вы можете добавить смайлы в свой файл Markdown двумя разными способами: первый — путем прямого копирования и вставки их с сайтов, предоставляющих смайлы, таких как Emojipedia , или с помощью короткого кода смайлов ( get list ).

Интерпретируется как:
```
## What did the cat say to the fishbowl?

You're looking fin-tastic today! :laughing:
```

Интерпретируется как:

## What did the cat say to the fishbowl?

You're looking fin-tastic today! :laughing:

18. Отключение автоматического связывания URL.
```
Automatic URL linked
//www.linuxtldr.com

Disable automatic URL linking
`//www.linuxtldr.com`
```

Интерпретируется как:

Automatic URL linked
//www.linuxtldr.com

Disable automatic URL linking
`//www.linuxtldr.com`

19. Добавление выделения в текст.
```
In Linux World, ==Linux TLDR== would be the best site.
```
Интерпретируется как:

In Linux World, ==Linux TLDR== would be the best site.

20. Указание нижнего и верхнего индекса.
```
C~2~H~3~O~2~NH~4~
X^3^Y^6
```
Интерпретируется как:

C~2~H~3~O~2~NH~4~
X^3^Y^6

Как практиковать синтаксис Markdown (онлайн и оффлайн)

Самый простой способ попрактиковаться в синтаксисе Markdown — использовать онлайн-платформы, такие как readme.so (обычно используется для создания файлов readme GitHub), или вы можете изучить Dillinger (который превосходен и поддерживает почти весь расширенный синтаксис).

Если вы предпочитаете офлайн-режим, вы можете попробовать расширение Runme Runs Markdown для VSCode. По установке вы можете ознакомиться с нашей отдельной статьей о VSCode и его расширениях.

И есть еще одно потрясающее автономное программное обеспечение под названием Marker (бесплатное и с открытым исходным кодом) или Typora (премиум), которое может легко позволить вам читать и писать, начиная с базового и расширяя синтаксис уценки, включая другие дополнительные функции.

## Оживите свой файл Markdown с помощью этих популярных процессоров

Весь синтаксис Markdown, является стандартным и поддерживается всеми процессорами Markdown. Однако существует целый ряд других процессоров, которые предоставляют дополнительные возможности.

Cемь лучших обработчиков уценки:

- Pandoc
- Commonmark
- Kramdown
- Goldmark
- AsciiDoc
- Org Mode
- reStructuredText





















