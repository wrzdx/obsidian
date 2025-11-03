- ***transform* не изменяет *document flow*:**
	При его использовании не пересчитывается весь макет, а изменяется лишь видимая часть, а именно в последней composite stage в [pixel pipeline](https://web.dev/articles/rendering-performance#the_pixel_pipeline). Поэтому он подходит для анимаций больше чем ручной способ с помощью изменения макета с js.  
	
	[Список триггеров css свойств](https://web.archive.org/web/20220727225220/https://csstriggers.com/)

- ***transform* можно применить к большинству элементов кроме inline:**

- **2d *transforms*: `{css}rotate`, `{css}scale`, `{css}skew`, `{css}translate`, `{css}matrix`**

- ***transforms* читаются справа на лево и накладываются относительно origin**
	origin – типа то что учитывает макет, там где оно было изначально
	[пример](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/transform#examples	)

- **3d *transforms*: `{css}rotate3d`, `{css}scale3d`, `{css}translate3d`, `{css}matrix3d`, `{css}perspective`**

- **3d *transforms* начинают работать когда объявлен `{css}perspective` and и важно объявлять его первым (самым левым)**
	`perspective` – заставляет объект рендерится как если бы он был на определенном расстоянии на *z* оси. Аналогия, представьте как если мы перед вами была полка, чем дальше вы от полки тем меньше видишь внутренние боковые стенки, однако чем ближе те лучше ты видишь их.

- ***transform* может использовать GPU ускорение рендеринга**
	Важно когда мы сочетаем *transform* с *transition*

- **tips / hints:**
	`{css}translate` - можно использовать для *close button*
	`{css}scale` - можно использовать для эффекта выключения старого телевизора
	`{css}skew` - можно использовать для создания немного искаженного фона [Stripe](https://stripe.com/)
	- Чтобы искажения не сказывались на потомках можно для них обратные трансформации делать “[Create Diagonal Layouts Like It's 2020](https://9elements.com/blog/pure-css-diagonal-layouts/)”
	- `{css}scale` с измененным *origin* можно создать эффект element "growing out of" another one
	- `{css}rotate` + `{css}translate` - эффект обращения
	
