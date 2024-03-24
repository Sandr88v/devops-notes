---
title: "Создание новой lvm группы"
date: 2024-03-24T19:20:09+03:00
slug: new_group_lvm
aliases:
  - new_group_lvm
weight: 10010
toc_hide: true
tags:
  - linux
  - lvm
---

## 1. Инициализация диска
```
sudo su
```
```
ls -l /dev/sd*
```
```
echo "- - -" > /sys/class/scsi_host/host0/scan
echo "- - -" > /sys/class/scsi_host/host1/scan
echo "- - -" > /sys/class/scsi_host/host2/scan
```
```
ls -l /dev/sd*
```
```
pvcreate /dev/sdb
```
```
pvscan
```
```
Посмотреть, что диск может использоваться LVM:
```
```
pvdisplay
```
## 2. Создание группы томов

```
vgcreate vg-data /dev/sdb
```

Посмотреть информацию о созданных группах:
```
vgdisplay
```

## 3. Создание логического тома

```
lvcreate -l 100%FREE -n lv-data vg-
```
Посмотреть информацию о созданном томе:

```
lvdisplay
```
## 4. Создание файловой системы и монтирование тома
```
mkfs.ext4 /dev/vg-data/lv-data
```
Разовое монтирование
```
mount /dev/vg-data/lv-data /opt
```
Постоянное монтирование. Добавить в /etc/fstab
```
/dev/vg-data/lv-data    /opt    ext4    defaults    1   2
```
Проверить настройку fstab, предварительно размонтировав /dev/vg-data/lv-data:

```
umount /opt
```
```
sudo mount -a
```
```
df -hT
```










