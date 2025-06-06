# Хеширование и HMAC


## Хеширование

Задачей хеширования является создание **дайджеста** &mdash; короткого, уникальнго отпечатка сообщения, используемого для контроля целостности данных.

### Пример

Есть два канала:

1. Надёжный, но дорогой и медленный
2. Дешевый и быстрый, но слабо защишённый

### Задача

Необходимо максимально надёжно, быстро и недорого передать длинное сообщение.
Стопроцентно выполнить все эти три условия сложно, поэтому приходится идти на компромисы.

### Решение с надёжным каналом

Отправитель создаёт дайджест (*хеш*) собщения, и отправляет его по надёжному каналу, а сообщение передаёт по ненадёжному.
На принимающей стороне, получатель заново вычисляет дайджест сообщения и сравнивает его с дайджестом который получил по доверенному каналу.
Если дайджесты совпадают, то можно большой долей уверенности считать, что сообщение не было изменено по дороге.

### Решение с использованием HASH-MAC

Что делать если сообшение передать надо с теми же требованиями (*скорость, надёжность, стоимость*), но при этом у нас есть всего один канал &mdash; ненадёжный? Дайджесту пришедшему по ненадёжному каналу доверять нельзя.

Тут на помощь приходит **HMAC**:
Хеш-Мак это тот же дайджест, но подписанный секретным ключом который имеют только отправляющая и принимающая стороны.

Отправитель передаёт сообщение и *HMAC* по незащищённому каналу, а получатель проверяет достоверность присланного сообщения вычисляя его HMAC используя общий секретный ключ.
