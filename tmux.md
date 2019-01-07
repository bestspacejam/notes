# Заметки о Tmux

Для более логичного разделения окна можно задать в конфигурации:

```
bind-key v split-window -h       # Создать панель справа (по горизонтали)
bind-key h split-window -v       # Создать панель снизу (по вертикали)
```

## Автоматическое изменение размеров панелей

    C-b M-1             # Вертикальное разделение, все панели одинаковой ширины
    C-b M-2             # Горизонтальное разделение, все панели одинаковой высоты
    C-b M-3             # horizontal split, main pane on top,
                          other panes on bottom, vertically split, all same width
    C-b M-4             # vertical split, main pane left,
                          other panes right, horizontally split, all same height
    C-b M-5             # tile, new panes on bottom, same height before same width

`M` обозначает мета-ключ, обычно это клавиша <kbd>ALT</kbd>.

Источник: [How to auto resize panes in tmux?](https://superuser.com/questions/456775/how-to-auto-resize-panes-in-tmux)
