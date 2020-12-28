
# JdbcConnectionBinding

提供数据库操作，对象通过 WebDriverBinding 中的 `createJdbcConnection` 或 `createMysqlConnection` 方法创建。

## query(sql, params)
* `sql` {string} SQL
* `params` {Object[]} 参数
* {Object[]} 返回查询结果列表

列表查询

```js
// 连接数据库
let db = createMysqlConnection('127.0.0.1', 3306, 'user', 'root', '123456');
// db = createJdbcConnection('jdbc:mysql://127.0.0.1:3306/user?useUnicode=true&characterEncoding=utf-8', 'root', '123456');

// 查询
let list = db.query('select id, user_name, sex from t_user where status = ? limit ?', [1, 10]);

for (let i in list) {
	println(list[i]); // { id: 1, userName: 'xxx' }
}

db.close();
```

## queryOnly(sql, params)
* `sql` {string} SQL
* `params` {Object[]} 参数

获取单个值

```js
// 连接数据库
let db = createMysqlConnection('127.0.0.1', 3306, 'user', 'root', '123456');
// db = createJdbcConnection('jdbc:mysql://127.0.0.1:3306/user?useUnicode=true&characterEncoding=utf-8', 'root', '123456');

db.queryOnly('select database()', null); // user

db.close();
```

## update(sql, params)
* `sql` {string} SQL
* `params` {Object[]} 参数
* {number} 返回影响条数

执行增删改

```js
db.update('update t_user set user_name = ? where id = ?', ['xxx', 1]);
```

## insert(sql, params)
* `sql` {string} SQL
* `params` {Object[]} 参数
* {number} 自增ID，无则返回空

执行新增，返回自增长id

```js
db.insert('insert into t_user(user_name, sex) values (?, ?)', ['veasion', '男']);
```

## executeDDL(sql)
* `sql` {string} SQL
* {number} 返回影响条数

执行DDL

```js
db.executeDDL("alter table t_user modify `name` varchar(255) not null comment '名称';");
```

## close()

关闭连接
