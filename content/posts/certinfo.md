---
title: "Certinfo - информация о сертификате"
date: 2024-03-16T17:09:48+03:00
slug: certinfo
aliases:
  - certinfo
weight: 10010
toc_hide: true
tags:
  - linux
---
## Установка и использование

1. Скачиваем и распаковываем готовый бинарник:

```
wget https://github.com/pete911/certinfo/releases/download/v1.0.4/certinfo_1.0.4_linux_amd64.tar.gz
tar xvfz certinfo_1.0.4_linux_amd64.tar.gz
```

2. Выполняем запрос к нужному нам сайту и получаем информацию о цепочке сертификатов на нём:

```
./certinfo youtube.com:443
```

3. Либо указываем конкретный файл сертификата или цепочки сертификатов для вывода информации о нём:

```
cat /etc/letsencrypt/live/chain.pem | ./certinfo 
```

## Проверка срока действия сертификатов.

Проверка срока действия сертификатов с помощью certinfo доступна с ключём -expiry:

```
./certinfo --expiry youtube.com:443
```

Проверка сертификатов в системе:

```
ls -d /etc/ssl/certs/*.crt | xargs ./certinfo -expiry
```







