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

## Ссылки
- [File System Mounting - Linux](https://www.youtube.com/watch?v=A8ITr5ZpzvA) - видео
