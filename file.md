# File

file 模块提供一系列文件操作函数，如读写文本文件等。

该 api 函数通过 file 变量访问，如 `file.readText(path)` 方式调用

js 脚本绑定的 java 后台类 cn.veasion.auto.bind.FileBean



## writeText(path, context, append)
* `path` {string} 路径
* `context` {string} 文本内容
* `append` {boolean} 是否追加
* {string}

写文本文件，默认utf-8



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



## readText(pathOrUrl)

* `pathOrUrl` {string} 路径或网址
* {string}

读取文本，可以读本地文本文件和网络文本，默认utf-8



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

