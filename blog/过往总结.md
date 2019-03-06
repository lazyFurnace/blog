## Node.js

### [glob](https://github.com/isaacs/node-glob#readme)

node 的 glob 模块允许你使用 \* 等符号，来写一个 glob 规则，像在 shell 里一样，获取匹配对应规则的文件。glob 工具是基于 JavaScript 的，它使用了 minimatch 库来进行匹配。

#### glob（pattern，[options]，cb）

- `pattern` `{String}` 要匹配的模式
- `options` `{Object}`
- `cb` `{Function}`
- `err` `{Error | null}`
- `matches` `{Array<String>}` 找到与模式匹配的文件名

执行异步全局搜索。

#### glob.sync（pattern，[options]）

- `pattern` `{String}` 要匹配的模式
- `options` `{Object}`
- `return` `{Array<String>}`找到与模式匹配的文件名

执行同步 glob 搜索。

#### 例如

读取文件夹该类型所有的文件

```js
glob.sync(pathVars.srcPath + "/pages/loginRegister/*/index.html");
// 结果
[
  "F:/liqi-webStudio/src/pages/loginRegister/forgetPassword/index.html",
  "F:/liqi-webStudio/src/pages/loginRegister/forgetPasswordEmail/index.html",
  "F:/liqi-webStudio/src/pages/loginRegister/login/index.html",
  "F:/liqi-webStudio/src/pages/loginRegister/register/index.html"
];
```

## Webpack

- 库类依赖使用 `webpack.DllPlugin` 整体提前打包
- `preload-webpack-plugin` 预加载插件

## React

- 受控表单读取数据可使用表单 `name` + `state` 控制

- 使用 `element` 作为起点，克隆并返回一个新的 React 元素。 所产生的元素将具有原始元素的 props ，新的 props 为浅层合并。 新的子元素将取代现有的子元素， `key` 和 `ref` 将被保留。

- ```js
  React.cloneElement(element, [props], [...children]);
  ```

## Javascript

- `requestIdleCallback` 和 `requestAnimationFrame`

- 新写法 `::` 是 `bind(this)`

- 调起全屏功能

- ```js
  toggleFullScreen() {
      const { isFullScreen } = this.state;
      const oFullScreenDiv = document.getElementById("dashBoardLayoutFullScreenBox");
      if (oFullScreenDiv){
          if (!isFullScreen) {
              if (oFullScreenDiv.requestFullscreen) {
                  oFullScreenDiv.requestFullscreen();
              } else if (oFullScreenDiv.mozRequestFullScreen) {
                  oFullScreenDiv.mozRequestFullScreen();
              } else if (oFullScreenDiv.webkitRequestFullScreen) {
                  oFullScreenDiv.webkitRequestFullScreen();
              } else if (oFullScreenDiv.msRequestFullScreen){
                  oFullScreenDiv.msRequestFullScreen();
              }
          } else {
              if (document.exitFullscreen) {
                  document.exitFullscreen();
              } else if (document.mozCancelFullScreen) {
                  document.mozCancelFullScreen();
              } else if (document.webkitCancelFullScreen) {
                  document.webkitCancelFullScreen();
              }
          }
      }
  }
  toggleFullScreenState() {
      //监听不同浏览器的全屏事件，并件执行相应的代码
      document.addEventListener("webkitfullscreenchange", () => {
          if (document.webkitIsFullScreen) {
              this.setState({ isFullScreen: true });
          } else {
              this.setState({ isFullScreen: false });
          }
      }, false);
      document.addEventListener("fullscreenchange", () => {
          if (document.fullscreen) {
              this.setState({ isFullScreen: true });
          } else {
              this.setState({ isFullScreen: false });
          }
      }, false);
      document.addEventListener("mozfullscreenchange", () => {
          if (document.mozFullScreen) {
              this.setState({ isFullScreen: true });
          } else {
              this.setState({ isFullScreen: false });
          }
      }, false);
      document.addEventListener("msfullscreenchange", () => {
          // ie
          if (document.msFullscreenElement) {
              this.setState({ isFullScreen: true });
          } else {
              this.setState({ isFullScreen: false });
          }
      }, false);
  }
  ```

* 字符串去除两边的空格用 `trim()`

* 使用 js 添加 css 属性时后面注意加上单位

* `introduce` 可用于判断原型链

* 一个循环数字可使用模赋值运算 `%` 来控制循环数字大小

* 获取当前页面的滚动条使用 `document.documentElement.scrollTop` , 而不是 `document.body.scrollTop` , `documentElement` 对应的是 html 标签 , 而 body 对应的是 body 标签。

* 网页屏幕相关属性

