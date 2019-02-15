# postMessage 实现跨域通信

## 介绍
postMessage 是 HTML5 提供的 API 之一，能够实现跨文档消息传输，功能简单易懂，但是如果你看文档时不够仔细，就会像我这样单独拿出来水了一篇文章。

### 使用方法
* 接收端 - 添加 message 事件监听即可。

```js
window.addEventListener('message', (e) => {
    console.log(e);
});
```

* 发送端

```js
otherWindow.postMessage(message, targetOrigin);
```

**message** - 要传递的消息，**targetOrigin** - 限定消息接收范围，不限制请使用 ‘*’。

**注意 otherWindow，otherWindow，otherWindow！**
**otherWindow 是接收端的 window 这点一定要注意！**
(曾经傻傻的用两个网址来回发消息试了半天都不行，后来仔细看文档才发现的...)

### 使用范围
网上很多例子都是在 iframe 嵌套的页面中使用的，这里就不介绍了。
在这里我们介绍一下在两个网页中如何使用这种通信方式。
首先给大家介绍一个熟悉的方法 `window.open`。
这是干啥的大家都知道，但是 `window.open('xxx')` 会返回打开窗口的 window。

```js
const otherWindow = window.open('xxx');
```

同时被打开的窗口会有一个 `opener` 的属性，这个属性指向打开这个窗口的 window。
这样我们的两个窗口都获取到了对方的 window。
虽然跨域条件下这两个 window 都无法读取使用，但拿来使用 postMessage 是没问题的。

### 结束
目前我所知道 postMessage 实现的两个页面间相互跨域通信的只有 window.open 和 opener 这一种。
哪位大佬知道其他的方法欢迎补充。