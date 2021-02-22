# WebElementBinding

element 对象，继承 SearchContextBinding 类，提供一系列元素操作方法。

该 api 函数同元素对象访问，不能直接访问，如 `let element = findOne(target)` 方式获取元素对象，然后调用函数方法 `element.click()`，等价于 `findOne(target).click()`

js 脚本绑定的 java 后台类 cn.veasion.auto.bind.WebElementBinding


## click()
* {WebElementBinding}

元素点击

```js
let element = findOne('id=xxx');
element.click();
```

## tryClick()
* {WebElementBinding}

点击这个元素区域 ( try 点击，如果失败不会抛出异常 )<br>
该点击函数跟 click 区别是：<br>
click 只能点击可见并且可以点击的元素<br>
tryClick 能点击所有元素，包含不可见元素

```js
element.tryClick();
```

## attr(attr)
* `attr` {string} 属性名称
* {Object}

获取元素属性

```js
element.attr('name');
```

## type(key)
* `key` {Object} 字符串/按键
* {WebElementBinding}

向元素发送文字/模拟按键（同 sendKeys 函数）

```js
element.type('你好');
```
## sendKeys(key)
* `key` {Object} 字符串/按键
* {WebElementBinding}

向元素发送文字/模拟按键（同 type 函数）

```js
element.sendKeys('你好');
```
## text()
* {string}

获取元素文本

## scrollToCenter()
* {WebElementBinding}

滚动到目标元素

## innerHtml()
* {string}

获取元素 inner  html 代码

## outerHtml()
* {string}

获取元素 outer  html 代码

## value()
* {string}

获取值。如 input 元素的 value 属性

```js
findOne("css=input").value();
```

## xpath()
* {string}

获取元素 xpath

## saveAsImage(path)
* `path` {string} 路径

保存为图片

## clear()
* {WebElementBinding}

清空值。如清空 input 元素的 value 属性

```js
findOne("css=input").clear();
// 等价于
findOne("css=input").setValue('');
```

## setValue(text)
* `text` {string} 字符串
* {WebElementBinding}

设置值。如设置 input 元素的 value 属性

```js
findOne("css=input").setValue('hello~');
```

## selectByLabel(value)
* `value` {Object} 选中值
* {WebElementBinding}

通过 label 选择下拉框

```js
// <select>
//   <option value="1">小明</option>
//   <option value="2">小红</option>
//   <option value="3">小李</option>
// </select>

// 选择小红
findOne("css=select").selectByLabel('小红');
```

## selectByValue(value)
* `value` {Object} 选中值
* {WebElementBinding}

通过 value 选择下拉框

```js
// <select>
//   <option value="1">小明</option>
//   <option value="2">小红</option>
//   <option value="3">小李</option>
// </select>

// 选择小红
findOne("css=select").selectByValue('2');
```
## select(label, value)
* `label` {string} 选择模式，支持:  index, label, value
* `value` {Object} 选中值
* {WebElementBinding}

选择下拉框

```js
// <select>
//   <option value="1">小明</option>
//   <option value="2">小红</option>
//   <option value="3">小李</option>
// </select>

// 选择小红
findOne("css=select").select('index', 1); // 根据下标
findOne("css=select").select('label', '小红'); // 根据 label
findOne("css=select").select('value', '2'); // 根据 value
```
## parent()
* {WebElementBinding}

获取父元素

## parentByTag(tagName)
* `tagName` {string} 元素 tagName
* {WebElementBinding}

获取指定 tagName 的父元素（向上迭代找指定 tagName 的元素）

```js
element.parentByTag("html"); // 顶层 html
```

## childList()
* {WebElementBinding[]}

子元素集合

```js
let childs = element.childList();
for (let i in childs) {
	println(childs[i]);
}
```
## leftSibling()
* {WebElementBinding[]}

左边兄弟节点集合

```js
// <div>
// 	<span>小明</span>
// 	<span id="xiaohong">小红</span>
// 	<span>小李</span>
// </div>

let element = findOne("id=xiaohong");
element.leftSibling(); // [<span>小明</span>]
```
## rightSibling()
* {WebElementBinding[]}

右边兄弟节点集合

```js
// <div>
// 	<span>小明</span>
// 	<span id="xiaohong">小红</span>
// 	<span>小李</span>
// </div>

let element = findOne("id=xiaohong");
element.rightSibling(); // [<span>小李</span>]
```

## findText(tagName, text)
* `tagName` {string} 元素 tagName，默认 * 所有
* `text` {string} 文本
* {WebElementBinding}

查找元素包含某文字的节点

```js
// <div>
// 	<span>小明</span>
// 	<span>小红</span>
// 	<span>小李</span>
// </div>

let element = findOne("css=div");
element.findText("span", "小红"); // <span>小红</span>
element.findText("*", "小红"); // <span>小红</span>
element.findText(null, "小红"); // <span>小红</span>
```

## tagName()
* {string}

元素 tagName，如 div/span/input 等

## isDisplayed()
* {boolean}

元素是否可见

## touch()
* {TouchActionsBinding}

触摸操作，返回元素触摸对象

## show()
* {WebElementBinding}

页面上突出显示

