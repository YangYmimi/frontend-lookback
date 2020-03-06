### Webpack 中 loaders 和 plugins 的区别以及一些常用的 loaders 和 plugins 的作用

#### loaders 作用

webpack 开箱即用只支持 js 和 json 两种文件类型，通过 loaders 去支持其他文件类型，并转换成有效的模块，添加到依赖图中。本身是一个函数，接受源文件为参数，返回转换后的结果。

|  常用loader名称  | 作用 |
|  ----  |  ----  |
| babel-loader | 转换 es6+ 语法 |
| css-loader | 支持 css 文件的加载和解析 |
| less-loader | 将 less 转换成 css |
| ts-loader | 将 ts 转换成 js |
| file-loader | 图片，字体等打包 |
| url-loader | 可以返回 data URL，像 file-loader 一样工作 |
| raw-loader | 将文件以字符串形式导入 |
| vue-loader | 加载和转译 vue 组件 |
| thread-loader | 多进程打包 js 和 css |

* 更多 loaders 可参考：https://webpack.docschina.org/loaders

#### plugins 作用

plugins 用于 bundle 文件的优化，资源管理和环境变量注入等，作用于整个构建过程

|  常用plugins名称  | 作用 |
|  ----  |  ----  |
| CommonsChunkPlugin | 将 chunks 中相同的模块代码提取成公共的 js |
| CleanWebpackPlugin | 清理构建目录 |
| ExtractTextWebpackPlugin | 将 css 从 bundle 文件里提取成一个一个独立的 css 文件 |
| CopyWebpackPlugin | 将文件或者文件夹拷贝到构建的输出目录 |
| HtmlWebpackPlugin | 创建 html 文件去承接输出的 bundle |
| HotModuleReplacementPlugin | 模块热更新插件 |
| MiniCssExtractPlugin | 为每个引入 CSS 的 JS 文件创建一个 CSS 文件 |
| UglifyjsWebpackPlugin | 压缩 js |
| ZipWebpackPlugin | 将打包出的资源生成一个 zip 包 |

* 更多 plugins 可参考：http://webpack.docschina.org/plugins