---
title: "Основы ОС Linux"
date: 2024-04-21T11:24:56+03:00
slug: linux_basics
aliases:
  - linux
weight: 10010
toc_hide: true
tags:
  - linux_basics
---

## Структура каталогов Linux — Файловая система Линукс

Файловая система Linux — это структура, в которой хранится вся информация на компьютере. Для работы с Linux очень важно знать, где что находится и как задействовать файловую систему из оболочки.

В Linux организована иерархия каталогов. В каждом каталоге находятся файлы и другие каталоги. Можно создать ссылку на любой файл или каталог, используя либо полный путь (например, /home/sandr/myfile.txt), либо относительный путь (например, если /home/sandr — это текущий каталог, то можно просто ссылаться на файл через myfile.txt).
- / — Корневой каталог, составляет основу файловой системы. Все файлы и каталоги логически содержатся внутри корневого каталога, независимо от их физического расположения.
- /bin — содержит исполняемые программы, которые являются частью операционной системы Linux. Многие команды Linux, такие как cat, cp, ls, more и tar, находятся в /bin.
/boot — содержит ядро ​​Linux и другие файлы, необходимые для менеджеров загрузки LILO и GRUB.
- /dev — содержит все файлы устройства. Linux рассматривает каждое устройство как особый файл. Все такие файлы находятся в /dev.
- /etc — содержит большинство файлов конфигурации системы и сценариев инициализации в подкаталоге /etc/rc.d.
- /home — Домашний каталог является родительским для домашних каталогов пользователей.
- /lib — содержит файлы библиотеки, включая загружаемые модули драйверов, необходимые для загрузки системы.
- /lost + found — Каталог потерянных файлов. В каждом разделе диска есть каталог «потерян + найден».
- /media — Каталог для монтирования файловых систем на съемных носителях, таких как DVD-ROM, флеш-накопители и Zip-накопители.
- /mnt — каталог для временно смонтированных файловых систем (т.е. программного обеспечения для резервного копирования).
- /opt — дополнительные программные пакеты копируют/устанавливают сюда файлы.
- /proc — специальный каталог в файловой системе виртуальной памяти. Он содержит информацию о различных аспектах системы Linux.
- /root — Домашний каталог пользователя root.
- /run —  В более новых версиях. Предоставляет приложениям стандартное место для хранения необходимых им временных файлов, таких как сокеты и идентификаторы процессов.
- /sbin — содержит административные двоичные файлы. Здесь находятся такие команды, как mount, shutdown, umount.
- /selinux — Если ваш дистрибутив Linux использует SELinux для безопасности. Содержит специальные файлы, используемые SELinux.
- /srv — содержит данные для служб (HTTP, FTP и т.д.), предлагаемых системой.
/sys — специальный каталог, содержащий информацию об устройствах с точки зрения ядра Linux.
- /tmp — временный каталог, который можно использовать как рабочий каталог (хранилище временных файлов). Содержимое этого каталога очищается при каждой загрузке системы.
- /usr — содержит подкаталоги для многих программ, таких как X или оконная система GUI.
- /usr/bin — содержит исполняемые файлы для многих команд Linux. Он не является частью основной операционной системы Linux.
- /usr/include — содержит файлы заголовков для языков программирования C
- /usr/lib — содержит библиотеки для языков программирования C.
- /usr/local — содержит локальные файлы. В нем есть каталоги, похожие на каталоги /usr.
- /usr/sbin — содержит административные команды.
- /usr/share — содержит общие файлы, например файлы конфигурации по умолчанию, изображения, документацию и т.д.
- /usr/src — содержит исходный код ядра Linux.
- /var — содержит различные системные файлы, такие как журнал, почтовые каталоги, спул печати и т.д., количество и размер которых со временем могут меняться.
- /var/cache — область хранения кешированных данных для приложений.
- /var/lib — содержит информацию о текущем состоянии приложений. Программы изменяют это при запуске.
- /var/lock — содержит файлы блокировки, которые проверяются приложениями, так что ресурс может использоваться только одним приложением.
- /var/log — содержит файлы журналов для различных приложений.
- /var/mail — содержит электронные письма пользователей, отправленные системой или сервером.
- /var/opt — содержит переменные данные для пакетов, хранящихся в каталоге opt.
- /var/run — содержит данные, описывающие систему с момента ее загрузки.
- /var/spool — содержит данные, ожидающие обработки.
- /var/tmp — временные файлы, сохраняемые между перезагрузками системы.

