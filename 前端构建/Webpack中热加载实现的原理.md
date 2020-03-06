### Webpack 中热加载实现的原理

#### 使用 webpack-dev-server

  - WDS 不刷新浏览器

  - WDS 不输出文件，而是放在内存中

  - 配合 HotModuleReplacementPlugin 插件

```javascript
'use strict';

const path = require('path');
const webpack = require('webpack');

module.exports = {
  entry: {
    // 多入口
    index: './src/index.js',
    search: './src/search.js'
  },
  output: {
    // 出口文件，用 [name] 占位符区分
    path: path.join(__dirname, 'dist'),
    filename: '[name].js'
  },
  mode: 'development', // HotModuleReplacementPlugin 只在 dev 环境用
  module: {
    rules: [
      {
        // 配置转换 es 语法
        test: /.js$/,
        use: 'babel-loader'
      },
      {
        // css 加载器
        test: /.css$/,
        use: [
          'style-loader',
          'css-loader'
        ]
      },
      {
        // less 加载器
        test: /.less$/,
        use: [
          'style-loader',
          'css-loader',
          'less-loader'
        ]
      },
      {
        // 文件资源（图片，gif）加载器
        test: /.(png|jpg|gif|jpeg)$/,
        use: [
          {
            loader: 'url-loader',
            options: {
              limit: 10240
            }
          }
        ]
      },
      {
        // 字体文件加载器
        test: /.(woff|woff2|eot|ttf|otf)$/,
        use: 'file-loader'
      }
    ]
  },
  plugins: [
    new webpack.HotModuleReplacementPlugin(),
    new HtmlWebpackPlugin({
      // 生成入口 html
      template: path.join(__dirname, 'src/index.html'),
      filename: 'index.html',
      chunks: ['index'],
      inject: true,
      minify: {
        html5: true,
        collapseWhitespace: true,
        preserveLineBreaks: false,
        minifyCSS: true,
        minifyJS: true,
        removeComments: false
      }
    }),
    new HtmlWebpackPlugin({
      // 多入口模板
      template: path.join(__dirname, 'src/search.html'),
      filename: 'search.html',
      chunks: ['search'],
      inject: true,
      minify: {
        html5: true,
        collapseWhitespace: true,
        preserveLineBreaks: false,
        minifyCSS: true,
        minifyJS: true,
        removeComments: false
      }
    })
  ],
  devServer: { // 配置 devServer
    contentBase: './dist',
    hot: true // 开启热更新
  }
};
```

#### 使用 webpack-dev-middleware

  - WDM 将 webpack 输出的文件传输给浏览器

  - Webpack Compile 会将 JS 编译成 bundle.js

  - HMR Server 会将热更新文件输出给 HMR Runtime

  - Bundle Server 提供文件在浏览器的访问

  - HMR Runtime 会被注入到浏览器，更新文件的变化

那么使用 `webpack-dev-middleware` 进行热更新的流程，可以如下总结：（1）启动阶段，`webpack compile` 编译器将文件进行编译打包成 `bundle.js`，然后将打包好的文件也就是 `bundle.js` 传输给 `bundle server`，这样浏览器就可以访问到这个文件了；（2）热更新阶段，当文件系统文件有了变化，`webpack compile` 会继续将文件编译成 `bundle.js`，然后会将文件传输给 `hmr server`，`hmr server` 会将变化的 `js` 模块通过 `websocket` 方式通知浏览器端进行更新，也就是 `hmr runtime` 会接收到这些文件（浏览器会看到 `hot-update.json` 文件传过来）