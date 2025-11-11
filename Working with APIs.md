## 1. Общая идея

`fetch()` — это современный API для работы с HTTP-запросами (GET, POST и др.).  
Он возвращает **Promise**, который:

- переходит в состояние _fulfilled_ после получения **HTTP-ответа** (даже если 404),
- переходит в _rejected_, если произошла **сетевая ошибка** (например, нет соединения).

```js
fetch(url)
  .then(response => {
    // Здесь у нас есть объект ответа, но не сами данные
  })
  .catch(error => {
    // Ошибка сети
  });
```

---

## 2. Получение данных (обычный GET-запрос)

```js
fetch('https://api.example.com/data')
  .then(response => {
    // Проверим статус
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    return response.json(); // Парсит тело ответа как JSON
  })
  .then(data => {
    console.log(data);
  })
  .catch(err => console.error('Ошибка запроса:', err));
```

### Что происходит под капотом:

1. `fetch` отправляет запрос.
2. Когда приходит ответ (заголовки), вызывается первый `.then`.
3. `response.json()` возвращает Promise, который выполняется, когда тело ответа считано и разобрано.
4. Второй `.then` получает уже JS-объект.

---

## 3. Использование `async/await`

Асинхронный синтаксис делает код линейным и читаемым:

```js
async function getData() {
  try {
    const response = await fetch('https://api.example.com/data');
    if (!response.ok) {
      throw new Error(`Ошибка HTTP: ${response.status}`);
    }
    const data = await response.json();
    console.log(data);
  } catch (err) {
    console.error('Ошибка запроса:', err);
  }
}
```

Такой код делает то же самое, но выглядит как «синхронный».

---

## 4. Параметры `fetch()`

По умолчанию `fetch()` делает **GET-запрос**, но можно указать параметры:

```js
fetch('https://api.example.com/items', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer your_token_here'
  },
  body: JSON.stringify({
    name: 'New item',
    price: 19.99
  })
});
```

### Важные поля объекта настроек:

- **method** — тип запроса (`GET`, `POST`, `PUT`, `DELETE` и т.д.)
- **headers** — HTTP-заголовки
- **body** — данные (обычно строка JSON, FormData или Blob)

---

## 5. Обработка разных типов ответа

`response` может содержать данные не только в формате JSON.

```js
const res = await fetch('/some-text.txt');
const text = await res.text();

const imageRes = await fetch('/cat.jpg');
const blob = await imageRes.blob(); // двоичные данные, например изображение
```

Методы для чтения тела:

- `.json()` — парсит JSON
- `.text()` — возвращает строку
- `.blob()` — возвращает двоичные данные
- `.arrayBuffer()` — низкоуровневый бинарный буфер
- `.formData()` — для multipart-ответов

---

## 6. Проверка ошибок

`fetch` **не бросает исключение при 404 или 500**. Он считает, что запрос прошёл успешно, если получен любой ответ.

Поэтому **нужно вручную** проверять `response.ok` (true, если статус от 200 до 299):

```js
if (!response.ok) {
  throw new Error(`HTTP error! Status: ${response.status}`);
}
```

---

## 7. Отмена запроса (AbortController)

Иногда нужно прервать долгий запрос. Это можно сделать через `AbortController`:

```js
const controller = new AbortController();

fetch('https://api.example.com/slow', { signal: controller.signal })
  .then(res => res.json())
  .then(console.log)
  .catch(err => {
    if (err.name === 'AbortError') {
      console.log('Запрос отменён');
    } else {
      console.error(err);
    }
  });

// Прервать через 2 секунды
setTimeout(() => controller.abort(), 2000);
```

---

## 8. Обработка нескольких запросов

Если нужно выполнить несколько запросов и дождаться всех:

```js
Promise.all([
  fetch('/data1.json').then(r => r.json()),
  fetch('/data2.json').then(r => r.json())
]).then(([data1, data2]) => {
  console.log(data1, data2);
});
```

Если важно, чтобы ошибки не останавливали цепочку, можно использовать `Promise.allSettled()`.

---

## 9. Типичные ошибки и советы

- Не забывай `await response.json()`, иначе получишь Promise, а не данные.
- Проверяй `response.ok`.
- Не храни API-ключи в открытом коде (используй .env на сервере).
- Не отправляй `body` в GET-запросах.
- Для кэширования можно использовать `Cache-Control` или `localStorage`.

---

## 10. Мини-шпаргалка

```js
// GET
await fetch(url);

// GET с обработкой
const res = await fetch(url);
const data = await res.json();

// POST
await fetch(url, {
  method: 'POST',
  headers: {'Content-Type': 'application/json'},
  body: JSON.stringify({name: 'Evgenii'})
});

// Проверка ошибок
if (!res.ok) throw new Error(res.status);

// Параллельные запросы
const [a, b] = await Promise.all([fetch(aUrl), fetch(bUrl)]);
```

---
