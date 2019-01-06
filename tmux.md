# Заметки о Tmux

- `tmux split-window -h` - добавляет панель справа (по горизонтали)
- `tmux split-window -v` - добавляет панель снизу (по вертикали)

Для более "логичного" разделения окна можно задать в конфигурации:

```
bind-key v split-window -h
bind-key h split-window -v
```

## Автоматическое изменение размеров панелей

    C-b M-1             # vertical split, all panes same width
    C-b M-2             # horizontal split, all panes same height
    C-b M-3             # horizontal split, main pane on top,
                          other panes on bottom, vertically split, all same width
    C-b M-4             # vertical split, main pane left,
                          other panes right, horizontally split, all same height
    C-b M-5             # tile, new panes on bottom, same height before same width

`M` обозначает мета-ключ, обычно это клавиша <kbd>ALT</kbd>.

Источник: [How to auto resize panes in tmux?](https://superuser.com/questions/456775/how-to-auto-resize-panes-in-tmux)
