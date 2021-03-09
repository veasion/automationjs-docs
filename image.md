
# Image

提供对图片操作函数，如图片找色找图、ocr文字识别、验证码识别等，该类只能通过 image 调用。

js 脚本绑定的 java 后台类 cn.veasion.auto.bind.ImageBean



## load(path)

* `path` {string} 路径
* {ImageWrapper} 图片信息对象
    * `getWidth()` {number} 获取图片宽度
    * `getHeight()` {number} 获取图片高度
    * `getRGB(x, y)` {number} 获取坐标像素RGB值
    * `saveTo(path)` 保存图片至path
    * `clone()` {ImageWrapper} 克隆
    * `show()` gui展示图片
    * `show(x, y)` gui展示图片，标记出坐标
    * `show(x, y, width, height)` gui展示图片，标记处坐标跟区域

加载图片

```js
let img = image.load('C:\\Users\\user\\Desktop\\test.jpg');
println('图片宽度: ' + img.getWidth());
println('图片高度: ' + img.getHeight());
```



## loadByUrl(url)

* `url` {string} 图片url地址
* {ImageWrapper} 图片信息对象

加载网络图片

```js
let img = image.loadByUrl('http://xxx.png');
```



## loadByScreenshot()

* {ImageWrapper} 图片信息对象

浏览器截图

```js
let img = loadByScreenshot();
img.show();
```



## loadByElement(element)

* `element` {WebElementBinding} 元素
* {ImageWrapper} 图片信息对象

元素渲染成图片

```js
let element = findOne('id=xxx');
let img = image.loadByElement(element);
```



## ocrByUrl(imgUrl)

* `imgUrl` {string} 图片url地址
* {OcrResult} 识别结果
    * `getContent()` {string} 获取失败内容
    * `getWordsList()` {Words[]} 获取识别词组详细数据（包含词组位置宽高等）

根据图片链接OCR识别

```js
let result = image.ocrByUrl('http://xxx.jpg');
println('文字识别结果: ' + result.getContent());
```



## captchaByUrl(imgUrl)

* `imgUrl` {string} 图片url地址
* {OcrResult} 识别结果

根据图片链接OCR识别验证码

```js
let result = image.captchaByUrl('http://xxx.jpg');
println('验证码识别结果: ' + result.getContent());
```



## ocrByElement(element)

* `element` {WebElementBinding} 元素
* {OcrResult} 识别结果

根据元素OCR识别

```js
let result = image.ocrByElement(findOne('css=.ver-code-img img'));
println('识别结果: ' + result.getContent());
```



## ocrByImage(imageWrapper)

* `imageWrapper` {ImageWrapper} 图片对象
* {OcrResult} 识别结果

根据图片OCR识别

```js
let result = image.ocrByImage(image.load('C:\\Users\\user\\Desktop\\test.jpg'));
println('识别结果: ' + result.getContent());
```



## captchaByElement(element)
* `element` {WebElementBinding} 元素
* {OcrResult} 识别结果

根据元素OCR识别验证码

```js
let result = image.captchaByElement(findOne('css=.ver-code-img img'));
println('识别结果: ' + result.getContent());
```



## captchaByImage(imageWrapper)

* `imageWrapper` {ImageWrapper} 图片对象
* {OcrResult} 识别结果

根据图片OCR识别验证码

```js
let result = image.captchaByImage(image.load('C:\\Users\\user\\Desktop\\test.jpg'));
println('识别结果: ' + result.getContent());
```



## findImage(image, template)

* `image` {ImageWrapper} 主图片
* `template` {ImageWrapper} 模板图片（被查找图片）
* {PointWrapper} 点位置坐标
    * `getX()` {number} x坐标
    * `getY()` {number} y坐标

查找图片

```js
let point = image.findImage(image.load('C:\\Users\\user\\Desktop\\test.jpg'), image.load('C:\\Users\\user\\Desktop\\template.png'));
println('x坐标: ' + point.getX());
println('y坐标: ' + point.getY());
```



## findImage(image, template, threshold)

* `image` {ImageWrapper} 主图片
* `template` {ImageWrapper} 模板图片（被查找图片）
* `threshold` {number} 相似度 0~1, 强阈值。该值用于检验最终匹配结果，以及在每一轮匹配中如果相似度大于该值则直接返回匹配结果
* {PointWrapper} 点位置坐标

查找图片

```js
let point = image.findImage(image.load('C:\\Users\\user\\Desktop\\test.jpg'), image.load('C:\\Users\\user\\Desktop\\template.png'), 0.9);
println('x坐标: ' + point.getX());
println('y坐标: ' + point.getY());
```



## findImage(image, template, threshold, region)

