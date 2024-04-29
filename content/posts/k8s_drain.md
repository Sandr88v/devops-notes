---
title: "Корректное завершение работы pod’ов в Kubernetes-кластере"
date: 2024-04-22T22:31:36+03:00
slug: k8s_drain
aliases:
  - k8s
weight: 10010
toc_hide: true
tags:
  - k8s_drain
---

## Ввод ноды в режим обслуживания
```
kubectl drain --ignore-daemonsets --delete-local-data test-kube-worker01
```
- **kubectl drain** — данная команда переводит ноду в режим обслуживания. Поды на указанной ноде корректно завершают работу, или киляются по таймауту, если они так и не успели выключиться. Не все поды завершают работу по умолчанию. Все поды, запущенные на выбранном узле, будут поставлены в состояние "Terminating" и перенесены на другие доступные узлы в кластере. **Replication Controllers**, **ReplicaSets** и **Deployments**, управляющие переносимыми подами, будут создавать новые поды на других узлах для поддержания желаемого количества запущенных подов.
- **ignore-daemonsets** — этот параметр нужен для того, чтобы игнорировать поды, созданные через DaemonSets. DaemonSets-поды должны работать на каждом узле, например, для мониторинга или сетевых служб.
- **delete-local-data (deprecated)** — удаляет поды, использующие EmptyDir (локальные данные будут удалены)

Все поды, кроме созданных через DaemonSets, корректно завершили работу на выбранной ноде и будут подняты на какой-то другой.

```
kubectl get node
```
У ноды появился статус **SchedulingDisabled**. Значит, новые поды на ноде запускаться не будут.

Список подов, которые остались на ноде. Они нам не помешают. Выключаем ноду, добавляем в неё CPU и память, включаем снова.

Статус выключенной ноды: **NotReady,SchedulingDisabled**.

Спокойно добавляем CPU и память, включаем ноду.

Дожидаемся, когда статус ноды сменится на **Ready,SchedulingDisabled**.

## Вывод ноды из режима обслуживания

Выводим ноду из режима обслуживания.
```
kubectl uncordon test-kube-worker01
```
```
kubectl get node
```
Статус ноды Ready.

## Примечания

Можно отслеживать количество подов на ноде командой:
```
kubectl get pods -o wide --all-namespaces | grep <имя_узла>
```

Посмотреть статус ноды:
```
kubectl get node | grep <имя_узла>
```
Запретить создавать новые поды на ноде, при этом старые поды не удалять:
```
kubectl cordon <имя_узла>
```

С помощью cordon можно предотвратить размещение планировщиком новых подов на хосте, при этом не оказывая влияние на существующие поды. Это полезно в качестве подготовительного шага перед перезагрузкой узла или другим обслуживанием. Статус ноды при этом Ready,SchedulingDisabled.

error: unable to drain node "ecom-evoprod-k8s-worker01" due to error:[cannot delete Pods with local storage (use --delete-emptydir-data to override):....

```
kubectl drain test-kube-worker01 --delete-emptydir-data --ignore-daemonsets
```
```
kubectl uncordon  test-kube-worker01
```

```
test-kube-worker01   NotReady   <none>         292d   v1.24.6
```


```
journalctl -xeu kubelet | tail -n1
Apr 22 12:43:59 test-kube-worker01 kubelet[27562]: Error: failed to run Kubelet: running with swap on is not supported, please disable swap! or set --fail-swap-on flag to false. /proc/swaps contained: [Filename                                Type                Size        Used        Priority /dev/sda3                               partition        2097148        0        -2]
```
Решение
```
root@test-kube-worker01:/etc/default# fdisk /dev/sda

Welcome to fdisk (util-linux 2.34).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Command (m for help): p
Disk /dev/sda: 250 GiB, 268435456000 bytes, 524288000 sectors
Disk model: Virtual disk
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 3D843FBE-3B21-400C-BEAD-F5033216244D

Device       Start       End   Sectors  Size Type
/dev/sda1     2048      4095      2048    1M BIOS boot
/dev/sda2     4096   2101247   2097152    1G Linux filesystem
/dev/sda3  2101248   6295551   4194304    2G Linux swap
/dev/sda4  6295552 524287966 517992415  247G Linux filesystem

Command (m for help): t
Partition number (1-4, default 4): 3
Partition type (type L to list all types): 20

Changed type of partition 'Linux swap' to 'Linux filesystem'.

Command (m for help): p
Disk /dev/sda: 250 GiB, 268435456000 bytes, 524288000 sectors
Disk model: Virtual disk
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 3D843FBE-3B21-400C-BEAD-F5033216244D

Device       Start       End   Sectors  Size Type
/dev/sda1     2048      4095      2048    1M BIOS boot
/dev/sda2     4096   2101247   2097152    1G Linux filesystem
/dev/sda3  2101248   6295551   4194304    2G Linux filesystem
/dev/sda4  6295552 524287966 517992415  247G Linux filesystem

Command (m for help): w
The partition table has been altered.
Syncing disks.

root@test-kube-worker01:/etc/default#
```
```
p, t, 3, 20, p, w
```
