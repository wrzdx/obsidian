- ***transform* не изменяет *document flow*:**
	При его использовании не пересчитывается весь макет, а изменяется лишь видимая часть. Поэтому он подходит для анимаций больше чем ручной способ с помощью js.  


- ***transform* можно применить к большинству элементов:**
	кроме `<col>`, `<colgroup>` и *non-replaced* инлайновым элементам (почти все инлайн элементы)

- **2d *transforms*: `rotate`, `scale`, `skew`, `translate`**
- ***transforms* читаются справа на лево и накладываются относительно origin**
	origin – типа то что учитывает макет, там где оно было изначально
	
	**Пример:**
	
	``` css
	.red-box,
	.blue-box {
	  position: absolute;
	  width: 100px;
	  height: 100px;
	}
	
	.red-box {
	  background: red;
	  transform: rotate(45deg) translate(200%);
	}
	
	.blue-box {
	  background: blue;
	  transform: translate(200%) rotate(45deg);
	}

	```