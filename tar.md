# Tar

## Список содержимого архива

```shell
tar -tf archive.tgz
```

## Удаление префикса "./" из пути архивируемых файлов

`tar` переключает рабочую директрию на указанную в параметре -C и архивирует все файлы.

```shell
tar --transform 's/^\.\///' -czpf archive.tgz -C directory/ .
```

## Добавление префикса к имени извлекаемых файлов

```shell
tar --transform='s/^/prefix_/' -C out -xzf archive.tgz dir1 dir2
```

## Создание архива tar со списком файлов без директории "."

```shell
(shopt -s dotglob && cd directory/ && tar -czpf ../archive.tgz -- *)
```

## Ссылки

* [GNU tar: an archiver tool](https://www.gnu.org/software/tar/manual/html_section/tar.html)
* [Modifying File and Member Names](https://www.gnu.org/software/tar/manual/html_section/tar_51.html)
