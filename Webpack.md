# Webpack模块打包工具

## Webpack 简介以及体验

Webpack 是一个静态模块打包工具，从入口构建依赖图，打包有关的模块，最后用于展示你的内容

静态模块：编写代码过程中的，html，css， js，图片等固定内容的文件

打包过程，注意：只有和入口有直接/间接引入关系的模块，才会被打包

`打包`：把静态模块内容，压缩，这个和，转译等（前端工程化）

- 把 less/sass 转成 css 代码
- 把 ES6+ 降级成 ES5 等
- 支持多种模块文件类型，多种模块标准语法

为何不学 vite？

> 现在很多项目还是基于 Webpack 来进行构建的，并为Vue、React脚手架使用做铺垫

体验 Webpack 打包 2 个 JS 文件内容

需求：封装 utils 包，校验手机号和验证码长度，在 `src/index.js` 中使用，使用 Webpack 打包

步骤：

1. 新建项目文件夹 Webpack_study，初始化包环境，得到 package.json 文件

   ```bash
   npm init -y
   ```

2. 新建 src `源代码`文件夹（书写代码）包括 utils/check.js 封装用户名和密码长度函数，引入到 src/index.js 进行使用

   - src/utils/check.js

     ```js
     // 封装校验手机号长度和校验验证码长度的函数
     export const checkPhone = phone => phone.length === 11
     export const checkCode = code => code.length === 6
     ```

   - src/index.js

     ```js
     /**
      * 目标1：体验 webpack 打包过程
      */
     // 1.1 准备项目和源代码
     import { checkPhone, checkCode } from '../utils/check.js'
     console.log(checkPhone('13900002020'))
     console.log(checkCode('123123123123'))
     // 1.2 准备 webpack 打包的环境
     // 1.3 运行自定义命令打包观察效果（npm run 自定义命令）
     ```

3. 下载 webpack webpack-cli 到当前项目（版本独立），并`配置`局部自定义命令

   ```bash
   npm i webpack webpack-cli --save-dev
   ```

   > 注意：虽然 webpack 是全局软件包，封装的是命令工具，但是为了保证项目之间版本分别独立，所以这次比较特殊，下载到某个项目环境下，但是需要把 webpack 命令配置到 package.json 的 scripts 自定义命令，作为局部命令使用

4. 项目中运行`打包`命令，采用自定义命令的方式（局部命令）

   ```bash
   npm run build
   ```

   > npm run 自定义命令名字
   >
   > 注意：实际上在终端运行的是 build 右侧的具体命名

5. 自动产生 dist 分发文件夹（压缩和优化后，用于最终运行的代码）

## 修改入口和出口

