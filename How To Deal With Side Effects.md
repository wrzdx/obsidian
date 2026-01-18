### Что такое side effects (побочные эффекты)

Когда React-компонент взаимодействует _с чем-то вне себя самого_ — например, загружает данные с сервера, меняет позицию в DOM, отправляет сообщения на сервер и т.п. — это называется _побочным эффектом_. Стандартный код рендера + обработчики событий не покрывают такие случаи, поэтому нужен механизм, чтобы синхронизировать компонент с внешним миром. ([The Odin Project](https://www.theodinproject.com/lessons/node-path-react-new-how-to-deal-with-side-effects?utm_source=chatgpt.com "How To Deal With Side Effects | The Odin Project"))

---

### **Хук `useEffect` — что это и зачем**

React предоставляет хук `useEffect`, который позволяет выполнять код _после рендера_ или когда изменяются указанные данные. Обычно его используют для:

- Запросов к API.
- Подписок.
- Таймеров.
- Взаимодействия с браузерным API помимо React. ([The Odin Project](https://www.theodinproject.com/lessons/node-path-react-new-how-to-deal-with-side-effects?utm_source=chatgpt.com "How To Deal With Side Effects | The Odin Project"))

---

### Почему обычный код внутри компонента — не решение

Если в теле компонента поставить что-то вроде `setInterval`, оно будет вызываться **при каждом рендере**. Компонент ререндерит → снова создаётся интервал → всё ускоряется и выходит из-под контроля. ([The Odin Project](https://www.theodinproject.com/lessons/node-path-react-new-how-to-deal-with-side-effects?utm_source=chatgpt.com "How To Deal With Side Effects | The Odin Project"))

Пример, который _не работает_:

```jsx
import { useState } from "react";

export default function Clock() {
  const [counter, setCounter] = useState(0);

  setInterval(() => {
    setCounter(count => count + 1)
  }, 1000);

  return <p>{counter} seconds have passed.</p>;
}
```

Этот код заводит бесконечный рост интервалов, потому что каждый рендер добавляет ещё один. ([The Odin Project](https://www.theodinproject.com/lessons/node-path-react-new-how-to-deal-with-side-effects?utm_source=chatgpt.com "How To Deal With Side Effects | The Odin Project"))

---

### Как правильно: использовать `useEffect`

Хук `useEffect` принимает функцию, в которой можно выполнить код _после рендера_. Если его не ограничить, он всё равно сработает при каждом обновлении. ([The Odin Project](https://www.theodinproject.com/lessons/node-path-react-new-how-to-deal-with-side-effects?utm_source=chatgpt.com "How To Deal With Side Effects | The Odin Project"))

```jsx
useEffect(() => {
  /* side effect */
});
```

---

### Массив зависимостей

Второй аргумент у `useEffect` — **массив зависимостей**.  
Он говорит React: “запустить хук только тогда, когда что-то в этом массиве изменится”.

- Если массив пуст `[]`: эффект выполнится **только при первом рендере** (как `componentDidMount`).
    
- Если есть переменные `[a, b]`: эффект запускается при изменении `a` или `b`.
    
- Без массива: эффект — при _каждом_ рендере. ([The Odin Project](https://www.theodinproject.com/lessons/node-path-react-new-how-to-deal-with-side-effects?utm_source=chatgpt.com "How To Deal With Side Effects | The Odin Project"))

Пример с пустым массивом:

```jsx
useEffect(() => {
  setInterval(() => {
    setCounter(count => count + 1)
  }, 1000);
}, []);
```

---

### Функция очистки (cleanup)

Когда вы создаёте подписки или таймеры, важно **избежать утечек**.  
React позволяет возвращать из `useEffect` функцию очистки — она выполнится перед следующим эффектом или при _демонтаже компонента_. ([The Odin Project](https://www.theodinproject.com/lessons/node-path-react-new-how-to-deal-with-side-effects?utm_source=chatgpt.com "How To Deal With Side Effects | The Odin Project"))

```jsx
useEffect(() => {
  const key = setInterval(() => {
    setCounter(count => count + 1)
  }, 1000);

  return () => clearInterval(key);
}, []);
```

Без очистки, например в режиме `StrictMode`, таймеры могут оставаться активными даже когда компонент удаляется. ([The Odin Project](https://www.theodinproject.com/lessons/node-path-react-new-how-to-deal-with-side-effects?utm_source=chatgpt.com "How To Deal With Side Effects | The Odin Project"))

---

### Когда `useEffect` _не нужен_

Важно понимать, что эффекты — всего лишь инструмент. Он нужен **только когда происходят побочные действия, не управляемые напрямую React-рендером**. ([The Odin Project](https://www.theodinproject.com/lessons/node-path-react-new-how-to-deal-with-side-effects?utm_source=chatgpt.com "How To Deal With Side Effects | The Odin Project"))

Примеры, где `useEffect` не нужен:

- **Чистые вычисления** — нет смысла в эффекте, если вы просто хотите показать `a + b`.
    
- **События UI** — обработчики делают своё дело сами (например, `onChange`), эффекты для них не нужны.
    
- **Синхронизация состояния** лучше делать через подъём state — _lifting state up_, а не через эффект. ([The Odin Project](https://www.theodinproject.com/lessons/node-path-react-new-how-to-deal-with-side-effects?utm_source=chatgpt.com "How To Deal With Side Effects | The Odin Project"))
    

---

### Короткая формула `useEffect`

```jsx
useEffect(() => {
  /* запускается после рендера */
  return () => {
    /* очистка — перед следующим эффектом или при удалении */
  }
}, [/* зависимости */]);
```

---

### Главный вопрос перед `useEffect`

Перед тем как использовать эффект, задайте себе:  
**должен ли компонент синхронизироваться с внешней системой (сеть, таймер, DOM)?** — только в этом случае `useEffect` оправдан. ([The Odin Project](https://www.theodinproject.com/lessons/node-path-react-new-how-to-deal-with-side-effects?utm_source=chatgpt.com "How To Deal With Side Effects | The Odin Project"))

---
