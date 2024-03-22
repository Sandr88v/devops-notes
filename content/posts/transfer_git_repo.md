---
title: "Перенос git репозитория"
date: 2024-03-22T10:34:33+03:00
slug: git_trasfer
aliases:
  - git_transfer
weight: 10010
toc_hide: true
tags:
  - git
---

Небольшой набор команд для переноса одного git репозитория в другой. Я, например, пользовался при переносе из Github в Gitlab.
```
git clone --bare git@git.test.com:my-repo-a.git
cd my-repo-a.git
git fetch origin
git remote add new-origin git@git.test.com:my-repo-b.git
git push --mirror new-origin
git remote rm origin
git remote rename new-origin origin
```
Разберем команды:

git clone --bare — клонируем не сам репозиторий, а директорию .git

git fetch origin — убеждаемся, что у нас все изменения присутствуют

git remote add — добавляем новый remote репозиторий

git push --mirror new-origin — загружаем весь наш репозиторий в новый. mirror передает все refs — тэги, бранчи

git remote rm — удаляем старый origin локально

git remote rename — переименовываем new-origin в origin, чтобы было проще работать