- ***transition* это сокращение для `transition-property`, `transition-duration`, `transition-timing-function` и `transition-delay` свойств:**
	Пример:
	`{css} transition: background-color 1s ease-out 0.25s;`

- **стараться использовать `opacity` или `transition` для производительности**

- **если свойств для которых мы хотим добавить переход больше чем значений в то эти значения повторяются:**
```css
div { 
	transition-property: opacity, left, top, height; 
	transition-duration: 3s, 5s; /* 3s 5s дополнительно добавляются*/ 
}	
```

- **если свойств для которых мы хотим добавить переход меньше чем значений в то лишние значения отбрасываются:**
```css
div {
  transition-property: opacity, left;
  transition-duration: 3s, 5s, 2s, 1s; /* последние два значения отбрасываются */
}
```

- **Дискретные значения как `display` или `content-visibility` переключаются после половины анимации**
	Однако, для `display: none` or `content-visibility: hidden` переход осуществляется так чтобы во время анимации элемент был виден, но для этого надо установить `transition-behavior: allow-discrete` 
	
	Когда мы изменяем `display`  во время перехода, мы должны установить `@starting-style` что предоставить начальные параметры, это необходимо чтобы избежать неопределенного поведения. Браузер не видит элемент когда у него `display: none`, поэтому, когда мы изменяем это значение, оно как будто бы изначально имело конечные параметры, игнорирую начальные, и чтобы указать браузеру как правильно сделать переход мы явно указываем `@starting-style`. В большинстве случае лучше использовать `content-visibility` так как браузер уже знает начальные параметры и сделает самостоятельно правильный переход.
	
	Примерно такая же ситуация когда используем js для изменения макета, браузер не знает, и чтобы правильно отрендерить переход надо `setTimeout()` использовать.

- **Используем `transitionend`,  `transitionrun`,  `transitionstart` события чтобы узнать то переход закончен, началось до задержки, началось после задержки соответственно.**

- ***stacking context* это как группа объектов в *Figma*, а *z-index* это позиция в группе, у самих *stacking context*’ов тоже есть свой *z-index***
```css
/* Способы создания контекстных стеков */
.some-element {
  position: relative; /* может быть и absolute */
  z-index: 1;
}
/*
- Setting `opacity` to a value less than `1`
- Setting `position` to `fixed` or `sticky` (No z-index needed for these values!)
- Applying a `mix-blend-mode` other than `normal`
- Adding a `z-index` to a child inside a `display: flex` or `display: grid` container
- Using `transform`, `filter`, `clip-path`, or `perspective`
- Using `will-change` with a value like `opacity` or `transform`
- Explicitly creating a context with `isolation: isolate` 
- and others ...
*/
```

- ***stacking context* это не про родитель/ребенок отношения (ребенок может быть наравне с дядей), однако его изменение сказывается на всех потомках**

- **Используем `isolation: isolate` для того чтобы сделать изолированную компоненту которая не будет конфликтовать с внешним миров**
