# CSS 3D
在实现比如web端，[贝壳全景看房](https://realsee.com/website/public/demo/fwmm/ryQkazl8xKdesBhKhVTkqqxTVLX6Rn9Km.html)的需求时，可以使用css3中关于3d的效果来实现。
## 什么是3D坐标
![3D坐标图](../statics/3d_axes.png)
其中z轴就是我们双眼看过去的方向，x轴为水平方向，y轴为垂直方向。
### css3D效果设置
如果我们需要用css来实现3D效果，首先要明白以下内容，也可直接查看[详情](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform-function)
#### perspective
指定了观察者与z=0平面的距离，使其具有三维的透视效果。在设置完perspective值后，如果translateZ>0，元素显示越大，translateZ<0,元素显示越小
#### transform-style
此元素在IE中不支持。
设置元素的子元素是位于3D空间中还是平面中
1. flat平面
2. preserve-3d
由于此元素不会集成，因此必须为元素的所有非叶子子元素设置
#### rotate3d(x,y,z,a)
定义一个3d旋转功能，改旋转使元素能够绕固定轴移动而不变形。移动量由指定角度定义，如果为正值，按顺时针旋转，如果为负值，按逆时针旋转。

旋转轴由[x,y,z]定义，且原点由 transform-origin 定义

**三维旋转的组成通常是不可交换的，即旋转应用的顺序很重要。**
