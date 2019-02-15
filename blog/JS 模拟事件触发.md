# JS 模拟事件触发

### 介绍
在通常情况下，事件的触发总是由用户完成的，如 click、keydown，blur等。
但是在特殊的环境下，我们需要自己通过 JS 模拟事件的触发。
如果是 click 事件，那么很简单只需要使用 element.click() 就可以触发点击事件。
但是其他的呢？我们应该如何触发这些事件？

### 模拟事件
```
var input = document.querySelector('input');
var event = new Event('blur');
input.dispatchEvent(event);
```
`var event = new Event('blur')` -> 创建一个事件，类别是 blur，赋值给 event
`input.dispatchEvent(event)` -> 在 input 元素上触发 event 事件
如果对应的事件处理函数需要其他值，可以在 event 上添加。

```
var input = document.querySelector('input');
var event = new Event('keydown');
event.keyCode = 13;
input.dispatchEvent(event);
```
但是这种方式模拟触发的事件，是否和真正触发的事件一样呢？
让我们来测试一下：

```
// 添加事件监听，打印 e
var input = document.querySelector('input');
input.addEventListener('keydown', e => console.log(e));

// 1.真正触发一下...

// 2.模拟触发一下
var event = new Event('keydown');
input.dispatchEvent(event);
```
结果(自己试一下吧)...
你会看到还是有一些差距的，我们模拟触发的事件相比真正触发的少了很多属性。
咦，等等...
我们模拟触发的事件打印出来是 `Event...` 而真正触发的事件打印出来是 `KeyboardEvent...`。
我们试试用 KeyboardEvent 来触发事件吧。

```
var input = document.querySelector('input');
var event = new KeyboardEvent('keydown');
input.dispatchEvent(event);
```
嗯，这回打印出来和真正触发的差不多了，只需要改一改几个属性就和真正触发差不多了。
同理还有 `InputEvent`、`MouseEvent`、`FocusEvent` 等。
用这种方式对于触发这些事件的监听函数会更加准确一些。
[Event 介绍 - MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/Event)

**对于现代浏览器这种方法能够解决大多数问题，但是对于老版本浏览器可能就不乐观了。**

在老版本浏览器下要使用另一种方式触发。

```
var input = document.querySelector('input');
var event = document.createEvent('HTMLEvents');
event.initEvent('mousedown', true, true);
input.dispatchEvent(event);
```
这种方式 MDN 上已经不推荐使用了，不做介绍，参考下 MDN 吧。
[Document.createEvent 介绍 - MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/Event)
[Event.initEvent 介绍 - MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/initEvent)

关于键盘模拟触发事件，网上有一位大佬写了一个公共方法挺好用的：

```
function fireKeyEvent(el, evtType, keyCode) {
    var doc = el.ownerDocument,
        win = doc.defaultView || doc.parentWindow,
        evtObj;
    if (doc.createEvent) {
        if (win.KeyEvent) {
            evtObj = doc.createEvent('KeyEvents');
            evtObj.initKeyEvent(evtType, true, true, win, false, false, false, false, keyCode, 0);
        }
        else {
            evtObj = doc.createEvent('UIEvents');
            Object.defineProperty(evtObj, 'keyCode', {
                get: function () { return this.keyCodeVal; }
            });
            Object.defineProperty(evtObj, 'which', {
                get: function () { return this.keyCodeVal; }
            });
            evtObj.initUIEvent(evtType, true, true, win, 1);
            evtObj.keyCodeVal = keyCode;
            if (evtObj.keyCode !== keyCode) {
                console.log("keyCode " + evtObj.keyCode + " 和 (" + evtObj.which + ") 不匹配");
            }
        }
        el.dispatchEvent(evtObj);
    }
    else if (doc.createEventObject) {
        evtObj = doc.createEventObject();
        evtObj.keyCode = keyCode;
        el.fireEvent('on' + evtType, evtObj);
    }
}
```
使用(模拟回车事件) `fireKeyEvent(elem, 'keydown', 13);`

大家可以参考一下原文章 [JavaScript 模拟键盘事件和鼠标事件](https://blog.csdn.net/lovelyelfpop/article/details/52471878)