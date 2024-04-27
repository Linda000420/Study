# AJAX

## AJAX 概念和 axios 使用

1.  axios 库，与服务器进行数据通信
   - 基于 XMLHttpRequest 封装、代码简单、月下载量在 14 亿次
   - Vue、React 项目中都会用到 axios
2. 在学习 XMLHttpRequest 对象的使用，了解 AJAX 底层原理

### AJAX概念

AJAX 是浏览器与服务器进行`数据通信`的技术

1. 什么是 AJAX ? [mdn](https://developer.mozilla.org/zh-CN/docs/Web/Guide/AJAX/Getting_Started)
   - 使用浏览器的 XMLHttpRequest 对象 与服务器通信
   - 浏览器网页中，使用 AJAX技术（XHR对象）发起获取省份列表数据的请求，服务器代码响应准备好的省份列表数据给前端，前端拿到数据数组以后，展示到网页
2. 什么是服务器？
   - 可以暂时理解为提供数据的一台电脑
3. 为何学 AJAX ?
   - 以前我们的数据都是写在代码里固定的, 无法随时变化
   - 现在我们的数据可以从服务器上进行获取，让数据变活
4. 怎么学 AJAX ?
   - 这里使用一个第三方库叫 axios, 后续在学习 XMLHttpRequest 对象了解 AJAX 底层原理
   - 因为 axios 库语法简单，让我们有更多精力关注在与服务器通信上，而且后续 Vue，React 学习中，也使用 axios 库与服务器通信

### axios 使用

步骤：

1. 引入 axios.js 文件到自己的网页中

   > axios.js文件链接: https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js

2. 使用 axios 函数

   - 传入配置对象
   - 再用 `.then` 回调函数接收结果，并做后续处理

   ```js
   axios({
     url: '目标资源地址'
   }).then((result) => {
     // 对服务器返回的数据做后续处理
   })
   ```

   > 请求的 url 地址, 就是标记资源的网址

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>AJAX概念和axios使用</title>
</head>

<body>
  <!--
    axios库地址：https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js
    省份数据地址：http://hmajax.itheima.net/api/province

    目标: 使用axios库, 获取省份列表数据, 展示到页面上
    1. 引入axios库
  -->
  <p class="my-p"></p>
  <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
  <script>
    // 2. 使用axios函数
    axios({
      url: 'http://hmajax.itheima.net/api/province'
    }).then(result => {
      console.log(result)
      // 好习惯：多打印，确认属性名
      console.log(result.data.list)
      console.log(result.data.list.join('<br>'))
      // 把准备好省份列表，插入到页面
      document.querySelector('.my-p').innerHTML = result.data.list.join('<br>') 
    })
  </script>
</body>

</html>
```

##  URL

URL 是`统一资源定位符`，简称`网址`，用于定位网络中的`资源`（资源指的是：网页，图片，数据，视频，音频等等）

URL 由`协议`，`域名`，`资源路径`（URL 组成有很多部分，我们先掌握这3个重要的部分即可）

http 协议 ：超文本传输协议，规定了浏览器和服务器传递数据的`格式`

域名 ：标记服务器在互联网当中的`方位`，网络中有很多服务器，你想访问哪一台，就需要知道它的域名才可以，是必须要写的

资源路径：一个服务器内有多个资源，用于标记资源在服务器下的`具体位置`

### URL 查询参数

查询参数：携带给服务器`额外信息`，让服务器返回我想要的某一部分数据而不是全部数据，例如：查询河北省下属的城市列表，需要先把河北省传递给服务器

语法：

- 在 url 网址后面用?拼接格式：http://xxxx.com/xxx/xxx?参数名1=值1&参数名2=值2
- 参数名一般是后端规定的，值前端看情况传递即可

### axios 查询参数

axios 使用 `params` 选项携带查询参数，在运行时把参数名和值会拼接到 url?参数名=值

```js
axios({
  url: '目标资源地址',
  params: {
    参数名: 值
  }
}).then(result => {
  // 对服务器返回的数据做后续处理
})
```

~~~html
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>
  axios ({
    url: 'http://hmajax.itheima.net/api/city',
    params: {
      pname: '广东省'
    }
  }).then(result => {
    console.log(result);
    document.querySelector('p').innerHTML = result.data.list.join('<br>')
  })
</script>
~~~

## 常用请求方法和数据提交

请求方法是一些固定单词的英文，例如：GET，POST，PUT，DELETE，PATCH（这些都是http协议规定的），每个单词对应一种对服务器`资源`要执行的`操作`

| 请求方法 |       操作       |
| :------: | :--------------: |
|  `GET`   |    `获取数据`    |
|  `POST`  |    `提交数据`    |
|   PUT    | 修改数据（全部） |
|  DELETE  |     删除数据     |
|  PATCH   | 修改数据（部分） |

前面我们获取数据其实用的就是GET请求方法，但是axios内部设置了默认请求方法就是GET，我们就没有写，但是提交数据需要使用POST请求方法

当数据需要再服务器上`保存`时就需要数据提交，例如：多端要查看同一份订单数据，或者使用同一个账号进行登录，那订单/用户名+密码，就需要保存在服务器上，随时随地进行访问

### axios 请求配置

url：请求的 URL 网址

method：请求的方法，GET 可以省略（不区分大小写）

data：提交数据

```js
axios({
  url: '目标资源地址',
  method: '请求方法',
  data: {
    参数名: 值
  }
}).then(result => {
  // 对服务器返回的数据做后续处理
})
```

~~~html
<body>
  <button class="btn">注册用户</button>
  <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
  <script>
    /*
      注册用户: http://hmajax.itheima.net/api/register
      请求方法: POST
      参数名:
        username: 用户名 (中英文和数字组成, 最少8位)
        password: 密码 (最少6位)

      目标: 点击按钮, 通过axios提交用户和密码, 完成注册
    */

    // 绑定事件
    document.querySelector('.btn').addEventListener('click', () => {
      axios ({
        url: 'http://hmajax.itheima.net/api/register',
        method: 'post',
        data: {
          username: 'itheima789',
          password: '123456'
        }
      }).then(result => {
        console.log(result);
      })
    })
    
  </script>
</body>
~~~

### axios 错误处理

场景：如果注册相同的账号，则会遇到报错信息，也就是 axios 请求响应失败了

处理：用更直观的方式，给`普通用户`展示错误信息

语法：在 `then` 方法的后面，通过点语法调用 `catch` 方法，传入`回调函数`并定义`形参`

```js
axios({
  // ...请求选项
}).then(result => {
  // 处理成功数据
}).catch(error => {
  // 处理失败错误
})
```

~~~html
<body>
  <button class="btn">注册用户</button>
  <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
  <script>
    /*
      注册用户: http://hmajax.itheima.net/api/register
      请求方法: POST
      参数名:
        username: 用户名 (中英文和数字组成, 最少8位)
        password: 密码 (最少6位)

      目标: 点击按钮, 通过axios提交用户和密码, 完成注册
      需求：使用 axios 错误处理语法，拿到报错信息，弹窗反馈给用户
    */
   document.querySelector('.btn').addEventListener('click', () => {
    axios({
      url: 'http://hmajax.itheima.net/api/register',
      // 指定请求方法
      method: 'post',
      data: {
        username: 'itheima007',
        password: '7654321'
      }
    }).then(result => {
      //  成功
      console.log(result)
    }).catch(error => {
      //  处理错误信息
      alert(error.response.data.message)
    });
   })
  </script>
</body>
~~~

## HTTP 协议

HTTP 协议规定了浏览器和服务器返回内容的`格式`

### 请求报文

`请求报文`：是浏览器按照 HTTP 协议要求的`格式`，发送给服务器的`内容`，例如刚刚注册用户时，有发起请求报文

请求报文的组成部分：

- `请求行：请求方法，URL`，协议
- `请求头`：以键值对的格式携带的附加信息，比如：`Content-Type`（指定了本次传递的内容类型）
- 空行：分割请求头，空行之后的是发送给服务器的资源
- `请求体：发送的资源`

我们可以在浏览器中查看请求报文，路径：开发者工具（检查） → Network（网络）→ Fetch/XHR → 点击对应请求 → Headers（标头）/ Payload（载荷）

Headers（标头）：General（常规）、Response Headers（响应标头）、Request Headers（请求标头）

Payload（载荷）：Request Payload（请求载荷）显示数据

### 请求报文-错误排查

查看请求报文可以用来确认我们代码发送的请求数据是否真的正确

1. 确认信息输入正确
2. 在载荷中查看携带信息，例如账号密码，发现信息不一样
3. 定位信息错误在代码中的携带位置并进行检查修改

### 响应报文

`响应报文`：是服务器按照 HTTP 协议要求的`格式`，返回给浏览器的`内容`

响应报文的组成：

- `响应行（状态行）`：协议，`HTTP响应状态码`，状态信息
- `响应头`：以键值对的格式携带的附加信息，比如：`Content-Type`（告诉浏览器，本次返回的内容类型）
- 空行：分割响应头，控制之后的是服务器返回的资源
- `响应体：返回的资源`

HTTP 响应状态码：用来表明请求`是否成功`完成，比如：`404（服务器找不到资源）`

查看响应报文路径：开发者工具（检查） → Network（网络）→ Fetch/XHR → 点击对应请求 → Headers（标头）/ Response（响应）/ Preview（预览）

| 状态码 |          说明          |
| :----: | :--------------------: |
|  1XX   |          信息          |
| `2XX`  |         `成功`         |
|  3XX   |       重定向消息       |
| `4XX`  | `客户端错误（浏览器）` |
|  5XX   |       服务端错误       |

## 接口文档

`接口文档`：描述`接口`的文章（一般是`后端工程师`，编写和提供）

`接口`：使用 AJAX 和 服务器通讯时，使用的 `URL，请求方法，以及参数`

## form-serialize 插件

我们前面收集表单元素的值，是一个个标签获取的

我们可以使用 form-serialize 插件提供的 serialize 函数做到`快速收集`表单元素的值

form-serialize 插件语法：

1. 引入 form-serialize 插件到自己网页中
2. 使用 serialize 函数
   - 参数1：要获取的 form 表单标签对象
     + 要求表单元素需要有 `name 属性`-用来作为收集的数据中`属性名`
     + 建议 name 属性的值最好和接口文档参数名一致
   - 参数2：配置对象
     - hash：设置获取数据的结构
       - true - 收集出来的是一个 JS 对象结构（推荐）
       - false - 收集出来的是一个查询字符串格式
     - empty：设置是否获取空值
       - true - 收集空值
       - false - 不收集空值

语法：

~~~js
const form = document.querySelector('form')
const data = serialize(from, { hash: true, empty: true})
~~~

## Bootstrap 弹框

功能：不离开当前页面，显示单独内容，供用户操作

单纯显示/隐藏用属性控制，有额外逻辑代码用 JS 控制，例如填写表单

### 属性控制

 Bootstrap 弹框的使用：

1. 先引入 bootstrap.css 和 bootstrap.js 到自己网页中
2. 准备`弹框标签`，确认结构（可以从 Bootstrap 官方文档的 Modal 里复制基础例子）- 运行到网页后，逐一对应标签和弹框每个部分对应关系
3. 通过`自定义属性`，通知弹框的`显示`和`隐藏`（默认隐藏）

语法：

```html
<button data-bs-toggle="modal" data-bs-target="css选择器">
  显示弹框
</button>

<button data-bs-dismiss="modal">Close</button>
```
### JS 控制

 JS 方式控制：当我显示之前，隐藏之前，需要执行一些 JS 逻辑代码，就需要引入 JS 控制弹框显示/隐藏的方式了，例如：点击编辑姓名按钮，在弹框显示之前，在输入框填入默认姓名、点击保存按钮，在弹框隐藏之前，获取用户填入的名字并打印

所以在现实和隐藏之前，需要执行 JS 代码逻辑，就使用 JS 方式 控制 Bootstrap 弹框显示和隐藏

语法如下：

```js
// 创建弹框对象
const modalDom = document.querySelector('css选择器')
const modal = new bootstrap.Modal(modelDom)

// 显示弹框
modal.show()
// 隐藏弹框
modal.hide()
```

## XX管理

自己的数据：给自己起个`外号`，并告诉服务器，默认会有三条数据，基于这三条数据做的`增删改查`

分析步骤和对应的视频模块

- 先学习 Bootstrap 弹框的使用（因为添加和编辑需要这个窗口来承载表单）
- 先做渲染列表（这样做添加和编辑以及删除可以看到数据变化，所以先做渲染）
- 再做新增功能 
- 再做删除功能
- 再做编辑功能（注意：编辑和新增是2套弹框-后续做项目我们再用同1个弹框）

### 渲染列表

步骤：

1. 获取数据
2. 渲染数据

> 因为默认展示列表，新增，修改，删除后都要重新获取并刷新列表，所以把获取数据渲染数据的代码封装在一个函数内，方便复用

### 新增

步骤：

1. 新增弹框（控制显示和隐藏）（基于 Bootstrap 弹框和准备好的表单-用属性和 JS 方式控制）
2. 在点击保存按钮时，收集数据&提交保存
3. 刷新-列表）（重新调用下之前封装的获取并渲染列表的函数）

### 删除

步骤：

1. 给删除元素，绑定点击事件（事件委托方式并判断点击的是删除元素才走删除逻辑代码），并获取到要删除的数据id
2. 基于 axios 和接口文档，调用删除接口，让服务器删除这条数据
3. 重新获取并刷新列表

### 编辑

编辑数据的核心思路：

1. 给编辑元素，绑定点击事件（事件委托方式并判断点击的是编辑元素才走编辑逻辑代码），并获取到要编辑的数据id
2. 基于 axios 和接口文档，调用查询详情接口，获取正在编辑的数据，并回显到表单中（页面上的数据是在用户的浏览器中不够准备，所以只要是查看数据都要从服务器获取）
3. 收集并提交保存修改数据，并重新从服务器获取列表刷新页面

### 总结

渲染数据（查）

> 核心思路：获取数据 -> 渲染数据

新增数据（增）

> 核心思路：准备页面标签 -> 收集数据提交（必须） -> 刷新页面列表（可选）

删除图书（删）

> 核心思路：绑定点击事件（获取要删除的图书唯一标识） -> 调用删除接口（让服务器删除此数据） -> 成功后重新获取并刷新列表

编辑图书（改）

> 核心思路：准备编辑图书表单 -> 表单回显正在编辑的数据 -> 点击修改收集数据 -> 提交到服务器保存 -> 重新获取并刷新列表

## 图片上传

图片上传：就是把本地的图片上传到网页上显示

图片上传先依靠文件选择元素获取用户选择的本地文件，接着提交到服务器保存，服务器会返回图片的 url 网址，然后把网址加载到 img 标签的 src 属性中即可显示

因为浏览器保存是临时的，如果你想随时随地访问图片，需要上传到服务器上

图片上传步骤：

1. 先获取`图片文件`对象

2. 使用 `FormData` 表单数据对象装入（因为图片是文件而不是以前的数字和字符串了所以传递文件一般需要放入 FormData 以键值对-文件流的数据传递（可以查看请求体-确认请求体结构）

   ```js
   const fd = new FormData()
   fd.append(参数名, 值)
   ```

3. 提交表单数据对象，使用服务器返回`图片 url 网址`

## 网站-更换背景图

网站更换背景图如何实现呢，并且保证刷新后背景图还在？具体步骤：

1. 先获取到用户选择的背景图片，上传并把服务器返回的图片 url 网址设置给 body 背景
2. 上传成功时，保存图片 url 网址到 localStorage 中
3. 网页运行后，获取 localStorage 中的图片的 url 网址使用（并判断本地有图片 url 网址字符串才设置）

## 个人信息设置

### 信息渲染

注意：还是需要准备一个外号，因为想要查看自己对应的用户信息，不想被别人影响

步骤：

1. 获取数据
2. 渲染数据到页面

### 头像修改

实现步骤如下：

1. 获取到用户选择的头像文件
2. 调用头像修改接口，并除了头像文件外，还要在 FormData 表单数据对象中携带外号
3. 提交到服务器保存此用户对应头像文件，并把返回的头像图片 url 网址设置在页面上

注意：重新刷新重新获取，已经是修改后的头像了（证明服务器那边确实保存成功）

### 信息修改

1. 收集表单数据
2. 提交到服务器保存-调用用户信息更新接口（注意请求方法是 PUT）代表数据更新的意思

### 提示框

bootstrap 的 toast 提示框和 modal 弹框使用很像，语法如下：

1. 先准备对应的标签结构（模板里已有）

2. 设置延迟自动消失的时间

   ```html
   <div class="toast" data-bs-delay="1500">
     提示框内容
   </div>
   ```

3. 使用 JS 的方式，在 axios 请求响应成功时，展示结果

   ```js
   // 创建提示框对象
   const toastDom = document.querySelector('css选择器')
   const toast = new bootstrap.Toast(toastDom)

   // 显示提示框
   toast.show()
   ```

## XMLHttpRequest - 基础使用

XMLHttpRequest （XHR）对象用于与服务器交互，通过 XMLHttpRequest 可以在不刷新页面的情况下请求特定 URL，获取数据。这允许网页在不影响用户操作的情况下，更新页面的局部内容。XMLHttpRequest 在 AJAX 编程中被大量使用。

axios 内部采用 XMLHttpRequest 与服务器交互，是对 XHR 相关代码进行了封装，让我们只关心传递的接口参数

学习 XHR 也是为了掌握使用 XHR 与服务器进行数据交互，了解 axios 内部与服务器交互过程的真正原理

步骤：

1. 创建 XMLHttpRequest 对象
2. 配置`请求方法`和请求` url `地址
3. 监听 loadend 事件，接收`响应结果`
4. 发起请求

语法：

```js
const xhr = new XMLHttpRequest()
xhr.open('请求方法', '请求url网址')
xhr.addEventListener('loadend', () => {
  // 响应结果
  console.log(xhr.response)
})
xhr.send()
```

   ### 查询参数

查询参数：浏览器提供给服务器的`额外信息`，让服务器返回浏览器想要的数据

查询参数原理要携带的位置和语法：http://xxxx.com/xxx/xxx?参数名1=值1&参数名2=值2

所以，原生 XHR 需要自己在 url 后面携带查询参数字符串，没有 axios 帮助我们把 params 参数拼接到 url 字符串后面了

但是多个查询参数，如果自己拼接很麻烦，这里用 URLSearchParams 把参数对象转成“参数名=值&参数名=值“格式的字符串，语法如下：

```js
// 1. 创建 URLSearchParams 对象
const paramsObj = new URLSearchParams({
  参数名1: 值1,
  参数名2: 值2
})

// 2. 生成指定格式查询参数字符串
const queryString = paramsObj.toString()
// 结果：参数名1=值1&参数名2=值2
```

### 数据提交

步骤和语法：

1. 设置`请求头` Content-Type：application/json，来告诉服务器端，我们发过去的内容类型是 JSON 字符串，让他转成对应数据结构取值使用

2. `请求体`数据需要我们自己把 JS 对象转成 JSON 字符串

3. 原生 XHR 需要在 send 方法调用时，传入请求体携带

   ```js
   const xhr = new XMLHttpRequest()
   xhr.open('请求方法', '请求url网址')
   xhr.addEventListener('loadend', () => {
     console.log(xhr.response)
   })

   // 1. 告诉服务器，我传递的内容类型，是 JSON 字符串
   xhr.setRequestHeader('Content-Type', 'application/json')
   // 2. 准备数据并转成 JSON 字符串
   const user = { username: 'itheima007', password: '7654321' }
   const userStr = JSON.stringify(user)
   // 3. 发送请求体数据
   xhr.send(userStr)
   ```

## Promise

Promise 对象用于表示一个`异步`操作的`最终状态`（或失败）及其`结果值`

Promise 的好处：

- 成功和失败状态可以关联对应处理函数
- 逻辑更清晰
- 了解 axios 函数内部运作的机制
- 能解决回调函数地狱问题

### Promise 管理异步任务

语法：

```js
// 1. 创建 Promise 对象
const p = new Promise((resolve, reject) => {
 // 2. 执行异步任务-并传递结果
 // 成功调用: resolve(值) 触发 then() 执行
 // 失败调用: reject(值) 触发 catch() 执行
})
// 3. 接收结果
p.then(result => {
 // 成功
}).catch(error => {
 // 失败
})
```

示例代码：

```js
/**
 * 目标：使用Promise管理异步任务
*/
// 1. 创建Promise对象
const p = new Promise((resolve, reject) => {
  // 2. 执行异步代码
  setTimeout(() => {
    // resolve('模拟AJAX请求-成功结果')
    reject(new Error('模拟AJAX请求-失败结果'))
  }, 2000)
})

// 3. 获取结果
p.then(result => {
  console.log(result)
}).catch(error => {
  console.log(error)
})
```

### Promise的三种状态

了解 Promise 的三种状态可以知道 Promise 对象如何`关联`的`处理函数`，以及代码的执行顺序

Promise 的三种状态：

> 每个 Promise 对象必定处于以下三种状态之一

1. `待定`（pending）：初始状态，既没有被兑现，也没有被拒绝
2. `已兑现`（fulfilled）：操作成功完成
3. `已拒绝`（rejected）：操作失败

> 状态的英文字符串，可以理解为 Promise 对象内的字符串标识符，用于判断什么时候调用哪一个处理函数

Promise 的状态改变有什么用：调用对应函数，改变 Promise 对象状态后，内部触发对应回调函数传参并执行

注意：每个 Promise 对象一旦被`兑现/拒绝`，那就是`已敲定`了，状态无法再被改变

### 链式调用

概念：依靠 then() 方法会返回一个`新生成的 Promise 对象`特性，继续串联下一环任务，直到结束

细节：then() 回调函数中的`返回值`，会影响新生成的 Promise 对象`最终状态和结果`

好处：通过链式调用，解决回调函数嵌套问题

```js
/**
 * 目标：掌握Promise的链式调用
 * 需求：把省市的嵌套结构，改成链式调用的线性结构
*/
// 1. 创建Promise对象-模拟请求省份名字
const p = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('北京市')
  }, 2000)
})

