# Node.js入门

## 什么是 Node.js

Node.js 是一个独立的 JavaScript 运行环境，能独立执行 JS 代码

作用：可以用来编写服务器后端的应用程序

- 编写数据接口，提供网页资源浏览功能等等
- `前端工程化`：集成各种开发中使用的工具和技术，为后续学习 Vue 和 React 等框架做铺垫

前端工程化：开发项目直到上线，过程中集成的所有`工具和技术`，压缩工具、格式化工具、转换工具、打包工具、脚手架工具等，Node.js 是前端工程化的基础（因为 Node.js 可以主动读取前端代码内容）

浏览器能执行 JS 代码，依靠的是内核中的 `V8 引擎`（C++程序），Node.js 是基于Chrome V8 引擎进行封装（运行环境），独立执行 JS 代码，但是语法和浏览器环境的 V8 有所不同，`Node.js 环境没有 DOM 和BOM 等`，但是都支持 ECMAScript 标准的代码语法，Node.js 有独立的 API

Node.js 作用除了编写后端应用程序，也可以对前端代码进行压缩，转译，整合等等，提高前端开发和运行效率

推荐下载 node-`v16.19.0`.msi 安装程序（指定版本：兼容 vue-admin-template 模版）

想要得到 Node.js 需要把这个软件安装到电脑，在素材里有安装程序（window 和 mac 环境的）参考 PPT 默认下一步安装即可

Node.js 没有图形化界面，需要使用 cmd 终端命令行（利用一些命令来操控电脑执行某些程序软件）输入，node -v 检查是否安装成功

```bash
node -v
```

Node.js 执行目标 JS 文件，需要使用 `node xxx.js` 命令来执行（我们可以借助 VSCode 集成终端使用，好处：可以快速切换到目标 JS 文件所在终端目录，利用相对路径找到要执行的目标 JS 文件

## fs模块-读写文件

模块：类似插件，封装了`方法和属性`供我们使用

fs 模块：封装了与本机文件系统进行交互的，方法和属性

fs 模块使用语法如下：

- `加载` fs 模块，得到 fs 对象

  ```js
  const fs = require('fs') // fs 是模块标识符：模块的名字
  ```

- `写入`文件内容语法：

  ```js
  fs.writeFile('文件路径', '写入内容', err => {
    // 写入后的回调函数
  })
  ```

- `读取`文件内容的语法：

  ```js
  fs.readFile('文件路径', (err, data) => {
    // 读取后的回调函数
    // data 是文件内容的 Buffer 数据流
  })
  ```

向 test.txt 文件写入内容并读取打印

```js
/**
 * 目标：使用 fs 模块，读写文件内容
 * 语法：
 * 1. 引入 fs 模块
 * 2. 调用 writeFile 写入内容
 * 3. 调用 readFile  读取内容
 */
//  加载 fs 模块对象
const fs = require('fs')
//  写入文件内容
fs.writeFile('./test.txt', 'hello,Node.js', (err) => {
  if (err) console.log(err)
  else console.log('写入成功')
})
//  读取文件内容
fs.readFile('./test.txt', (err, data) => {
  if (err) console.log(err)
  //  data 是 buffer 16 进制数据流对象，.toString（）转换成字符串
  else console.log(data.toString())
})
```

## path模块-路径处理

Node.js 执行 JS 代码时，代码中的路径都是以`终端所在路径`来查找的，而不是以我们认为的从代码本身出发，可能无法找到你想要，所以在 Node.js 要执行的代码中，访问其他文件，建议使用`绝对路径`

解决方案：使用模块内置变量 `__dirname`配合 path.join() 来得到绝对路径使用

`__dirname`：内置变量（获取当前模块目录-绝对路径）

`path.join()` 会使用特定于平台的分隔符`,`作为定界符，将所有给定的路径片段连接在一起

1. 加载 path 模块

   ```js
   const path = require('path')
   ```

2. 使用 path.join 方法拼接路径

   ```js
   path.join('路径1', '路径2', ...)
   ```

