# 前端模块化
## commonjs
通过使用require同步加载模块，使用module.exports导出需要暴露的接口，此模块主要在NodeJs中使用。
此只能通过工具转换成标准的ES5才能再浏览器中使用
## AMD
采用异步方式加载模块，最具代表性的是requirejs。
```
采用 AMD 导入及导出的代码如下：
／／ 定义 个模块
define (’module ’,[’dep ’] , function (dep) { 
  return exports; 
}); 
／／导入和使用
require ( [’module ’] , function (module) { 
});
```
1. 没有原生支持AMD，需要导入实现了AMD的库后才能使用
2. 可异步加载模块
3. 可并行加载多个模块
4. 可在不转换代码情况下在浏览器中运行

## ES6模块化
ES6 模块化是国际标准化组织 ECMA 提出的 JavaScript 模块化规范，它在语言层面上实
现了模块化。浏览器厂商和 Node 都宣布要原生支持该规范 它将逐渐取代 CommonJS
AMD 规范，成为浏览器和服务器通用的模块解决方案
```
／／导入
import { readFile } from ’ fs ’; 
import React from ’ react ’ ; 
／／导出
export function hello {) { } ; 
export default { 
//
}
```
ES6 模块虽然是终极模块化方案，但它的缺点在于目前无法直接运行在大部分 JavaScript
运行环境下，必须通过工具转换成标准的 ES5 后才能正常运行。
## 样式模块化
样式可以写到单独文件中，并通过@import方式导入到其他文件中

## webpack
在 Webpack一切文件皆模块，通过 Loader 转换文件，通过 Plugin 注入钩子，最后输出由多个模块组合成的
文件。 Webpack 专注于构建模块化项目。
使用loader来对文件进行转换，
```
module.exports = {
  entry: '',
  output: {},
  module: {
    rules:[
      {
        test: /\.css$/,
        use: [’style-loader ’,’css-loader?minimize ’ ]
        // 或者如下
        use: [
          'style-loader',
          {
            loader: 'style-loader',
            options:{
              minimize:true
            }
          }
        ]
      }
    ]
  }
}
```
使用plugings来对webapck进行扩展，通过在构建过程里注入钩子实现。

### 配置节点说明
- Entry 配置模块的入口
- Output 配置如何输出最终想要的代码
- Module 配置处理模块的规则
- Resolve 配置寻找模块的规则
- Plugins 配置扩展插件
- Mode 选择development和production之一
- externals 排除import的包打包到bundle中，在运行时从外部环境获取
- performance 配置超过指定文件限制的性能信息
- DevServer 配置DevServer
