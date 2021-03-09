
# EnvironmentBinding

该类用来操作环境变量，可以直接通过 env 访问。

配置文件 `config.json` 中的配置会默认加载到 env 全局变量中，可以直接获取，如 `env.getString('USER_NAME')`



## put(key, value)

* `key` {string} key
* `value` {string} value

存储变量（当前脚本）



## putGlobal(key, value)

* `key` {string} key
* `value` {string} value

存储全局变量（当前驱动）



## putSystemVar(key, value)

* `key` {string} key
* `value` {string} value

存储系统变量（当前系统）



## getSystemVar(key)

* `key` {string} key
* {Object}

获取系统变量（当前系统）



## get(key)

* `key` {string} key
* {Object}

获取变量



## getString(key)

* `key` {string} key
* {string}

获取变量



## getOrDefault(key, defaultVal)

* `key` {string} key
* `defaultVal` {Object} defaultVal 默认值（取不到数据时返回该值）
* {Object}

获取变量



## remove(key)

* `key` {string} key

移除当前变量 （当前脚本）



## translate(str)

* `str` {string} 表达式

解析表达式

```js
env.put("name", "veasion");
env.translate("hello ${name}"); // hello veasion
```



## translate(str, object)

* `str` {string} 表达式
* `object` {Object} 对象

解析表达式

```js
env.translate("hello ${name}", { name: 'veasion' }); // hello veasion
```



## getPath(path)

* `path` {string} 路径
* {string}

获取class决定路径

```js
// 如代码在 D:\projects\automation_testing 运行
env.getPath('/common/proxy.js'); // D:\projects\automation_testing\target\classes\common\proxy.js
```



## getSourcePath(path)

* `path` {string} 路径
* {string}

获取源文件绝对路径

```js
// 如代码在 D:\projects\automation_testing 运行
env.getSourcePath('/common/proxy.js'); // D:\projects\automation_testing\src\main\resources\common\proxy.js
```



# 获取常用按键 KEY

env 可以直接获取常用按键，如回车按键 `env.get('KEY_ENTER')`

支持以下按键获取：

`KEY_BACK_SPACE`
`KEY_TAB`
`KEY_ENTER`
`KEY_SHIFT`
`KEY_CONTROL`
`KEY_ALT`
`KEY_ESCAPE`
`KEY_PAGE_UP`
`KEY_PAGE_DOWN`
`KEY_END`
`KEY_HOME`
`KEY_ARROW_LEFT`
`KEY_ARROW_UP`
`KEY_ARROW_RIGHT`
`KEY_ARROW_DOWN`
`KEY_F12`

