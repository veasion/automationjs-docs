# 模块及函数

基于 JS 自动化测试框架扩展的业务模块及函数，方便直接调用封装函数解决问题。

如登录 `auto.randMobile()` 等。

- 业务基础函数在 include 目录下（包含auto / jira 等对象定义）
- 业务模块在 common 目录下（包含http/代理等模块）
- 业务数据依赖在 dependency 目录下（可以直接依赖基础数据）

## 基础函数

### auto

auto 对象提供常用的自动化函数，具体查看  include/auto.js

```js
// 加载 http 模块
auto.loadCommon('http');

// 依赖demo数据
auto.dependency('demo', {name: 'xxx'});

// table 滚动到最右边
auto.scroll(findOne('css=.el-table__body-wrapper'), null, 0);
```

### jira

jira 对象提供 JIRA 操作，具体函数见  include/jira.js

```js
// 登录 jira
jira.login();

// 提bug
jira.createIssue('测试', '程序有bug');
```

## 业务模块

调用模块需要先引用模块，如 `auto.loadCommon('http');` 建议放代码最前面。

### http

http 模块，主要操作HTTP请求，如GET/POST请求，具体函数见 common/http.js

```js
auto.loadCommon('http');

http.get('http://www.baidu.com');

http.post('/api/ouser-web/mobileLogin/login.do', { username: 'superadmin', password: '123456'});

let response = http.request('/oms-web/so/list.do', 'POST');
println('response: ' + response.data);
let ut = http.getCookie('ut');
println('ut: ' + ut);
```

### proxy

proxy 模块，主要用于 js 对象代理，具体函数见 common/proxy.js

```js
auto.loadCommon('proxy');

let p = new ProxyAdapter({}, function (obj, name, args, apply) {
	println(name + '方法被代理了 --before');
	let result = apply();
	println(name + '方法被代理了 --after');
	return result;
});

p.hello = function() {
	println('hello~');
}

p.hello();
// hello方法被代理了 --before
// hello~
// hello方法被代理了 --after
```
