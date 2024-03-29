---
title: "Подробная инструкция по работе с SCP"
date: 2024-03-16T12:50:40+03:00
slug: scp_command
aliases:
  - scp_command
weight: 10010
toc_hide: true
tags:
  - linux
---

SCP (Secure Copy Protocol) — это протокол для копирования файлов между удаленными хостами по SSH протоколу. Ниже приведена подробная инструкция по использованию SCP с большим количеством возможностей.

1. Подключение к удаленному хосту

Для подключения к удаленному хосту через SSH используйте следующую команду:

```
ssh [опции] [имя пользователя]@[адрес или имя хоста]
```

Например, чтобы подключиться к удаленному хосту с адресом 192.168.1.100 под именем пользователя user, выполните следующую команду:
```
ssh user@192.168.1.100
```

2. Копирование файлов

Для копирования файла с локального хоста на удаленный хост используйте следующую команду:
```
scp [опции] [путь к локальному файлу] [имя пользователя]@[адрес или имя хоста]:[путь на удаленном хосте]
```

Чтобы скопировать файл /home/user/docs/file.txt на удаленный хост 192.168.1.100 в директорию /home/user/backup/, выполните следующую команду:

```
scp /home/user/docs/file.txt user@192.168.1.100:/home/user/backup/
```

Для копирования файла с удаленного хоста на локальный хост используйте следующую команду:

```
scp [опции] [имя пользователя]@[адрес или имя хоста]:[путь на удаленном хосте] [путь на локальном хосте]
```
Например, чтобы скопировать файл /home/user/docs/file.txt с удаленного хоста 192.168.1.100 на локальный хост в директорию /home/user/backup/, выполните следующую команду:

```
scp user@192.168.1.100:/home/user/docs/file.txt /home/user/backup/
```

Если необходимо скопировать целую директорию, используйте опцию -r, например:

```
scp -r /home/user/docs/ user@192.168.1.100:/home/user/backup/
```

3. Опции SCP

SCP имеет множество опций, которые расширяют его возможности:

```
-P [порт]: указывает порт SSH на удаленном хосте для подключения
-v: выводит подробную отладочную информацию о процессе передачи файла
-p: сохраняет атрибуты файла, такие как время изменения, владелец и права доступа
-q: запускает SCP в тихом режиме, без вывода сообщений
-C: включает сжатие данных при передаче
```

