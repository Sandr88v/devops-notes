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
sudo dpkg -ihugo_extended_0.120.4_linux-amd64.deb
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
