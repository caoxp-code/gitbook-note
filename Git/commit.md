## 提交规范
规范提交信息，有如下好处：
- 能够清晰的展示本次提交的更改
- 方便后期查找
- 自动生成修改日志
- 基于提交类型，触发构建和部署流程

### 规范选择
Conventional Commits(约定式提交规范)，是目前使用最广泛的提交信息规范，其主要受[*anglejs规范*](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#-git-commit-guidelines)的启发，以下是一个规范信息的结构:
```
<type>[optional scope]: <subject>
// 空一行
[optional body]
// 空一行
[optional footer]
```
#### 规范说明
type提交的类型，为以下类型中的一个
```
  feat：增加一个新功能
  fix：修复bug
  docs：只修改了文档
  style：做了不影响代码含义的修改，空格、格式化、缺少分号等等
  refactor：代码重构，既不是修复bug，也不是新功能的修改
  perf：改进性能的代码
  test：增加测试或更新已有的测试
  chore：构建或辅助工具或依赖库的更新
  revert: 返回先前的提交
```

scope: 可选，标识影响的范围、功能、模块

subject: 必填，简单说明，不超过50个字

body: 选填，详细描述

footer: 选填，用于关联issus，或BREAK CHANGE(一个破坏性API变更)。

footer只会在以下情况下，添加
1. 不兼容变动
2. 关闭issue

### 工具
可以使用工具来对提交信息进行生成和校验，可以使用[commitizen](https://www.npmjs.com/package/commitizen)。
此工具为nodejs版本，需要先安装node才能使用。
```
# 安装全局commitizen
npm i -g commitizen
#本地安装适配器
npm i cz-conventional-changelog --save-dev
#添加适配器配置文件 .czrc
{
  "path": "cz-conventional-changelog"
}
```
通过以上几部后，使用git cz或cz替换git commit则会打开提交弹窗，进行选择