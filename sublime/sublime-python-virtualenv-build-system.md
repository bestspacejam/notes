# Запуск Python скриптов в Virtualenv 


В файле *.sublime-project:

```
"build_systems":
	[
		{
			"shell": true,
			"name": "Python (lk.itpc)",
			"cmd": ["%userprofile%\\Envs\\lk.itpc\\Scripts\\python", "-u", "$file"],
			"file_regex": "py$",
			"selector": "source.python"
		}
	]
```