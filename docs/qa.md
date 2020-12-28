# Q & A

## 如何启动程序

首先安装 chrome 浏览器，浏览器访问 chrome://settings/help 打开关于 chrome 页面

找到 chrome 版本，然后打开 [chromedriver](http://npm.taobao.org/mirrors/chromedriver/) 下载网站，找到对应版本驱动（版本号匹配要求很严格）

下载对应驱动放到 C:\\data\\auto\\ 目录下（不强烈要求，可以自定义路径）

修改项目下的`config.json`文件，修改浏览器驱动路径，修改以下条目：

```json
{
	"CHROME_DRIVER_PATH": "C:\\data\\auto\\chromedriver.exe"
}
```



然后运行 `cn.veasion.auto.Development` 类的 main 方法即可。



## 启动后如何运行 js 自动化脚本

由于 Development 类没有明确指定运行文件，所以通过控制台命令运行：

> 如运行 script 目录下 crawler.js

```
run script/crawler.js
```
> 目录层级太多，也可以直接命令行执行（会自动匹配查找）

```
> baidu.js
```

> 重新运行该 js 命令

```
reload
```

> 重置脚本引擎

```
reset
```
> 运行某作者所有 js 脚本 （根据 js 文件中 @author 查找）

```
author luozhuowei
```

> 退出

  ```
  exit
  ```

> 直接命令行执行 js 脚本

  ```
open('http://www.baidu.com')
  ```

> 执行多行 js 脚本

  ```
  >>>
  function hello() {
  	log.info("hello automation js")
  }
  >>>
  ```

> 打印已执行的历史命令

  ```
  // 上一条命令
  top
  // 前3条命令
  top 3
  ```



## 如何指定运行某 js 自动化脚本

`cn.veasion.auto.Development` 类的 main 方法代码：

```java
public static void main(String[] args) throws Exception {
    // ...省略其他代码
    
    // 默认 script 下的脚本文件
    String jsPath = "script/crawler.js";
    
    // 指定js文件执行
    JavaScriptCore.execute(driver, env, new File(getFilePath(jsPath)));
    
    // ...省略其他代码
}
```



## 如何以 jar 方式运行

jar包路径 resources/automation.jar, 运行脚本路径 resources/automation.bat。

安装 jdk 环境，双击 `automation.bat` 即可运行。