```js
const fs = require('fs')
console.log(__dirname) // D:\备课代码\2_node_3天\Node_代码\Day01_Node.js入门\代码\03

// 1. 加载 path 模块
const path = require('path')
// 2. 使用 path.join() 来拼接路径
const pathStr = path.join(__dirname, '..', 'text.txt')
console.log(pathStr)

fs.readFile(pathStr, (err, data) => {
  if (err) console.log(err)
  else console.log(data.toString())
})
```

## 压缩前端html

前端工程化：前端代码压缩，整合，转译，测试，自动部署等等工具的集成统称，为了提高前端开发项目的效率

需求：把准备好的 html 文件里的回车符（\r）和换行符（\n）去掉进行压缩，写入到新 html 中

步骤：

1. `读取`源 html 文件内容
2. 正则`替换`字符串
3. `写入`到新的 html 文件中，并运行查看是否能正常打开网页

```js
/**
 * 目标一：压缩 html 里代码
 * 需求：把 public/index.html 里的，回车/换行符去掉，写入到 dist/index.html 中
 *  1.1 读取 public/index.html 内容
 *  1.2 使用正则替换内容字符串里的，回车符\r 换行符\n
 *  1.3 确认后，写入到 dist/index.html 内
 */
const fs = require('fs')
const path = require('path')
// 1.1 读取 public/index.html 内容
fs.readFile(path.join(__dirname, 'public', 'index.html'), (err, data) => {
  const htmlStr = data.toString()
  // 1.2 使用正则替换内容字符串里的，回车符\r 换行符\n
  const resultStr = htmlStr.replace(/[\r\n]/g, '')
  // 1.3 确认后，写入到 dist/index.html 内
  fs.writeFile(path.join(__dirname, 'dist', 'index.html'), resultStr, err => {
    if (err) console.log(err)
    else console.log('压缩成功')
  })
})
```

## 认识URL中的端口号

URL 是统一资源定位符，简称网址，用于访问网络上的资源

端口号的作用：标记服务器里对应的`服务程序`，值为（0-65535 之间的任意整数）

注意：http 协议，`默认`访问的是 `80` 端口

`Web服务程序`：用于提供网上信息浏览功能

注意：0-1023 和一些特定的端口号被占用，我们自己编写服务程序请避开使用

## http模块-创建Web服务

需求：引入 http 模块，使用相关语法，创建 Web 服务程序并响应内容给服务器

步骤：

1. 引入加载 `http 模块`，创建 Web 服务对象
2. 监听 `request` 请求事件，对本次请求，做一些响应处理，设置响应头和响应体
3. 配置`端口号`并`启动` Web 服务监听对应`端口号`
4. 运行本服务在终端进程中，用浏览器发起请求，浏览器请求 http://localhost:3000 测试

注意：本机的域名叫做 `localhost`

```js
/**
 * 目标：基于 http 模块创建 Web 服务程序
 *  1.1 加载 http 模块，创建 Web 服务对象
 *  1.2 监听 request 请求事件，设置响应头和响应体
 *  1.3 配置端口号并启动 Web 服务
 *  1.4 浏览器请求（http://localhost:3000）测试
 */
// 1.1 加载 http 模块，创建 Web 服务对象
const http = require('http')
const server = http.createServer()
// 1.2 监听 request 请求事件，设置响应头和响应体
server.on('request', (req, res) => {
  // 设置响应头-内容类型-普通文本以及中文编码格式
  res.setHeader('Content-Type', 'text/plain;charset=utf-8')
  // 设置响应体内容，结束本次请求与响应
  res.end('欢迎使用 Node.js 和 http 模块创建的 Web 服务')
})
// 1.3 配置端口号并启动 Web 服务
server.listen(3000, () => {
  console.log('Web 服务启动成功了')
})
```

## 案例-浏览时钟

需求：基于 Web 服务，开发提供`网页资源`的功能，了解下后端的代码工作过程

步骤：

