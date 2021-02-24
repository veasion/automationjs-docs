# WebDriverBinding

driver 模块提供一系列函数，继承 SearchContextBinding 类，用于元素查找，数据库操作等。

该 api 函数可以直接方法访问，如 `click(target)` 方式调用，等价于 `driver.click(target)`

js 脚本绑定的 java 后台类 cn.veasion.auto.bind.WebDriverBinding



## open(url)
* `url` {string} 网址

打开页面并等待页面加载

```js
open("http://www.baidu.com");
```

## pause(millis)
* `millis` {number} 毫秒

暂停多少毫秒，等价于 sleep

```js
pause(500);
```

## sleep(millis)
* `millis` {number} 毫秒

暂停多少毫秒，等价于 pause

```js
sleep(500);
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

## input(title)
* `title` {string} 输入提示
* {string}

控制台输入

```js
let name = input('请输入姓名: ');
```

## info
* {string}

获取当前脚本环境信息。

## assertResult(flag, message)
* `flag` {boolean} 是否通过
* `message` {string} 断言信息

断言，当 flag 为 true 时表示断言通过，false 为断言失败抛出异常 message

```js
assertResult(true, '断言测试通过');
// 断言元素存在
assertResult(findOne('id=xxx') != null, '断言元素存在');
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

## formatDate(date, pattern)
* `date` {Object} 时间 (时间对象/毫秒数)
* `pattern` {string} 格式化 format
* {string}

格式化时间

```js
// 时间格式化
formatDate(new Date(), 'yyyy-MM-dd HH:mm:ss');
// 毫秒数格式化
formatDate(1607430878907, 'yyyy-MM-dd HH:mm:ss');
```
## randCode(length)
* `length` {number} 长度
* {string}

随机字符串（数字）

```js
randCode(8);
```

## println(message, args)
* `message` {Object} 消息
* `args` {array?} 参数

打印，输出到控制台

## calculate(str, n)
* `str` {string} 运算表达式
* `n` {number} 保留几位小数
* {string} 返回计算结果

计算器

```js
// 计算，保留两位小数
let result = calculate('√(3*3)+4.99+(5.99+6.99)*1.06^2', 2);
println('计算结果：' + result);
```
## writeText(path, context, append, charsetName)
* `path` {string} 路径
* `context` {string} 文本内容
* `append` {boolean} 是否追加
* `charsetName` {string?} 编码，默认UTF-8
* {string}

写文本文件

```js
// 写文本文件
writeText('C:\\Users\\user\\Desktop\\test.txt', 'hello', false);
// 追加文本文件
writeText('C:\\Users\\user\\Desktop\\test.txt', 'veasion', true);
```
## readText(pathOrUrl, charsetName)
* `pathOrUrl` {string} 路径或网址
* `charsetName` {string?} 编码，默认UTF-8
* {string}

读取文本，可以读本地文本文件和网络文本

```js
// 读取网络文本
readText('http://www.baidu.com', 'utf-8');
// 读取本地文本文件
readText('C:\\Users\\user\\Desktop\\test.txt', 'utf-8');
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
## createJdbcConnection(jdbcUrl, user, password)
* `jdbcUrl` {string} 数据库jdbc连接url
* `user` {string} 数据库用户名
* `password` {string} 数据库密码
* {JdbcConnectionBinding}

数据库连接，操作数据库

```js
// 创建连接
let db = createJdbcConnection('jdbc:mysql://127.0.0.1:3306/user?useUnicode=true&characterEncoding=utf-8', 'root', '123456');
// 查询列表
db.query('select id, user_name, sex from t_user where status = ? limit ?', [1, 10]);
// 查询单个
db.queryOnly('select database()', null);
// 新增
db.insert('insert into t_user(user_name, sex) values (?, ?)', ['veasion', '男']);
// 修改
db.update('update t_user set user_name = ? where id = ?', ['xxx', 1]);
// 关闭连接
db.close();
```
## createMysqlConnection(ip, port, database, user, password)
* `ip` {string} 数据库ip地址
* `port` {number} 数据库端口
* `database` {string} 数据库
* `user` {string} 数据库用户名
* `password` {string} 数据库密码
* {JdbcConnectionBinding}

mysql 数据库连接，操作 mysql 数据库

```js
// mysql 数据库连接
createMysqlConnection('127.0.0.1', 3306, 'user', 'root', '123456');
// 等价于
createJdbcConnection('jdbc:mysql://127.0.0.1:3306/user?useUnicode=true&characterEncoding=utf-8', 'root', '123456');
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
