# Заметки о Tmux

- `tmux split-window -h` - добавляет панель справа (по горизонтали)
- `tmux split-window -v` - добавляет панель снизу (по вертикали)

Для более "логичного" разделения окна можно задать в конфигурации:

```
bind-key v split-window -h
bind-key h split-window -v
```