1. 基于 http 模块，创建 Web 服务
2. 使用 `req.url` 获取请求`资源路径`，判断并`读取 index.html` 里字符串内容返回给请求方
3. 其他路径，暂时返回不存在的提示
4. 运行 Web 服务，用浏览器发起请求

```js
/**
 * 目标：编写 web 服务，监听请求的是 /index.html 路径的时候，返回 dist/index.html 时钟案例页面内容
 * 步骤：
 *  1. 基于 http 模块，创建 Web 服务
 *  2. 使用 req.url 获取请求资源路径，并读取 index.html 里字符串内容返回给请求方
 *  3. 其他路径，暂时返回不存在提示
 *  4. 运行 Web 服务，用浏览器发起请求
 */
const fs = require('fs')
const path = require('path')
// 1. 基于 http 模块，创建 Web 服务
const http = require('http')
const server = http.createServer()
server.on('request', (req, res) => {
  // 2. 使用 req.url 获取请求资源路径，并读取 index.html 里字符串内容返回给请求方
  if (req.url === '/index.html') {
    fs.readFile(path.join(__dirname, 'dist/index.html'), (err, data) => {
      res.setHeader('Content-Type', 'text/html;charset=utf-8')
      res.end(data.toString())
    })
  } else {
    // 3. 其他路径，暂时返回不存在提示
    res.setHeader('Content-Type', 'text/html;charset=utf-8')
    res.end('你要访问的资源路径不存在')
  }
})
server.listen(8080, () => {
  console.log('Web 服务启动了')
})
```

# Node.js模块化

## 模块化简介

在 Node.js 中每个文件都被当做是一个独立的模块，模块内定义的变量和函数都是独立作用域的，因为 Node.js 在执行模块代码时，将使用如下所示的函数封装器对其进行封装

而且项目是由多个模块组成的，每个模块之间都是独立的，而且提高模块代码复用性，按需加载，`独立作用域`

但是因为模块内的属性和函数都是私有的，如果对外使用，需要使用标准语法`导出`和`导入`才可以，而这个标准叫 `CommonJS 标准`，接下来我们在一个需求中，体验下模块化导出和导入语法的使用

定义：CommonJS 模块是为 Node.js 打包 JavaScript 代码的原始方式。Node.js 还支持浏览器和其他 JavaScript 运行时使用的 ECMAScript 运行时使用的 ECMAScript 模块标准。

概念：项目是由很多个模块文件组成的

好处：提高代码复用性，按需加载，`独立作用域`

使用：需要标准语法`导出`和`导入`进行使用

需求：定义 utils.js 模块，封装基地址和求数组总和的函数，导入到 index.js 使用查看效果

`导出`语法：

```js
module.exports = {
  对外属性名: 模块内私有变量
}
```

`导入`语法：

- 内置模块：直接写名字（例如：fs、path、http）
- 自定义模块：写模块文件路径（例如：./util.js）

```js
const 变量名 = require('模块名或路径')
// Node.js 环境内置模块直接写模块名（例如：fs，path，http）
// 自定义模块：写模块文件路径（例如：./utils.js)
```

> 变量名的值接收的就是目标模块导出的对象

代码实现

- utils.js：导出

  ```js
  /**
   * 目标：基于 CommonJS 标准语法，封装属性和方法并导出
   */
  const baseURL = 'http://hmajax.itheima.net'
  const getArraySum = arr => arr.reduce((sum, item) => sum += item, 0)

  // 导出
  module.exports = {
    url: baseURL,
    arraySum: getArraySum
  }
  ```

- index.js：导入使用

  ```js
  /**
   * 目标：基于 CommonJS 标准语法，导入工具属性和方法使用
   */
  // 导入
  const obj = require('./utils.js')
  console.log(obj)
  const result = obj.arraySum([5, 1, 2, 3])
  console.log(result)
  ```

## ECMAScript 标准

### 默认导出和导入

CommonJS 规范是 Node.js 环境中默认的，后来官方推出 ECMAScript 标准语法，我们接下来在一个需求中，体验下这个标准中默认导出和导入的语法要如何使用

