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
	
	Когда мы изменяем `display`  во время перехода, мы должны установить `@starting-style` что предоставить начальные параметры, это необходимо чтобы избежать неопределенного поведения. Это, можно сказать, самая отправная точка 
  