[Webpack 配置]([https://webpack.docschina.org/concepts/#entry](https://webpack.docschina.org/concepts/))：影响 Webpack 打包过程和结果

步骤：

1. 项目根目录，新建 `Webpack.config.js` 配置文件

2. 导出`配置对象`，配置入口，出口文件路径（别忘了修改磁盘文件夹和文件的名字）

   ```js
   const path = require('path');

   module.exports = {
     //  入口
     entry: path.resolve(__dirname,'src/login/index.js'),
     //  出口
     output: {
       path: path.resolve(__dirname, 'dist'),
       filename: './login/index.js',
       clean: true //  生成打包后内容之前，清空输出目录
     },
   };
   ```

3. 重新打包观察

   > 注意：只有和入口有直接/间接引入关系的模块，才会被打包

## 案例-用户登录-长度判断

需求：点击登录按钮，判断手机号和验证码长度是否符合要求

`核心`：Webpack 打包后的代码，作用在前端网页中使用

步骤：

1. 新建 public/login.html 准备网页模板（方便查找标签和后期自动生成 html 文件做准备）

2. 核心 JS 代码写在 src/login/index.js 文件

   ```js
   /**
    * 目标3：用户登录-长度判断案例
    *  3.1 准备用户登录页面
    *  3.2 编写核心 JS 逻辑代码
    *  3.3 打包并手动复制网页到 dist 下，引入打包后的 js，运行
    */
   // 3.2 编写核心 JS 逻辑代码
   document.querySelector('.btn').addEventListener('click', () => {
     const phone = document.querySelector('.login-form [name=mobile]').value
     const code = document.querySelector('.login-form [name=code]').value

     if (!checkPhone(phone)) {
       console.log('手机号长度必须是11位')
       return
     }

     if (!checkCode(code)) {
       console.log('验证码长度必须是6位')
       return
     }

     console.log('提交到服务器登录...')
   })
   ```

   1. 运行自定义命令，让 Webpack 打包 JS 代码
   2. 手动复制 public/login.html 到 dist 下，手动引入打包后的 JS 代码文件，运行 dist/login.html 在浏览器查看效果



## 自动生成 html 文件

[插件 html-webpack-plugin 作用](https://webpack.docschina.org/plugins/html-webpack-plugin/)：在 Webpack 打包时生成 html 文件，并引入其他打包后的资源

步骤：

1. 下载 `html-webpack-plugin` 本地软件包到项目中

   ```bash
   npm i html-webpack-plugin --save-dev
   ```

2. `配置` webpack.config.js 让 Webpack 拥有插件功能

   ```js
   // ...
   const HtmlWebpackPlugin = require('html-webpack-plugin')

   module.exports = {
     // ...
     plugins: [
       new HtmlWebpackPlugin({
         template: path.resolve(__dirname,'public/login.html'), // 模板文件
         filename: path.resolve(__dirname,'dist/login/index.html') // 输出文件
       })
     ],
   }
   ```

3. 指定以 public/login.html 为模板复制到 dist/login/index.html，并自动引入其他打包后资源

4. 运行`打包`命令，观察打包后 dist 文件夹下内容并运行查看效果

## 打包 css 代码

注意：Webpack 默认只识别 JS 和 JSON 文件内容，所以想要让 Webpack 识别更多不同内容，需要使用加载器

介绍需要的 2 个加载器来辅助 Webpack 才能打包 css 代码

- [加载器 css-loader](https://webpack.docschina.org/loaders/css-loader/)：解析 css 代码
- [加载器 style-loader](https://webpack.docschina.org/loaders/style-loader/)：把解析后的 css 代码插入到 DOM（style 标签之间）

步骤：

1. 准备 css 文件`代码`引入到 src/login/index.js 中（压缩转译处理等）

   ```js
   /**
    * 目标5：打包 css 代码
    *  5.1 准备 css 代码，并引入到 js 中
    *  5.2 下载 css-loader 和 style-loader 本地软件包
    *  5.3 配置 webpack.config.js 让 Webpack 拥有该加载器功能
    *  5.4 打包后观察效果
    */
   // 5.1 准备 css 代码，并引入到 js 中
   import 'bootstrap/dist/css/bootstrap.min.css'
   import './index.css'
   ```

   > 注意：这里只是引入代码内容让 Webpack 处理，不需定义变量接收在 JS 代码中继续使用，所以没有定义变量接收

2. `下载` css-loader 和 style-loader 本地软件包

   ```bash
   npm i css-loader style-loader --save-dev
   ```

3. `配置` webpack.config.js 让 Webpack 拥有该加载器功能

   ```js
   // ...

   module.exports = {
     // ...
     module: { // 加载器
       rules: [ // 规则列表
         {
           test: /\.css$/i, // 匹配 .css 结尾的文件
           use: ['style-loader', 'css-loader'], // 使用从后到前的加载器来解析 css 代码和插入到 DOM
         }
       ]
     }
   };
   ```

4. 下载 bootstrap 并在 .js 文件中配置

   ```js
   import "bootstrap/dist/css/bootstrap.min.css"
   ```

5. 打包后运行 dist/login/index.html 观察效果，看看准备好的样式是否作用在网页上

## 优化-提取 css 代码

需求：让 webpack 把 css 代码内容字符串单独提取到 dist 下的 css 文件中

插件mini-css-extract-plugin ：提取 css 代码

好处：css 文件可以被浏览器缓存，减少 JS 文件体积，让浏览器并行下载 css 和 js 文件

步骤：

1. `下载` mini-css-extract-plugin 插件软件包到本地项目中

   ```bash
   npm i --save-dev mini-css-extract-plugin
   ```

2. `配置` webpack.config.js 让 Webpack 拥有该插件功能

   ```js
   // ...
   const MiniCssExtractPlugin = require("mini-css-extract-plugin")

   module.exports = {
     // ...
     module: {
       rules: [
         {
           test: /\.css$/i,
           // use: ['style-loader', 'css-loader']
           use: [MiniCssExtractPlugin.loader, "css-loader"],
         },
       ],
     },
     plugins: [
       // ...
       new MiniCssExtractPlugin()
     ]
   };
   ```

   1. 打包后观察效果

      > 注意：不能和 style-loader 一起使用

## 优化-压缩过程

需求：把提出的 css 文件内样式代码压缩

解决：使用css-minimizer-webpack-plugin 插件来实现

步骤：

1. `下载` mini-css-extract-plugin 插件软件包到本地项目中

   ```bash
   npm i css-minimizer-webpack-plugin --save-dev 
   ```

2. `配置` webpack.config.js 让 Webpack 拥有该插件功能

   ```js
   // ...
   const CssMinimizerPlugin = require("css-minimizer-webpack-plugin");

   module.exports = {
     // ...
     // 优化
     optimization: {
       // 最小化
       minimizer: [
         // 在 webpack@5 中，你可以使用 `...` 语法来扩展现有的 minimizer（即 
         // `terser-webpack-plugin`），将下一行取消注释（保证 JS 代码还能被压缩处理）
         `...`,
         new CssMinimizerPlugin(),
       ],
     }
   };
   ```

3. 打包后观察 css 文件内自己代码是否被压缩了

## 打包 less 代码

[加载器 less-loader](https://webpack.docschina.org/loaders/less-loader/)：把 less 代码编译为 css 代码，还需要依赖 less 软件包

步骤：

1. 新建 less `代码`（设置背景图）

   ```less
   html {
     body {
       background: url('./assets/login-bg.png') no-repeat center/cover;
     }
   }
   ```

   1. less 样式引入到 src/login/index.js 中

      ```js
      /**
       * 目标8：打包 less 代码
       *  8.1 新建 less 代码（设置背景图）并引入到 src/login/index.js 中
       *  8.2 下载 less 和 less-loader 本地软件包
       *  8.3 配置 webpack.config.js 让 Webpack 拥有功能
       *  8.4 打包后观察效果
       */
      // 8.1 新建 less 代码（设置背景图）并引入到 src/login/index.js 中
      import './index.less'
      ```

   2. `下载` less 和 less-loader 本地软件包

      ```bash
      npm i less less-loader --save-dev
      ```

   3. `配置` webpack.config.js 让 Webpack 拥有功能

      ```js
      // ...

      module.exports = {
        // ...
        module: {
          rules: [
            // ...
            {
              test: /\.less$/i,
              use: [MiniCssExtractPlugin.loader, "css-loader", "less-loader"]
            }
          ]
        }
      }
      ```

   4. 打包后运行  观察效果

## 打包图片

[资源模块](https://webpack.docschina.org/guides/asset-modules/)：Webpack5 内置了资源模块的打包，无需下载额外 loader 

步骤：

1. `配置` webpack.config.js 让 Webpack 拥有打包图片功能

   占位符 【hash】对模块内容做算法计算，得到映射的数字字母组合的字符串

   占位符 【ext】使用当前模块原本的占位符，例如：.png / .jpg 等字符串

   占位符 【query】保留引入文件时代码中查询参数（只有 URL 下生效）

   1. 注意：判断临界值默认为 `8KB`

      大于 8KB 文件：发送一个单独的文件并导出 URL 地址

      小于 8KB 文件：导出一个 data URI（base64字符串）

   2. 在 src/login/index.js 中给 img 标签添加 logo 图片

      ```js
      /**
       * 目标9：打包资源模块（图片处理）
       *  9.1 创建 img 标签并动态添加到页面，配置 webpack.config.js
       *  9.2 打包后观察效果和区别
       */
      // 9.1 创建 img 标签并动态添加到页面，配置 webpack.config.js
      // 注意：js 中引入本地图片资源要用 import 方式（如果是网络图片http地址，字符串可以直接写）
      import imgObj from './assets/logo.png'
      const theImg = document.createElement('img')
      theImg.src = imgObj
      document.querySelector('.login-wrap').appendChild(theImg)
      ```

   3. 配置 webpack.config.js 让 Webpack 拥有打包图片功能

      ```js
      // ...

      module.exports = {
        // ...
        module: {
          rules: [
            // ...
            {
              test: /\.(png|jpg|jpeg|gif)$/i,
              type: 'asset',
              generator: {
                filename: 'assets/[hash][ext][query]'
              }
            }
          ]
        }
      }
      ```

   4. 打包后运行观察效果

## 案例-用户登录-完成功能

需求：点击登录按钮，基于 npm 下载 axios 包，完成验证码登录功能的核心流程，以及Alert警告框使用

步骤：

1. 使用 npm 下载 axios（体验 npm 作用在前端项目中）

   ```bash
   npm i axios
   ```

2. 准备并修改 utils 工具包源代码`导出`实现函数

3. `导入`到 src/login/index.js 中编写业务实现

   ```js
   /**
    * 目标10：完成登录功能
    *  10.1 使用 npm 下载 axios（体验 npm 作用在前端项目中）
    *  10.2 准备并修改 utils 工具包源代码导出实现函数
    *  10.3 导入并编写逻辑代码，打包后运行观察效果
    */
   // 10.3 导入并编写逻辑代码，打包后运行观察效果
   import myAxios from '../utils/request.js'
   import { myAlert } from '../utils/alert.js'
   document.querySelector('.btn').addEventListener('click', () => {
     const phone = document.querySelector('.login-form [name=mobile]').value
     const code = document.querySelector('.login-form [name=code]').value

     if (!checkPhone(phone)) {
       myAlert(false, '手机号长度必须是11位')
       console.log('手机号长度必须是11位')
       return
     }

     if (!checkCode(code)) {
       myAlert(false, '验证码长度必须是6位')
       console.log('验证码长度必须是6位')
       return
     }

     myAxios({
       url: '/v1_0/authorizations',
       method: 'POST',
       data: {
         mobile: phone,
         code: code
       }
     }).then(res => {
       myAlert(true, '登录成功')
       localStorage.setItem('token', res.data.token)
       location.href = '../content/index.html'
     }).catch(error => {
       myAlert(false, error.response.data.message)
     })
   })
   ```

4. 打包后运行观察效果

## 搭建开发环境

每次改动代码，都要重新打包才能运行查看，效率很低

开发环境：配置 webpack-dev-server 快速开发应用程序

作用：启动 Web 服务，`自动`检测代码编号，`热更新`到网页

> dist 目录和打包内容是在内存里（更新快）

步骤；

1. `下载` webpack-dev-server 软件包到当前项目

   ```bash
   npm i webpack-dev-server --save-dev
   ```

2. `配置自定义命令`，并设置打包的模式为`开发模式`

   ```js
   // ...

   module.exports = {
     // ...
     mode: 'development'
   }
   ```

   ```json
   "scripts": {
     // ...
     "dev": "webpack serve --open"
   },
   ```

3. 使用 npm run dev 来启动开发服务器，访问提示的域名+端口号，在浏览器访问打包后的项目网页，修改代码后试试热更新效果

   > 在 js / css 文件中修改代码保存后，会实时反馈到浏览器
   >
   > webpack-dev-server 借助 http 模块创建 8080 默认 Web 服务
   >
   > 默认以 public 文件夹作为服务器的根目录
   >
   > webpack-dev-server 根据配置，打包相关代码在内存当中，以 ouutput.path 的值作为服务器根目录，所以可以直接自己拼接访问 dist 目录下内容

## 打包模式

[打包模式](https://webpack.docschina.org/configuration/mode/)：告知 Webpack 使用相应模式的内置优化

分类：

| **模式名称** | **模式名字** | **特点**                         | 场景     |
| ------------ | ------------ | -------------------------------- | -------- |
| 开发模式     | development  | 调试代码，实时加载，模块热替换等 | 本地开发 |
| 生产模式     | production   | 压缩代码，资源优化，更轻量等     | 打包上线 |

设置影响 Webpack：

- 方式1：在 webpack.config.js 配置文件设置 mode 选项

  ```js
  // ...

  module.exports = {
    // ...
    mode: 'production'
  }
  ```

- 方式2：在 package.json 命令行设置 mode 参数

  ```json
  "scripts": {
    "build": "webpack --mode=production",
    "dev": "webpack serve --mode=development"
  },
  ```

注意：命令行设置的优先级高于配置文件中的，推荐用命令行设置

### 应用

需求：在开发模式下用 style-loader 内嵌更快，在生产模式下提取 css 代码

[方案](https://webpack.docschina.org/configuration/mode/)[1](https://webpack.docschina.org/configuration/mode/)：webpack.config.js 配置导出函数，但是局限性大（只接受 2 种模式）

方案2：借助 cross-env （跨平台通用）包命令，设置参数区分环境

[方案](https://webpack.docschina.org/guides/production/)[3](https://webpack.docschina.org/guides/production/)：配置不同的 webpack.config.js （适用多种模式差异性较大情况）

主要使用方案 2 尝试，其他方案可以结合点击跳转的官方文档查看尝试

步骤：

1.`下载` cross-env 软件包到当前项目

```js
npm i cross-env --save-dev
```

   2.`配置`自定义命令，传入参数名和值（会绑定到 `process.env` 对象下）

   3.在 webpack.config.js 区分不同环境`使用`不同配置

```js
   module: {
       rules: [
         {
           test: /\.css$/i,
           // use: ['style-loader', "css-loader"],
           use: [process.env.NODE_ENV === 'development' ? 'style-loader' : MiniCssExtractPlugin.loader, "css-loader"]
         },
         {
           test: /\.less$/i,
           use: [
             // compiles Less to CSS
             process.env.NODE_ENV === 'development' ? 'style-loader' : MiniCssExtractPlugin.loader,
             'css-loader',
             'less-loader',
           ],
         }
       ],
     },
```

   4.重新打包观察两种配置区别

## 前端注入环境变量

需求：`前端`项目中，开发模式下打印语句生效，生产模式下打印语句失效

问题：cross-env 设置的只在 Node.js 环境生效，前端代码无法访问 process.env.NODE_ENV

[解决](https://webpack.docschina.org/plugins/define-plugin)：使用 Webpack 内置的 DefinePlugin 插件

作用：在编译时，将前端代码中匹配的变量名，替换为值或表达式

配置 webpack.config.js 中给前端注入环境变量

```js
// ...
const webpack = require('webpack')

module.exports = {
  // ...
  plugins: [
    // ...
    new webpack.DefinePlugin({
      // key 是注入到打包后的前端 JS 代码中作为全局变量
      // value 是变量对应的值（在 corss-env 注入在 node.js 中的环境变量字符串）
      'process.env.NODE_ENV': JSON.stringify(process.env.NODE_ENV)
    })
  ]
}
```

## 开发环境调错 source map

[source map]([https://webpack.docschina.org/guides/development/#using-source-maps](https://webpack.docschina.org/guides/development/))：可以准确追踪 error 和 warning 在原始代码的位置

问题：代码被压缩和混淆，无法正确定位源代码位置（行数和列数）

设置：webpack.config.js 配置 devtool 选项

```js
// ...

module.exports = {
  // ...
  devtool: 'inline-source-map'
}
```

> inline-source-map 选项：把源码的位置信息一起打包在 JS 文件内

注意：source map 适用于开发环境，不要在生产环境使用（防止被`轻易`查看源码位置）

## 设置解析别名路径

[解析别名]([https://webpack.docschina.org/configuration/resolve#resolvealias](https://webpack.docschina.org/configuration/resolve))：配置模块如何解析，创建 import 或 require 的别名，来确保模块引入变得更简单

例如：

1. 原来路径如下：

   ```js
   import { checkPhone, checkCode } from '../src/utils/check.js'
   ```

2. 配置解析别名：在 webpack.config.js 中配置解析别名 @ 来代表 src 绝对路径

   ```js
   // ...

   const config = {
     // ...
     resolve: {
       alias: {
         '@': path.resolve(__dirname, 'src')
       }
     }
   }
   ```

3. 这样我们以后，引入目标模块写的路径就更简单了

   ```js
   import { checkPhone, checkCode } from '@/utils/check.js'
   ```

修改代码的路径后，重新打包观察效果是否正常！

## 优化-CDN使用

需求：`开发模式`使用`本地`第三方库，`生产模式`下使用 `CDN 加载`引入

[CDN](https://developer.mozilla.org/zh-CN/docs/Glossary/CDN)[定义](https://developer.mozilla.org/zh-CN/docs/Glossary/CDN)：内容分发网络，指的是一组分布在各个地区的服务器

作用：把静态资源文件/第三方库放在 CDN 网络中各个服务器中，供用户就近请求获取

好处：减轻自己服务器请求压力，就近请求物理延迟低，配套缓存策略

步骤：

1.在 html 中引入第三方库的 [CDN ](https://www.bootcdn.cn/)[地址](https://www.bootcdn.cn/)[ ](https://www.bootcdn.cn/)并用模板语法判断

```html
<% if(htmlWebpackPlugin.options.useCdn){ %>
    <link href="https://cdn.bootcdn.net/ajax/libs/twitter-bootstrap/5.2.3/css/bootstrap.min.css" rel="stylesheet">
<% } %>
```

   2.配置 webpack.config.js 中 [externals](https://webpack.docschina.org/configuration/externals) 外部扩展选项（防止某些 import 的包被打包）

```js
   // 生产环境下使用相关配置
   if (process.env.NODE_ENV === 'production') {
     // 外部扩展（让 webpack 防止 import 的包被打包进来）
     config.externals = {
       // key：import from 语句后面的字符串
       // value：留在原地的全局变量（最好和 cdn 在全局暴露的变量一致）
       'bootstrap/dist/css/bootstrap.min.css': 'bootstrap',
       'axios': 'axios'
     }
   }
```

```js
   // ...
   const config = {
     // ...
     plugins: [
       new HtmlWebpackPlugin({
         // ...
         // 自定义属性，在 html 模板中 <%=htmlWebpackPlugin.options.useCdn%> 访问使用
         useCdn: process.env.NODE_ENV === 'production'
       })
     ]
   }
```

   3.两种模式下打包观察效果

## 多页面打包

概念：

[单页面](https://developer.mozilla.org/zh-CN/docs/Glossary/SPA)：`单个 html `文件，切换 DOM 的方式实现不同业务逻辑展示，后续 Vue/React 会学到

多页面：`多个 html `文件，切换页面实现不同业务逻辑展示

需求：把黑马头条-数据管理平台-内容页面一起引入打包使用

步骤：

1. 准备`源码`（html，css，js）放入相应位置，并改用模块化语法`导出`

2. 下载 form-serialize 包并`导入`到核心代码中使用

3. 配置 webpack.config.js `多入口`和`多页面`的设置

   ```js
   // ...
   const config = {
     entry: {
       '模块名1': path.resolve(__dirname, 'src/入口1.js'),
       '模块名2': path.resolve(__dirname, 'src/入口2.js'),
     },
     output: {
       path: path.resolve(__dirname, 'dist'),
       filename: './[name]/index.js'  
     }
     plugins: [
       new HtmlWebpackPlugin({
         template: './public/页面1.html', // 模板文件
         filename: './路径/index.html', // 输出文件
         chunks: ['模块名1']
       })
       new HtmlWebpackPlugin({
         template: './public/页面2.html', // 模板文件
         filename: './路径/index.html', // 输出文件
         chunks: ['模块名2']
       })
     ]
   }
   ```

4. 重新打包观察效果

## 案例-发布文章页面打包

需求：把发布文章页面一起打包

步骤：

1.准备发布文章页面源代码，改写成模块化的导出和导入方式

2.修改 webpack.config.js 的配置，增加一个入口和出口

3.打包观察效果

## 优化-分割公共代码

需求：把 2 个以上页面引用的公共代码提取

步骤：

1.`配置` webpack.config.js 的 splitChunks 分割功能

```js
// ...
const config = {
  // ...
  optimization: {
    // ...
    splitChunks: {
      chunks: 'all', // 所有模块动态非动态移入的都分割分析
      cacheGroups: { // 分隔组
        commons: { // 抽取公共模块
          minSize: 0, // 抽取的chunk最小大小字节
          minChunks: 2, // 最小引用数
          reuseExistingChunk: true, // 当前 chunk 包含已从主 bundle 中拆分出的模块，则它将被重用
          name(module, chunks, cacheGroupKey) { // 分离出模块文件名
            const allChunksNames = chunks.map((item) => item.name).join('~') // 模块名1~模块名2
            return `./js/${allChunksNames}` // 输出到 dist 目录下位置
          }
        }
      }
    }
      
 
```

   2.打包观察效果

