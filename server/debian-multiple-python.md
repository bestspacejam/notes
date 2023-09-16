#Установка нескольких версий Python на Debian

Поставить **[pyenv-installer](https://github.com/yyuu/pyenv-installer)**:

```bash
curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash
pyenv update
```

Не забыть прописать в **~/.bashrc**:

```bash
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

Установить пакеты необходимые для компиляции:

```bash
apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev \
libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils
```

Установить необходимую версию Питона:

```bash
pyenv install 3.5.2
```

Проверить установленные версии:

```bash
pyenv versions
```

Команды pyenv:
<https://github.com/yyuu/pyenv/blob/master/COMMANDS.md>

Список проблем и решений при установке Питона через pyenv:
<https://github.com/yyuu/pyenv/wiki/Common-build-problems>