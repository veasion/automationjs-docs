# WebDriverBinding

driver 模块提供一系列函数，继承 SearchContextBinding 类，用于元素查找，驱动操作等。

该 api 函数可以直接方法访问，如 `click(target)` 方式调用，等价于 `driver.click(target)`

js 脚本绑定的 java 后台类 cn.veasion.auto.bind.WebDriverBinding



## open(url)
* `url` {string} 网址

打开页面并等待页面加载

```js
open("http://www.baidu.com");
```



## newTouchActions()

* {TouchActionsBinding}

鼠标动作

```js
let touch = newTouchActions();
let element = findOne('id=xxx');
touch.clickAndHold(element);
touch.moveByOffset(300, 0);
touch.release().perform();
```



## clickPoint(x, y)

* `x` {number} x坐标
* `y` {number} y坐标

根据坐标点击

```js
clickPoint(300, 400);
```



## executeScript(jsCode)

* `jsCode` {string} js 脚本
* {Object}

向浏览器驱动执行 js 代码

```js
executeScript("alert('hello');");
```



## executeScriptByParams(jsCode, args)

* `jsCode` {string} js代码
* `args` {array?} 参数
* {Object}

向浏览器驱动执行 js 代码（带参数）

```js
executeScriptByParams("arguments[0].click()", element);
```



## waitForPageLoaded(seconds)

* `seconds` {number?} 最大等待秒数

等待页面加载，通常在页面重新加载或刷新时使用。

```js
waitForPageLoaded(10);
```



## iframe(target, fun)

* `target` {string} 元素选择器
* `fun` {Function} 函数

当前浏览器操作切换至 target 元素  iframe 框架里

```js
iframe('id=iframe', function () {
	println(findOne('css=body').text());
});
```



## screenshot(path)

* `path` {string} 图片存放路径
* {boolean}

浏览器截图并保存到指定位置

```js
screenshot('C:\\Users\\user\\Desktop\\temp.png');
```



## getWindowHandle()

* {string}

获取当前窗口句柄



## openNewWindow()

打开并切换到新的窗口



## withNewWindow(fun)

* `fun` {Function} 方法

在新的窗口中执行函数

```js
// 新窗口执行代码
withNewWindow(function () {
    open('http://www.baidu.com');
});
```



## switchToNextWindow(windowHandle)

* `windowHandle` {string} 指定窗口句柄，为 null 则切换为下一个窗口

切换窗口

```js
// 获取当前窗口句柄
let currentHandle = getWindowHandle();
// 切换下一个窗口
switchToNextWindow();
// 切换到指定窗口
switchToNextWindow(currentHandle);
```



## runNewScript(path)

* `path` {string} 路径

在一个新的环境运行脚本

```js
// 相对路径
runNewScript(env.getSourcePath('/demo/demo.js'));
// 绝对路径
runNewScript('D:\Veasion\projects\\automation_testing\src\main\resources\demo\demo.js');
// 运行文件夹下所有脚本（递归运行）
runNewScript(env.getSourcePath('/demo'));
```



## runScriptWithNewDriver(env, path, async)

* {EnvironmentBinding}

* `env` {Object} 初始env环境变量
* `path` {string} 运行指定脚本路径
* `env` {boolean} 是否异步，true 异步时返回 null可以通过 env.putSystemVar 来传递数据

在新的浏览器驱动中执行脚本

```js
// 同步执行（返回env对象）
let newEnvResult = runScriptWithNewDriver({name: 'veasion'}, env.getPath('/script/baidu.js'), false);
// veasion
println(newEnvResult.name);

// 异步执行（无返回值）
runScriptWithNewDriver({
    "DRIVER_OPTIONS": {
        "arguments": [
            "no-sandbox",
            "--disable-popup-blocking",
            "--disable-blink-features=AutomationControlled",
            "--ignore-certificate-errors"
        ],
        "experimentalOptions": {
            "excludeSwitches": [
                "enable-automation"
            ]
        },
        // "proxy": {
        //     "proxyType": "MANUAL",
        //     "httpProxy": "127.0.0.1:8080"
        // },
        "capability": {}
    }
}, env.getPath("/script/crawler.js"), false);
```



## toChromeDriver()

* {ChromeDriverBinding}

chrome driver 专用对象

```js
let chrome = toChromeDriver();
// cdp
chrome.executeCdpCommand('Network.setUserAgentOverride', { userAgent: 'xxx' });
```



## request(url, method, content, headers)

* `url` {string} 请求url/uri
* `method` {string?} 请求方式 POST/GET 默认GET
* `content` {Object?} 请求body内容
* `headers` {Object?} 请求头
* {Object}
    * `status`{number} 请求状态，正常 200
    * `success` {boolean} 请求是否成功
    * `data` {string} 返回数据，response
    * `headers` {Object} 返回 headers
    * `targetHost` {string} 目标服务器ip地址

http 请求，请求 XHR 接口

```js
// GET请求
let getResp = request('http://www.baidu.com', 'GET');
if (getResp.success) {
	log.info('请求成功：' + getResp.data);
} else {
	log.error("请求失败，status: " + getResp.status);
}

// POST请求
let postResp = request('/api/ouser-web/mobileLogin/login.do', 'POST', { username: 'superadmin', password: '123456'}, { 'Content-Type': 'application/json;charset=UTF-8' });
if (postResp.success) {
	log.info('请求成功：' + JSON.parse(postResp.data));
} else {
	log.error("请求失败，status: " + postResp.status);
}
```
