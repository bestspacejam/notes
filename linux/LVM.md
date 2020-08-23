# Logical Volume Manager (LVM)

- **Physical Volume** - физический том, напимер накопитель `/dev/sdb` или раздел `/dev/sdb1`
- **Volume Group** - группа физических томов
- **Logical Volume** - логический том, использует выделенное место на связанном Volume Group

Основные команды:
- vgs
- lvs
- pvs
- vgcreate
- pvcreate
- lvcreate
- vgremove
- pvremove
- lvremove
- vgdisplay
- lvdisplay
- pvdisplay
- vgscan
- lvscan
- pvscan

## Ссылки
- [Logical Volume Manager (LVM)](https://help.ubuntu.ru/wiki/lvm)
- [Как управлять и создавать LVM (логические тома) с помощью команд vgcreate, lvcreate и lvextend — LFCS часть 11](https://blog.sedicomm.com/2018/09/15/kak-upravlyat-i-sozdavat-lvm-logicheskie-toma-s-pomoshhyu-komand-vgcreate-lvcreate-i-lvextend-lfcs-chast-11/)
- [LVM](https://www.kryukov.biz/soderzhanie/rabota-s-nakopitelyami/lvm/) - Записки Линуксоида
- [Logical Volume Management (LVM) - Linux](https://www.youtube.com/watch?v=fadQX2e_PGk) - видео