## Типы содержимого

Основные типы контента, хранящегося в файловой системе Linux:

- Постоянный (Persistent) — это содержимое, которое должно быть постоянным после перезагрузки, например, параметры конфигурации системы и приложений.
- Время выполнения (Runtime) — контент, созданный запущенным процессом, обычно удаляется перезагрузкой.
- Переменный/Динамический (Variable/Dynamic) — это содержимое может быть добавлено или изменено процессами, запущенными в системе Linux.
- Статический контент (Static) — остается неизменным до тех пор, пока не будет явно отредактирован или перенастроен.

## Корневой каталог (root)

Все в системе Linux находится в каталоге /, известном как root или корневой каталог.

Поскольку все остальные каталоги или файлы происходят от корня, абсолютный путь к любому файлу проходит через корень. Например, если у вас есть файл в /home/user/documents, структура каталогов идет как root -> home -> user -> documents.

## /bin — Основные пользовательские двоичные файлы

Каталог /bin содержит основные пользовательские двоичные файлы (программы), которые должны присутствовать при монтировании системы в однопользовательском режиме. Приложения, например, такие как браузер Firefox, хранятся в /usr/bin, а важные системные программы и утилиты, такие как оболочка bash, находятся в /bin. Каталог /usr может храниться в другом разделе — размещение этих файлов в каталоге /bin гарантирует, что в системе будут эти важные утилиты, даже если другие файловые системы не смонтированы.

/bin непосредственно содержит исполняемые файлы многих основных команд оболочки, таких как ps, ls, ping, grep, cp.

## /boot — Статические загрузочные файлы

Каталог /boot содержит файлы, необходимые для загрузки системы. Включает в себя загрузочное ядро Linux, диск начальной инициализации и файлы конфигурации загрузчика (GRUB).

Однако файлы конфигурации загрузчика находятся в /etc.

## /dev — Файлы устройства

Содержит файлы, представляющие точки доступа к устройствам в системах пользователя. К ним относятся устройства терминала (tty*), жесткие диски (hd* и sd*), оперативная память (ram*) и CD-ROM (cd*). Пользователи могут получить доступ к этим устройствам непосредственно через файлы устройств, однако приложения часто скрывают фактические имена устройств от конечных пользователей.

Linux представляет устройства в виде файлов. Это не настоящие файлы в том виде, в каком мы их знаем, но они отображаются как файлы — например, /dev/sda представляет собой первый диск SATA в системе. Второй диск будет называться /dev/sdb.

## /etc — Файлы конфигурации

Содержит файлы конфигурации администратора. Большинство этих файлов являются обычными текстовыми файлами, которые, если у пользователя есть соответствующие права доступа, можно отредактировать с помощью любого текстового редактора.

## /home — Домашние папки

Содержит каталоги, назначенные каждому обычному пользователю с учетной записью входа. (Суперпользователь — исключение, он использует /root в качестве домашнего каталога.)

## /lib — Основные общие библиотеки

Содержит общие библиотеки, необходимые приложениям в /bin и /sbin для загрузки системы. Библиотеки, необходимые для двоичных файлов в папке /usr/bin, находятся в /usr/lib.

Имена файлов библиотеки: ld* или lib*.so.*

Если вы используете 64-bit операционную систему, то у вас есть пара каталогов: /lib, /lib32 и /lib64. Те библиотеки, которые не содержат кода, специфичного для версии процессора, находятся в папке /lib. Те, которые зависят от версии, находятся в каталогах /lib32 (32-bit) или /lib64 (64-bit), в зависимости от ситуации.

## /lost+found — Восстановленные файлы

