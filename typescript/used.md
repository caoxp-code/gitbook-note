### 使用中遇到的问题
#### 声明一个对象
```
声明：
type BufferDirector<T> = {[key: string]: T}
使用：
private _arrayBuffer!: BufferDirector<Buffer>
this._arrayBuffer[id] = buffer
```
其中，T为value值，及传入的类型。key关键字设置字符串索引签名