* ```js
  网页可见区域宽: document.body.clientWidth;
  网页可见区域高: document.body.clientHeight;
  网页可见区域宽: document.body.offsetWidth;
  网页可见区域高: document.body.offsetHeight;
  网页正文全文宽: document.body.scrollWidth;
  网页正文全文高: document.body.scrollHeight;
  网页被卷去的高: document.body.scrollTop;
  网页被卷去的左: document.body.scrollLeft;
  网页正文部分上: window.screenTop;
  网页正文部分左: window.screenLeft;
  屏幕分辨率的高: window.screen.height;
  屏幕分辨率的宽: window.screen.width;
  屏幕可用工作区高度: window.screen.availHeight;
  屏幕可用工作区宽度: window.screen.availWidth;
  ```

* 高度和坐标相关属性 clientHeight、offsetHeight、scrollHeight、offsetTop、scrollTop。

* 点击事件相关坐标

  ```js
  event.clientX 相对文档的水平座标
  event.clientY 相对文档的垂直座标
  event.offsetX 相对容器的水平坐标
  event.offsetY 相对容器的垂直坐标
  ```

* 无限滚动实现

  ```js
  document.body.onscroll = function() {
    var t = document.documentElement.scrollTop || document.body.scrollTop;
    var h =
      window.innerHeight ||
      document.documentElement.clientHeight ||
      document.body.clientHeight;
    if (t >= document.documentElement.scrollHeight - h) {
      // do something
    }
  };
  ```

* 定位鼠标相对于页面的绝对位置

  ```js
  if (document.body && document.body.scrollTop && document.body.scrollLeft) {
    top = document.body.scrollTop;
    left = document.body.scrollleft;
  }
  if (
    document.documentElement &&
    document.documentElement.scrollTop &&
    document.documentElement.scrollLeft
  ) {
    top = document.documentElement.scrollTop;
    left = document.documentElement.scrollLeft;
  }
  ```

- `jQuery` 的 `trigger` 方法可以触发许多浏览器事件

- 修改 `select` 标签的选中项可以使用 `selectIndex`

- 移动端事件 `touchstart`，`touchend`，`touchmove`，移动端获取位置 `e.touches[0].pageX/Y`

- 禁止鼠标拖动 `ondragstart="return false"`

- 获取图片 `base64` 码

  ```js
  function getBase64Image(img) {
    var canvas = document.createElement("canvas");
    canvas.width = img.width;
    canvas.height = img.height;
    var ctx = canvas.getContext("2d");
    ctx.drawImage(img, 0, 0, img.width, img.height);
    var dataURL = canvas.toDataURL("image/png");
    return dataURL;
  }
  ```

- 清除浏览器缓存 `chrome://appcache-internals/`

- 简单柯里化

  ```js
  Function.prototype.currying = function(text) {
    var that = this;
    return function(name) {
      that.apply(null, [text, name]);
    };
  };
  ```

## 算法

- 二分查找

## 工具

#### MODx

MODx 是一个开源的 PHP 应用框架，可以帮助使用者控制自己的网上内容。它是开发人员和高级用户理想的控制系统，任何人都可以使用 MODx 发布、更新、维护动态网站，或 html 静态页面的网站内容。

#### Typescript

TypeScript 是一种由微软开发的自由和开源的编程语言。它是 JavaScript 的一个超集，而且本质上向这个语言添加了可选的静态类型和基于类的面向对象编程。

#### Flow

Flow 是个 JavaScript 的静态类型检查工具，由 Facebook 出品的开源码项目，问世只有两三年，是个相当年轻的项目。简单来说，它是对比 TypeScript 语言的解决方式。

#### 网站

- [MDN - Web 开发者文档](https://developer.mozilla.org/zh-CN/)
- [维基百科](https://www.wikipedia.org/)
- [绘图软件](https://affinity.serif.com/zh-cn/designer/)
- [在线调试工具](https://jsfiddle.net/)
- [common.js 介绍](http://javascript.ruanyifeng.com/nodejs/module.html)
- [fis3 百度自动化管理工具](http://fis.baidu.com/fis3/index.html)
- [event 事件信息](http://www.cnblogs.com/coolicer/archive/2010/10/04/1842653.html)
- [元素宽高概念](http://www.cnblogs.com/zourong/p/4049012.html)

## Linux

连接远程 Linux `ssh 192.168...`

## CSS

- 计算属性 `height: calc( ~"100% - 40px")`

- 粘性布局 `position: sticky`

- 这三个属性搭配对付 table 的宽度问题有奇效

- ``` css
  width: 140px;
  min-width: 140px;
  word-break: break-all;
  ```

- `:last-of-type` 选择器

- `prefixfree.js` 增加 css 各种后缀

- `autoprefixer` css 兼容工具

- `-webkit-appearance: none` 修改 `checkbox` 默认样式

- 选择器 `+` `~` 都很好用

- `pointer-events: none` 禁用事件
