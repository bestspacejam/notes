# Сжать PDF с помощью GhostScript

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

* [Shrinkpdf: shrink PDF files with Ghostscript](http://www.alfredklomp.com/programming/shrinkpdf/)
* [How can I reduce the file size of a scanned PDF file?](https://askubuntu.com/questions/113544/how-can-i-reduce-the-file-size-of-a-scanned-pdf-file)
