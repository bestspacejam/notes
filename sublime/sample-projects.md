# Заготовки для проектов Sublime Text


## Linux / Python + venv

```json
{
	"folders":
	[
		{
			"path": "."
		}
	],
	
	"build_systems":
	[
		{
			"name": "Python (venv)",
			"cmd": ["${project_path}/venv/bin/python", "-u", "$file"],
			"working_dir": "${project_path}",
			"file_regex": "py$",
			"selector": "source.python"
		}
	]
}

```


## Windows / Python + venv 

```json
{
	"folders":
	[
		{
			"path": ".",
			"folder_exclude_patterns": ["node_modules/", "dist"],
			"binary_file_patterns": ["node_modules/", "dist/"]
		}
	],
	
	"build_systems":
	[
		{
			"shell": true,
			"name": "Python (uploads)",
			"cmd": ["%userprofile%\\Envs\\uploads\\Scripts\\python", "-u", "$file"],
			"file_regex": "py$",
			"selector": "source.python",
			"env": {"PYTHONIOENCODING": "utf8"}
		}
	]
}

```