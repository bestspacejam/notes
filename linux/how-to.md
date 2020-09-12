# Как в Linux...

## Создать символическую ссылку
```shell
ln -s ../sites-available/001-website.conf sites-enabled/
```
**Замечания:**
- Путь на который указывает файл символической ссылки может быть как относительным так и абсолютным.
- Команда `ln -s` не проверяет наличие исходного файла на который создаётся ссылка, а просто записывает указаный путь в файл ссылки.
- Если не указать второй аргумент, ссылка будет создана в текущей директории с `basename` исходного файла.
- Если вторым аргументом передать имя директории, то ссылка будет создана в ней.

## Создать архив `tar` без родительской директории

Для того что бы файлы содержащиеся в директории ./Прайс-лист были в корне архива, необходимо выполнить `tar` в контексте директории.

```
$ (cd Прайс-лист/ && tar -czf ../Прайс-лист.tgz *)
```

## Сжать PDF

```shell
gs \
  -dNOPAUSE \
  -dBATCH \
  -sDEVICE=pdfwrite \
  -dCompatibilityLevel=1.4 \
  -dPDFSETTINGS=/ebook \
  -sOutputFile=./dist/main.pdf \
  ./src/main.pdf
```
Ссылки:
  - [Shrinkpdf: shrink PDF files with Ghostscript](http://www.alfredklomp.com/programming/shrinkpdf/)
  - [How can I reduce the file size of a scanned PDF file?](https://askubuntu.com/questions/113544/how-can-i-reduce-the-file-size-of-a-scanned-pdf-file)
  
## Терминал
```shell
# Для поддержки комбинации "Ctrl-S" в терминале
stty -ixon
```
