# web-app-x-example
wax 小程序示例

示例APP 下载 https://github.com/taoweiji/web-app-x-example/releases/download/0.0.1/example-release.apk

<img src="https://user-images.githubusercontent.com/3044176/120747848-5af66300-c534-11eb-926a-0a1fb2cfdffa.png" alt="image" style="zoom:33%;" />


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











