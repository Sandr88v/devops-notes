---
title: "Установка CMS Hugo"
date: 2024-03-10T15:07:22+03:00
slug: hugo
aliases:
  - hugo
weight: 10010
toc_hide: true
tags:
  - hugo
  - linux
---
## Установка Hugo
Hugo является генератором статических сайтов, который вы можете использовать для создания своего сайта. Чтобы начать, вам нужно установить Hugo на свой компьютер. В этом разделе мы распишем процесс установки Hugo на Linux, Mac OS и Windows.

## Установка Hugo в Linux

```
wget https://github.com/gohugoio/hugo/releases/download/v0.120.4/hugo_extended_0.120.4_linux-amd64.deb
```

```
sudo dpkg -i hugo_extended_0.120.4_linux-amd64.deb
```
Проверить версию Hugo
```
hugo version
```

## Создание нового сайта с Hugo

После установки Hugo нужно создать новый сайт. Для этого нужно открыть терминал, перейти в директорию в которой у вас будут храниться файлы сайта и ввести следующую команду:
```
hugo new site MyFreshWebsite --format yaml
# replace MyFreshWebsite with name of your website
```
После этого Hugo создаст структуру каталогов для вашего сайта.

Примечание:
```
Старые версии Hugo могут не поддерживать --format yaml
```
## Hugo команды и конфигурация

Команды CLI:
```
hugo check — запускает различные проверки
hugo config – отображает конфигурацию сайта Hugo
hugo convert - конвертирует контент в разные форматы
hugo deploy – развертывает ваш сайт у облачного провайдера
hugo env – отображает версию Hugo и информацию о среде
hugo gen - обеспечивает доступ к различным генераторам
hugo help – отображает информацию о команде
hugo import – позволяет импортировать сайт из другого места
hugo list – отображает список различных типов контента
hugo mod – обеспечивает доступ к различным помощникам модуля
hugo new – позволяет создавать новый контент для вашего сайта
hugo server – запускает локальный сервер разработки
hugo version – отображает текущую версию
hugo help - вывода списка всех доступных флагов
```
## Назначения директорий сайта Hugo

Краткое описание назначения каталогов созданных Hugo

```
└───test
    │   config.toml
    │
    ├───archetypes
    │       default.md
    │
    ├───assets
    ├───content
    ├───data
    ├───layouts
    ├───public
    ├───static
    └───themes
```
Чтобы вывести дерево каталогов используется команда tree
```
config.toml : Конфигурационный файл. Содержит настройки сайта
archetypes : Для шаблонов, часто используемых элементов на страницах сайта.
assets : Хранит все файлы, которые должны быть обработаны Hugo Pipes . Только файлы, чьи .Permalink или .RelPermalink будут опубликованы в public каталоге.
content : Контент одним словом. Тексты постов.
data : Этот каталог используется для хранения файлов конфигурации, которые используются Hugo при создании веб-сайта. Файлы должны быть в формате YAML, JSON или TOML. В дополнение к файлам, которые размещаются в этой папке, можно создавать шаблоны данных , которые извлекаются из динамического содержимого.
layouts : Хранит шаблоны в виде файлов .html, которые определяют, как просмотры вашего контента будут отображаться на статическом веб-сайте.
public : Здесь будет находится готовый сайт, файлы этой папки необходимо размещать на своем хостинге. Любым удобным способом скопировать на сервер.
static : Любые статические файла изображения, видео, css, html и т.д. и т.п.
themes : Папка для хранения тем, которые скачиваем или клонируем. Их может быть множество, но использоваться может только одна.
```
