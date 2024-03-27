---
title: "Локальное хранилище Git: git stash"
date: 2024-03-26T11:10:35+03:00
slug: git_stash
aliases:
  - git_stash
weight: 10010
toc_hide: true
tags:
  - git
---

## Что делает команда git stash

Команда git stash упрощает работу с изменениями в коде. Она помогает быстро сохранить всё в архив и скрыть правки, чтобы переключиться на другую ветку и продолжить работу без них.

При этом изменения не добавляются в репозиторий в виде коммита: они складываются в локальное хранилище на компьютере. Этим git stash и удобна.

## git stash save

Код ещё не дописан, поэтому коммитить его в основную ветку — бессмысленно. Значит, нам нужно сохранить изменения локально. Для этого воспользуемся командой git stash save:
```
git status
On branch main
Changes not staged for commit:

    modified:   index.html
    modified:   style.css

$ git stash save
Saved working directory and index state WIP on main: 4532d67 our new homepage
HEAD is now at 4532d67 our new homepage

$ git status
On branch main
nothing to commit, working tree clean
```
Мы видим, что изначально у нас были изменения в файлах: index.html и style.css. А после запуска команды git stash save все изменения пропали — но это не навсегда.

Теперь все правки лежат в локальном хранилище, а наш проект как бы находится в состоянии, в котором он был до того, как мы начали фиксить баг. В подобный локальный архив можно положить сколько угодно сохранений. Все они будут лежать там в виде списка, или, лучше сказать, стека, работающего по принципу: «Первый вошёл — первый вышел».

Хорошо, мы можем сложить много изменений в хранилище — но как мы потом разберём, какое именно сохранение нам нужно достать. Хотелось бы как-то подписать все эти сейвы. Для этого нужно всего лишь указать в кавычках имя сохранения:
```
$ git stash save "Bug Fix: Main page"
```
Ещё может так случиться, что мы добавили новые файлы, которых изначально в проекте не было, — следовательно, их нам тоже нужно будет спрятать. Делается это всё той же командой git stash save, но с добавлением параметра --include-untracked, или -u:
```
$ git stash save -u "Bug Fix: Main page"
```
Если нужно добавить в локальное хранилище все игнорируемые файлы, то используем параметр --all, или -a:
```
$ git stash save -a "Bug Fix: Main page"
```

Есть ещё более продвинутый способ добавления отдельных файлов через git stash — с помощью параметра --patch, или -p. Если указать его, Git будет предлагать вам по очереди все файлы, в которых содержатся изменения, и спрашивать: добавлять ли их в локальное хранилище или нет.
```
$ git stash save -p "Bug Fix: Main page"

$ git stash -p
diff --git a/style.css b/style.css
new file mode 100644
index 0000000..d92368b
--- /dev/null
+++ b/style.css
@@ -0,0 +1,3 @@
+* {
+  color: black;
+}
Stash this hunk [y,n,q,a,d,/,e,?]? y
diff --git a/index.html b/index.html
index 9daeafb..ebdcbd2 100644
--- a/index.html
+++ b/index.html
@@ -1 +1,2 @@
+<link rel="stylesheet" href="style.css"/>
Stash this hunk [y,n,q,a,d,/,e,?]? n
```
Чтобы понять, что означают все эти буквы при выборе, можно ввести знак ?, и появится справка:
```
$ git stash save -p "Bug Fix: Main page"

$ git stash -p
diff --git a/style.css b/style.css
new file mode 100644
index 0000000..d92368b
--- /dev/null
+++ b/style.css
@@ -0,0 +1,3 @@
+* {
+  color: black;
+}
Stash this hunk [y,n,q,a,d,/,e,?]? ?

This lets you choose one path out of a status like selection. After choosing the path, it presents the diff between the index and the working tree file and asks you if you want to stage the change of each hunk. You can select one of the following options and type return: 
    y - stage this hunk 
    n - do not stage this hunk 
    q - quit; do not stage this hunk nor any of the remaining ones
    a - stage this hunk and all later hunks in the file 
    d - do not stage this hunk nor any of the later hunks in the file 
    / - search for a hunk matching the given regex 
    e - manually edit the current hunk 
    ? - print help
```
Основными опциями тут будут y и n, которые означают: откладывать файл или не откладывать.

## git stash list

Мы пошли делать ту самую срочную задачу и быстро её закончили. Пора возвращаться к нашим изменениям. Но для начала нужно посмотреть, что мы вообще закинули в локальное хранилище. Делается это командой git stash list:
```
$ git stash list
stash@{0}: "Bug Fix: Main page"
stash@{1}: WIP on main: 4532d67 our new homepage
```
Команда выводит список всех сохранений и их описания, которые задаются в кавычках после команды git stash save. Мы также видим, что у нас есть непонятное сохранение «WIP on main: 4532d67 our new homepage». Оно получило такое название по дефолту — просто потому, что мы не задали ему название в кавычках.

