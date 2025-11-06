**Webpack** – является одним из полпулярных **сборщиков**. Суть его заключается в том что бы весь наш исходники скомковать в один кусок кода. 

Начинает строить дерево зависимостей начинаю с точки входа, тем самым отбрасывая все лишнее, тем самым оптимизирует код. Кроме того оно может также убрать все лишние пробелы и отсупы. 

**Использование:**

```bash
npm install --save-dev webpack webpack-cli # Можно использовать -D вместо --save-dev
```

Далее надо создать папку для нашего исходного кода и в нем точку входа в нашу программу

```bash
mkdir src && touch src/index.js
```

В корне нужно создать конфиг для *webpack*

```bash
touch webpack.config.js
```

В нем прописать наши настройки

```javascript
// webpack.config.js
const path = require("path");

module.exports = {
  mode: "development",
  entry: "./src/index.js",
  output: {
    filename: "main.js",
    path: path.resolve(__dirname, "dist"),
    clean: true,
  },
};
```



