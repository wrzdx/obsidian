# Basics

Пример объекта:

```js
const myObject = {
  property: 'Value!',
  otherProperty: 77,
  "obnoxious property": function() {
    // do stuff!
  }
};

```

Существует два типа нотации: *dot* и *bracket*

```javascript
// dot notation
myObject.property; // 'Value!'

// bracket notation
myObject["obnoxious property"]; // [Function]

const variable = 'property';

myObject.variable; // this gives us 'undefined' because it's looking for a property named 'variable' in our object

myObject[variable]; // this is equivalent to myObject['property'] and returns 'Value!'

```

# Object constructors
Пример конструктора:

```javascript
function Player(name, marker) {
  this.name = name;
  this.marker = marker;
}
```

Использование:

```javascript
const player = new Player('steve', 'X');
console.log(player.name); // 'steve'
```

Для проверки правильного использования конструкора добавляют в нее следующее условие:

```javascript
function Player(name, marker) {
  if (!new.target) {
    throw Error("You must use the 'new' operator to call the constructor");
  }
  this.name = name;
  this.marker = marker;
  this.sayName = function() {
    console.log(this.name)
  };
}
```

# The prototype

У всех объектов в JS есть прототип. Прототип это еще один объект от которого наследуется настоящий объект. У настоящего объекта есть все методы и поля его прототипа.

```javascript
Object.getPrototypeOf(player1) === Player.prototype; // returns true
Object.getPrototypeOf(player2) === Player.prototype; // returns true
```

## Prototypal inheritance

Почти как классовое наследство, за исключение того что можно изменять уже объявленные методы и поля прототипов.

Каждый прототипный объект, наследуется от Object.prototype по умолчанию.

Несмотря на то что я сказал что можно изменять поля и методы, данные манипуляции должны быть совершенны до создания первого объекта этого прототипа, иначе скажется на производительности.