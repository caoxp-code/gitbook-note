# 在react中引入typescript
通过使用npx creat-react-app my-app --template typescript脚手架，自动生成react+typescript项目。
## tsconfig.json
ts的配置编译选项，可以参考[编译详细配置](https://www.tslang.cn/docs/handbook/compiler-options.html)
最常用的配置选项如下：
```
{
  "compilerOptions": {
    "target": "es5", // 指定 ECMAScript 版本
    "lib": [
      "dom",
      "dom.iterable",
      "esnext"
    ], // 要包含在编译中的依赖库文件列表
    "allowJs": true, // 允许编译 JavaScript 文件
    "skipLibCheck": true, // 跳过所有声明文件的类型检查
    "esModuleInterop": true, // 禁用命名空间引用 (import * as fs from "fs") 启用 CJS/AMD/UMD 风格引用 (import fs from "fs")
    "allowSyntheticDefaultImports": true, // 允许从没有默认导出的模块进行默认导入
    "strict": true, // 启用所有严格类型检查选项
    "forceConsistentCasingInFileNames": true, // 不允许对同一个文件使用不一致格式的引用
    "module": "esnext", // 指定模块代码生成
    "moduleResolution": "node", // 使用 Node.js 风格解析模块
    "resolveJsonModule": true, // 允许使用 .json 扩展名导入的模块
    "noEmit": true, // 不输出(意思是不编译代码，只执行类型检查)
    "jsx": "react", // 在.tsx文件中支持JSX
    "sourceMap": true, // 生成相应的.map文件
    "declaration": true, // 生成相应的.d.ts文件
    "noUnusedLocals": true, // 报告未使用的本地变量的错误
    "noUnusedParameters": true, // 报告未使用参数的错误
    "experimentalDecorators": true, // 启用对ES装饰器的实验性支持
    "incremental": true, // 通过从以前的编译中读取/写入信息到磁盘上的文件来启用增量编译
    "noFallthroughCasesInSwitch": true //报告switch语句的fallthrough错误。（即，不允许switch的case语句贯穿）
  },
  "include": [
    "src/**/*" // *** TypeScript文件应该进行类型检查 ***
  ],
  "exclude": ["node_modules", "build"] // *** 不进行类型检查的文件 ***
}
```
## 添加eslint/prettier
由于，tslint已不提供支持，为了规范团队代码的风格统一和默认规则的编写，引入eslint和prettier。
```
yarn add eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin eslint-plugin-react --dev
yarn add prettier eslint-config-prettier eslint-plugin-prettier --dev
```
在根目录中创建.eslintrc文件
```
{
  "parser": "@typescript-eslint/parser", // 指定eslint解析器
  "extends": [
    "plugin:react/recommended",  // 使用来自 @eslint-plugin-react 的推荐规则
    "plugin:@typescript-eslint/recommended",  // 使用来自@typescript-eslint/eslint-plugin的推荐规则
    "prettier/@typescript-eslint",  // 使用 ESLint -config-prettier 禁用来自@typescript-eslint/ ESLint 与 prettier 冲突的 ESLint 规则
    "plugin:prettier/recommended"
  ],
  "parserOptions": {
    "ecmaVersion": 2018, // 允许解析最新的 ECMAScript 特性
    "sourceType": "module", // 允许使用import
    "ecmaFeatures": {
      "jsx": true // 允许对JSX进行解析
    }
  },
  "rules": {
    // 自定义规则
  },
  "settings": {
    "react": {
      "version": "detect" // 告诉 eslint-plugin-react 自动检测 React 的版本
    }
  }
}
```

在根目录添加.prettierrc文件
```
{
  "semi": true,
  "trailingComma": "all",
  "singleQuote": true,
  "printWidth": 120,
  "tabWidth": 4
}
```
## 添加vscode支持
在vscode中添加安装eslint和prettier插件,然后在本项目设置页中选中Format ON Save,其会生成.vscode下的settings.json
```
{
  "editor.formatOnSave": true
}
```
可以直接在项目中添加此文件，从而支持eslint和prettier

## 声明
[react+typescript建议](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/function_components)
1. typescript+react中，函数式组件，返回React.ReactNode对象，箭头函数返回React.FC类型
2. 在interface作为公共API的定义，将type为react组件声明state和props。
3. 在书写注释时，始终使用/** comment */
4. 在引入第三方库是，需要将其声明类型引入，@types/\<package-name\>
