# Почему `object.__getattribute__()` не вызывает рекурсии при доступе к аттрибутам объекта экземпляра

Вопрос: https://stackoverflow.com/questions/13538324/python-avoiding-infinite-loops-in-getattribute

## Объяснение

You seem to be under the impression that your implementation of `__getattribute__` is merely a hook, that if you provide it Python will call it, and otherwise the interpreter will do it's normal magic directly.

That is not correct. When python looks up attributes on instances, `__getattribute__` is the main entry for all attribute access, and `object` provides the default implementation. Your implementation is thus *overriding* the original, and if your implementation provides no alternative means of returning attributes it fails. You *cannot* use attribute access in that method, since all attribute access to the instance (`self`) is channelled again through `type(self).__getattribute__(self, attr)`.

The best way around this is by calling the overridden original again. That's where `super(C, self).__getattribute__(attr)` comes in; you are asking the next class in the class-resolution order to take care of the attribute access for you.

Alternatively, you can call the unbound `object.__getattribute__()` method directly. The C implementation of this method is the final stop for attribute access (it has direct access to `__dict__` and is thus not bound to the same limitations).

Note that `super()` returns a proxy object that'll look up whatever method can be found next in the method-resolution ordered base classes. If no such method exists, it'll fail with an attribute error. It will *never* call the original method. Thus `Foo.bar()` looking up `super(Foo, self).bar` will either be a base-class implementation or an attribute error, *never* `Foo.bar` itself.

Ссылка на ответ: http://stackoverflow.com/q/13538324


## Коротко

Метод `object.__getattribute__()` имеет прямой доступ к `__dict__` и обходит запрос на рекурсию