# Монтирование файловой системы

```shell
# Монтирование тома
mount -t ext4 /mnt/storage /dev/sdb1

# Монтирование с автоматическим определением файловой системы
mount -a /mnt/storage /dev/sdb1

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

Инструкции для автоматического монтирования содержатся в файле `/etc/fstab`

## Ссылки
[File System Mounting - Linux](https://www.youtube.com/watch?v=A8ITr5ZpzvA) - видео