// 2. 获取省份名字
const p2 = p.then(result => {
  console.log(result)
  // 3. 创建Promise对象-模拟请求城市名字
  // return Promise对象最终状态和结果，影响到新的Promise对象
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(result + '--- 北京')
    }, 2000)
  })
})

// 4. 获取城市名字
p2.then(result => {
  console.log(result)
})

// then()原地的结果是一个新的Promise对象
console.log(p2 === p)
```

### all 静态方法

概念：合并多个 Promise 对象，等待所有`同时成功`完成（或某一个失败），做后续逻辑

语法：

```js
const p = Promise.all([Promise对象, Promise对象, ...])
p.then(result => {
  // result 结果: [Promise对象成功结果, Promise对象成功结果, ...]
}).catch(error => {
  // 第一个失败的 Promise 对象，抛出的异常对象
})
```

## 封装_简易axios

### 基础封装

步骤：

1. 定义 myAxios 函数，接收`配置对象`，返回 `Promise 对象`
2. 发起 `XHR 请求，默认请求方法`为 GET
3. 调用成功/失败的处理程序
4. 使用 myAxios 函数，获取省份列表展示

核心语法：

```js
function myAxios(config) {
  return new Promise((resolve, reject) => {
    // XHR 请求
    // 调用成功/失败的处理程序
    const xhr = new XMLHttpRequest()
    xhr.open(config.method || 'get', config.url)
    xhr.addEventListener('loadend', () => {
      if(xhr.status >= 200 && xhr.status < 300) {
        resolve(JSON.parse(xhr.response))
      }else {
        reject(new Error(xhr.response))
      }
    })
    xhr.send()
  })
}