В каждой файловой системе Linux есть каталог /lost+found. В случае сбоя файловой системы проверка файловой системы будет выполнена при следующей загрузке. Любые найденные поврежденные файлы будут помещены в каталог lost+found, чтобы вы могли попытаться восстановить как можно больше данных.

## /media — Съемный носитель

Стандартное расположение для автоматически монтируемых устройств, в частности съемных носителей. Если у тома носителя есть имя, то оно обычно используется в качестве точки монтирования. Например, USB-накопитель с именем myusb будет смонтирован как /media/myusb.

## /mnt — Временные точки монтирования

Общая точка монтирования для многих устройств до того, как она была вытеснена стандартным каталогом /media. Некоторые загрузочные системы Linux еще задействуют этот каталог для монтирования разделов жесткого диска и удаленных файловых систем. Многие все еще применяют его для временного монтирования локальных или удаленных файловых систем, которые не монтируются постоянно.

## /opt — Дополнительные пакеты

Структура каталогов, доступная для хранения дополнительного прикладного программного обеспечения. Каталог /opt обычно используется проприетарным программным обеспечением, которое подчиняется стандартной иерархии файловой системы — например, проприетарная программа может выгружать свои файлы в /opt/application при ее установке.

## /proc — Файлы ядра и процессов

Содержит информацию о системных ресурсах.

Каталог /proc похож на каталог /dev, потому что он не содержит стандартных файлов. Он содержит специальные файлы, которые представляют информацию о системе и процессах.

Это псевдофайловая система, которая содержит информацию о запущенном процессе. Например, каталог /proc/{pid} содержит информацию о процессе с этим конкретным pid. Также тут можно получить текстовую информацию о системных ресурсах. Например, узнать uptime /proc/uptime, проверить информацию о процессоре /proc/cpuinfo или проверить использование памяти вашений системой Linux /proc/meminfo.

## /root — Корневой домашний каталог

Домашний каталог суперпользователя root. Этот домашний каталог не находится ниже /home из соображений безопасности.

## /run — Файлы состояния приложения

Каталог /run является довольно новым и предоставляет приложениям стандартное место для хранения необходимых им временных файлов, Таких как сокеты и идентификаторы процессов. Эти файлы нельзя хранить в /tmp, потому что файлы в /tmp могут быть удалены.

## /sbin — Двоичные файлы системного администрирования

Каталог /sbin аналогичен /bin — он содержит важные двоичные файлы системного администрирования, такие как iptables, reboot, fdisk, ifconfig, swapon.

Содержит административные команды и демонические процессы.

## /selinux — Виртуальная файловая система SELinux

Если ваш дистрибутив Linux использует SELinux для обеспечения безопасности (например, Fedora и Red Hat), каталог /selinux содержит специальные файлы, используемые SELinux. Это похоже на /proc.

## /srv — Сервисные данные

Этот каталог предоставляет пользователям расположение файлов данных для конкретной службы, такой как FTP, WWW или CVS. Если вы использовали http-сервер Apache для обслуживания website, то вы вероятно сохранили бы файлы своего веб-сайта внутри каталога /srv.

## /sys —

Содержит параметры для настройки хранения блоков и управления контрольными группами.

## /tmp — Временные файлы

Содержит временные файлы приложений. Эти файлы обычно удаляются при перезапуске вашей системы и могут быть удалены в любое время с помощью таких утилит, как tmpwatch.

## /usr — Пользовательские двоичные файлы и данные только для чтения

Содержит пользовательскую документацию, игры, графические файлы (X11), библиотеки (lib) и множество других команд и файлов, не требующихся в процессе загрузки. Каталог /usr предназначен для файлов, которые не изменяются после установки (теоретически /usr может быть смонтирован только для чтения).

## /var — Файлы переменных данных

Содержит каталоги данных приложений. В частности, именно здесь размещаются файлы, которые передаются через FTP-сервер (/var/ftp) или веб-сервер (/var/www). Он также содержит все файлы системного журнала (/var/log) и файлы, находящиеся в очереди на обработку в /var/spool (такие как mail, cups, news). Каталог /var содержит каталоги и файлы, которые часто изменяются. На серверных компьютерах он обычно создается как отдельная файловая система, которую можно легко расширить.

