- ***transition* это сокращение для `{css}transition-property`, `{css}transition-duration`, `{css}transition-timing-function` и `{css}transition-delay` свойств:**
	Пример:
	`{css} transition: background-color 1s ease-out 0.25s;`

- **стараться использовать `{css}opacity` или `{css}transition` для производительности**

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

- **Дискретные значения как `{css}display` или `{css}content-visibility` переключаются после половины анимации**
	Однако, для `{css}display: none` or `{css}content-visibility: hidden` переход осуществляется так чтобы во время анимации элемент был виден, но для этого надо установить `{css}transition-behavior: allow-discrete` 
	
	Когда мы изменяем `{css}display`  во время перехода, мы должны установить `{css}@starting-style` что предоставить начальные параметры, это необходимо чтобы избежать неопределенного поведения. Браузер не видит элемент когда у него `{css}display: none`, поэтому, когда мы изменяем это значение, оно как будто бы изначально имело конечные параметры, игнорирую начальные, и чтобы указать браузеру как правильно сделать переход мы явно указываем `{css}@starting-style`. В большинстве случае лучше использовать `{css}content-visibility` так как браузер уже знает начальные параметры и сделает самостоятельно правильный переход.
	
	Примерно такая же ситуация когда используем js для изменения макета, браузер не знает, и чтобы правильно отрендерить переход надо `{css}setTimeout()` использовать.

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

- **Инструменты для отслеживания и отладки *z-index*’a “Andrea Dragotta created an _incredible_ browser extension that adds a bunch of super-important information about z-index and stacking contexts. It’s available for [Chrome](https://chrome.google.com/webstore/detail/css-stacking-context-insp/apjeljpachdcjkgnamgppgfkmddadcki) and [Firefox](https://addons.mozilla.org/en-US/firefox/addon/css-stacking-context-inspector/)” и “[3D view](https://docs.microsoft.com/en-us/microsoft-edge/devtools-guide-chromium/3d-view/)”**

- **Можно заранее сказать браузеру создать объект на другом слое чтобы все другие слои пропустили некоторые стадии отрисовки страницы. Для этого используют `will-change`. Однако надо измерять performance. Кроме того, объект начинает сразу рендерится GPU, а не передаваться от CPU к GPU и обратно, и благодаря этому нет прыжков и искажений, но потребление памяти чуть-чуть возрастает**

- **Использование GPU (`transform`) также нам дает доступ к подпикселям, что не доступно CPU операциям e.g. `margin`, из-за чего переход более плавный**

- ***easy-out* – для появления, *easy-in* – для ухода, *easy-in-out* – для циклических анимаций, *easy* – значение по-умолчанию. https://easingwizard.com/, https://easings.net/**
```css
.btn {
  /* ease-out */
  transition-timing-function: cubic-bezier(0.215, 0.61, 0.355, 1);

  /* ease-in */
  transition-timing-function: cubic-bezier(0.75, 0, 1, 1);

  /* ease-in-out */
  transition-timing-function: cubic-bezier(0.645, 0.045, 0.355, 1);

  /* ease */
  transition-timing-function: cubic-bezier(0.44, 0.21, 0, 1);
}
```

- *Delay* можно использовать, допустим для dropdown menus или подобных динамических элементов которые должны не сразу же исчезать

- В ситуациях когда эффект тригера тушит тригер, мы должны отделить их друг от друга, чтобы допустим родитель запускал тригер, однако эффект был у ребенка
```css
<button class="btn">
  <span class="background">
    Hello World
  </span>
</button>

<style>
  .background {
    will-change: transform;
    transition: transform 450ms;
  }
  
  .btn:hover .background {
    transition: transform 150ms;
    transform: translateY(-10px);
  }
  
  /* Toggle me on for a clue! */
  .btn {
     outline: auto;
  }
  .btn {
  width: 100px;
  height: 100px;
  border: none;
  background: transparent;
  padding: 0px;
}

.background {
  display: flex;
  align-items: center;
  width: 100%;
  height: 100%;
  border-radius: 50%;
  background: slateblue;
  color: white;
  font-size: 20px;
  font-weight: 500;
  line-height: 1;
}
</style>
```

