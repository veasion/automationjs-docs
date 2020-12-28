
# TouchActionsBinding

该类用来操作复杂的手势，如元素滚动，元素移动等，对象通过 `element.touch()` 获取。
目前兼容性差，建议使用 js 自行扩展。

## click()
* {TouchActionsBinding}

点击

## doubleClick()
* {TouchActionsBinding}

双击

## singleTap()
* {TouchActionsBinding}

单次触摸点击

## doubleTap()
* {TouchActionsBinding}

两次触摸点击

## longPress()
* {TouchActionsBinding}

长按

## flick()
* {TouchActionsBinding}

flick

## flickByElement(xOffset, yOffset, speed)
* {TouchActionsBinding}

flick

## down(x, y)
* `x` {number} x坐标
* `y` {number} y坐标
* {TouchActionsBinding}

down

## up(x, y)
* `x` {number} x坐标
* `y` {number} y坐标
* {TouchActionsBinding}

up

## move(x, y)
* `x` {number} x坐标
* `y` {number} y坐标
* {TouchActionsBinding}

move

## scroll(x, y)
* `x` {number} x坐标
* `y` {number} y坐标
* {TouchActionsBinding}

滚动

## scrollByElement(x, y)
* `x` {number} x坐标
* `y` {number} y坐标
* {TouchActionsBinding}

滚动

## perform()
* {TouchActionsBinding}

执行

```js
findOne("id=xxx").touch().click().move(124, 435).perform();
```