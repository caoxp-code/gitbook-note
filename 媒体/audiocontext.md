## AudioContext
一般我们在网页中，使用audio标签来进行音频的处理。其中一些个性化操作，比如处理音频文件，添加音效等，比较复杂。

AudioContext为 web API，通过此api可以灵活的对音频进行处理，并能生成一些复杂的音频效果。

在我们拿到音频文件，到输出到音频设备之间，可以创建不同的AudioNode(音频节点),每一种音频节点可以处理不同的音频数据，比如音频可视化(AnalyserNode)等

所有的音频节点都集成子AudioNode

具体api可以查看[此处](https://developer.mozilla.org/zh-CN/docs/Web/API/AudioContext/AudioContext)

## 常用api说明
### createBuffer(Number numOfChannels, Number length, Number sampleRate)
创建音频数据，返回AudioBuffer。
> numOfChannels 此buffer中包含的声频通道数量的整数， 标注声道至少有32个
> length 样本帧数
> sampleRate 采样率，即一秒中关键帧的个数
```
var audioCtx = new AudioContext();
var buffer = audioCtx.createBuffer(2, 22050, 44100);
此创建0.5s中音频文件 22050 / 44100
```

## 常用属性说明
### context.state
一个音频有3个状态：closed（关闭），running（运行中），suspended（暂停）

## 步骤
我们可以从一个或多个音频源，经过一个或多个音频节点，最终输出到一个终端设备(或者不输出),一般的创建简单的步骤，如下：
1. 创建AudioContext实例
2. 创建音频源，即AudioSource
3. 构建EffectNode，实现音效，效果
4. 选择音频输出设备
5. 链接音频源到效果，效果到音频输出设备
   ```
   ```

