***transform* не изменяет *document flow*:**

При его использовании не пересчитывается весь макет, а изменяется лишь видимая часть. Поэтому он подходит для анимаций больше чем ручной способ с помощью js.  

- ***transform* можно применить к большинству элементов**
- кроме `<col>`, `<colgroup>` и *non-replaced* инлайновым элементам (почти все инлайн элементы)


>Almost all elements can have the `transform` property applied to them, with the exceptions being , and . “Non-replaced” refers to elements whose content is contained within the HTML document (`<span>`, `<b>`, and `<em>`, for example), as opposed to a “replaced” element’s content being contained outside of the document, the element itself being “replaced” by the external content (`<video>`, `<iframe>`, and `<img>`, for example). You do not need to memorize every element that is non-replaced, but rather keep this knowledge in mind should you try to apply the `transform` property to an element and aren’t sure why it isn’t working.

## 2d transforms

- rotate
- scale
- skew
- translate

## 
