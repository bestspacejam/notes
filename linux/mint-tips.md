# Проблемы и решения при работе в Linux Mint

## Сохранение настроек Cinnamon

```shell
# Backup
dconf dump /org/cinnamon/ > cinnamon_settings

# Reset to defaults
# Cinnamon may freeze or crash doing this
dconf reset -f /org/cinnamon/

# Restore settings
# Cinnamon may freeze crash after this (recommend at least logging out/back in)
dconf load /org/cinnamon/ < cinnamon_settings
```