myAxios({
  url: '目标资源地址'
}).then(result => {
    
}).catch(error => {
    
})
```

### 支持传递查询参数

步骤：

1. myAxios 函数调用后，传入 `params` 选项
2. 基于 URLSearchParams 转换`查询参数字符串`
3. 使用自己封装的myAxios函数展示列表

~~~js
function myAxios(config) {
  return new Promise((resolve, reject) => {
    // XHR 请求
    // 调用成功/失败的处理程序
    const xhr = new XMLHttpRequest()
    if(config.params) {
      const paramsObj = new URLSearchParams(config.params)
      const queryString = paramsObj.toString()
      config.url += `?${queryString}`
    }
    xhr.open(config.method || 'GET', config.url)
    xhr.addEventListener('loadend', () => {
      if (xhr.status >= 200 && xhr.status < 300) {
        resolve(JSON.parse(xhr.response))
      } else {
        reject(new Error(xhr.response))
      }
    })
    xhr.send()
  })
}

myAxios({
  url: '目标资源地址',
  params: {
    参数名1: 值1,
    参数名2: 值2
  }
})
~~~

### 支持传递请求体数据

步骤：

1. myAxios 函数调用后，判断 data 选项
2. 转换数据类型，在 send 方法中发送
3. 使用函数

~~~js
function myAxios(config) {
  return new Promise((resolve, reject) => {
    // XHR 请求
    // 调用成功/失败的处理程序
    const xhr = new XMLHttpRequest()
    if (config.params) {
      const paramsObj = new URLSearchParams(config.params)
      const queryString = paramsObj.toString()
      config.url += `?${queryString}`
    }
    xhr.open(config.method || 'GET', config.url)

    xhr.addEventListener('loadend', () => {
      if (xhr.status >= 200 && xhr.status < 300) {
        resolve(JSON.parse(xhr.response))
      } else {
        reject(new Error(xhr.response))
      }
    })
    if(config.data) {
      const jsonStr = JSON.stringify(config.data)
      xhr.setRequestHeader('Content-Type', 'application/json')
      xhr.send(jsonStr)
    } else {
      xhr.send()
    }
  })
}

myAxios({
  url: '目标资源地址',
  data: {
    参数名1: 值1,
    参数名2: 值2
  }
})
~~~

## 同步代码和异步代码

同步代码：逐行执行，需`原地等待结果`后，才继续向下执行

异步代码：调用后`耗时`，不阻塞代码继续执行（不必原地等待），在将来完成后触发`回调函数`传递结果

回答代码打印顺序：发现异步代码接收结果，使用的都是回调函数

```js
const result = 0 + 1
console.log(result)
setTimeout(() => {
  console.log(2)
}, 2000)
document.querySelector('.btn').addEventListener('click', () => {
  console.log(3)
})
document.body.style.backgroundColor = 'pink'
console.log(4)	//	1,4,2,3
```

## 回调函数地狱

概念：在回调函数中`嵌套回调函数`，一直嵌套下去就形成了回调函数地狱

缺点：可读性差，异常无法捕获，耦合性严重，牵一发动全身

```js
axios({ url: 'http://hmajax.itheima.net/api/province' }).then(result => {
  const pname = result.data.list[0]
  document.querySelector('.province').innerHTML = pname
  // 获取第一个省份默认下属的第一个城市名字
  axios({ url: 'http://hmajax.itheima.net/api/city', params: { pname } }).then(result => {
    const cname = result.data.list[0]
    document.querySelector('.city').innerHTML = cname
    // 获取第一个城市默认下属第一个地区名字
    axios({ url: 'http://hmajax.itheima.net/api/area', params: { pname, cname } }).then(result => {
      document.querySelector('.area').innerHTML = result.data.list[0]
    })
  })
})
```

### 解决回调地狱

目标：使用 Promise 链式调用，解决回调函数地狱问题

做法：每个 Promise 对象中管理一个异步任务，用 then 返回 Promise 对象，串联起来

```js
/**
 * 目标：把回调函数嵌套代码，改成Promise链式调用结构
 * 需求：获取默认第一个省，第一个市，第一个地区并展示在下拉菜单中
*/
let pname = ''
// 1. 得到-获取省份Promise对象
axios({url: 'http://hmajax.itheima.net/api/province'}).then(result => {
  pname = result.data.list[0]
  document.querySelector('.province').innerHTML = pname
  // 2. 得到-获取城市Promise对象
  return axios({url: 'http://hmajax.itheima.net/api/city', params: { pname }})
}).then(result => {
  const cname = result.data.list[0]
  document.querySelector('.city').innerHTML = cname
  // 3. 得到-获取地区Promise对象
  return axios({url: 'http://hmajax.itheima.net/api/area', params: { pname, cname }})
}).then(result => {
  console.log(result)
  const areaName = result.data.list[0]
  document.querySelector('.area').innerHTML = areaName
})
```

## async 函数和 await

概念：在 async 函数内，使用 await 关键字取代 then 函数，`等待`获取 Promise 对象`成功状态的结果值`

做法：使用 async 和 await 解决回调地狱问题，使用 await 替代 then 的方法

```js
/**
 * 目标：掌握async和await语法，解决回调函数地狱
 * 概念：在async函数内，使用await关键字，获取Promise对象"成功状态"结果值
 * 注意：await必须用在async修饰的函数内（await会阻止"异步函数内"代码继续执行，原地等待结果）
*/
// 1. 定义async修饰函数
async function getData() {
  // 2. await等待Promise对象成功的结果
  const pObj = await axios({url: 'http://hmajax.itheima.net/api/province'})
  const pname = pObj.data.list[0]
  const cObj = await axios({url: 'http://hmajax.itheima.net/api/city', params: { pname }})
  const cname = cObj.data.list[0]
  const aObj = await axios({url: 'http://hmajax.itheima.net/api/area', params: { pname, cname }})
  const areaName = aObj.data.list[0]


  document.querySelector('.province').innerHTML = pname
  document.querySelector('.city').innerHTML = cname
  document.querySelector('.area').innerHTML = areaName
}

