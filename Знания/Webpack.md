# Basics

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
    clean: true, // Очищает старый dist, и создает новый
  },
};
```

Синтаксис *CommonJS* так как сборщики изначально для бэкэнда создавались.
В конфиге прописано где будет наш готовая сборка в папке dist в корне.

Команда для сборки
```bash
npx webpack
```

# Handling HTML

По дефолту *webpack* работает только с *\*.js* файлами, и чтобы он начал работать с *html* надо установить плагин *HtmlWebpackPlugin*
```bash
npm install --save-dev html-webpack-plugin
```

И чтобы он работал надо в исходниках создать html файл и в файле конфигурации прописать путь до него

```javascript
// webpack.config.js
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  mode: "development",
  entry: "./src/index.js",
  output: {
    filename: "main.js",
    path: path.resolve(__dirname, "dist"),
    clean: true,
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: "./src/index.html",
    }),
  ],
};
```

В html файле не надо добавлять тэг для нашего скрипта, она сама добавиться туда.

# Loading CSS

Для использования стилей на снова нужно скачивать плагины
```bash
npm install --save-dev style-loader css-loader
```

Один экспортирует стили в виде строки в js код другой применяет эти самые стили к элементам.

```javascript
// webpack.config.js
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  mode: "development",
  entry: "./src/index.js",
  output: {
    filename: "main.js",
    path: path.resolve(__dirname, "dist"),
    clean: true,
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: "./src/index.html",
    }),
  ],
  module: {
    rules: [
      {
        test: /\.css$/i,
        use: ["style-loader", "css-loader"], // Порядок важен, сначала мы загружаем стили потом только используем их. Сначала идем css-loader.
      },
    ],
  },
};
```

Использование

```javascript
// src/index.js
import "./styles.css";
import { greeting } from "./greeting.js";

console.log(greeting);
```

# Loading images

Изображения которые импортируются в *css* уже обрабатываются *css-loader*’ом

Для изображений которые импортируются в *html* надо снова скачивать плагин

```bash
npm install --save-dev html-loader
```

В `rules` добавляем

```javascript
{
  test: /\.html$/i,
  loader: "html-loader",
}
```

Для изображений которые импортируются в *js* мы должны написать правило в параметрах *webpack*

В `rules` добавляем

```javascript
{
  test: /\.(png|svg|jpg|jpeg|gif)$/i,
  type: "asset/resource",
}
```

Использование 

```javascript
// src/index.js
import odinImage from "./odin.png";
   
const image = document.createElement("img");
image.src = odinImage;
   
document.body.appendChild(image);
```

Итого наш *webpack.config.js*

```javascript
// webpack.config.js
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  mode: "development",
  entry: "./src/index.js",
  output: {
    filename: "main.js",
    path: path.resolve(__dirname, "dist"),
    clean: true,
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: "./src/index.html",
    }),
  ],
  module: {
    rules: [
      {
        test: /\.css$/i,
        use: ["style-loader", "css-loader"],
      },
      {
        test: /\.html$/i,
        loader: "html-loader",
      },
      {
        test: /\.(png|svg|jpg|jpeg|gif)$/i,
        type: "asset/resource",
      },
    ],
  },
};
```

# Webpack dev server

Для автоматической трансляции изменений мы можем скачать плагин

```bash
npm install --save-dev webpack-dev-server
```

И обновить конфиг файл

```javascript
// webpack.config.js
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  mode: "development",
  entry: "./src/index.js",
  output: {
    filename: "main.js",
    path: path.resolve(__dirname, "dist"),
    clean: true,
  },
  devtool: "eval-source-map", // Для корректного отображения различных сообщений и нашего кода в devtools, так как webpack комкует весь код и чтобы мы не увидили какой-нибудь хэш
  devServer: {
    watchFiles: ["./src/index.html"], // просматриваемый файл
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: "./src/index.html",
    }),
  ],
  module: {
    rules: [
      {
        test: /\.css$/i,
        use: ["style-loader", "css-loader"],
      },
      {
        test: /\.html$/i,
        loader: "html-loader",
      },
      {
        test: /\.(png|svg|jpg|jpeg|gif)$/i,
        type: "asset/resource",
      },
    ],
  },
};
```

Команда для запуска

```bash
npx webpack serve
```

# Deploy

```bash
git add dist -f && git commit -m "Deployment commit"
git subtree push --prefix dist origin gh-pages
git checkout main
```

# npm scripts

Можно использовать свои кастомные скрипты, объявив их в *package.json*

```json
"scripts": {
	"build": "webpack --config webpack.prod.js", // Разделение конфигов, будет
	"dev": "webpack serve --config webpack.dev.js", // Освещено далее
	"deploy": "git subtree push --prefix dist origin gh-pages"
},
```

# Webpack modes

Короче, можно разделить конфиги для продакшена и для разработки.
Делается это с помощью плагина *webpack merge*
```bash
npm install --save-dev webpack-merge
```

Общая часть конфигов может быть такой *webpack.common.js*

```js
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
	entry: "./src/index.js",
	output: {
		filename: "main.js",
		path: path.resolve(__dirname, "dist"),
		clean: true,
	},
	plugins: [
		new HtmlWebpackPlugin({
			template: "./src/index.html",
		}),
	],
	module: {
		rules: [
			{
				test: /\.css$/i,
				use: ["style-loader", "css-loader"],
			},
		],
	},
};
```

Конфиг для разработки *webpack.dev.js*

```js
const { merge } = require('webpack-merge');
const common = require('./webpack.common.js');

module.exports = merge(common, {
	mode: 'development',
	devtool: "eval-source-map",
	devServer: {
		watchFiles: ["./src/index.html"],
	},
});
```

Конфиг для разработки *webpack.prod.js*

```js
const { merge } = require('webpack-merge');
const common = require('./webpack.common.js');

module.exports = merge(common, {
	mode: 'production',
	devtool: 'source-map',
});
```