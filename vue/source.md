# 源码解析
## src文件目录
- src
  - compiler 编译相关
  - core 核心代码
  - platforms 平台相关，有web和weex2个入口
  - server 服务端渲染
  - sfc 解析.vue文件到JavaScript对象
  - shared 共享代码，浏览器端和服务器端vue使用
## Object.defineProperty(obj, prop, descriptor)
会创建新的对象属性，或修改已存在的属性，并返回此对象
```
const obj = {};
Object.defineProperty(obj, 'prop', {
    value: 42,
    writable: true
});
console.log(obj); // {prop: 42}
obj.prop = 43; // {prop: 43}
```