getData()
```

### 捕获错误

try 和 catch 的作用：语句标记要尝试的语句块，并指定一个出现异常时抛出的响应

```js
try {
  // 要执行的代码
} catch (error) {
  // error 接收的是，错误消息
  // try 里代码，如果有错误，直接进入这里执行
}
```

> try 里有报错的代码，会立刻跳转到 catch 中

尝试把代码中 url 地址写错，运行观察 try catch 的捕获错误信息能力

```js
/**
 * 目标：async和await_错误捕获
*/
async function getData() {
  // 1. try包裹可能产生错误的代码
  try {
    const pObj = await axios({ url: 'http://hmajax.itheima.net/api/province' })
    const pname = pObj.data.list[0]
    const cObj = await axios({ url: 'http://hmajax.itheima.net/api/city', params: { pname } })
    const cname = cObj.data.list[0]
    const aObj = await axios({ url: 'http://hmajax.itheima.net/api/area', params: { pname, cname } })
    const areaName = aObj.data.list[0]

    document.querySelector('.province').innerHTML = pname
    document.querySelector('.city').innerHTML = cname
    document.querySelector('.area').innerHTML = areaName
  } catch (error) {
    // 2. 接着调用catch块，接收错误信息
    // 如果try里某行代码报错后，try中剩余的代码不会执行了
    console.dir(error)
  }
}

