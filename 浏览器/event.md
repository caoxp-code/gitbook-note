## 事件
### 捕获事件、冒泡事件
html文档为层级嵌套结构，页面元素处理事件时，可以有2中处理方式
1. 从最外层元素先捕获事件，再一层一层往下传递到子元素，此为捕获事件顺序
2. 从最里层元素触发事件，然后再一层一层往上传递到父元素，刺猬冒泡事件顺序

![事件](./../statics/事件顺序.svg)

根据浏览器历史，最早声明事件方式，都是捕获方式，比如
```
element.onclick = function(){
    alert("click event!"); 
};

// 移除事件处理操作
element.onclick = null;
```

后来W3C标准重新定义了事件声明方式，如下：
```
// options.capture与下边useCapture一致
// options.once为此事件是否触发一次
// options.passive 为true时，表示事件永远不会调用preventDefault，如果事件中
// 声明此方法，浏览器会告警
target.addEventListener(type, listener, options)
// useCapture, 为true时，为捕获方式，为false，为冒泡方式
target.addEventListener(type, listener, useCapture);
```

为了防止声明事件在多个元素中多次触发，可以在事件中使用stopPropagation()来阻止冒泡和捕获