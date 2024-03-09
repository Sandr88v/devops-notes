---
title: "Linux. LVM добавление нового диска, расширение существующего раздела и удаление старого диска"
slug: linux
aliases:
  - linux
weight: 10010
toc_hide: true
tags:
  - linux
  - lvm
---

На примере db1

Смотрим, что добавлено куча маленьких кусочков в одну волюмгруппу (и что все они идут в одну логикал группу).
```
db1:~$ sudo pvscan
  PV /dev/sda5   VG vg00            lvm2 [519.76 GiB / 0    free]   - Трогать нельзя, т.к. на /dev/sda1  Boot
  PV /dev/sdb    VG vg00            lvm2 [80.00 GiB / 0    free]
  PV /dev/sdc    VG vg00            lvm2 [50.00 GiB / 0    free]
  PV /dev/sdd    VG vg00            lvm2 [100.00 GiB / 0    free]
  PV /dev/sde    VG vg00            lvm2 [50.00 GiB / 0    free]
  PV /dev/sdf    VG vg00            lvm2 [70.00 GiB / 0    free]
  PV /dev/sdg    VG vg00            lvm2 [130.00 GiB / 0    free]
  PV /dev/sdh    VG vg00            lvm2 [100.00 GiB / 0    free]
  PV /dev/sdi    VG vg00            lvm2 [200.00 GiB / 0    free]
  Total: 9 [1.27 TiB] / in use: 9 [1.27 TiB] / in no VG: 0 [0   ]
```
Какие диски есть на текущий момент(ls -l /dev/sd*):
```
sda   sda1  sda2  sda5  sdb   sdc   sdd   sde   sdf   sdg   sdh   sdi
```
Добавляем новый диск на 1ТБ (мелкие куски занимают 780Гб + немного добавим)
Сканируем в поисках нового диска:
```
db1:~# echo "- - -" > /sys/class/scsi_host/host0/scan
db1:~# echo "- - -" > /sys/class/scsi_host/host1/scan
db1:~# echo "- - -" > /sys/class/scsi_host/host2/scan
```
Видим, что появился (ls -l /dev/sd*):
```
sda   sda1  sda2  sda5  sdb   sdc   sdd   sde   sdf   sdg   sdh   sdi   sdj
```
Засовываем его в физикалгруп
```
db1:~# pvcreate /dev/sdj
  Physical volume "/dev/sdj" successfully created.
```
Смотрим, что добавился. Видим, что свободен.
```
db1:~# pvscan 
  PV /dev/sda5   VG vg00            lvm2 [519.76 GiB / 0    free]
  PV /dev/sdb    VG vg00            lvm2 [80.00 GiB / 0    free]
  PV /dev/sdc    VG vg00            lvm2 [50.00 GiB / 0    free]
  PV /dev/sdd    VG vg00            lvm2 [100.00 GiB / 0    free]
  PV /dev/sde    VG vg00            lvm2 [50.00 GiB / 0    free]
  PV /dev/sdf    VG vg00            lvm2 [70.00 GiB / 0    free]
  PV /dev/sdg    VG vg00            lvm2 [130.00 GiB / 0    free]
  PV /dev/sdh    VG vg00            lvm2 [100.00 GiB / 0    free]
  PV /dev/sdi    VG vg00            lvm2 [200.00 GiB / 0    free]
  PV /dev/sdj                       lvm2 [1.00 TiB]
```
Сморим в какую волюмгруппу его добавить:
```
vgdisplay 
  --- Volume group ---
  VG Name               vg00
  System ID             
  Format                lvm2
  Metadata Areas        9
  Metadata Sequence No  19
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                2
  Open LV               2
  Max PV                0
  Cur PV                9
  Act PV                9
  VG Size               1.27 TiB
  PE Size               4.00 MiB
  Total PE              332730
  Alloc PE / Size       332730 / 1.27 TiB
  Free  PE / Size       0 / 0   
  VG UUID               3jmhw4-X5c6-7HH9-g68x-pJqv-ET3u-kHDopG
```

Добавляем:
```
vgextend vg00 /dev/sdj
```

Проверяем:
```
db1:~# vgdisplay 
  --- Volume group ---
  VG Name               vg00
  System ID             
  Format                lvm2
  Metadata Areas        10
  Metadata Sequence No  20
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                2
  Open LV               2
  Max PV                0
  Cur PV                10
  Act PV                10
  VG Size               2.27 TiB
  PE Size               4.00 MiB
  Total PE              594873
  Alloc PE / Size       332730 / 1.27 TiB
  Free  PE / Size       262143 / 1024.00 GiB
  VG UUID               3jmhw4-X5c6-7HH9-g68x-pJqv-ET3u-kHDopG
```
Смотрим какую лоджикалгрупп расширить:
```
lvdisplay 
  --- Logical volume ---
  LV Path                /dev/vg00/root
  LV Name                root
  VG Name                vg00
  LV UUID                LEvNoO-cDyK-2LNh-JB5H-iDDD-gRJ2-44S9Cd
  LV Write Access        read/write
  LV Creation host, time db1, 2018-10-25 17:54:57 +0300
  LV Status              available
  # open                 1
  LV Size                1.27 TiB
  Current LE             332218
  Segments               9
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     256
  Block device           254:0
```