需求：封装并导出基地址和求数组元素和的函数，导入到 index.js 使用查看效果

导出语法：

```js
export default {
  对外属性名: 模块内私有变量
}
```

导入语法：

```js
import 变量名 from '模块名或路径'
```

> 变量名的值接收的就是目标模块导出的对象

注意：Node.js 默认只支持 CommonJS 标准语法，如果想要在当前项目环境下使用 ECMAScript 标准语法，请新建 package.json 文件设置 type: 'module' 来进行设置

```json
{ “type”: "module" }
```

utils.js：导出

```js
/**
 * 目标：基于 ECMAScript 标准语法，封装属性和方法并"默认"导出
 */
const baseURL = 'http://hmajax.itheima.net'
const getArraySum = arr => arr.reduce((sum, item) => sum += item, 0)

// 默认导出
export default {
  url: baseURL,
  arraySum: getArraySum
}
```

index.js：导入

```js
/**
 * 目标：基于 ECMAScript 标准语法，"默认"导入，工具属性和方法使用
 */
// 默认导入
import obj from './utils.js'
console.log(obj)
const result = obj.arraySum([10, 20, 30])
console.log(result)
```

### 命名导出和导入

ECMAScript 标准的语法有很多，常用的就是默认和命名导出和导入，这节课我们来学习下命名导出和导入的使用

需求：封装并导出基地址和数组求和函数，导入到 index.js 使用查看效果

命名导出语法：

```js
export 修饰定义语句
```

命名导入语法：

```js
import { 同名变量 } from '模块名或路径'
```

> 注意：同名变量指的是模块内导出的变量名

utils.js 导出

```js
/**
 * 目标：基于 ECMAScript 标准语法，封装属性和方法并"命名"导出
 */
export const baseURL = 'http://hmajax.itheima.net'
export const getArraySum = arr => arr.reduce((sum, item) => sum += item, 0)

```

index.js 导入

```js
/**
 * 目标：基于 ECMAScript 标准语法，"命名"导入，工具属性和方法使用
 */
// 命名导入
import {baseURL, getArraySum} from './utils.js'
console.log(obj)
console.log(baseURL)
console.log(getArraySum)
const result = getArraySum([10, 21, 33])
console.log(result)
```

与默认导出如何选择：

- `按需`加载，使用`命名`导出和导入
- `全部`加载，使用`默认`导出和导入

|      |                  命名                   |               默认                |
| :--: | :-------------------------------------: | :-------------------------------: |
| 导出 |          export 修饰定义的语句          |         export default {}         |
| 导入 | import { 同名变量 } from '模块名或路径' | import 变量名 from '模块名或路径' |



## 包的概念

包：将`模块，代码，其他资料`整合成一个文件夹，这个文件夹就叫包

包分类：

- 项目包：主要用于编写项目和业务逻辑
- 软件包：`封装工具和方法`进行使用

包要求：根目录中，必须有 package.json 文件（记录包的清单信息）

```json
{
  "name":	"utils",		//	软件包名称
  "version": "1.0.0",		//	软件包当前版本
  "description": "一个数组和字符串常用工具方法的包",		//	软件包简短描述
  "main": "index.js",		//	软件包入口点
  "author": "",		//	软件包作者
  "license": "MIT"		//	软件包许可证（商用后可以用作者名字宣传）
}
```

包使用：导入软件包时，引入的默认是 index.js 模块文件 / main 属性指定的模块文件

需求：封装数组求和函数的模块，封装判断用户名和密码长度函数的模块，形成一个`软件包`，并导入到 index.js 中使用查看效果

utils/lib 相关代码在素材里准备好了，只需要自己在 utils/index.js 统一出口进行导出

```js
/**
 * 本文件是，utils 工具包的唯一出口
 * 作用：把所有工具模块方法集中起来，统一向外暴露
 */
const { getArraySum } = require('./lib/arr.js')
const { checkUser, checkPwd } = require('./lib/str.js')

// 统一导出所有函数
module.exports = {
  getArraySum,
  checkUser,
  checkPwd
}

```