## Базовые команды файловой системы Linux

Команды для каталогов

Список основных команд:

```
- pwd — вывод полного пути к текущему каталогу.
```
```
- cd — переход с текущего каталога на домашний пользовательский.
```
```
- cd dirname — перейти в папку «dirname».
```
```
- cd / — переход по директориям относительно корневого каталога.
```
```
- ls — просмотреть список файлов в каталоге.
```
```
ls -d */ — просмотреть список папок в текущем каталоге.
```
```
ls dirname — вывод содержимого каталога «dirname» на экран.
```
```
mkdir dirname — создать папку с наименованием «dirname».
```
```
rmdir dirname — удалить папку «dirname».
```
```
rm -rf dirname — удалить папку «dirname» с её содержимым (опция -r) без предупреждения пользователя (опция -f).
```
```
du -h dirname — размер папки «dirname».
```
Помимо этого, существуют полезные сокращения. Например, текущая директория обозначается с помощью «.». Знак «..» позволяет задействовать родительский каталог. Для представления домашней директории используется «~».

Пример использования сокращений:
```
root@test:~/dirname/files# cd ..  # переход в родительский (предыдущий) каталог
root@test:~# du -h .              # вывод данных о размере текущего каталога и его элементов
4,0K    ./files
8,0K    .
root@test:~/dirname# cd ~         # переход в домашний каталог
root@test:~#
```

Команды для файлов

Список основных команд
```
touch file — создать файл
```
```
realpath file — узнать абсолютный путь к файлу.
```
```
stat file1 — получение информации о «file1» (размер файла, дата создания файла и т. д.) и проверка существования файла.
```
```
cat > file — запись в файл.
```
```
cat file — чтение файла.
```
```
echo текст >> file — дописать в файл текст.
```
```
find file — поиск файла.
```
```
mcedit file — редактирование файла (также можно использовать редакторы Nano, Vim и другие).
```
```
cat file1 file2 > file12 — объединение файлов.
```
```
sh filename — запустить файл со сценарием Bash.
```
```
./filename — запустить исполняемый файл.
```
```
cp file1 file2 — копировать файл «file1» с переименованием на «file2». Произойдёт замена файлов, если элемент с таким же названием существует.
```
```
mv file1 file2 — переименовать файл «file1» в «file2».
```
```
mv filename dirname — переместить файл «filename» в каталог «dirname».
```
```
less filename — открыть файл в окне терминала.
```
```
file filename — определение типа файла.
```
```
head filename — вывод нескольких начальных строк из файла на экран (построчное чтение файла). По умолчанию строк 10.
```
```
tail filename — вывод нескольких конечных строк из файла на экран.
```
```
diff file1 file2 — сравнение файлов.
```
```
grep text filename — поиск и вывод строк из файла, содержащих «text».
```
```
rm filename — удалить файл.
```
Подробную информацию об утилитах можно получить, воспользовавшись справочной службой: «man <название утилиты>».

## Базовые команды для работы с терминалом Linux

**Ctrl + Alt + T** — запуск терминала.
**Ctrl + Shift + T** — открыть новую вкладку.
**Ctrl + Shift + W** или **Ctrl + D** — закрыть текущую вкладку (или весь терминал, если вкладка одна).
**Ctrl + Shift + N** — открыть новое окно терминала.
**Ctrl + C** — отмена выполнения ранее введённой команды.

==clear== — очищение окна терминала.
==history== — история ввода.

### Горячие клавиши

**Ctrl + Shift + T** — открыть новую вкладку в терминале.
**Ctrl + Shift + C** — копировать текст из терминала, аналог **Ctrl + C**.

**Ctrl + Shift + V** — вставить текст в терминал, аналог **Ctrl + V**.

**Ctrl + A**, **Ctrl + E** — перемещение в начало/конец строки в терминале.

**Alt + B**, **Alt + F** — перемещение по слову назад/вперёд.

**Alt + D** — удаление следующего слова.

**Ctrl + U** — удалить всё до начала.

