# Монтирование файловой системы

Файл `/etc/fstab` содержит инструкции для автоматического монтирования.

```shell

# Монтирование тома
mount /dev/sdb1 /mnt/storage

# Монтирование тома с явным указанием файловой системы
mount -t ext4 /dev/sdb1 /mnt/storage

# Монтирование всех файловых систем указанных в `/etc/fstab`
mount -a

# Монтирование ISO-образа
mount -o loop image.iso /mnt/iso

# Размонтирование тома
umount /dev/sdb1
umount /mnt/storage

# Информация о монтированиях
mount
cat /etc/mtab
cat /proc/mounts
```

### Отключение автоматического монтирования

Если добавить `noauto` в опции `/etc/fstab` то диск не будет монтироваться автоматически, но при этом его можно будет смонтировать вручную с предустановленными параметрами (допустим `noatime`  или `ro`).

```
$ cat /etc/fstab
UUID=f50c9c13-032b-44d3-82b0-4fffa249077c /mnt/backups  ext4    defaults,noatime        0       0

$ mount /mnt/backups
```

То есть fstab по сути содержит информацию для монтирования устройств которые *могут быть* подключены, но не всегда доступны при загрузке системы. Это может быть съёмный носитель или сетевой ресурс



## Информация о дисках

```shell
# Имена томов и их точки монтирования
lsblk

# Список UUID томов
blkid
```

## Видео
- [File System Mounting - Linux](https://www.youtube.com/watch?v=A8ITr5ZpzvA)
- [Linux Essentials - Automatically mounting storage volumes with /etc/fstab](https://www.youtube.com/watch?v=A7xH74o6kY0&list=WL)