index.js 导入软件包文件夹使用（注意：这次导入的是包文件夹，不是模块文件）

```js
/**
 * 目标：导入 utils 软件包，使用里面封装的工具函数
 */
const obj = require('./utils')
console.log(obj)
const result = obj.getArraySum([10, 20, 30])
console.log(result)
```

## npm软件包管理器

npm 简介[链接]([http://dev.nodejs.cn/learn/an-introduction-to-the-npm-package-manager#npm-%E7%AE%80%E4%BB%8B](http://dev.nodejs.cn/learn/an-introduction-to-the-npm-package-manager))： 软件包管理器，用于下载和管理 Node.js 环境中的软件包

npm 使用步骤：

1. 初始化清单文件： npm init -y （得到 package.json 文件，有则跳过此命令）

   > 注意 -y 就是所有选项用默认值，所在文件夹不要有中文/特殊符号，建议英文和数字组成，因为 npm 包名限制建议用英文和数字或者下划线中划线

2. 下载软件包：`npm i 软件包名称`

3. 使用软件包

### 安装所有依赖

我们拿到了一个别人编写的项目，但是没有 node_modules，项目能否正确运行？

> 不能，因为缺少了项目需要的依赖软件包，比如要使用 dayjs 和 lodash 但是你项目里没有这个对应的源码，项目会报错的

为何没有给我 node_modules？

> 因为每个人在自己的本机使用 npm 下载，要比磁盘间传递要快（npm 有缓存在本机）

如何得到需要的所有依赖软件包呢？

> 直接在项目目录下，运行终端命令：`npm i` 即可安装 package.json 里记录的所有包和对应版本到本项目中的 node_modules

### 全局软件包-nodemon

软件包区别：

- 本地软件包：`当前项目`内使用，封装`属性和方法`，存在于 node_modules
- 全局软件包：`本机`所有项目使用，封装`命令和工具`，存在于系统设置的位置

nodemon 作用：替代 node 命令，检测代码更改，`自动重启`程序

使用：

1. 安装：npm i nodemon -g （-g 代表安装到全局环境中）
2. 运行：nodemon 待执行的目标 js 文件
3. 退出运行：Ctrl + C

## Node.js概念和常用命令总结

Node.js 模块化：把每个文件当做一个模块，独立作用域，按需加载

使用：采用特定的标准语法导出和导入进行使用

|                       |         导出          |                 导入                  |   说明   |
| :-------------------: | :-------------------: | :-----------------------------------: | :------: |
|  CommonJS标准 · 语法  | `modile.exports = {}` |       `require('模块名或路径')`       |          |
| ECMAScript标准 · 默认 |   export default {}   |   import 变量名 from '模块名或路径'   | 全部加载 |
| ECMAScript标准 · 命名 |  export 修饰定义语句  | import {同名变量} from '模块名或路径' | 按需加载 |

> CommonJS 标准：一般应用在 Node.js 项目环境中
>
> ECMAScript 标准：一般应用在前端工程化项目中

Node.js 包：把模块文件，代码文件，其他资料聚合成一个文件夹就是包

> 项目包：编写项目需求和`业务逻辑`的文件夹
>
> 软件包：`封装工具和方法`进行使用的文件夹（一般使用 npm 管理）
>
> - 本地软件包：作用在`当前`项目，一般封装的`属性/方法`，供项目调用编写业务需求
> - 全局软件包：作用在`所有`项目，一般封装的`命令/工具`，支撑项目运行

Node.js 常用命令：

|        功能         |       命令        |
| :-----------------: | :---------------: |
|    执行 js 文件     |     node xxx      |
| 初始化 package.json |    npm init -y    |
|   下载本地软件包    |  npm i 软件包名   |
|   下载全局软件包    | npm i 软件包名 -g |
|     删除软件包      | npm uni 软件包名  |

# 