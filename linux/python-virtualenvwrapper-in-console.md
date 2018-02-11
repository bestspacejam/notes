# Python / virtualenvwrapper - Включение поддержки команды `workon` в консоли

Записать в `~.bash_aliases`:

```shell
venvwrap="virtualenvwrapper.sh"
which $venvwrap > /dev/null
if [ $? -eq 0 ]; then
    source `which $venvwrap`
fi
```

Источник: https://stackoverflow.com/questions/21928555/virtualenv-workon-command-not-found
