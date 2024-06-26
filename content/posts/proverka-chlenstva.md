---
title: "Проверка членства пользователей в группах"
date: 2024-05-09T11:29:08+03:00
slug: proverka_chlenstva
aliases:
  - proverka_chlenstva
weight: 10010
toc_hide: true
tags:
  - linux
---

Очень часто необходимо посмотреть список пользователей Linux в определенной группе, что понять, имеет ли он доступ к определенному ресурсу.

Вот список полезных команд.

Для начала получим полный список всех пользователей системы Linux из файла /etc/passwd:
```
cat /etc/passwd | cut -d: -f1
```

Такой же список пользователей можно получить командой:
```
getent passwd
```

Если вам требуется информация по конкретному пользователю, то добавьте юзернейм этого пользователя в конце:
```
getent passwd <username>
```

Аналогично, чтобы посмотреть список имеющихся групп, который содержится в файл /etc/group (группы выводятся согласно увеличения их номера GUID):

```
cat /etc/group | cut -d: -f1
```

Теперь, имея список групп перед глазами, мы можем посмотреть членов нужной группы:
```
cat /etc/group | grep
```

Тот же эффект можно получить командой:

```
getent group <groupname>
```

А чтобы получить список групп, членом которых является нужный пользователь, запустите:

```
groups <username>
```
