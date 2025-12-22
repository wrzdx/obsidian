## Проблема:

Мы не можем отделить программы друг от друга (инкапсулировать)

```html
<script src="one.js" defer></script>
<script src="two.js" defer></script>
```

```javascript
// one.js
const greeting = "Hello, Odinite!";
```

```javascript
// two.js
console.log(greeting);
```

Второй скрипт прекрасно видит константу *greeting*.

## Решение

Раньше использовали замыкания для инкапсуляции:

```javascript
// one.js
(() => {
  const greeting = "Hello, Odinite!";
})();
```

Однако с выходом ES6 появились модули – `import` и `export`


### Бывает именнованный export 
```javascript
// one.js
export const greeting = "Hello, Odinite!";
export const farewell = "Bye bye, Odinite!";
```

или

```javascript
// one.js
const greeting = "Hello, Odinite!";
const farewell = "Bye bye, Odinite!";
export { greeting, farewell };
```

Для использования
```javascript
// two.js
import { greeting, farewell } from "./one.js";

console.log(greeting); // "Hello, Odinite!"
console.log(farewell); // "Bye bye, Odinite!"
```

### А бывает export по умолчанию

```javascript
// one.js
export default "Hello, Odinite!";
```

или

```javascript
// one.js
const greeting = "Hello, Odinite!";
export default greeting;
```

Использование:

```javascript
// two.js
import helloOdinite from "./one.js";

console.log(helloOdinite); // "Hello, Odinite!"
```

**Можно совмещать с именнованным `export`**

```javascript
// one.js
export default "Hello, Odinite!";
export const farewell = "Bye bye, Odinite!";
```

и

```javascript
// two.js
import greeting, { farewell } from "./one.js";

console.log(greeting); // "Hello, Odinite!"
console.log(farewell); // "Bye bye, Odinite!"
```



