# typescript
## 配置开发环境
### vscode
1. 可以在项目中直接使用ts-node来运行当前某个ts文件，此为node环境，需要本地安装nodejs环境。
>> yarn add -D ts-node typescript
>> yarn ts-node index.ts
2. 也可以直接在根目录里配置tsconfig.json文件，使用此命令初始化此文件
>> yarn tsc --init
3. 引入tslint，和eslint用法差不多，此为配置ts的代码风格检查
>> yarn add -D tslint
4. 引入husky，声明hook，规范git提交之前的操作
```
"husky": {
 "hooks": {
   "pre-commit": "lint-staged"
 }
},
```
lint-staged可以是package中的配置节点，也可以是一系列yarn命令

