# [Documentation](https://webpack.js.org/concepts/)

# Install Webpack

### `npm init -y`

- Initialize `package.json`

### `npm i -D webpack webpack-cli`

### `package.json`

```json
  "scripts": {
    "build": "webpack",
    "watch": "webpack --watch"
  },

```

- `npm run build` runs Webpack
- `npm run watch` runs Webpack with the `--watch` flag

# Webpack Config

### `webpack.config.js`

```js
const path = require("path");

module.exports = {
  entry: './src/index.js',
  output: {
    filename: "bundle.js",
    path: path.join(__dirname, "build")
  }
}
```

- `entry` is the first file in the dependency graph
- `path` is always an absolute path
    - Defaults to `./dist`
- Here, we join the current directory `__dirname` with a directory named `build`

## Dependency Graph

- Webpack starts from the entry file and goes and looks for each `import`/`export` statement and bundles them into required module dependencies

# Loaders

- Webpack allows any type of asset to be treated as a module and transformed
- In the end, the asset is converted back to JS and added back to the dependency graph

## `use & test`

```js
// webpack.config.js

module.exports = {
  ...,
  module: {
    rules: [
      {
        test: /\.js$/,
        use:"babel-loader"
      },
      {
        test: /\.css$/,
        use: [
          "style-loader",
          "css-loader"
        ]
      }
    ]
  }
}
```

- `test` tells Webpack to match files against Regex and perform a transformation 
- The transformation is a loader

### Multiple Loaders

```js
styleLoader(cssLoader(source));
```
```json
use: [
  "style-loader",
  "css-loader"
]
```

# Plugins

- Loaders can only apply changes to a single file right before it can be added to the dependency graph
- Plugins do what loaders cannot (ex. change multiple files, create bundles)

```js
class ExamplePlugin {
  apply(compiler) {
    compiler.plugin("run", (compiler, callback) => {
      console.log('webpack is running');
      callback();
    });
  }
}

module.exports = ExamplePlugin;
```

```js
// webpack.config.js

const ExamplePlugin = require("./ExamplePlugin.js");

module.exports = {
  ...,
  plugins: [
    new ExamplePlugin()
  ]
}
```

# Recap

### Entry 

- The root of the webpack dependency graph

### Output 

- How and where to put the bundles

### Rules + Loaders 

- How to treat folders before they are added to the dependency graph
- Allows any asset to be treated like a module

### Plugins

- Any other functionality
- Class based, extremely customizable

# [Webpack 5](https://www.youtube.com/watch?v=X1nxTjVDYdQ)

## Why we need Webpack

`Uncaught SyntaxError: Cannot use import statement outside a module`

- using imports and exports with multiple JS files
    - there can only be one js file for our html :)
    - webpack bundles all the modules up into 1 entry point
    - also cleans out all the unnecessary stuff; keeps the goods 
        - (ex. outputting the function body code instead of importing the function)

1. Install Webpack
2. Put all the js files inside a `src` folder
3. `npx webpack` to compile our `src` files
4. Check `dist` for our output `main.js`

