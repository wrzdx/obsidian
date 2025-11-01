- ***transform* не изменяет *document flow*:**
	При его использовании не пересчитывается весь макет, а изменяется лишь видимая часть, а именно composite stage в [pixel pipeline](https://web.dev/articles/rendering-performance#the_pixel_pipeline). Поэтому он подходит для анимаций больше чем ручной способ с помощью js.  
	
	[Список триггеров css свойств](https://web.archive.org/web/20220727225220/https://csstriggers.com/)

- ***transform* можно применить к большинству элементов:**
	кроме `<col>`, `<colgroup>` и *non-replaced* инлайновым элементам (почти все инлайн элементы)

- **2d *transforms*: `rotate`, `scale`, `skew`, `translate`, `matrix`**

- ***transforms* читаются справа на лево и накладываются относительно origin**
	origin – типа то что учитывает макет, там где оно было изначально
	[пример](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/transform#examples	)

- **3d *transforms*: `rotate3d`, `scale3d`, `translate3d`, `matrix3d`, `perspective`**

- **3d *transforms* works when you declared `perspective` and it’s important to declared it first (leftmost)**
	`perspective` – make object to render as it was from specific distance on *z*-axis
