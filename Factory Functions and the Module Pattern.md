**Closure (Замыкание)** – комбинация функции и окружающей среды в которой фукнция была объявлена. 

На основе этой идеи был придуман паттерн **Factory functions**, они пришли на замену конструктора, так как те сложны в использовании (всякие протототипы и тд).
```javascript
const User = function (name) {
  this.name = name;
  this.discordName = "@" + name;
}
// hey, this is a constructor - 
// then this can be refactored into a factory!

function createUser (name) {
  const discordName = "@" + name;
  return { name, discordName };
}
// and that's very similar, except since it's just a function,
// we don't need a new keyword
```

Фабрики еще хороши для приватных полей, к ним никак не получится извне 