**Ctrl + K** — удалить всё до конца.

**Ctrl + L** — очистить экран, не удаляя текущую команду.

### Команды управления пользователями Linux
**sudo adduser username** - чтобы добавить нового пользователя
**sudo passwd -l 'username'** - чтобы изменить пароль пользователя
**sudo userdel -r 'username'** - чтобы удалить вновь созданного пользователя
**sudo usermod -a -G GROUPNAME USERNAME** - чтобы добавить пользователя в группу
**sudo deluser USER GROUPNAME** - чтобы удалить пользователя из группы
**finger** - показывает информацию обо всех вошедших в систему пользователях.
**finger username** - предоставляет информацию о конкретном пользователе.

### Специальные атрибуты файлов

**chattr +a file1** - позволить открывать файл на запись только в режиме добавления
**chattr +c file1** - позволяет ядру автоматически сжимать/разжимать содержимое файла.
**chattr +d file1** - указавет утилите dump игнорировать данный файл во время выполнения backup'а
**chattr +i file1** - делает файл недоступным для любых изменений: редактирование, удаление, перемещение, создание линков на него.
**chattr +s file1** - позволяет сделать удаление файла безопасным, т.е. выставленный атрибут s говорит о том, что при удалении файла, место, занимаемое файлом на диске заполняется нулями, что предотвращяет возможность восстановления данных.
**chattr +S file1** - указывает, что, при сохранении изменений, будет произведена синхронизация, как при выполнении команды sync
**chattr +u file1** - данный атрибут указывает, что при удалении файла содержимое его будет сохранено и при необходимости пользователь сможет его восстановить
**lsattr** - показать атрибуты файлов

### Архивирование и сжатие файлов
**bunzip2 file1.bz2**- разжимает файл 'file1.gz'
**gunzip file1.gz** -
**gzip file1**
**bzip2 file1** - сжимает файл 'file1'
**gzip -9 file1** - сжать файл file1 с максимальным сжатием
**rar a file1.rar test_file** - создать rar-архив 'file1.rar' и включить в него файл test_file
**rar a file1.rar file1 file2 dir1** - создать rar-архив 'file1.rar' и включить в него file1, file2 и dir1
**rar x file1.rar** - распаковать rar-архив
unrar x file1.rar -
**tar -cvf archive.tar file1** - создать tar-архив archive.tar, содержащий файл file1
**tar -cvf archive.tar file1 file2 dir1** - создать tar-архив archive.tar, содержащий файл file1, file2 и dir1
**tar -tf archive.tar** - показать содержимое архива
**tar -xvf archive.tar** - распаковать архив
**tar -xvf archive.tar -C /tmp**- распаковать архив в /tmp
**tar -cvfj archive.tar.bz2 dir1** - создать архив и сжать его с помощью bzip2(Прим.переводчика. ключ -j работает не во всех *nix системах)
**tar -xvfj archive.tar.bz2** - разжать архив и распаковать его(Прим.переводчика. ключ -j работает не во всех *nix системах)
**tar -cvfz archive.tar.gz dir1** - создать архив и сжать его с помощью gzip
**tar -xvfz archive.tar.gz** - разжать архив и распаковать его
**zip file1.zip file1** - создать сжатый zip-архив
**zip -r file1.zip file1 file2 dir1** - создать сжатый zip-архив и со включением в него нескольких файлов и/или директорий
**unzip file1.zip** - разжать и распаковать zip-архив

