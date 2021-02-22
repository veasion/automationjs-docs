# 综述

JS自动化测试 automation_js 使用 [JavaScript](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript) 作为脚本语言，目前使用 [Java 1.8 Nashorn](http://openjdk.java.net/projects/nashorn/) 作为脚本引擎，支持ES5与部分ES6特性。

* 因为是基于JavaScript的，学习API之前建议先学习JavaScript的基本语法和内置对象。

* 建议通过 [IntelliJ IDEA](https://www.jetbrains.com/idea/)  开发，支持 js 代码提示

* 支持通过 jar 包方式直接运行

* 浏览器驱动建议使用 [chromedriver](http://npm.taobao.org/mirrors/chromedriver/)

  

本文档的章节大致上是以模块来分的，总体上可以分成内置基础函数跟业务扩展函数，包括 元素操作，浏览器窗口操作, http 请求，数据库操作等。

内置函数的部分又可以大致分为基于选择器和基于元素的操作。基于选择器的操作是传统 selenium的方式，通过选择来查找元素。

例如 selenium `findElement(By.id("veasion"))`, `findElement(By.name("veasion"))`等，在 js 脚本中则是 `findOne("id=veasion")`, `findOne("name=veasion")`。这种方式省略了 By 这个参数，而是通过字符串表示。

其他部分主要包括：
* WebDriverBinding: driver 驱动对象。元素操作、元素查找、窗口、iframe、数据库、http、按键、url等。

* WebElementBinding: element 元素对象。操作元素点击、输入、文本、属性、查找等。

* EnvironmentBinding: env 环境变量。读取和操作环境变量数据等。

* JdbcConnectionBinding: jdbc 数据库连接。操作数据库

* Image: 元素图片找色找图、ocr文字识别、验证码识别等。

* Auto: auto 模块及函数封装。

* Demo: demo 示例。

  

除此之外，还支持业务脚本扩展，如业务基础扩展 `auto.getIcon()` 见 include/auto.js， 模块扩展见 common 目录，依赖扩展见 dependency，脚本代码示例见 script/readme.js。如何运行启动程序相关请见 Q&A



## 自动化测试示例：

* 百度搜索 “中国”，打印出搜索结果

```js
open("https://www.baidu.com");
sendKeys('id=kw', '中国');
click("css=input[value='百度一下']");
waitForPageLoaded();
let list = findDisplayed('css=div#content_left > div');
for (let i in list) {
    println(list[i].text());
}
```

* 百度搜索 “中国”，进入百度百科结果

```js
// 百度搜索，调用封装函数
baiduSearch('中国');
// 获取搜索结果
let list = findDisplayed('css=div#content_left > div');
// 变量搜索结果
for (let i in list) {
    let element = list[i].findOne("css=h3 > a");
    // 判断结果是否为百度百科
    if (element && element.text().endsWith("百度百科")) {
        // 点击
		element.click();
        // 等待页面加载
        waitForPageLoaded(10);
        // 切换到新打开的窗口
        switchToNextWindow();
        break;
	}
}

function baiduSearch(str) {
    open("https://www.baidu.com");
    sendKeys('id=kw', str);
    click("css=input[value='百度一下']");
    waitForPageLoaded(5);
}
```



更多示例请见 Demo 示例



## 元素 target 选择器说明：

`id=`   根据 id 查找元素

`name=`   根据name查找元素

`xpath=`   根据xpath查找元素

`css=`   根据css查找元素

`tagName=`   根据tagName查找元素

`className=`   根据className查找元素

`linkText=`   根据linkText查找元素

示例：
```html
<div>
	<span id="wd">哈哈哈</span>
	<span name="text">嘿嘿</span>
	<ul class="test_ul">
		<li>1</li>
		<li>2</li>
	</ul>
	<a href="https://www.baidu.com">百度一下</a>
</div>
```
```js
// 根据id查询
println(findOne("id=wd").text()); // 输出：哈哈哈

// 根据name查询
println(findOne("name=text").text()); // 输出：嘿嘿

// 根据xpath查询
println(findOne("xpath=//div/span[1]").text()); // 输出：哈哈哈

// 根据css查询
println(findOne("css=div > span[name='text']").text()); // 输出：嘿嘿

// 根据tagName查询
println(find("tagName=span")); // 输出：[<span>哈哈哈</span>, <span>嘿嘿</span>]

// 根据className查询
println(find("className=test_ul")); // 输出：[<li>1</li>, <li>2</li>]

// 根据linkText查询
println(findOne("linkText=百度一下").text()); // 输出：百度一下
```