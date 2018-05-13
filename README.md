# vue-cli-multiplePage

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```
## [博客地址](https://bruceshang.github.io/2018/05/05/vue%E9%A1%B9%E7%9B%AEwebpack%E5%A4%9A%E9%A1%B5%E9%9D%A2%E6%9E%84%E5%BB%BA/)

### 1.配置多入口
```js
// utils.js
// 查找符合特定规则的文件路径名
var glob = require('glob')
//获取多级的入口文件
exports.getMultiEntry = function (globPath) {
  var entries = {},
    basename, tmp, pathname;

  glob.sync(globPath).forEach(function (entry) {
    basename = path.basename(entry, path.extname(entry));
    tmp = entry.split('/').splice(-4);

    var pathsrc = tmp[0] + '/' + tmp[1];
    if (tmp[0] == 'src') {
      pathsrc = tmp[1];
    }
    pathname = pathsrc + '/' + basename; // 正确输出js和html的路径
    entries[pathname] = entry;

  });

  return entries;

}

```
### 2. 在webpack.base.conf.js中赋值给entry

```js
const utils = require('./utils')
// 多页面设置入口文件
const entries = utils.getMultiEntry('./src/' + config.moduleName + '/**/**/*.js');
module.exports = {
  entry: entries,
}
```

### 3. 构建生成多页面的HtmlWebpackPlugin配置

```js
// webpack.dev.conf.js webpack.prod.conf.js
分别在webpack.dev.conf.js 和webpack.prod.conf.js中设置
var pages = utils.getMultiEntry('./src/' + config.moduleName + '/**/**/*.html');
for (var pathname in pages) {
  var conf = {
    filename: pathname + '.html',
    template: pages[pathname], // 模板路径
    chunks: ['vendor', pathname], // 每个html引用的js模块
    inject: true,              // js插入位置
    hash: true
  };

  webpackConfig.plugins.push(new HtmlWebpackPlugin(conf));
}

module.exports = webpackConfig
```