getData()
```

## 事件循环

事件循环（EventLoop）：掌握后知道 JS 是如何安排和运行代码的

作用：事件循环负责执行代码，收集和处理事件以及执行队列中的子任务

原因：JavaScript 单线程（某一刻只能执行一行代码），为了让耗时代码不阻塞其他代码运行，设计了`事件循环模型`

概念：`执行代码`和收集异步任务的模型，在调用栈空闲，反复调用任务队列里回调函数的执行机制，就叫事件循环

```js
/**
 * 目标：阅读并回答执行的顺序结果
*/
console.log(1)
setTimeout(() => {
  console.log(2)
}, 0)
console.log(3)
setTimeout(() => {
  console.log(4)
}, 2000)
console.log(5)	//	1, 3, 5, 2, 4
```

## 宏任务与微任务

ES6 之后引入了 Promise 对象， 让 JS 引擎也可以发起异步任务

异步任务划分为了

- `宏任务`：由`浏览器`环境执行的异步代码
- `微任务`：由 `JS 引擎`环境执行的异步代码

Promise 本身是同步的，而 then 和 catch `回调函数`是异步的

`微任务`队列清空`后`才会执行下一个`宏任务`

宏任务和微任务具体划分：

|       任务（代码）        | 执行所在环境 |
| :-----------------------: | :----------: |
| JS 脚本执行事件（script） |    浏览器    |
| setTimeout / setInterval  |    浏览器    |
|     AJAX 请求完成事件     |    浏览器    |
|      用户交互事件等       |    浏览器    |
|    Promise 对象.then()    |   JS 引擎    |

事件循环模型

```js
/**
 * 目标：阅读并回答打印的执行顺序
*/
console.log(1)
setTimeout(() => {
  console.log(2)
}, 0)
const p = new Promise((resolve, reject) => {
  console.log(3)
  resolve(4)
})
p.then(res => {
  console.log(res)
})
console.log(5)	//	1, 3, 5, 4, 2
```

> 注意：宏任务每次在执行同步代码时，产生微任务队列，清空微任务队列任务后，微任务队列空间释放！
>
> 下一次宏任务执行时，遇到微任务代码，才会再次申请微任务队列空间放入回调函数消息排队
>
> 总结：一个宏任务包含微任务队列，他们之间是包含关系，不是并列关系

## 经典面试题

~~~js
console.log(1)
setTimeout(() => {
  console.log(2)
  const p = new Promise(resolve => resolve(3))
  p.then(result => console.log(result))
}, 0)
const p = new Promise(resolve => {
  setTimeout(() => {
    console.log(4)
  }, 0)
  resolve(5)
})
p.then(result => console.log(result))
const p2 = new Promise(resolve => resolve(6))
p2.then(result => console.log(result))
console.log(7)		// 1 7 5 6 2 3 4
~~~

# 实战项目：数据管理平台

技术：

基于 `Bootstrap` 搭建网站标签和样式

集成 `wangEditor` 插件实现富文本编辑器

使用原生 JS 完成增删改查等业务

基于 axios 与黑马头条线上接口交互

使用 axios 拦截器进行权限判断



目录管理：建议这样管理，方便查找和扩展

assets：资源文件夹（图片，字体等）

lib：资料文件夹（第三方插件，例如：form-serialize）

page：页面文件夹

utils：实用程序文件夹（工具插件）

## 验证码登录

步骤：

1.在 utils/request.js 配置 axios 请求`基地址`

​	作用：提取公共前缀地址，配置后 axios 请求时都会 baseURL + url

```js
axios.defaults.baseURL = 'http://geek.itheima.net'
```

2.收集手机号和验证码数据

3.基于 axios 调用验证码登录接口

4.使用 Bootstrap 的 Alert 警告框反馈结果给用户



手机号+验证码，登录流程：

1.输入手机号，点击发送验证码

2.携带手机号，调用服务器发送`短信验证码接口`

3.为此手机号生成验证码，记录生成时间，并存在服务器

4.携带手机号，验证码调用运营商接口

5.通过基站给指定手机号，发送验证码短信（无连接）

6.发送成功

7.返回验证码发送成功

8.根据手机短信填入验证码到页面

9.携带手机号，验证码，调用`验证码登录`接口

10.服务器接收手机号和验证码与之前第3步生成的记录对比，判断验证码是否正确，以及是否在有效期内并返回，登录成功/失败的结果

11.登录结果反馈给用户

## token

概念：访问权限的`令牌`，本质上是一串`字符串`

创建：正确登录后，由后端签发并返回

作用：判断是否有`登录状态`等，控制访问权限

注意：`前端`只能判断token`有无`，而`后端`能通过解密可以提取ttoken字符串的原始信息，判断token的`有效性`

### token的使用

目标：只有登录状态，才能访问内容页面

步骤：

1.在 utils/auth.js 中判断无 token 令牌字符串，则强制跳转到登录页（手动修改地址栏测试）

2.在登录成功后，保存 token 令牌字符串到本地，再跳转到首页（手动修改地址栏测试）

```js
const token = localStorage.getItem('token')
// 没有 token 令牌字符串，则强制跳转登录页
if (!token) {
  location.href = '../login/index.html'
}
```

## 个人信息设置和 axios 请求拦截器

需求：设置用户昵称

语法：axios 可以在 headers 选项传递请求头参数

问题：很多接口，都需要携带 token 令牌字符串

解决：在[请求拦截器](https://www.axios-http.cn/docs/interceptors)统一设置公共 headers 选项

​	axios 请求拦截器：发起请求之前，触发的配置函数，对   `请求参数`进行额外配置

对应代码：

```js
axios({
  url: '目标资源地址',
  headers: {
    Authorization: `Bearer ${localStorage.getItem('token')}`
  }
})
```

```js
axios.interceptors.request.use(function (config) {
  // 在发送请求之前做些什么
  return config
}, function (error) {
  // 对请求错误做些什么
  return Promise.reject(error)
})
```

```js
axios({
  // 个人信息
  url: '/v1_0/user/profile'
}).then(result => {
  // result：服务器响应数据对象
}).catch(error => {
    
})
```

```js
// 添加请求拦截器
axios.interceptors.request.use(function (config) {
  const token = location.getItem('token')  
  token && config.headers.Authorization = `Bearer ${token}`
  // 在发送请求之前做些什么
  return config
}, function (error) {
  // 对请求错误做些什么
  return Promise.reject(error)
})
```

##axios 响应拦截器和身份验证失败

axios 响应拦截器：响应回到 then/catch 之前，触发的`拦截函数`，对`响应结果统一处理`

例如：身份验证失败，统一判断并做处理

~~~js
// 添加响应拦截器
axios.interceptors.response.use(function (response) {
    // 2xx 范围内的状态码都会触发该函数。
    // 对响应数据做点什么
    return response;
  }, function (error) {
    // 超出 2xx 范围的状态码都会触发该函数。
    // 对响应错误做点什么，例如：判断响应状态为 401 代表身份验证失败
    if (error?.response?.status === 401) {
      alert('登录状态过期，请重新登录')
      localStorage.clear()
      location.href = '../login/index.html'
    }
    return Promise.reject(error);
  });
~~~

##axios 响应结果

目标：axios 直接接收服务器返回的响应结果

思路：其实就是在响应拦截器里，response.data 把后台返回的数据直接取出来统一返回给所有使用这个 axios 函数的逻辑页面位置的 then 的形参上

好处：可以让逻辑页面少点一层 data 就能拿到后端返回的真正数据对象

对应代码如下：

```js
// 添加响应拦截器
axios.interceptors.response.use(function (response) {
  // 2xx 范围内的状态码都会触发该函数。
  // 对响应数据做点什么，例如：直接返回服务器的响应结果对象
  const result = response.data
  return result;
}, function (error) {
  // 超出 2xx 范围的状态码都会触发该函数。
  // 对响应错误做点什么，例如：判断响应状态为 401 代表身份验证失败
  if (error?.response?.status === 401) {
    alert('登录状态过期，请重新登录')
    window.location.href = '../login/index.html'
  }
  return Promise.reject(error);
});
```

## 发布文章

###富文本编辑器

富文本：带样式，多格式的文本，在前端一般使用标签配合内联样式实现

富文本编辑器：用于编写富文本内容的容器

目标：发布文章页，富文本编辑器的集成

使用：wangEditor 插件

[步骤](https://www.wangeditor.com/v5/getting-started.html)：参考文档

1.引入 CSS 定义样式

2.定义 HTML 结构

3.引入 JS 创建编辑器

4.监听内容改变，保存在隐藏文本域（便于后期收集）

### 频道列表

目标：展示频道列表，供用户选择

步骤：

1. `获取`频道列表数据
2. `展示`到下拉菜单中

### 封面设置

目标：文章封面的设置

步骤：

1. 准备标签`结构和样式`
2. `选择文件`并保存在 FormData
3. 单独`上传`图片并得到`图片 URL 地址`
4. `回显`并`切换` img 标签展示（隐藏 + 号上传标签）

注意：图片地址临时存储在 img 标签上，并未和文章关联保存

### 收集并保存

目标：收集文章内容，并提交保存

步骤：

1. 基于 form-serialize 插件`收集`表单数据对象
2. 基于 axios 提交到服务器`保存`
3. 调用 Alert 警告框`反馈`结果给用户
4. `重置表单`并跳转到列表页


## 内容管理

### 文章列表展示

目标：获取文章列表并展示

步骤：

1. 准备查询`参数对象 `
2. `获取`文章列表数据
3. `展示`到指定的标签结构中

### 筛选功能

目标：根据筛选条件，获取匹配数据展示

步骤：

1.设置频道列表数据

2.监听筛选条件改变，保存查询信息到`查询参数对象`

3.点击筛选时，传递`查询参数对象`到服务器

4.获取匹配数据，覆盖到页面展示

### 分页功能

目标：完成文章列表，分页管理功能

步骤：

1.保存并设置文章`总条数`

2.点击下一页，做`临界值判断`，并`切换页码参数`请求最新数据

3.点击上一页，做临界值判断，并切换页码参数`请求最新数据`

### 删除功能

目标：完成删除文章功能

步骤：

1. 关联`文章 id `到删除图标
2. 点击删除时，获取文章 id
3. 调用`删除接口`，传递文章 id 到服务器
4. `重新获取`文章列表，并覆盖展示


#### 删除最后一条

目标：在删除`最后一页，最后一条`时有 Bug

解决：

1. 删除成功时，判断 `DOM 元素只剩一条`，让当前页码 `page--`
2. 注意，当前页码为 1 时不能继续向前翻页
3. 重新设置页码数，获取最新列表展示

### 编辑文章

#### 回显

目标：编辑文章时，回显数据到表单

步骤：

1. 页面`跳转传参`（URL 查询参数方式）
2. 发布文章页面`接收参数判断`（共用同一套表单）
3. 修改标题和按钮文字
4. 获取文章详情数据并回显表单

对应代码：

```js
const params = `?id=1001&name=xiaoli`
// 查询参数字符串 => 查询参数对象
const result = new URLSearchParams(params)
// 需要遍历使用
result.forEach((value, key) => { 
  console.log(value, key)
  // 1001 id
  // xiaoli name
})
```

#### 保存

目标：确认修改，保存文章到服务器

步骤：

1. `判断`按钮文字，区分业务（因为共用一套表单）
2. 调用编辑文章接口，保存信息到服务器
3. 基于 Alert 反馈结果消息给用户

### 退出登录

目标：完成退出登录效果

步骤：

1.绑定点击事件

2.清空本地缓存，跳转到登录页面



















