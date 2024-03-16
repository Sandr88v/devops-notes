---
title: "Шпаргалка по Ansible"
date: 2024-03-16T12:19:16+03:00
slug: ansible_trips
aliases:
  - anssible_trips
weight: 10010
toc_hide: true
tags:
  - ansible
  - trips
---

## Шпаргалка по Ansible, часто используемые команды

Шпаргалка по Ansible — листинг команд, которые постоянно нужны при работе с системой управления серверами. К каждой команде приведены краткие комментарии.

### Работа с задачами с использованием playbook

Вывести список в всех задач в playbook

```
ansible-playbook play.yml --list-tasks
```

Начать выполнение playbook с определенной задачи

```
ansible-playbook play.yml --start-at-task="task name"
```

Выполнять задачи из playbook одну за одной. Одну задачу за раз.

```
ansible-playbook play.yml --step
```

### Синтаксис и проверка playbook

Проверить синтаксис playbook и вывести ошибки в консоль (если они есть)

```
ansible-playbook play.yml --check-syntax
```

Работа в режиме, аналогичном dry-run. Симулируется исполнение инструкций, фактически никаких изменений на подконтрольных серверах не вносится

```
ansible-playbook play.yml --check
```

### Разделение хостов и групп хостов

Вывести список хостов, к которым будет применен указанный playbook

```
ansible-playbook play.yml --list-hosts
```

Вывести список машин, входящих в группу «subnet»

```
ansible-playbook play.yml --list-hosts -l subnet
```

Список тэгов в playbook

```
ansible-playbook play.yml --list-tags
```

Отсортировать задачи по тэгам
```
ansible-playbook play.yml --tags tag1,tag2
```

Отсортировать по тэгам с исключением (выбрать все тэги, кроме указанных)

```
ansible-playbook play.yml --skip-tags tag1,tag2
```

Выполнять параллельно определенное количество команд (число нужно подставить вместо NUM)

```
ansible-playbook play.yml --forks=NUM
```
По умолчанию значение равно пяти.

Без группы или вхождения в /etc/ansible/hosts применить playbook к машине можно так

```
ansible-playbook play.yml -i [IP|Server Name],
```
В конце — после домена или IP адреса, обязательно следует запятая.



