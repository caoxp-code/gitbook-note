# 微信开发中有关问题
## 微信网页开发问题
### 1.在IOS手机中返回上一页，页面不进行刷新

在[微信开发文档](https://developers.weixin.qq.com/doc/offiaccount/OA_Web_Apps/iOS_WKWebview.html)中，
由于iphone微信中使用Safari。

Safari或微信WKWebview中，页面A跳转到页面B再返回页面A后不会重新执行Script和Ajax(也不会触发页面reload),但会触发页面的pageshow pageHide等事件。

此使用BF Cache进行缓存数据和页面。

会话中某个页面显示/隐藏时，会触发pagehide和pageshow事件，事件都有一个persisted属性来指示当前页是否被BF cache缓存。因此可以使用如下方法
```
window.onpageshow = function(event) {
    if (event.persisted) {
        window.location.reload() 
    }
};
```
注意: *pageshow 不仅在显示被缓存的页面时触发，在第一次加载页面时也会触发。 因此需要检测事件的 persisted 属性，页面第一次加载时它的值是 false*
