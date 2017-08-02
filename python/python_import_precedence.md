
# Приоритет импорта объектов в Python

В операциях `from ..` и `import ..` если у пакета и модуля одинаковые имена, приоритет отдаётся __пакету__.

`from PACKAGE import ..` &mdash; Сначала ищет свойство пакета, затем вложенный пакет, затем вложенный модуль.

`from MODULE import ..` &mdash; Ищет свойство в модуле.

`import ..` &mdash; Ищет пакет, если такого пакета нет, ищет модуль.


## Кросс-импорты и циклические ссылки *(перевести)*

Взято со [Stackoverflow.com](https://stackoverflow.com/questions/744373/circular-or-cyclic-imports-in-python):

Imports are pretty straightforward really. Just remember the following:

'import' and 'from xxx import yyy' are executable statements. They execute when the running program reaches that line.

If a module is not in sys.modules, then an import creates the new module entry in sys.modules and then executes the code in the module. It does not return control to the calling module until the execution has completed.

If a module does exist in sys.modules then an import simply returns that module whether or not it has completed executing. That is the reason why cyclic imports may return modules which appear to be partly empty.

Finally, the executing script runs in a module named __main__, importing the script under its own name will create a new module unrelated to __main__.

Take that lot together and you shouldn't get any surprises when importing modules.