## git stash show

Посмотрим, что находится внутри наших сохранений — а уже потом применим их к проекту. Используем команду git stash show:
```
$ git stash show
 index.html | 1 +
 style.css | 4 +++
 2 files changed, 5 insertions(+)
```
Когда ввели эту команду, то взяли самое верхнее локальное сохранение — «stash@{0}: "Bug Fix: Main page"». Оно берётся по умолчанию, так как у него индекс 0. Если нам нужно взять другое, придётся дописать к команде stash@{индекс_сохранения}:
```
$ git stash show stash stash@{1}
 index.html | 1 +
 style.css | 4 +++
 2 files changed, 5 insertions(+)
```
Ещё не очень понятно, какие именно в этом сохранении изменения. Чтобы устранить эту неопределённость, воспользуемся параметром --patch, или -p, который покажет разницу между вашими файлами и изменёнными:
```
$ git stash show -p
diff --git a/style.css b/style.css
new file mode 100644
index 0000000..d92368b
--- /dev/null
+++ b/style.css
@@ -0,0 +1,3 @@
+* {
+  color: black;
+  font-size: 16px;
+}
diff --git a/index.html b/index.html
index 9daeafb..ebdcbd2 100644
--- a/index.html
+++ b/index.html
@@ -1 +1,2 @@
+<link rel="stylesheet" href="style.css"/>
```
## git stash apply
Теперь, когда мы нашли нужные изменения, пора их достать и применить к проекту. Для этого воспользуемся командой git stash apply. Она достанет из локального хранилища последнее сохранение:
```
$ git stash apply
On branch main
Changes not staged for commit:

    modified:   index.html
    modified:   style.css
```
Если хотим применить другое сохранение, то указываем его после слова apply:
```
$ git stash apply stash@{1}
On branch main
Changes not staged for commit:

    modified:   index.html
    modified:   style.css
```
## git stash pop

После вызова команды git stash apply изменения всё ещё остаются в локальном архиве. Чтобы достать сохранение и полностью удалить его из хранилища, используем команду git stash pop:
```
$ git status
On branch main
nothing to commit, working tree clean
$ git stash pop
On branch main
Changes not staged for commit:

    modified:   index.html
    modified:   style.css

Dropped refs/stash@{0} (32b3aa1d185dfe6df7b3c3ccgb32cbf3e380ac6a)
```

Если теперь посмотреть список сохранений, последнего там уже не окажется:
```
$ git stash list
stash@{0}: WIP on main: 4532d67 our new homepage
```

Чтобы удалить конкретное сохранение, нужно указать его после слова pop:
```
$ git status
On branch main
nothing to commit, working tree clean
$ git stash pop stash@{1}
On branch main
Changes not staged for commit:

    modified:   index.html
    modified:   style.css

Dropped refs/stash@{0} (32b3aa1d185dfe6df7b3c3ccgb32cbf3e380ac6a)
$ git stash list
stash@{0}: "Bug Fix: Main page"
```

## git stash branch

Хотим создать новую ветку в репозитории со всеми изменениями из локального хранилища. Для этого есть команда git stash branch:
```
$ git stash branch new-main-page
Switched to a new branch 'new-main-page'
On branch new-main-page
Changes not staged for commit:

    modified:   index.html
    modified:   style.css

Dropped refs/stash@{1} (32b3aa1d185dfe6df7b3c3ccgb32cbf3e380ac6a)
```
И вот уже готова новая ветка, в которую накатили все нужные изменения из локального хранилища. При этом сохранение в самом хранилище удалилось:
```
$ git stash list
stash@{0}: WIP on main: 4532d67 our new homepage
```
## git stash drop

Бывает, что нужно удалить старые сохранения из локального хранилища, чтобы они не занимали лишнего места или просто не мешали. Это можно сделать с помощью команды git stash drop:
```
$ git stash list
stash@{0}: "Bug Fix: Main page"
stash@{1}: WIP on main: 4532d67 our new homepage
$ git stash drop stash@{1}
Dropped stash@{1} (17e2697fd8241df61651172b3d58c1f62aae7cdb)
$ git stash list
stash@{0}: "Bug Fix: Main page"
```

## git stash clear

Закончили работу над проектом на сегодня и запушили все коммиты, но список локальных сохранений до сих пор не пуст. Пора его полностью удалить. Применяем команду git stash clear:
```
$ git stash list
stash@{0}: "Bug Fix: Main page"
stash@{1}: WIP on main: 4532d67 our new homepage
$ git stash clear
$ git stash list
```


