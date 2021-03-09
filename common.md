# Common

common 模块提供一系列公共函数，如等待、随机数、断言、创建数据库连接等。

该 api 函数可以直接方法访问，如 `println(message)` 方式调用，等价于 `common.println(message)`

js 脚本绑定的 java 后台类 cn.veasion.auto.bind.CommonBean




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



## input(title)

* `title` {string} 输入提示
* {string}

控制台输入



## sleep(millis)

* `millis` {number} 毫秒

暂停多少毫秒，等价于 pause

```js
sleep(500);
```



## pause(millis)

* `millis` {number} 毫秒

暂停多少毫秒，等价于 sleep

```js
pause(500);
```

```js
let name = input('请输入姓名: ');
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



## assertResult(flag, message)

* `flag` {boolean} 是否通过
* `message` {string} 断言信息

断言，当 flag 为 true 时表示断言通过，false 为断言失败抛出异常 message

```js
assertResult(true, '断言测试通过');
// 断言元素存在
assertResult(findOne('id=xxx') != null, '断言元素存在');
```



## info

* {string}

获取当前脚本环境信息。

