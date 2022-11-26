# Шпаргалка по GnuPG

```bash
# Генерация ключа
gpg --full-generate-key

# Получение списка ключей
gpg --list-secret-keys

# Создание подписанного файла
gpg --sign test.txt

# Создание отдельной подписи для файла
gpg --detach-sign test.txt

# Редактирование параметров приватного ключа
gpg --edit-key "<email>"

# Изменение пароля приватного ключа
gpg --passwd

# Экспорт публичного ключа
gpg --export --armor "<email>"
```