### RPM пакеты (Fedora, Red Hat и тому подобное)
**rpm -ivh package.rpm** - установить пакет с выводом сообщений и прогресс-бара
**rpm -ivh --nodeps package.rpm** - установить пакет с выводом сообщений и прогресс-бара без контроля зависимостей
**rpm -U package.rpm** - обновить пакет без изменений конфигурационных файлов, в случае отсутствия пакета, он будет установлен
**rpm -F package.rpm**- обновить пакет только если он установлен
**rpm -e package_name.rpm** - удалить пакет
**rpm -qa** - отобразить список всех пакетов, установленных в системе
**rpm -qa | grep httpd** - среди всех пакетов, установленных в системе, найти пакет содержащий в своём имени "httpd"
**rpm -qi package_name** - вывести информацию о конкрентном пакете
**rpm -qg "System Environment/Daemons"** - отобразить пакеты входящие в группу пакетов
**rpm -ql package_name** - вывести список файлов, входящих в пакет
**rpm -qc package_name** - вывести список конфигурационных файлов, входящих в пакет
**rpm -q package_name --whatrequires** - вывести список пакетов, необходимых для установки конкретного пакета по зависимостям
**rpm -q package_name --whatprovides** - show capability provided by a rpm package
**rpm -q package_name --scripts** - отобразит скрипты, запускаемые при установке/удалении пакета
**rpm -q package_name --changelog** - вывести историю ревизий пакета
**rpm -qf /etc/httpd/conf/httpd.conf** - проверить какому пакету принадлежит указанный файл. Указывать следует полный путь и имя файла.
**rpm -qp package.rpm -l** - отображает список файлов, входящих в пакет, но ещё не установленных в систему
**rpm --import /media/cdrom/RPM-GPG-KEY** - ипортировать публичный ключ цифровой подписи
**rpm --checksig package.rpm** - проверит подпись пакета
**rpm -qa gpg-pubkey** - проверить целостность установленного содержимого пакета
**rpm -V package_name** - проверить размер, полномочия, тип, владельца, группу, MD5-сумму и дату последнего изменеия пакета
**rpm -Va** - проверить содержимое всех пакеты установленные в систему. Выполняйте с осторожностью!
**rpm -Vp package.rpm** - проверить пакет, который ещё не установлен в систему
**rpm2cpio package.rpm | cpio --extract --make-directories *bin*** - извлечь из пакета файлы содержащие в своём имени bin
**rpm -ivh /usr/src/redhat/RPMS/`arch`/package.rpm** - установить пакет, собранный из исходных кодов
**rpmbuild --rebuild package_name.src.rpm** - собрать пакет из исходных кодов

### YUM - средство обновления пакетов(Fedora, RedHat и тому подобное)

**yum install package_name** - закачать и установать пакет
**yum update** - обновить все пакеты, установленные в систему
**yum update package_name** - обновить пакет
**yum remove package_name** - удалить пакет
**yum list** - вывести список всех пакетов, установленных в систему
**yum search package_name** - найти пакет в репозитории
**yum clean packages** - очисть rpm-кэш, удалив закачанные пакеты
**yum clean headers** - удалить все заголовки файлов, которые система использует для разрешения зависимостей
**yum clean all**- очисть rpm-кэш, удалив закачанные пакеты и заголовки

### DEB пакеты (Debian, Ubuntu и тому подобное)

**dpkg -i package.deb** - установить / обновить пакет
**dpkg -r package_name** - удалить пакет из системы
**dpkg -l** - показать все пакеты, установленные в систему
**dpkg -l | grep httpd** - среди всех пакетов, установленных в системе, найти пакет содержащий в своём имени "httpd"
**dpkg -s package_name** -
отобразить инфрмацию о конкретном пакете
**dpkg -L package_name** - вывести список файлов, входящих в пакет, установленный в систему
**dpkg --contents package.deb** - отобразить список файлов, входящих в пакет, который ешё не установлен в систему
**dpkg -S /bin/ping** - найти пакет, в который входит указанный файл.

###APT - средство управление пакетами (Debian, Ubuntu и тому подобное)

**apt-get install package_name** - установить / обновить пакет
**apt-cdrom install package_name** - установить / обновить пакет с cdrom'а
**apt-get update** - получить обновлённые списки пакетов
**apt-get upgrade** - обновить пакеты, установленные в систему
**apt-get remove package_name** - удалить пакет, установленный в систему с сохранением файлов конфигурации
**apt-get purge package_name** - удалить пакет, установленный в систему с удалением файлов конфигурации
**apt-get check** - проверить целостность зависимостей
**apt-get clean** - удалить загруженные архивные файлы пакетов
**apt-get autoclean** - удалить старые загруженные архивные файлы пакетов