* `image` {ImageWrapper} 主图片
* `template` {ImageWrapper} 模板图片（被查找图片）
* `threshold` {number} 相似度 0~1, 强阈值。该值用于检验最终匹配结果，以及在每一轮匹配中如果相似度大于该值则直接返回匹配结果
* `region` {number[]} 找图区域 [x, y, width, height]
* {PointWrapper} 点位置坐标

查找图片

```js
let point = image.findImage(image.load('C:\\Users\\user\\Desktop\\test.jpg'), image.load('C:\\Users\\user\\Desktop\\template.png'), 0.9, [0, 270, 300, 20]);
println('x坐标: ' + point.getX());
println('y坐标: ' + point.getY());
```



## findColor(image, color, threshold)

* `image` {ImageWrapper} 图片
* `color` {string} 颜色代码 eg: #FFFFFF
* `threshold` {number} 相识度 0-255，越小越匹配
* {PointWrapper} 点位置坐标

查找颜色

```js
let point = image.findColor(image.load('C:\\Users\\user\\Desktop\\test.jpg'), '#E31716', 4);
println('x坐标: ' + point.getX());
println('y坐标: ' + point.getY());
```



## findColor(image, color, threshold, region)

* `image` {ImageWrapper} 图片
* `color` {string} 颜色代码 eg: #FFFFFF
* `threshold` {number} 相识度 0-255，越小越匹配
* `region` {number[]} 查找区域 [x, y, width, height]
* {PointWrapper} 点位置坐标

查找颜色

```js
let point = image.findColor(image.load('C:\\Users\\user\\Desktop\\test.jpg'), '#620081', 4, [0, 270, 300, 20]);
println('x坐标: ' + point.getX());
println('y坐标: ' + point.getY());
```



## findMultiColors(image, firstColor, threshold, colorPoints)

* `image` {ImageWrapper} 图片
* `firstColor` {string} 第一个 颜色代码 eg: #FFFFFF
* `threshold` {number} 相识度 0-255，越小越匹配
* `colorPoints` {number[]} 相对于第一个点的位置和颜色的数组, 如: [[x, y, color], [0, 3, '#FFFFFF'], [1, 6, '#000000']]
* {PointWrapper} 点位置坐标

匹配多个颜色

```js
let point = image.findMultiColors(image.load('C:\\Users\\user\\Desktop\\test.jpg'), '#E51B1B', 4, [
    [0, 1, '#E51B1B'],
    [1, 0, '#E51B1B']
]);
println('x坐标: ' + point.getX());
println('y坐标: ' + point.getY());
```



## findMultiColors(image, firstColor, threshold, colorPoints, region)

* `image` {ImageWrapper} 图片
* `firstColor` {string} 第一个 颜色代码 eg: #FFFFFF
* `threshold` {number} 相识度 0-255，越小越匹配
* `colorPoints` {number[]} 相对于第一个点的位置和颜色的数组, 如: [[x, y, color], [0, 3, '#FFFFFF'], [1, 6, '#000000']]
* `region` {number[]} 查找区域 [x, y, width, height]
* {PointWrapper} 点位置坐标

匹配多个颜色

```js
let point = image.findMultiColors(image.load('C:\\Users\\user\\Desktop\\test.jpg'), '#E51B1B', 4, [
    [0, 1, '#E51B1B'],
    [1, 0, '#E51B1B']
], [0, 270, 300, 20]);
println('x坐标: ' + point.getX());
println('y坐标: ' + point.getY());
```



## findAllColor(image, color, threshold)

* `image` {ImageWrapper} 图片
* `color` {string} 颜色代码 eg: #FFFFFF
* `threshold` {number} 相识度 0-255，越小越匹配
* {PointWrapper[]} 所有颜色点位置坐标

查找颜色

```js
let points = image.findColor(image.load('C:\\Users\\user\\Desktop\\test.jpg'), '#E31716', 4);
for (let i = 0; i < points.length; i++) {
    println('第' + (i + 1) + '个点');
    println('x坐标: ' + points[i].getX());
    println('y坐标: ' + points[i].getY());
}
```



## findAllColor(image, color, threshold, region)

* `image` {ImageWrapper} 图片
* `color` {string} 颜色代码 eg: #FFFFFF
* `threshold` {number} 相识度 0-255，越小越匹配
* `region` {number[]} 查找区域 [x, y, width, height]
* {PointWrapper[]} 所有颜色点位置坐标

查找颜色

```js
let points = image.findColor(image.load('C:\\Users\\user\\Desktop\\test.jpg'), '#E31716', 4, [0, 270, 300, 20]);
for (let i = 0; i < points.length; i++) {
    println('第' + (i + 1) + '个点');
    println('x坐标: ' + points[i].getX());
    println('y坐标: ' + points[i].getY());
}
```

