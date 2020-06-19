# next+typescript 使用

## 初始化 next

1. 手动添加，执行如下命令
   ```
   yarn add @types/node @types/react next react react-dom typescript antd
   yarn add -D @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint eslint-config-prettier eslint-plugin-prettier eslint-plugin-react prettier
   ```
   通过以上命令，将会添加 next、react、typescript、eslint、prettier 支持
2. 配置 eslint 和 prettier，请查看[样式配置](./typescript.md)
3. 为了支持 next 的声明文件，需要在根目录添加 next-env.d.ts,将声明文件引入项目中

```
/// <reference types="next" />
/// <reference types="next/types/global" />
```

4. 在引入 antd 时，如果使用 next-less，引入 css Module 默认的时候，会将 antd 样式也按照 css Module 形式引入。
   为了移除对 antd 样式按照 css Module 方式，需要按照如下方式使用 getLocalIdent 方法进行排除
   ```
   const lessConfig = withLess({
    cssModules: true,
    lessLoaderOptions: {
      javascriptEnabled: true,
      exclude: [/node_modules/]
    },
    cssLoaderOptions: {
      importLoaders: 1,
      localIdentName: '[name]__[local]__[hash:base64:5]',
      getLocalIdent: (context, localIdentName, localName, options) => {
        let hz = context.resourcePath.replace(context.rootContext, '')
        if (/node_modules/.test(hz) || !/(\.module\.)/.test(hz)) {
          return localName
        }
        return localIdentName
      }
    }
   })
   ```

## next 文件介绍

next 中是按照约定文件，对系统进行架构。业务代码可以写入 src 文件夹中，也可以去除 src，直接写入根路径下。

1. pages：所有业务页面写在此下，自动生成路由信息：/xxx，根据文件路径生成路由。
   - 默认会查找 index 页面，比如 pages/center/index.tsx---->生成路由为/center，
   - 如果需要路由带参数，比如参数 id：pages/center/\[id\].tsx---->生成路由为/center/1.

包括路径参数和 url 参数可以通过如下代码获取：

```
import { useRouter } from 'next/router'
const router = useRouter()
const { pid } = router.query
```

2. \_app.tsx: 默认 next 页面都是通过 index 页面默认创建，如果需要自定义的话，可以在 pages/\_app.tsx。文件名称不能修改。
   可以通过修改此文件，打到自定义页面的需求

3. \_document.tsx: 自定义页面中html、header、body等内容，其在server端运行，
 ```
  import Document, { Html, Head, Main, NextScript } from 'next/document'

  class MyDocument extends Document {
    static async getInitialProps(ctx) {
      const initialProps = await Document.getInitialProps(ctx)
      return { ...initialProps }
    }

    render() {
      return (
        <Html>
          <Head />
          <body>
            <Main />
            <NextScript />
          </body>
        </Html>
      )
    }
  }

  export default MyDocument
 ```

4. next.config.js: 自定义配置一些信息，包括环境变量、webpack 等,webpack会同时在server端和client运行，如果是需要只在某端进行webpack配置的话，需要判断isServer
5. 在引入 css 文件时，分为全局和局部样式文件。全局样式为 style.css，局部为 style.module.css.
   sass 支持，需要安装 npm install sass
   ```
   const path = require('path')
   module.exports = {
     sassOptions: {
       includePaths: [path.join(__dirname, 'styles')],
     },
   }
   ```
   less 支持，可以安装@zeit/next-less

## next.config.js

此文件需要按照 node 的 commonjs 方式书写。可以返回对象，也可以返回一个方法

```
module.exports = {
  /* config options here */
}
module.exports = (phase, { defaultConfig }) => {
  return {
    /* config options here */
  }
}
```
