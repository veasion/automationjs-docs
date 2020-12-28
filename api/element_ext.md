
# SearchContextBinding

WebDriverBinding 跟 WebElementBinding 对象都继承该对象，可以直接访问该类所有函数。

该类所有方法均可以直接访问，或者通过元素对象访问（元素对象访问时，target 基于元素查找）

## findOne(target)
* `target` {string} 元素选择器
* {WebElementBinding}

查找一个元素

## find(target)
* `target` {string} 元素选择器
* {WebElementBinding[]}

查找多个元素

## findList(targets)
* `targets` {string[]} 元素选择器数组
* {WebElementBinding[]}

查找多个元素

## findDisplayed(target)
* `target` {string} 元素选择器
* {WebElementBinding[]}

查找多个可见元素

## findText(tagName, text, fuzzyMatches)
* `tagName` {string} 元素 tagName，默认 * 所有
* `text` {string} 文本
* `fuzzyMatches` {boolean} 是否模糊匹配
* {WebElementBinding}

查找元素包含某文字的节点

```js
// <div>
// 	<span>小明</span>
// 	<span>小红</span>
// 	<span>小李</span>
// </div>

// 精确匹配
findText("span", "小红", false); // <span>小红</span>
// 模糊匹配
findText("span", "红", true); // <span>小红</span>
```
## findTextAll(tagName, text, fuzzyMatches)
* `tagName` {string} 元素 tagName，默认 * 所有
* `text` {string} 文本
* `fuzzyMatches` {boolean} 是否模糊匹配
* {WebElementBinding[]}

查找元素包含某文字的节点

```js
// <div>
// 	<span>小明</span>
// 	<span>小红</span>
// 	<span>小李</span>
// </div>

// 精确匹配
findTextAll("span", "小红", false); // [<span>小红</span>]
// 模糊匹配
findTextAll("span", "小", true); // [<span>小明</span>, <span>小红</span>, <span>小李</span>]
```
## click(target)
* `target` {string} 元素选择器
* {SearchContextBinding}

点击元素

```js
click("id=xxx");
```
## tryClick(target)
* `target` {string} 元素选择器
* {SearchContextBinding}

点击这个元素区域 ( try 点击，如果失败不会抛出异常 )<br>
该点击函数跟 click 区别是：<br>
click 只能点击可见并且可以点击的元素<br>
tryClick 能点击所有元素，包含不可见元素

```js
tryClick("id=xxx");
```
## attr(target, attr)
* `target` {string} 元素选择器
* `attr` {string} 属性名称
* {Object}

获取元素属性

```js
attr('css=input', "value"); // 获取input标签的value属性
```
## text(target)
* `target` {string} 元素选择器
* {string}

获取元素文本

## type(target, key)
* `target` {string} 元素选择器
* `key` {Object} 字符串/按键
* {SearchContextBinding}

向元素发送文字/模拟按键（同 sendKeys 函数）

```js
type('css=input', '你好');
```
## sendKeys(target, key)
* `target` {string} 元素选择器
* `key` {Object} 字符串/按键
* {SearchContextBinding}

向元素发送文字/模拟按键（同 type 函数）

```js
sendKeys('css=input', '你好');
```
## mouseOver(target)
* `target` {string} 元素选择器
* {SearchContextBinding}

鼠标移动到目标元素

## scrollToCenter(target)
* `target` {string} 元素选择器
* {SearchContextBinding}

滚动到目标元素
## selectByLabel(target, value)
* `target` {string} 元素选择器
* `value` {Object} 选中值
* {SearchContextBinding}

通过 label 选择下拉框

```js
// <select>
//   <option value="1">小明</option>
//   <option value="2">小红</option>
//   <option value="3">小李</option>
// </select>

// 选择小红
selectByLabel('css=select', '小红');
```

## selectByValue(target, value)
* `target` {string} 元素选择器
* `value` {Object} 选中值
* {SearchContextBinding}

通过 value 选择下拉框

```js
// <select>
//   <option value="1">小明</option>
//   <option value="2">小红</option>
//   <option value="3">小李</option>
// </select>

// 选择小红
selectByValue('css=select', '2');
```
## select(target, label, value)
* `target` {string} 元素选择器
* `label` {string} 选择模式，支持:  index, label, value
* `value` {Object} 选中值
* {SearchContextBinding}

选择下拉框

```js
// <select>
//   <option value="1">小明</option>
//   <option value="2">小红</option>
//   <option value="3">小李</option>
// </select>

// 选择小红
select('css=select', 'index', 1); // 根据下标
select('css=select', 'label', '小红'); // 根据 label
select('css=select', 'value', '2'); // 根据 value
```
## waitForElementDisplayed(target, seconds)
* `target` {string} 元素选择器
* `seconds` {number?} 最大等待多少秒
* {SearchContextBinding}

等待元素显示（可见）

## waitForElementNotDisplayed(target, seconds)
* `target` {string} 元素选择器
* `seconds` {number?} 最大等待多少秒
* {SearchContextBinding}

等待元素隐藏（不可见）

## waitForElementPresent(target, seconds)
* `target` {string} 元素选择器
* `seconds` {number?} 最大等待多少秒
* {SearchContextBinding}

等待元素出现

## waitForElementNotPresent(target, seconds)
* `target` {string} 元素选择器
* `seconds` {number?} 最大等待多少秒
* {SearchContextBinding}

等待元素消失
