# Tar

## Преобразование путей в архиве

```shell
# 1. Список содержимого архива
tar -tf archive.tgz

# 2. Удаление префикса "./" из пути архивируемых файлов
#    tar переключает рабочую директрию на указанную в параметре -C 
#    и архивирует все файлы.
tar --transform 's/^\.\///' -czpf archive.tgz -C directory/ .

# 3. Добавление префикса к имени извлекаемых файлов
tar --transform='s/^/prefix_/' -C out -xzf archive.tgz dir1 dir2

# 4. Создание архива tar со списком файлов без директории "."
#     Команда запускается в подоболочке для того чтобы не менять текущее окружение.
(shopt -s dotglob && cd directory/ && tar -czpf ../archive.tgz -- *)
```

Ссылки: 

* [GNU tar: an archiver tool](https://www.gnu.org/software/tar/manual/html_section/tar.html)
* [Modifying File and Member Names](https://www.gnu.org/software/tar/manual/html_section/tar_51.html)
