# ChromeDriverBinding

chromeDriver 模块是 driver 对 chrome 的扩展，继承 WebDriverBinding 类，可以执行 chrome driver 的 cdp 协议命令，通过 `toChromeDriver()` 获取如 `toChromeDriver().executeCdpCommand('xxx', {})` 

js 脚本绑定的 java 后台类 cn.veasion.auto.bind.ChromeDriverBinding



## executeCdpCommand(commandName, parameters)

* `commandName` {string} cdp命令
* `parameters` {Object} cdp命令参数
* {Object}

执行cdp命令

```js
let chrome = toChromeDriver();

// modify user agent
chrome.executeCdpCommand("Network.setUserAgentOverride", { userAgent: 'xxx' });

// script
let js = file.readText(env.getPath('/files/set_crawler.js'));
chrome.executeCdpCommand('Page.addScriptToEvaluateOnNewDocument', {source: js});
```



## setUserAgent(userAgent)

设置UA

```js
let chrome = toChromeDriver();
chrome.setUserAgent('xxx');
```



## activateDevTools()

激活 chrome dev tools

```js
toChromeDriver().activateDevTools();
```



## addRequestHandler(filter, fun)

* `filter` {Function} 过滤函数
* `fun` {Function} 处理函数

浏览器http请求处理

```js
// 需要激活 dev tools
toChromeDriver().activateDevTools();

// 请求拦截处理
toChromeDriver().addRequestHandler(function(request) {
	// 拦截指定请求
	return request.getUri().indexOf('www.baidu.com') != -1;
}, function(request) {
	// 修改请求响应
	let response = {};
	response.status = 200;
	response.content = '请求被修改了！';
	response.headers = { 'Content-Type': 'text/html;charset=utf-8' };
	return response;
});

// 测试
open('http://www.baidu.com');
```



## getAllResponse()

根据日志获取全部请求response


