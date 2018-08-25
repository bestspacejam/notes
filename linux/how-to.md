# Как в Linux...

## Создать символическую ссылку
```shell
ln -s ../sites-available/001-website.conf sites-enabled/
```
**Замечание:**

`../sites-available/001-website.conf` - путь на который будет указывать файл символической ссылки, данном случае он относительный.

Сама команда `ln` может быть выполнена из любой директории, на ссылку это не повлияет. По сути мы записваем указанное значение пути в файл ссылки.

Если вторым аргументом передать имя директории то файл ссылки будет создан в ней с именем исходного файла.

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
  
