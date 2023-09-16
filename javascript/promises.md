# Описание работы Promises

Состояние Обещания определяется сразу при его создании, в результате выполнения Исполнителя.
> Исполнитель - функция определения состояния обещания.

Исполнитель выполняется сразу и регистрирует в себе ссылки на коллбеки *resolve* и *rejected*, которые вызываются по завершении работы асинхронного кода.

Ветвь выполнения дочернего обещания (*resolve* это будет или *reject*) зависит от того в каком состоянии верётся обещание из коллбэка.

Выполнится ветвь:
**resolve** &mdash; если коллбэк вовращает *значение* или Обещание в состоянии *resolved*
**reject** &mdash; если коллбэк вызывает *исключение* или Обещание в состоянии *rejected*

## Пример

```javascript
// Исполнитель с удачным решением
function resolveLaterExecutor(resolve, reject)
{
	setTimeout(function(){ resolve(10); }, 1000);
}

// Исполнитель с отказом от решения
function rejectLaterExecutor(resolve, reject)
{
	setTimeout(function(){ reject(20); }, 1000);
}

// Важно:
// Процесс решения запускается исполнителем сразу при передаче его Обещанию.

var p;

// Возвращает всегда удачное решение со значением "foo"
var p1 = Promise.resolve('foo');

// Создаёт новое Обещание с исполнителем, которому передаётся два колбэка
// "resolve" - для передачи ему значения с удачным решением
// "reject" - для передачи ему значения с отказом от решения
// 
// Когда решение, запущенное исполнителем, будет готово - оно передаёт результат
// в соответствующий его статусу коллбэк (удачному решению или отказу от решения).
var p2 = p1.then(
	function(value)
	{
		// Здесь, в качестве значения удачного решения, создаётся новое обещание
		// с исполнителем вызывающим коллбэк другого удачного решения по прошествии 1 секунды.
		
		// Обещание с исполнителем вызывающим коллбэк удачного решения по прошествии 1 секунды.
		return new Promise(resolveLaterExecutor);
	}
);


// Создаёт новое Обещание с исполнителем которому передаются указанные коллбэки
// котые выполняются в зависимости от результата родительского Обещания
p2.then(
	// resolveLaterExecutor вызывает только коллбэки с удачным решением
	function(v)
	{
		// "resolved", 10
		console.log('resolved', v);
	},
	// Этот колбэк не будет вызван
	function(e)
	{
		console.log('rejected', e);
	}
);

var p3 = p1.then(
	function()
	{
		// Новое Обещание вызывающее исполнителя который по прошествии 1 секунды
		// вызывает коллбэк с отказом от решения со значением 20
		return new Promise(rejectLaterExecutor);
	}
);

p3.then(
	// Этот коллбэк не будет вызван, так исполнитель rejectLaterExecutor вызывает
	// коллбек "reject" с отказом от решения
	function(v)
	{
		console.log('resolved', v);
	},
	// Этот коллбэк вызовется решением исполнителя "rejectLaterExecutor"
	function(e)
	{
		console.log('rejected', e); // "rejected", 20
	}
);
```


## Ссылки

- [Promises/A+](https://promisesaplus.com/)
- [Promise (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- [Understanding javascript promises; stacks and chaining](https://stackoverflow.com/questions/29853578/understanding-javascript-promises-stacks-and-chaining/29854205#29854205)