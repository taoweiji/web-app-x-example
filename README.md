# web-app-x-example
wax 小程序示例

[示例APP 下载](https://github.com/taoweiji/web-app-x-example/releases/download/0.0.1/example-release.apk)


![image](https://user-images.githubusercontent.com/3044176/120807122-2f966700-c57a-11eb-9bd0-62a46cc1a181.png)


- 小程序示例代码
- 设计理念
- 和微信小程序区别



## Wax 对比微信小程序

|                     | 微信小程序                                                   | Wax                                                          |
| ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 运行环境            | 在 Android 上，逻辑层的 javascript 代码运行在 [V8](https://developers.google.com/v8/) 中，视图层是由自研 XWeb 引擎基于 Mobile Chrome 内核来渲染的，称为双线程模式 | 在 Android 上，逻辑层的 javascript 代码和视图渲染都是在运行在 WebView，拥有完整的 WebView 能力，属于单线程模式 |
| 多线程 Worker       | 基于 V8 引擎，一些异步处理的任务，可以放置于 Worker 中运行，待运行结束后，再把结果返回到小程序主线程。Worker 运行于一个单独的全局上下文与线程中，不能直接调用主线程的方法。 | 基于 QuickJS 封装的 [quickjs-android](https://github.com/taoweiji/quickjs-android) 框架，这个框架也是我开源的，工作模式和使用方式和微信小程序一样。 |
| JavaScript 支持情况 | 不支持使用 `eval` 执行 JS 代码，不支持动态代码；不支持使用 `new Function` 创建函数； | 无限制，和WebView支持无差别，拥有完整的能力。                |
| 全局配置/页面配置   | 使用json描述，决定页面文件的路径、窗口表现、设置网络超时时间、设置多 tab 等。 | 使用json描述，为了降低开发者的理解成本，采用了和微信小程序完全相同的描述规则。 |
| 样式语言            | WXSS，具有 CSS 大部分特性，同时为了更适合开发微信小程序，WXSS 对 CSS 进行了扩充以及修改，增加了尺寸单位和样式导入。 | CSS，荣有CSS完整的特性，同时为了适合小程序开发，对CSS进行了扩充，和微信小程序一样增加了样式导入。 |
| 标签语言            | WXML（WeiXin Markup Language）是框架设计的一套标签语言，结合[基础组件](https://developers.weixin.qq.com/miniprogram/dev/component/)、[事件系统](https://developers.weixin.qq.com/miniprogram/dev/framework/view/wxml/event.html)，可以构建出页面的结构。 | HTML，采用标准的HTML语言，同时为了适合小程序开发，也开发了一套移动开发常用的UI基础组件，可以构建出好看的页面。 |
| API 能力            | 小程序开发框架提供丰富的微信原生 API，可以方便的调起微信提供的能力，如获取用户信息，本地存储，支付功能等。 | Wax 开发框架提供了丰富的原生API，使用方式和微信小程序基本一样，可以方便调起原生提供的各种能力，比如网络请求、本地存储等。 |
|                     |                                                              |                                                              |
|                     |                                                              |                                                              |



## 你的第一个 Wax 小程序

为了降低学习成本，Wax小程序参考了微信小程序的架构，所以Wax小程序和开发思想和微信小程序极为相似。

### 目录结构

```
├── app.css
├── app.js
├── app.json
├── images
│   ├── ic_setting.png
└── pages
    ├── index
    │   ├── index.css
    │   ├── index.html
    │   ├── index.js
    │   └── index.json
    ├── logs
    │   ├── logs.css
    │   ├── logs.html
    │   ├── logs.js
    │   └── logs.json
```

### JSON 配置

JSON 是一种数据格式，并不是编程语言，在小程序中，JSON扮演的静态配置的角色。

我们可以看到在项目的根目录有一个 `app.json` 和 `project.config.json`，此外在 `pages/logs` 目录下还有一个 `logs.json`，我们依次来说明一下它们的用途。

#### 小程序配置 app.json

`app.json` 是当前小程序的全局配置，包括了小程序的所有页面路径、界面表现、网络超时时间、底部 tab 等。 示例项目里边的 `app.json` 配置内容如下：

```json
{
  "pages":[
    "pages/index/index",
    "pages/logs/logs"
  ],
  "window":{
    "backgroundTextStyle":"light",
    "navigationBarBackgroundColor": "#fff",
    "navigationBarTitleText": "Weixin",
    "navigationBarTextStyle":"black"
  }
}
```

我们简单说一下这个配置各个项的含义:

1. `pages`字段 —— 用于描述当前小程序所有页面路径，这是为了让微信客户端知道当前你的小程序页面定义在哪个目录。
2. `window`字段 —— 定义小程序所有页面的顶部背景颜色，文字颜色定义等。

其他配置项细节可以参考文档 [小程序的配置 app.json](https://developers.weixin.qq.com/miniprogram/dev/framework/config.html) 。

#### 页面配置 page.json

这里的 `page.json` 其实用来表示 pages/logs 目录下的 `logs.json` 这类和小程序页面相关的配置。

如果你整个小程序的风格是蓝色调，那么你可以在 `app.json` 里边声明顶部颜色是蓝色即可。实际情况可能不是这样，可能你小程序里边的每个页面都有不一样的色调来区分不同功能模块，因此我们提供了 `page.json`，让开发者可以独立定义每个页面的一些属性，例如刚刚说的顶部颜色、是否允许下拉刷新等等。

其他配置项细节可以参考文档 [页面配置](https://developers.weixin.qq.com/miniprogram/dev/framework/config.html#页面配置) 。

### HTML 模板

从事过网页编程的人知道，网页编程采用的是 HTML + CSS + JS 这样的组合，其中 `HTML` 是用来描述当前这个页面的结构，`CSS` 用来描述页面的样子，`JS` 通常是用来处理这个页面和用户的交互。

同样道理，在小程序中也有同样的角色。打开 `pages/index/index.html`，你会看到以下的内容:

```html
<div class="container">
  <div class="userinfo">
    <button wx:if="{{!hasUserInfo && canIUse}}"> 获取头像昵称 </button>
    <block wx:else>
      <image src="{{userInfo.avatarUrl}}" background-size="cover"></image>
      <text class="userinfo-nickname">{{userInfo.nickName}}</text>
    </block>
  </div>
  <div class="usermotto">
    <text class="user-motto">{{motto}}</text>
  </div>
</div>
```

这里HTML是使用W3C标准，不同的是，不需要编写header、body等信息，仅需要编写body里面的内容。

### CSS 样式

这里CSS是使用W3C标准，和普通的web开发没有任何差异。

### JS 逻辑交互

一个服务仅仅只有界面展示是不够的，还需要和用户做交互：响应用户的点击、获取用户的位置等等。在小程序里边，我们就通过编写 `JS` 脚本文件来处理用户的操作。

```
Page({
  clickMe: function() {
    this.setData({ msg: "Hello World" })
  }
})
```

### 运行GIF



## 总结

开发过小程序的开发者应该发现，这个示例和[微信小程序的示例](https://developers.weixin.qq.com/miniprogram/dev/framework/quickstart/code.html)，没有太大的区别，不同的是小程序的WXML改成了HTML，WXSS改成了CSS，微信小程序是自定义了一套DSL语言，虽然和W3C很接近，但依旧有差异，而Wax则基本完全遵循W3C标准，大大降低了开发者的学习成本。







