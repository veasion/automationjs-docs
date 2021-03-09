
# Log

提供日志记录，可以直接通过 log 访问，如 `log.info('xxx')`



## debug(message)

* `message` {string} 消息
debug 日志



## warn(message)

* `message` {string} 消息
warn 日志



## info(message)

* `message` {string} 消息
info 日志



## error(message)

* `message` {string} 消息
error 日志



## error(message, e)

* `message` {string} 消息
* `e` {Object} 异常
error 日志



## invokeMethod(name, args)

* `name` {string} 方法名
* `args` {Object[]} 方法参数
打印 方法及参数的 info 日志
```js
log.invokeMethod('login', ['admin', '123456']);
// 等价于
log.info('login("admin", "123456")');
```