Расширяем:
```
lvextend -L +50g /dev/vg00/root
```
Проверяем:
```
 --- Logical volume ---
  LV Path                /dev/vg00/root
  LV Name                root
  VG Name                vg00
  LV UUID                LEvNoO-cDyK-2LNh-JB5H-iDDD-gRJ2-44S9Cd
  LV Write Access        read/write
  LV Creation host, time db1, 2018-10-25 17:54:57 +0300
  LV Status              available
  # open                 1
  LV Size                1.32 TiB
  Current LE             345018
  Segments               10
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     256
  Block device           254:0
```
Проверяем объем, НЕМНОГО! увеличиваем файловую систему и еще раз проверяем.
```
/dev/mapper/vg00-root ext4      1.3T  1.2T   54G  96% /
resize2fs /dev/mapper/vg00-root
/dev/mapper/vg00-root ext4      1.3T  1.2T  101G  93% /
```
Смотрим еще раз состояние физических групп и убеждаемся, что есть ДОСТАТОЧНО свободного места для переезда.
```
db1:~# pvscan 
  PV /dev/sda5   VG vg00            lvm2 [519.76 GiB / 0    free]
  PV /dev/sdb    VG vg00            lvm2 [80.00 GiB / 0    free]
  PV /dev/sdc    VG vg00            lvm2 [50.00 GiB / 0    free]
  PV /dev/sdd    VG vg00            lvm2 [100.00 GiB / 0    free]
  PV /dev/sde    VG vg00            lvm2 [50.00 GiB / 0    free]
  PV /dev/sdf    VG vg00            lvm2 [70.00 GiB / 0    free]
  PV /dev/sdg    VG vg00            lvm2 [130.00 GiB / 0    free]
  PV /dev/sdh    VG vg00            lvm2 [100.00 GiB / 0    free]
  PV /dev/sdi    VG vg00            lvm2 [200.00 GiB / 0    free]
  PV /dev/sdj    VG vg00            lvm2 [1024.00 GiB / 974.00 GiB free]
```
ВАЖНО!!! Идем в скрин, что бы в случае дисконекта процесс не наебнул систему!!!
go to SCREEN!

Засекаем время и начинаем переезд.
```
Пт фев 21 13:49:57 MSK 2020
pvmove -v /dev/sdb
Пт фев 21 14:20:42 MSK 2020
```
Проверяем, что наш диск освободился, а новый стал чуть заполненным:
```
db1:~# pvscan 
PV /dev/sda5   VG vg00            lvm2 [519.76 GiB / 0    free]
  PV /dev/sdb    VG vg00            lvm2 [80.00 GiB / 80.00 GiB free]
  PV /dev/sdc    VG vg00            lvm2 [50.00 GiB / 0    free]
  PV /dev/sdd    VG vg00            lvm2 [100.00 GiB / 0    free]
  PV /dev/sde    VG vg00            lvm2 [50.00 GiB / 0    free]
  PV /dev/sdf    VG vg00            lvm2 [70.00 GiB / 0    free]
  PV /dev/sdg    VG vg00            lvm2 [130.00 GiB / 0    free]
  PV /dev/sdh    VG vg00            lvm2 [100.00 GiB / 0    free]
  PV /dev/sdi    VG vg00            lvm2 [200.00 GiB / 0    free]
  PV /dev/sdj    VG vg00            lvm2 [1024.00 GiB / 894.00 GiB free]
  Total: 10 [2.27 TiB] / in use: 10 [2.27 TiB] / in no VG: 0 [0   ]
```
Выводим диск из волумгруппы и убеждаемся, что он её больше не принадлежит:

vgreduce  vg00 /dev/sdb
```
db1:~# pvscan 
  PV /dev/sda5   VG vg00            lvm2 [519.76 GiB / 0    free]
  PV /dev/sdc    VG vg00            lvm2 [50.00 GiB / 0    free]
  PV /dev/sdd    VG vg00            lvm2 [100.00 GiB / 0    free]
  PV /dev/sde    VG vg00            lvm2 [50.00 GiB / 0    free]
  PV /dev/sdf    VG vg00            lvm2 [70.00 GiB / 0    free]
  PV /dev/sdg    VG vg00            lvm2 [130.00 GiB / 0    free]
  PV /dev/sdh    VG vg00            lvm2 [100.00 GiB / 0    free]
  PV /dev/sdi    VG vg00            lvm2 [200.00 GiB / 0    free]
  PV /dev/sdj    VG vg00            lvm2 [1024.00 GiB / 894.00 GiB free]
  PV /dev/sdb                       lvm2 [80.00 GiB]
  Total: 10 [2.27 TiB] / in use: 9 [2.19 TiB] / in no VG: 1 [80.00 GiB]
```
Смонтированная система на месте, с объемом тоже все ОК.
```
df -mh
/dev/mapper/vg00-root ext4      1.3T  1.2T  101G  93% /
```
Попутно мониторим процесс, всякими топами, пээсами …
```
\_ sshd: a.b0nd [priv]
|   \_ sshd: a.b0nd@pts/0
|       \_ -bash
|           \_ sudo su -
|               \_ su -
|                   \_ -su
|                       \_ screen -S pvmoveTask
|                           \_ SCREEN -S pvmoveTask
|                               \_ /bin/bash
|                                   \_ pvmove -v /dev/sdb
```
После всех манипуляций диск можно удалить: pvremove и затем отключить в vSphere.
```
pvremove /dev/sdb
echo 1 > /sys/block/sdb/device/delete
```
Посмотреть место с указанием диска в виртуализации
```
 lsblk -o name,kname,size,mountpoint,maj:min,fstype,HCTL
 ```

Когда проверили все и отмонтировали диск, можно добавить окончательное место:
Для того, чтобы расширить на все имеющееся свободное пространство выполняем команду:
```
lvextend -l +100%FREE /dev/vg00/root
```
Centos8
```
lvresize -r -l+100%FREE centos/root
```
Теперь ресайзим раздел:
```
resize2fs /dev/vg00/root
```
либо
```
xfs_growfs /dev/vg00/root
```


