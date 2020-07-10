# Install Webpack

### `npm init -y`

- Initialize `package.json`

### `npm install webpack webpack-cli --save-dev`

### `package.json`

```json
  "scripts": {
    "build": "webpack",
    "watch": "webpack --watch"
  },

```

- `npm run build` runs with Webpack
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

### `npm run build`

```json
"scripts": {
  "build": "webpack"
},
```

- Builds app with Webpack

## Dependency Graph

- Webpack starts from the entry file and goes and looks for each `import`/`export` statement and bundles them into required module dependencies

# Loaders

