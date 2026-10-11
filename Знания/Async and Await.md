
## Введение

Сложная часть: асинхронный код становится трудночитаемым, когда туда входят множество промисов и колбэков. Ключевые слова `async` и `await` позволяют писать асинхронный код так, будто он синхронный — облегчая чтение и поддержку.

```js
function getPersonsInfo(name) {
  return server.getPeople().then(people => {
    return people.find(person => person.name === name);
  });
}

async function getPersonsInfo(name) {
  const people = await server.getPeople();
  const person = people.find(person => person.name === name);
  return person;
}
```

Оба делают одно и то же, но второй выглядит «чисто». 

---

## Что делает `async`

- Если перед объявлением функции поставить `async`, то эта функция **всегда** возвращает промис (Promise).
    
- Возвращание значения (например `return result`) внутри `async` функции — эквивалентно `Promise.resolve(result)`. 
    
- Если внутри `async` функции происходит `throw`, это аналог `Promise.reject(error)`. 
    
- `async` требуется, если ты хочешь использовать `await` внутри функции. `await` вне `async` функции вызовет синтаксическую ошибку. 
    

---

## Что делает `await`

- `await` ставится перед выражением-промисом: `let data = await somePromise`. Функция «приостанавливается» до тех пор, пока промис не выполнится. 
    
- Если промис успешно выполнен, `await` возвращает значение. Если промис отклонён (reject) — `await` «бросит» ошибку (как будто `throw`). 
    
- Это позволяет писать код линейно, без цепочек `.then(…)`. Например:
    

```js
async function getCats() {
  const response = await fetch(url);
  const catData = await response.json();
  img.src = catData.data.images.original.url;
}
```

Как вариант примера из курса. 

---

## Обработка ошибок

- Поскольку `async` функции возвращают промис, ты можешь вызывать их и делать `.catch(...)` снаружи:
    

````js
asyncFunctionCall().catch(err => console.error(err));
``` :contentReference[oaicite:11]{index=11}  
- Часто лучше использовать `try … catch` внутри `async` функции:  
```js
async function foo() {
  try {
    const response = await fetch(url);
    const data = await response.json();
    // работать с data
  } catch(error) {
    // обработка ошибки
    console.error(error);
  }
}
````

Так можно ловить ошибки как из `fetch`, так и из `response.json()`. 

---

## Примеры и практическое применение

- Код, использующий `fetch` + промисы:

```js
fetch(url)
  .then(response => response.json())
  .then(data => { /*…*/ })
  .catch(error => { /*…*/ });
```

- Ему на смену может прийти `async/await`:

```js
async function getCats() {
  const response = await fetch(url);
  const data = await response.json();
  img.src = data.data.images.original.url;
}
getCats();
``` 
  
- Обрати внимание: если ты вызываешь `await` вне `async` функции (например на верхнем уровне, без модулей), могут быть ограничения (в старых окружениях). 

---

## Что возвращает `async` функция  
- Всегда промис (Promise).  
- Если функция возвращает некоторое значение `return x`, то это эквивалентно `Promise.resolve(x)`.  
- Если внутри функция кидает ошибку (`throw`), то промис будет отклонён (`Promise.reject(...)`).

---

## Почему использовать `async/await`  
- Код становится более читабельным, ближе к синхронному стилю.  
- Чего не видно на первый взгляд: `async/await` **не отменяет** то, что за ним стоят промисы — просто скрывает синтаксическую сложность. 
- Упрощает цепочки промисов, уменьшает вложенность, делает ошибки легче обрабатывать.  
- Однако: не всегда он “лучше” — если нужно запустить множество промисов параллельно и ждать всех — нужно применять `Promise.all` и всё такое. `async/await` пригоден, но нужно знать, как работает “под капотом”.  

---

## Подводные камни и нюансы  
- `await` **приостанавливает** выполнение функции, но **не блокирует** основной поток JavaScript — цикл событий (event loop) продолжает работать. Это важно понимать.  
- Если у тебя есть несколько независимых промисов, которые можно запустить параллельно, не стоит делать:
  ```js
  const a = await promiseA;
  const b = await promiseB;
```

Потому что `promiseB` стартует только после `promiseA` завершится. Лучше:

```js
const [a, b] = await Promise.all([promiseA, promiseB]);
```

Или:

```js
const promiseA = promiseAStart();
const promiseB = promiseBStart();
const a = await promiseA;
const b = await promiseB;
```


- Верхний уровень (top-level) вызова `await` может не работать, если среда не поддерживает “top-level await”. Тогда `await` нужно внутри `async` функции.

---

## Итоговая мини-шпаргалка

- `async function foo() { … }`: функция возвращает промис.
- `await promise`: жди результата промиса, получи его или ошибка.
- Используй `try/catch` внутри `async`, либо `.catch()` снаружи.
- `async/await` — синтаксический сахар над промисами, улучшает читаемость.
- Параллельные задачи: думай о `Promise.all` или стартуй промисы до `await`.
- Не забывай, что `await` можно только внутри `async` функции (или на уровне модуля в некоторых средах).
