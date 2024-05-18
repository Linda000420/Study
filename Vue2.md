#  Vue2

概念：Vue (读音 /vjuː/，类似于 view) 是一套`构建用户界面`的`渐进式框架`

构建用户界面：基于数据`渲染出用户可以看到的`界面

渐进式：所谓渐进式就是`循序渐进`，不一定非得把Vue中的所有API都学完才能开发Vue，可以学一点开发一点

Vue的两种开发方式：

1. Vue核心包开发

   场景：`局部`模块改造

2. Vue核心包&Vue插件&工程化

   场景：`整站`开发


优点：大大`提升开发效率`（`70%↑`）

缺点：需要理解记忆`规则 `→ 官网

​	Vue2官网：<https://v2.cn.vuejs.org/>

框架：就是一套完整的解决方案

**举个栗子**	

如果把一个完整的项目比喻为一个装修好的房子，那么框架就是一个毛坯房。

我们只需要在“毛坯房”的基础上，增加功能代码即可。

提到框架，不得不提一下库。

- 库，类似工具箱，是一堆方法的集合，比如 axios、lodash、echarts等
- 框架，是一套完整的解决方案，实现了大部分功能，我们只需要按照一定的规则去编码即可。

框架的特点：有一套必须让开发者遵守的**规则**或者**约束**

咱们学框架就是学习的这些规则 [官网](https://v2.cn.vuejs.org/)

## 创建Vue实例

我们已经知道了Vue框架可以 基于数据帮助我们渲染出用户界面，那应该怎么做呢？

比如就上面这个数据，基于提供好的msg 怎么渲染后右侧可展示的数据呢？

**核心步骤（4步）：**

1. 准备容器

2. 引包（官网） — `开发版本`/生产版本

   开发版本包包含完整的注释和警告，一旦引入 VueJS 核心包，在全局环境就有了 Vue 构造函数

3. 创建Vue实例  new Vue()

4. 指定配置项，渲染数据
   1. el：指定挂载点，选择器指定控制的是哪个盒子
   2. data：提供数据

~~~html
<!-- 准备容器，Vue所管理的范围 -->
<div id="app">
  <!-- 编写用于渲染的代码逻辑 -->
  {{ msg }}
</div>

<!-- 引入开发版本包，包含完整的注释和警告 -->
<script src="./js/vue.js"></script>

<script>
  // 一旦引入 VueJS 核心包，在全局环境就有了 Vue 构造函数
  const app = new Vue({
    // 通过 el 配置选择器，指定 Vue 管理的是哪个盒子
    el: '#app',
    // 通过 data 提供数据
    data: {
      msg: 'Hello'
    }
  })
</script>
~~~

## 插值表达式 {{}}

插值表达式是一种Vue的模板语法，我们可以用插值表达式渲染出Vue提供的数据

`作用`：利用表达式进行插值，渲染到页面中

表达式：是可以被求值的代码，JS引擎会将其计算出一个结果

以下的情况都是表达式：

```js
money + 100
money - 100
money * 10
money / 10 
price >= 100 ? '真贵':'还行'
obj.name
arr[0]
fn()
obj.fn()
```

`语法`：{{ 表达式 }}

```js
<h3>{{title}}<h3>

<p>{{nickName.toUpperCase()}}</p>

<p>{{age >= 18 ? '成年':'未成年'}}</p>

<p>{{obj.name}}</p>

<p>{{fn()}}</p>
```

> 注意点：
>
> 1.使用的数据必须存在（data）
>
> 2.支持的是表达式，而非语句，比如： if、for ...
>
> 3.不能在标签属性中使用{{ }}插值

```js
1.在插值表达式中使用的数据 必须在data中进行了提供
<p>{{hobby}}</p>  //如果在data中不存在 则会报错

2.支持的是表达式，而非语句，比如：if   for ...
<p>{{if}}</p>

3.不能在标签属性中使用 {{  }} 插值 (插值表达式只能标签中间使用)
<p title="{{username}}">我是P标签</p>
```

## 响应式特性

响应式：简单理解就是`数据变化，视图自动更新`。 

访问 和 修改 data中的数据（响应式演示）：

data中的数据, 最终会被添加到实例上

① 访问数据：` 实例.属性名`

② 修改数据：` 实例.属性名 = 值`

`聚焦于数据 → 数据驱动视图`

使用 Vue 开发，关注`业务的核心逻辑`，根据业务`修改数据`即可


## Vue开发者工具安装

1. 通过谷歌应用商店安装（国外网站）
2. 极简插件下载（推荐） <https://chrome.zzzmh.cn/index>
3. 打开 Vue `运行的页面`，调试工具中 `Vue 栏`，即可查看`修改数据`，进行调试

## Vue中的常用指令

Vue 会根据不同的`指令`，针对标签实现不同的`功能`

指令（Directives）是 Vue 提供的带有` v- 前缀`的 特殊`标签属性`。

为啥要学：提高程序员操作 DOM 的效率。

vue 中的指令按照不同的用途可以分为如下 6 大类：

-  内容渲染指令（v-html、v-text）
-  条件渲染指令（v-show、v-if、v-else、v-else-if）
-  事件绑定指令（v-on）
-  属性绑定指令 （v-bind）
-  双向绑定指令（v-model）
-  列表渲染指令（v-for）

指令是 vue 开发中最基础、最常用、最简单的知识点。

### 内容渲染指令

内容渲染指令用来辅助开发者渲染 DOM 元素的文本内容。常用的内容渲染指令有如下2 个：

#### v-text

类似innerText

- 使用语法：`<p v-text="uname">hello</p>`，意思是将 uame 值渲染到 p 标签中
- 类似 innerText，使用该语法，会覆盖 p 标签原有内容


#### v-html

类似 innerHTML

- 使用语法：`<p v-html="intro">hello</p>`，意思是将 intro 值渲染到 p 标签中
- 类似 innerHTML，使用该语法，会覆盖 p 标签原有内容
- 类似 innerHTML，使用该语法，能够将HTML标签的样式呈现出来。

代码演示：

```js
 
  <div id="app">
    <h2>个人信息</h2>
	// 既然指令是vue提供的特殊的html属性，所以咱们写的时候就当成属性来用即可
    <p v-text="uname">姓名：</p> 
    <p v-html="intro">简介：</p>
  </div> 

<script>
        const app = new Vue({
            el:'#app',
            data:{
                uname:'张三',
                intro:'<h2>这是一个<strong>非常优秀</strong>的boy<h2>'
            }
        })
</script>
```

### 条件渲染指令

条件判断指令，用来辅助开发者按需控制 DOM 的显示与隐藏。条件渲染指令有如下两个，分别是：

#### v-show

1. 作用：  控制元素显示隐藏
2. 语法：  v-show = "`表达式`"   表达式值为 `true 显示`， `false 隐藏`
3. 原理：  `切换 display:none` 控制显示隐藏
4. 场景：频繁切换显示隐藏的场景

#### v-if

1. 作用：  控制元素显示隐藏（`条件渲染`）
2. 语法：  v-if= "`表达式`"          表达式值` true显示`，` false 隐藏`
3. 原理：  基于`条件判断`，是否`创建` 或 `移除`元素节点
4. 场景：  要么显示，要么隐藏，不频繁切换的场景

#### v-else 和 v-else-if

作用：辅助 v-if 进行判断渲染

语法：v-else  v-else-if="`表达式`"

> 需要紧接着 v-if 一起使用

```js
<div id="app">
  <p v-if="gender === 1">性别：♂ 男</p>
	<p v-else>性别：♀ 女</p>
<hr>
  <p v-if="score >= 90">成绩评定A：奖励电脑一台</p>
  <p v-else-if="score >= 70">成绩评定B：奖励周末郊游</p>
  <p v-else-if="score >= 60">成绩评定C：奖励零食礼包</p>
  <p v-else>成绩评定D：惩罚一周不能玩手机</p>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>

  const app = new Vue({
    el: '#app',
    data: {
      gender: 2,
      score: 95
    }
  })
</script>
```

### 事件绑定指令(v-on)

作用：注册事件 = `添加监听 + 提供处理逻辑`

语法：

- `v-on:事件名="内联语句"`
- `v-on:事件名="methods 中的函数名"`
- `v-on:事件名="函数名(参数)"`
- 简写： `@事件名`

1. 内联语句

   ```js
   <div id="app">
       <button @click="count--">-</button>
       <span>{{ count }}</span>
       <button v-on:click="count++">+</button>
     </div>
     <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
     <script>
       const app = new Vue({
         el: '#app',
         data: {
           count: 100
         }
       })
     </script>
   ```

2. 事件处理函数

   注意：

   - 事件处理函数应该写到一个跟data同级的配置项（methods）中
   - methods中的函数内部的this都指向Vue实例

```js
<div id="app">
    <button @click="fn">切换显示隐藏</button>
    <h1 v-show="isShow">Vue</h1>
  </div>
  <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        isShow: true
      },
      methods: {
        fn() {
          this.isShow = !this.isShow
        }
      }
    })
  </script>
```

  3.给事件处理函数传参

- 如果不传递任何参数，则方法无需加小括号；methods方法中可以直接使用 e 当做事件对象


- 如果传递了参数，则实参 `$event` 表示事件对象，固定用法。

```js
<div id="app">
  <div class="box">
    <h3>小黑自动售货机</h3>
    <button @click="buy(5)">可乐5元</button>
    <button @click="buy(10)">咖啡10元</button>
    <button @click="buy(8)">牛奶8元</button>
  </div>
	<p>银行卡余额：{{ money }}元</p>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      money: 100
    },
    methods: {
      buy(price){
        this.money -= price
      }
    }
  })
</script>
```

### 属性绑定指令(v-bind)

1. **作用：**动态设置html的`标签属性` 比如：src、url、title
2. **语法**：`v-bind:属性名="表达式"`
3. 简写：` :属性名="表达式"`

比如，有一个图片，它的 `src` 属性值，是一个图片地址。这个地址在数据 data 中存储。

则可以这样设置属性值：

- `<img v-bind:src="url" />`
- `<img :src="url" />`   （v-bind可以省略）

```js
  <div id="app">
    <img v-bind:src="imgUrl" v-bind:title="msg" alt="">
    <img :src="imgUrl" :title="msg" alt="">
  </div>
  <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        imgUrl: './imgs/10-02.png',
        msg: 'hello 波仔'
      }
    })
  </script>
```

### 列表渲染指令(v-for)

作用：基于`数据`循环，`多次`渲染整个元素 → `数组`、对象、数字...

遍历数组语法：`v-for="(item,index) in 数组"`，其中：

- item 是数组中的每一项
- index 是每一项的索引（下标），不需要可以省略
- arr 是被遍历的数组

~~~html
<div id="app">
  <h3>小黑的书架</h3>
  <ul>
    <li v-for="item in booksList" :key="item.id">
      <span> {{ item.name }} </span>
      <span> {{ item.author }} </span>
      <button @click="del(item.id)">删除</button>
    </li>
  </ul>
</div>
<script src="./js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      booksList: [
        { id: 1, name: '《红楼梦》', author: '曹雪芹' },
        { id: 2, name: '《西游记》', author: '吴承恩' },
        { id: 3, name: '《水浒传》', author: '施耐庵' },
        { id: 4, name: '《三国演义》', author: '罗贯中' }
      ]
    },
    methods: {
      del(id) {
        // 通过 id 进行删除数组中的对应项 → filter（不会改变原数组）
        // filter：根据条件，保留满足条件的对应项，得到一个新数组
        this.booksList = this.booksList.filter(item => item.id !== id)
      }
    }
  })
</script>
~~~

此语法也可以遍历**对象和数字**

```js
//遍历对象
<div v-for="(value, key, index) in object">{{value}}</div>
value:对象中的值
key:对象中的键
index:遍历索引从0开始

//遍历数字
<p v-for="item in 10">{{item}}</p>
item从1 开始
```

#### v-for中的key

**语法：** `key属性="唯一标识"`

**作用：**给列表项添加的`唯一标识`。便于Vue进行列表项的`正确排序复用`。

**为什么加key：**Vue 的默认行为会尝试`原地修改元素`（**就地复用**）

实例代码：

```js
<ul>
  <li v-for="(item, index) in booksList" :key="item.id">
    <span>{{ item.name }}</span>
    <span>{{ item.author }}</span>
    <button @click="del(item.id)">删除</button>
  </li>
</ul>
```

> 1. key 的值只能是`字符串`或 `数字类型`
> 2. key 的值必须具有`唯一性`
> 3. 推荐使用 ` id` 作为 key（唯一），不推荐使用` index` 作为 key（会变化，不对应）

### 双向绑定指令(v-model)

**作用：** 给`表单元素`（input、radio、select）使用，`双向数据绑定 `，可以快速`获取或设置`表单元素内容

1. 数据变化 → 视图自动更新
2. `视图`变化 → `数据`自动更新

**语法：**`v-model="变量"`

**需求：**使用双向绑定实现以下需求

1. 点击登录按钮获取表单中的内容
2. 点击重置按钮清空表单中的内容

```js
<div id="app">
  账户：<input type="text" v-model="username"> <br><br>
  密码：<input type="password" v-model="password"> <br><br>
  <button @click="login">登录</button>
	<button @click="reset">重置</button>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      username: '',
      password: ''
    },
    methods: {
      login () {
        cosole.log(this.username, this.password)
      },
      reset () {
        this.username = ''
        this.password = ''
      }
    }
  })
</script>
```

## 指令修饰符

指令修饰符：就是通过 `.` 指明一些指令`后缀`，不同的后缀封装了不同的处理操作  —> 简化代码

### 按键修饰符

- `@keyup.enter` → 键盘回车监听

```js
<div id="app">
  <h3>@keyup.enter  →  监听键盘回车事件</h3>
	<input placeholder="请输入任务" class="new-todo" v-model="name" @keyup.enter="add()"/>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      name: '',
      list: [
        {id: 1, name: '跑步一公里'},
        {id: 2, name: '跳绳200次'},
        {id: 3, name: '游泳100米'},
      ]
    },
    methods: {
      add (name) {
        if(this.name.trim() === ''){
          return
        }
        this.list.unshift({
          id: +new Date(),
          name: this.name
        })
        this.name=''
      }
    }
  })
</script>
```

### v-model修饰符

- `v-model.trim`  →  去除首位空格
- `v-model.number`→ 转数字

### 事件修饰符

- @事件名.stop →  阻止冒泡
- @事件名.prevent → 阻止默认行为
- @事件名.stop.prevent → 可以连用 即阻止事件冒泡也阻止默认行为

```js
<div id="app">
  <h3>v-model修饰符 .trim .number</h3>
	姓名：<input v-model="username" type="text"><br>
  年纪：<input v-model="age" type="text"><br>


  <h3>@事件名.stop     →  阻止冒泡</h3>
	<div @click="fatherFn" class="father">
  	<div @click="sonFn" class="son">儿子</div>
	</div>

	<h3>@事件名.prevent  →  阻止默认行为</h3>
	<a @click href="http://www.baidu.com">阻止默认行为</a>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      username: '',
      age: '',
    },
    methods: {
      fatherFn () {
        alert('老父亲被点击了')
      },
      sonFn (e) {
        // e.stopPropagation()
        alert('儿子被点击了')
      }
    }
  })
</script>
```

## v-bind对样式控制的增强

### 操作class

为了方便开发者进行`样式控制`， Vue 扩展了 `v-bind` 的语法，可以针对`class 类名`和`style 行内样式`进行控制 。

语法：`:class="对象/数组"`

`对象` → 键就是类名，值就是布尔值，如果值是 `true`，就有这个类，否则没有这个类

```html
<div class="box" :class="{ 类名1: 布尔值, 类名2: 布尔值 }"></div>
```

​    适用场景：一个类名，来回切换

`数组` → 数组中所有的类，都会添加到盒子上，本质就是一个 `class 列表`

```html
<div class="box" :class="[ 类名1, 类名2, 类名3 ]"></div>
```

   使用场景:批量添加或删除类

```html
<div id="app">
  <!--绑定对象-->
  <div class="box" :class="{ pink: true, big: false}">黑马程序员</div>
  <!--绑定数组-->
  <div class="box" :class="['pink', 'big']">黑马程序员</div>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {

    }
  })
</script>
```

### 操作style

语法：`:style="样式对象"`

```html
<div class="box" :style="{ CSS属性名1: CSS属性值, CSS属性名2: CSS属性值 }"></div>
```

进度条案例：

```html
<div id="app">
  <div class="progress">
    <div class="inner" :style="{ width: percent + '%' }">
      <span>{{ percent }}%</span>
    </div>
  </div>
  <button @click="percent = 25">设置25%</button>
  <button @click="percent = 50">设置50%</button>
  <button @click="percent = 75">设置75%</button>
  <button @click="percent = 100">设置100%</button>
</div>
<script src="./js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      percent: 0
    }
  })
</script>
```

## v-model在其他表单元素的使用

讲解内容：

常见的表单元素都可以用 v-model 绑定关联  →  快速`获取`或`设置`表单元素的值

它会根据`控件类型`自动选取`正确的方法`来更新元素

```js
输入框  input:text   ——> value
文本域  textarea	 ——> value
复选框  input:checkbox  ——> checked
单选框  input:radio   ——> checked
下拉菜单 select    ——> value
...
```

```html
<div id="app">
  <h3>小黑学习网</h3>
  姓名：
  <input type="text" v-model="username"> 
  <br><br>
  是否单身：
  <input type="checkbox" v-model="isSingle"> 
  <br><br>
  <!-- 
前置理解：
1. name:  给单选框加上 name 属性 可以分组 → 同一组互相会互斥
2. value: 给单选框加上 value 属性，用于提交给后台的数据
结合 Vue 使用 → v-model
-->
  性别: 
  <input type="radio" name="gender" value="1" v-model="gender">男
  <input type="radio" name="gender" value="2" v-model="gender">女
  <br><br>
  <!-- 
前置理解：
1. option 需要设置 value 值，提交给后台
2. select 的 value 值，关联了选中的 option 的 value 值
结合 Vue 使用 → v-model
-->
  所在城市:
  <select v-model="cityId">
    <option value="101" >北京</option>
    <option value="102">上海</option>
    <option value="103">成都</option>
    <option value="104">南京</option>
  </select>
  <br><br>
  自我描述：
  <textarea v-model="desc"></textarea> 
  <button>立即注册</button>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
			username: '',
      isSingle: false,
      gender: "1",
      cityId: "102",
      desc: ""
    }
  })
</script>
```

## computed计算属性

概念：基于`现有的数据`，计算出来的`新属性`。 `依赖`的数据变化，`自动`重新计算。

语法：

~~~js
<script>
  const app = new Vue({
    el: '#app',
    data: {

    },
    computed: {
      计算属性名 () {
        基于现有数据，编写求值逻辑
        return 结果
      }
  	},
  })
</script>
~~~

1. 声明在 `computed 配置项`中，一个计算属性对应一个函数
2. 使用起来和普通属性一样使用  {{ `计算属性名` }}   

计算属性 → 可以将一段`求值的代码`进行封装

> computed 配置项和 data 配置项是同级的
>
> computed 中的计算属性虽然是函数的写法，但他依然是个属性
>
> computed 中的计算属性不能和 data 中的属性同名
>
> 使用 computed 中的计算属性和使用 data 中的属性是一样的用法
>
> computed 中计算属性内部的 this 依然指向的是 Vue 实例

```html
<div id="app">
  <h3>小黑的礼物清单</h3>
  <table>
    <tr>
      <th>名字</th>
      <th>数量</th>
    </tr>
    <tr v-for="(item, index) in list" :key="item.id">
      <td>{{ item.name }}</td>
      <td>{{ item.num }}个</td>
    </tr>
  </table>

  <!-- 目标：统计求和，求得礼物总数 -->
  <p>礼物总数：{{ totalCount }} 个</p>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      // 现有的数据
      list: [
        { id: 1, name: '篮球', num: 1 },
        { id: 2, name: '玩具', num: 2 },
        { id: 3, name: '铅笔', num: 5 },
      ]
    },
    computed: {
      totalCount () {
        //	对 this.list 数组里面的 num 进行求和 → reduce
        let total = this.list.reduce((sum,item) => sum + item.num, 0)
        return total
      }
    }
  })
</script>
```

## computed计算属性 VS methods方法

### computed计算属性

作用：封装了一段对于`数据`的处理，求得一个`结果`

语法：

1. 写在`computed`配置项中
2. 作为属性，直接使用
   - js中使用计算属性： `this.计算属性`
   - 模板中使用计算属性：`{{ 计算属性 }}`

### methods计算属性

作用：给Vue实例提供一个`方法`，调用以处理`业务逻辑`。

语法：

1. 写在`methods`配置项中
2. 作为方法调用
   - js中调用：`this.方法名()`
   - 模板中调用 `{{ 方法名() }}`  或者 `@事件名="方法名"`

### 计算属性的优势

1. `缓存特性（提升性能）`：

   计算属性会对计算出来的`结果缓存`，再次使用直接读取缓存，

   依赖项变化了，会`自动`重新计算 → 并`再次缓存`

2. methods没有缓存特性

3. 通过代码比较

```html
<div id="app">
  <h3>小黑的礼物清单🛒<span>{{ totalCount }}</span></h3>
  <table>
    <tr>
      <th>名字</th>
      <th>数量</th>
    </tr>
    <tr v-for="(item, index) in list" :key="item.id">
      <td>{{ item.name }}</td>
      <td>{{ item.num }}个</td>
    </tr>
  </table>

  <p>礼物总数：{{ totalCount }} 个</p>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      // 现有的数据
      list: [
        { id: 1, name: '篮球', num: 3 },
        { id: 2, name: '玩具', num: 2 },
        { id: 3, name: '铅笔', num: 5 },
      ]
    },
    computed: {
      totalCount () {
        let total = this.list.reduce((sum, item) => sum + item.num, 0)
        return total
      }
    }
  })
</script>
```

## 计算属性的完整写法

计算属性默认的简写，只能读取访问，`不能 “修改”`

如果要`修改`  → 需要写计算属性的`完整写法`

~~~js
computed: {
  计算属性名: {
    get() {
      一段代码逻辑（计算逻辑）
      return 结果
    },
    set(修改的值) {
      一段代码逻辑（修改逻辑）
    }
  }
}
~~~

```html
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      firstName: '刘',
      lastName: '备'
    },
    methods: {
      changeName () {
        this.fullName = '吕小布'
      }
    },
    computed: {
			//	简写 → 获取，没有配置设置的逻辑
      // fullName() {
      //   reurn this.firsttName + this.lastName
      // }
      
      //	完整写法 → 获取 + 设置
      fullName: {
        //	当 fullName 计算属性被获取求值时，执行 get （有缓存）
        //	会将返回值作为求值的结果
        get () {
          reurn this.firsttName + this.lastName
        },
        //	当 fullName 计算属性被修改赋值时，执行 set
        //	修改的值传递给 set 方法的形参
        set (value) {
          this.firstName = value.slice(0,1)
          this.lastName = value.slice(1)
        }
      }
    },
  })
</script>
```

## watch侦听器（监视器）

作用：`监视数据变化`，执行一些业务逻辑或异步操作

watch同样声明在跟data同级的配置项中

语法：

1. 简单写法 → 简单类型数据，直接监视
2. 完整写法 → 添加额外配置项

### 简单写法

 `简单类型数据，直接监视`

```js
data: { 
  words: '苹果',
  obj: {
    words: '苹果'
  }
},

watch: {
  // 该方法会在数据变化时，触发执行
  数据属性名 (newValue, oldValue) {
    一些业务逻辑 或 异步操作。 
  },
  '对象.属性名' (newValue, oldValue) {
    一些业务逻辑 或 异步操作。 
  }
}
```
```html
<div id="app">
  <!-- 条件选择框 -->
  <div class="query">
    <span>翻译成的语言：</span>
    <select>
      <option value="italy">意大利</option>
      <option value="english">英语</option>
      <option value="german">德语</option>
    </select>
  </div>

  <!-- 翻译框 -->
  <div class="box">
    <div class="input-wrap">
      <textarea v-model="words"></textarea>
      <span><i>⌨️</i>文档翻译</span>
    </div>
    <div class="output-wrap">
      <div class="transbox">{{ result }}</div>
    </div>
  </div>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>
  // 接口地址：https://applet-base-api-t.itheima.net/api/translate
  // 请求方式：get
  // 请求参数：
  // （1）words：需要被翻译的文本（必传）
  // （2）lang： 需要被翻译成的语言（可选）默认值-意大利
  // -----------------------------------------------

  const app = new Vue({
    el: '#app',
    data: {
      words: '',
      result: '',	//	翻译结果
    },
    // 具体讲解：(1) watch语法 (2) 具体业务实现
    watch: {
      words (newValue) {
        clearTimeout(this.timer)
        this.timer = setTimeout(async () => {
          const res = await axios({
            url: 'https://applet-base-api-t.itheima.net/api/translate',
            params: {
              words: newValue
            }
          })
          this.result = res.data.data
        }, 300)
      }
    }
  })
</script>
```

### 完整写法

添加额外的`配置项`

1. `deep:true` 对复杂类型进行深度监听
2. `immdiate:true` 初始化立刻执行一次 handler 方法

```js
data: {
  obj: {
    words: '苹果',
    lang: 'italy'
  },
},

watch: {// watch 完整写法
  对象: {
    deep: true, // 深度监视
    immdiate:true,//立即执行handler函数
    handler (newValue) {
      console.log(newValue)
    }
  }
}

```

需求：输入内容，`修改语言`，都实时翻译

```js
<div id="app">
  <!-- 条件选择框 -->
  <div class="query">
    <span>翻译成的语言：</span>
    <select v-model="obj.lang">
      <option value="italy">意大利</option>
      <option value="english">英语</option>
      <option value="german">德语</option>
    </select>
  </div>

  <!-- 翻译框 -->
  <div class="box">
    <div class="input-wrap">
      <textarea v-model="obj.words"></textarea>
      <span><i>⌨️</i>文档翻译</span>
    </div>
    <div class="output-wrap">
      <div class="transbox">{{ result }}</div>
    </div>
  </div>
</div>

<script> 
  const app = new Vue({
    el: '#app',
    data: {
      obj: {
        words: '小黑',
        lang: 'italy'
      },
      result: '', // 翻译结果
    },
    watch: {
      obj: {
        deep: true, // 深度监视
        immediate: true, // 立刻执行，一进入页面handler就立刻执行一次
        handler (newValue) {
          clearTimeout(this.timer)
          this.timer = setTimeout(async () => {
            const res = await axios({
              url: 'https://applet-base-api-t.itheima.net/api/translate',
              params: newValue
            })
            this.result = res.data.data
            console.log(res.data.data)
          }, 300)
        }
      } 
    }
  })
</script>
```

## 购物车业务技术点总结

渲染功能：`v-if / v-else`、`v-for`、`:class`

删除功能：`点击传参`，`filter` 过滤覆盖原数组

修改个数：`点击传参`，`find` 找对象

全选反选：计算属性 `computed`，完整写法 `get / set`

统计选中的总价和总数量：计算属性 `computed`，`reduce` 条件求和

持久化到本地：`watch` 监视，`localStorage`，`JSON.stringify`，`JSON.parse`

## Vue生命周期

发送`初始化渲染请求`越早越好，至少 dom 渲染出来才可以开始`操作 dom`

Vue生命周期：就是一个Vue实例从`创建`到`销毁`的整个过程。

### 生命周期四个阶段

① 创建 ② 挂载 ③ 更新 ④ 销毁

1.创建阶段：创建响应式数据，`发送初始化渲染请求`

2.挂载阶段：渲染模板，`操作 dom`

3.更新阶段：修改数据，更新视图

4.销毁阶段：销毁Vue实例

### Vue生命周期函数（钩子函数）

Vue生命周期过程中，会`自动运行一些函数`，被称为`生命周期钩子` →  让开发者可以在`特定阶段`运行`自己的代码`

1. 创建阶段：beforeCreate、`created（发送初始化渲染请求）`
2. 挂载阶段：beforeMount、`mounted（操作 dom）`
3. 更新阶段：beforeUpdate、updated
4. 销毁阶段：beforeDestroy（`释放 Vue 以外的资源，清除定时器，延时器等`）、destroyed

```html
<div id="app">
  <h3>{{ title }}</h3>
  <div>
    <button @click="count--">-</button>
    <span>{{ count }}</span>
    <button @click="count++">+</button>
  </div>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      count: 100,
      title: '计数器'
    },
    // 1. 创建阶段（准备数据）
    beforeCreate () {
      console.log('brforeCreate：响应式数据准备好之前', this.count)
    },	//	brforeCreate：响应式数据准备好之前 undefined
    created () {
      console.log('created：响应式数据准备好之后', this.count)
      //	this.数据名 = 请求回来的数据
      //	可以开始发送初始化渲染的请求了
    },	//	created：响应式数据准备好之后 100

    // 2. 挂载阶段（渲染模板）
		beforeMount () {
      console.log('beforeMount：模版渲染之前', document.querySelector('h3').innerHTML)
    },	//	beforeMount：模版渲染之前 {{ title }}
    mounted () {
      console.log('mounted：模版渲染之后', document.querySelector('h3').innerHTML)
      //	可以开始操作 dom 了
    },	//	mounted：模版渲染之后 计数器

    // 3. 更新阶段(修改数据 → 更新视图)
		beforeUpdate () {
      console.log('beforeUpdate：数据修改了，视图还没更新', document.querySelector('span').innerHTML)
    },	//	beforeUpdate：数据修改了，视图还没更新 100
    updated () {
      console.log('updated：数据修改了，视图已经更新', document.querySelector('span').innerHTML)
    },	//	beforeUpdate：数据修改了，视图还没更新 101

    // 4. 卸载阶段
		beforeDestroy () {
      console.log('beforeDestroy：卸载之前')
      //	清除掉一些 Vue 以外的资源占用，定时器，延时器...
    },
    destroyed () {
      console.log('destroyed：卸载之后')
    },
  })
</script>
```

## 工程化开发和脚手架

### 1.开发Vue的两种方式

- 核心包传统开发模式：基于html / css / js 文件，直接引入核心包，开发 Vue。
- `工程化开发模式：基于构建工具（例如：webpack）的环境中开发Vue。`

工程化开发模式优点：

   提高编码效率，比如使用JS新语法、Less/Sass、Typescript等通过webpack都可以编译成浏览器识别的ES3/ES5/CSS等

工程化开发模式问题：

- webpack配置`不简单`
- `雷同`的基础配置
- 缺乏`统一标准`

为了解决以上问题，所以我们`需要一个工具，生成标准化的配置`

### 2.脚手架Vue CLI

 Vue CLI 是 Vue 官方提供的一个`全局命令工具`

 可以帮助我们`快速创建`一个开发Vue项目的`标准化基础架子`。【集成了webpack配置】

好处：

1. 开箱即用，零配置
2. 内置babel等工具
3. 标准化的webpack配置

使用步骤：

1. 全局安装（只需安装一次即可）` yarn global add @vue/cli` 或者 `npm i @vue/cli -g`
2. 查看vue/cli版本： `vue --version`
3. 创建项目架子：`vue create project-name` (项目名不能使用中文)
4. 启动项目：`yarn serve` 或者 `npm run serve` (命令不固定，找package.json)

## 项目目录介绍和运行流程

### 1.项目目录介绍

虽然脚手架中的文件有很多，目前咱们只需人事三个文件即可

1. main.js  入口文件，作用：导入 App.vue，基于 App.vue 创建结构渲染 index.html
2. App.vue  App根组件 
3. index.html 模板文件

VUE-DEMO

​	node_modules				第三包文件夹

​	public						放 html 文件的地方

​		favicon.ico				网站图标

​	  	   ` index.html`			`index.html 模版文件`

​	src							源代码目录 → 以后写代码的文件夹

​		assets					静态资源目录 → 存放图片、字体等

​		components			组件目录 → 存放通用组件

​		`App.vue`				`App 根组件 → 项目运行看到的内容就在这里编写`

​		`main.js`				`入口文件 → 打包或运行，第一个执行的文件`

​	.gitignore					git 忽视文件

​	babel.config.js				babel 配置文件

​	jsconfig.json				js 配置文件

​	package.json				项目配置文件 → 包含项目名、版本号、scripts、依赖包

​	README.md				项目说明文档

​	vue.config.js				vue-cli 配置文件

​	yarn.lock					yarn 锁文件，由 yarn 自动生成的，锁定安装版本

### 2.运行流程

1. yarn serve
2. main.js
   - 导入 Vue
   - 导入 App.vue
   - 实例化 Vue，将 App.vue 渲染到 index.html 容器中
3. index.html

## 组件化开发

组件化：一个页面可以拆分成`一个个组件`，每个组件有着自己独立的`结构`、`样式`、`行为`。

好处：便于`维护`，利于`复用` → 提升`开发效率`。

组件分类：普通组件、根组件。

### 根组件 

根组件 App.vue：整个应用`最上层`的组件，包裹所有普通小组件

App.vue 文件（单文件组件）的三个组成部分

- 语法高亮插件：Vetur


- `三部分组成`

  - `template`：结构 （有且只能一个根元素）
  - `script`:   js逻辑 
  - `style`： 样式 (可支持less，需要装包)

- 让组件支持less

  （1） style标签，lang="less" 开启less功能 

  （2） 装包: `yarn add less less-loader` -D（开发依赖） 或者npm i less less-loader -D

### 普通组件的注册使用

组件注册的两种方式：

1. 局部注册：只能在注册的组件内使用
   - 创建 .vue 文件（三个组成部分）
   - 在使用的组件内导入并注册
2. 全局注册：所有组件内都能使用

技巧：一般都用`局部注册`，如果发现确实是`通用组件`，再抽离到全局

#### 局部注册

特点：只能在注册的组件内使用

步骤：

1. 创建.vue文件（三个组成部分）
2. 在`使用的组件内`先导入，并局部注册 `components:{ 组件名: 组件对象 }`，最后使用

使用方式：当成html标签使用即可  `<组件名></组件名>`

>  组件名规范 —> 大驼峰命名法， 如 HmHeader

语法：

```js
// 导入需要注册的组件
import 组件对象 from '.vue文件路径'
import HmHeader from './components/HmHeader'

export default {  // 局部注册
  components: {
   '组件名': 组件对象,
    HmHeader:HmHeaer,
    HmHeader
  }
}
```

#### 全局注册

特点：全局注册的组件，在项目的`任何`组件中都能使用

步骤

1. 创建 .vue 组件（三个组成部分）
2. `main.js` 中进行全局注册 `Vue.component('组件名', 组件对象)`

使用方式：当成HTML标签直接使用

> <组件名></组件名>
>
> 组件名规范 —> 大驼峰命名法， 如 HmHeader

语法：`Vue.component('组件名', 组件对象)`

```js
// 导入需要全局注册的组件
import HmButton from './components/HmButton'
Vue.component('HmButton', HmButton)
```

## 页面开发思路

1. 分析页面，`按模块拆分组件`，搭架子（`局部或全局注册`）
2. 根据设计图，编写组件 html 结构 css 样式
3. 拆分封装`通用小组件`（局部或全局注册）
4. 通过 js 动态渲染，实现功能

## scoped 解决样式冲突

默认情况：写在组件中的样式会`全局生效` →  因此很容易造成多个组件之间的样式冲突问题。

`全局样式`：默认组件中的样式会作用到全局，任何一个组件中都会受到此样式的影响

`局部样式`：可以给组件加上 `scoped` 属性，`可以让样式只作用于当前组件`

原理：

1. 当前组件内标签都被添加 `data-v-hash 值`的属性 
2. css选择器都被添加 `[ data-v-hash值 ]` 的属性选择器

最终效果：`必须是当前组件的元素`，才会有这个自定义属性, 才会被这个样式作用到 

```vue
<style scoped>
</style>
```

## data必须是一个函数

一个组件的 `data` 选项必须是一个`函数`，目的是为了：保证每个组件实例，维护`独立`的一份数据对象。

每次创建新的组件实例，都会新执行一次 data 函数，得到一个新对象。

BaseCount.vue

```vue
<template>
  <div class="base-count">
    <button @click="count--">-</button>
    <span>{{ count }}</span>
    <button @click="count++">+</button>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      count: 100,
    }
  },
}
</script>

<style>
.base-count {
  margin: 20px;
}
</style>
```

App.vue

```vue
<template>
  <div class="app">
    <BaseCount></BaseCount>
    <BaseCount></BaseCount>
    <BaseCount></BaseCount>
  </div>
</template>

<script>
import BaseCount from './components/BaseCount'
export default {
  components: {
    BaseCount,
  },
}
</script>
```

## 组件通信

组件通信，就是指`组件与组件`之间的`数据传递`

- 组件的数据是`独立`的，无法直接访问其他组件的数据。
- 想使用其他组件的数据，就需要组件通信

组件关系分类

1. 父子关系
2. 非父子关系

### 父子通信流程

1. 父组件通过 `props` 将数据传递给子组件
2. 子组件利用 `$emit` 通知父组件修改更新

### 父向子通信

父组件通过  `props` 将数据传递给子组件

父向子传值步骤

1. 给子组件以添加属性的方式传值
2. 子组件内部通过props接收
3. 模板中直接使用 props接收的值

父组件App.vue

```vue
<template>
  <div class="app" style="border: 3px solid #000; margin: 10px">
    我是APP组件 
    <Son :title="myTitle"></Son>
  </div>
</template>

<script>
import Son from './components/Son.vue'
export default {
  name: 'App',
  data() {
    return {
      myTitle: '学前端，就来黑马程序员',
    }
  },
}
</script>
```

子组件Son.vue

```vue
<template>
  <div class="son" style="border:3px solid #000;margin:10px">
    我是Son组件 {{ title }}
  </div>
</template>

<script>
export default {
  //	通过 props 进行接收
  props: ['title']
}
</script>
```

### 子向父通信

子组件利用 `$emit` 通知父组件，进行修改更新

子向父传值步骤

1. $emit触发事件，给父组件发送消息通知
2. 父组件监听$emit触发的事件
3. 提供处理函数，在函数的性参中获取传过来的参数

父组件App.vue

```vue
<template>
  <div class="app" style="border: 3px solid #000; margin: 10px">
    我是APP组件 
    <Son :title="myTitle" @changeTitle="handleChange"></Son>
  </div>
</template>

<script>
import Son from './components/Son.vue'
export default {
  name: 'App',
  data() {
    return {
      myTitle: '学前端，就来黑马程序员',
    }
  },
  methods:{
    //	提供处理函数，提供逻辑
    handleChange (newTitle) {
      this.myTitle = newTitle
    }
  },
}
</script>
```

子组件Son.vue

```vue
<template>
  <div class="son" style="border:3px solid #000;margin:10px">
    我是Son组件 {{ title }}
    <button @click="changeFn">修改title</button>
  </div>
</template>

<script>
export default {
  props: ['title'],
  methods: {
    changeFn() {
      //	通过 $emit，向父组件发送消息通知
      this.$emit('changeTitle', '传智教育')
    }
  }
}
</script>
```

## props

定义：`组件上`注册的一些`自定义属性`

作用：向子组件传递数据

特点

1. 可以传递`任意数量`的 prop
2. 可以传递`任意类型`的 prop

父组件App.vue

```vue
<template>
  <div class="app">
    <UserInfo
      :username="username"
      :age="age"
      :isSingle="isSingle"
      :car="car"
      :hobby="hobby"
    ></UserInfo>
  </div>
</template>

<script>
import UserInfo from './components/UserInfo.vue'
export default {
  data() {
    return {
      username: '小帅',
      age: 28,
      isSingle: true,
      car: {
        brand: '宝马',
      },
      hobby: ['篮球', '足球', '羽毛球'],
    }
  },
  components: {
    UserInfo,
  },
}
</script>
```

子组件UserInfo.vue

```vue
<template>
  <div class="userinfo">
    <h3>我是个人信息组件</h3>
    <div>姓名：{{ username }}</div>
    <div>年龄：{{ age }}</div>
    <div>是否单身：{{ isSingle ? '是' : '否' }}</div>
    <div>座驾：{{ car.brand }}</div>
    <div>兴趣爱好：{{ hobby.join('、') }}</div>
  </div>
</template>

<script>
export default {
  props: ['username', 'age', 'isSingle', 'car', 'hobby']
}
</script>
```

### props的校验

作用：为组件的 prop 指定`验证要求`，不符合要求，控制台就会有`错误提示` → 帮助开发者，快速发现错误

语法

- `类型校验`

  ~~~js
  props: {
    校验的属性名: 类型	//	Number、String、Boolean...
  }
  ~~~

- 非空校验

- 默认值

- 自定义校验

~~~js
props: {
  校验的属性名: {
    type: 类型,  // Number String Boolean ...
    required: true, // 是否必填
    default: 默认值, // 默认值
    validator (value) {
      // 自定义校验逻辑
      return 是否通过校验
    }
  }
},
~~~

App.vue

```vue
<template>
  <div class="app">
    <BaseProgress :w="width"></BaseProgress>
  </div>
</template>

<script>
import BaseProgress from './components/BaseProgress.vue'
export default {
  data() {
    return {
      width: 30,
    }
  },
  components: {
    BaseProgress,
  },
}
</script>

<style>
</style>
```

BaseProgress.vue

```vue
<template>
  <div class="base-progress">
    <div class="inner" :style="{ width: w + '%' }">
      <span>{{ w }}%</span>
    </div>
  </div>
</template>

<script>
export default {
  //	基础写法
  //	props: {
  //		w: Number,
  //	},
  
  //	完整写法（类型，非空，默认，自定义校验）
  props: {
    w: {
      type: Number,
      required: true,
      default: 0,
      validator(val) {
        // console.log(val)
        if (val >= 100 || val <= 0) {
          console.error('传入的范围必须是0-100之间')
          return false
        } else {
          return true
        }
      },
    },
  },
}
</script>
```

> default和required一般不同时写（因为当时必填项时，肯定是有值的）
>
> default后面如果是简单类型的值，可以直接写默认。如果是复杂类型的值，则需要以函数的形式return一个默认值

### props&data、单向数据流

共同点：都可以给组件提供数据

区别（`谁的数据谁负责`）

- data 的数据是`自己`的  →   随便改  
- prop 的数据是`外部`的  →   不能直接改，要遵循`单向数据流`

单向数据流：父级 props 的数据更新，会向下流动，影响子组件。这个数据流动是单向的

App.vue

```vue
<template>
  <div class="app">
    <BaseCount :count="count" @changeCount="handleChange"></BaseCount>
  </div>
</template>

<script>
import BaseCount from './components/BaseCount.vue'
export default {
  components:{
    BaseCount
  },
  data(){
    return {
      count: 666
    }
  },
  methods: {
    handleChange (newCount) {
      this.count = newCount
    }
  }
}
</script>
```

BaseCount.vue

```vue
<template>
  <div class="base-count">
    <button @click="handleSub">-</button>
    <span>{{ count }}</span>
    <button @click="handleAdd">+</button>
  </div>
</template>

<script>
export default {
  // 1.自己的数据随便修改  （谁的数据 谁负责）
  // data () {
  //   return {
  //     count: 100,
  //   }
  // },
  // 2.外部传过来的数据 不能随便修改
  props: {
    count: {
      type: Number,
    }, 
  },
  methods: {
    handleAdd () {
      //	子传父 this.$emit(事件名,参数)
      this.$emit('changeCount', this.count + 1)
    },
    handleSub () {
      this.$emit('changeCount', this.count - 1)
    },
  }
}
</script>
```

## 非父子通信

### event bus 事件总线

作用：非父子组件之间，进行`简易`消息传递。(复杂场景→ Vuex)

步骤：

1. 创建一个都能访问的事件总线 （空Vue实例）→ utils / EventBus.js

   ```js
   import Vue from 'vue'
   const Bus = new Vue()
   export default Bus
   ```

2. A 组件（接受方），监听 `Bus 实例`的 `$on` 事件（订阅事件）

   ```vue
   created () {
     Bus.$on('sendMsg', (msg) => {
       this.msg = msg
     })
   }
   ```

3. B组件（发送方），触发 `Bus 实例`的 `$emit` 事件（发布消息）

   ```vue
   Bus.$emit('sendMsg', '这是一个消息')
   ```

EventBus.js

```js
import Vue from 'vue'
const Bus  =  new Vue()
export default Bus
```

BaseA.vue(接受方)

```vue
<template>
  <div class="base-a">
    我是A组件（接收方）
    <p>{{msg}}</p>  
  </div>
</template>

<script>
import Bus from '../utils/EventBus'
export default {
  data() {
    return {
      msg: '',
    }
  },
  created () {
    Bus.$on('sendMsg', (msg) => {
      this.msg = msg
    })
  }
}
</script>
```

BaseB.vue(发送方)

```vue
<template>
  <div class="base-b">
    <div>我是B组件（发布方）</div>
    <button @click="clickSend">发送消息</button>
  </div>
</template>

<script>
import Bus from '../utils/EventBus'
export default {
  methods: {
    clickSend() {
      Bus.$emit('sendMsg', '今日晴天，适合郊游')
    }
  }
}
</script>
```

### provide & inject

作用：`跨层级`共享数据

语法：

1. 父组件 provide提供数据

```js
export default {
  provide () {
    return {
       // 普通类型【非响应式】
       color: this.color, 
       // 复杂类型【响应式】
       userInfo: this.userInfo, 
    }
  },
  data() {
    return {
      color: 'pink',
      userInfo: {
        name: 'zs',
        age: 18
      }
    }
  }
}
```

2.子/孙组件 inject获取数据

```js
<template>
  <div class="grandSon">
    我是GrandSon组件
		{{ color }} - {{ userInfo.name}}
	</div>
</template>

<script>
export default {
  inject: ['color','userInfo']
}
</script>
```

>  provide提供的简单类型的数据不是响应式的，复杂类型数据是响应式。（推荐提供复杂类型数据）
>
> 子/孙组件通过inject获取的数据，不能在自身组件内修改

## v-model

原理：v-model本质上是一个`语法糖`。例如应用在输入框上，就是 `value 属性`和 `input事件`的合写

```vue
<template>
  <div id="app" >
    <input v-model="msg" type="text">

    <input :value="msg" @input="msg = $event.target.value" type="text">
  </div>
</template>

```

作用：

提供数据的双向绑定

- 数据变，视图跟着变 `:value`
- 视图变，数据跟着变 `@input`

> `$event` 用于在模板中，获取事件的形参

```vue
<template>
  <div class="app">
    <input v-model="msg1" type="text"  />
    <br /> 
    <input :value="msg2" @input="msg2 = $even.target.value" type="text" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      msg1: '',
      msg2: '',
    }
  },
}
</script> 
<style>
</style>
```

### v-model使用在其他表单元素上的原理

不同的表单元素， v-model 在底层的处理机制是不一样的。比如给 checkbox 使用 v-model

底层处理的是 checked 属性和 change 事件。

不过咱们只需要掌握应用在文本框上的原理即可

## 表单类组件封装

实现子组件和父组件数据的`双向绑定` 

1. `父传子`：数据应该是父组件 `props` 传递过来的，v-model `拆解`绑定数据
2. `子传父`：监听输入，子传父传值给父组件修改

App.vue

```vue
<template>
  <div class="app">
    <BaseSelect :cityId="selectId" @changeId="selectId = $event"></BaseSelect>
  </div>
</template>

<script>
import BaseSelect from './components/BaseSelect.vue'
export default {
  data() {
    return {
      selectId: '102',
    }
  },
  components: {
    BaseSelect,
  },
}
</script>
```

BaseSelect.vue

```vue
<template>
  <div>
    <select :value="cityId" @change="handleChange">
      <option value="101">北京</option>
      <option value="102">上海</option>
      <option value="103">武汉</option>
      <option value="104">广州</option>
      <option value="105">深圳</option>
    </select>
  </div>
</template>

<script>
export default {
  props: {
    cityId: String
  },
  methods: {
    handleChange(e) {
      this.$emit('changeId', e.target.value)
    }
  }
}
</script>
```

### v-model简化代码

父组件通过 v-model `简化代码`，实现子组件和父组件数据`双向绑定`

v-model 其实就是 :value 和 @input 事件的简写

- 子组件：props 通过 `value` 接收数据，事件触发 `input`
- 父组件：`v-model` 直接绑定数据

子组件

```vue
<select :value="value" @change="handleChange">...</select>
props: {
  value: String
},
methods: {
  handleChange (e) {
    this.$emit('input', e.target.value)
  }
}
```

父组件

```vue
<BaseSelect v-model="selectId"></BaseSelect>
```

## .sync修饰符

作用：可以实现`子组件`与`父组件数据`的`双向绑定`，简化代码

特点：prop 属性名可以`自定义`，非固定为 `value`

简单理解：子组件可以修改父组件传过来的props值

场景：封装弹框类的基础组件， `visible 属性` true 显示 false 隐藏

本质：.sync 修饰符 就是 `: 属性名`和 `@update : 属性名`合写

语法：

父组件

```vue
//.sync写法
<BaseDialog :visible.sync="isShow" />
--------------------------------------
//完整写法
<BaseDialog 
  :visible="isShow" 
  @update:visible="isShow = $event" 
/>
```

子组件

```vue
props: {
  visible: Boolean
},

this.$emit('update:visible', false)
```

App.vue

```vue
<template>
  <div class="app">
    <button @click="isShow = true">退出按钮</button>
    <BaseDialog :visible.sync="isShow"></BaseDialog>
  </div>
</template>

<script>
import BaseDialog from './components/BaseDialog.vue'
export default {
  data() {
    return {
      isShow: false,
    }
  },
  components: {
    BaseDialog,
  },
}
</script>

<style>
</style>
```

BaseDialog.vue

```vue
<template>
  <div v-show="visible" class="base-dialog-wrap" v-show="isShow">
    <div class="base-dialog">
      <div class="title">
        <h3>温馨提示：</h3>
        <button class="close" @click="close">x</button>
      </div>
      <div class="content">
        <p>你确认要退出本系统么？</p>
      </div>
      <div class="footer">
        <button @click="close">确认</button>
        <button @click="close">取消</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    visible: Boolean,
  },
  methods: {
    close() {
      this.$emit('update:visible', false)
    }
  }
}
</script>
```

## ref 和 $refs

作用：利用 ref 和 $refs 可以用于`获取 dom 元素`或`组件实例`

`特点`：查找范围 →  `当前组件内(更精确稳定)`

### 获取 dom

1.给要获取的盒子添加 ref 属性

```html
<div ref="chartRef">我是渲染图表的容器</div>
```

2.获取时通过 this.\$refs.xxx 获取目标标签

```html
mounted () {
  console.log(this.$refs.chartRef)
}
```

> 之前只用document.querySelect('.box') 获取的是整个页面中的盒子

App.vue

```vue
<template>
  <div class="app">
    <BaseChart></BaseChart>
  </div>
</template>

<script>
import BaseChart from './components/BaseChart.vue'
export default {
  components:{
    BaseChart
  }
}
</script>
```

BaseChart.vue

```vue
<template>
  <div class="base-chart-box" ref="mychart">子组件</div>
</template>

<script>
// yarn add echarts 或者 npm i echarts
import * as echarts from 'echarts'

export default {
  mounted() {
    // 基于准备好的dom，初始化echarts实例
    var myChart = echarts.init(this.$refs.mychart)
    // 绘制图表
    myChart.setOption({
      title: {
        text: 'ECharts 入门示例',
      },
      tooltip: {},
      xAxis: {
        data: ['衬衫', '羊毛衫', '雪纺衫', '裤子', '高跟鞋', '袜子'],
      },
      yAxis: {},
      series: [
        {
          name: '销量',
          type: 'bar',
          data: [5, 20, 36, 10, 10, 20],
        },
      ],
    })
  },
}
</script>
```

### 获取组件实例

1. 目标组件 - 添加 ref 属性

~~~ vue
<BaseForm ref="baseForm"></BaseForm>
~~~

2. 恰当时机，通过 this.$refs.xxx 获取目标组件，就可以`调用组件对象里面的方法`

~~~vue
this.$refs.baseForm.组件方法()
~~~

App.vue

```vue
<template>
  <div class="app">
    <BaseFrom ref="baseForm"></BaseFrom>
    
    <button @click="handleGet">获取数据</button>
    <button @click="handleReset">重置数据</button>
  </div>
</template>

<script>
import BaseFrom from './components/BaseFrom.vue'
export default {
  components:{
    BaseFrom
  },
  data() {
  	return {
  
		}
	},
  methods: {
    handleGet() {
      this.$refs.baseForm.getValues()
    },
    handleReset() {
      this.$refs.baseForm.resetValues()
    },
  }
}
</script>
```

BaseFrom.vue

```vue
<template>
  <form action="">
    账号：<input type="text" v-model="account" />
    密码：<input type="password" v-model="password" />
  </form>
</template>

<script>
export default {
  data() {
    return {
      account: '',
      password: ''
    }
  },
  methods: {
    //	收集表单数据，返回一个对象
    getValues() {
      return {
        account: this.account,
        password: this.password
      }
    },
    //	重置表单
    resetValues() {
      this.account = '',
      this.password = ''
    }
  },
}
</script>
```

## 异步更新 & $nextTick

需求：编辑标题,  编辑框自动聚焦

1. 点击编辑，显示编辑框
2. 让编辑框，`立刻获取焦点`

~~~vue
this.isShowEdit = true  	// 显示输入框
this.$refs.inp.focus() 		// 获取焦点
~~~

问题："显示之后"，立刻获取焦点是不能成功的！

原因：`Vue 是异步更新 DOM (提升性能)`

解决方案：

$nextTick：`等 DOM更新后`，`立刻触发`执行此方法里的函数体

语法： `this.$nextTick(函数体)`

```js
this.$nextTick(() => {
  this.$refs.inp.focus()
})
```

> $nextTick 内的函数体 一定是箭头函数，这样才能让函数内部的this指向Vue实例

```vue
<template>
  <div class="app">
    <div v-if="isShowEdit">
      <input type="text" v-model="editValue" ref="inp" />
      <button>确认</button>
    </div>
    <div v-else>
      <span>{{ title }}</span>
      <button @click="editFn">编辑</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: '大标题',
      isShowEdit: false,
      editValue: '',
    }
  },
  methods: {
    editFn() {
      // 显示输入框
      this.isShowEdit = true  
      // 获取焦点
      this.$nextTick(() => {
        this.$refs.inp.focus() 
      })
    }
  },
}
</script> 
```

## 自定义指令

内置指令：v-html、v-if、v-bind、v-on... 这都是Vue给咱们内置的一些指令，可以直接使用，同时Vue也支持让开发者，自己注册一些指令。这些指令被称为自定义指令

每个指令都有自己各自独立的功能

自定义指令：自己定义的指令，可以`封装一些 DOM 操作`，扩展额外的功能

语法：

- 全局注册

  ```js
  //在main.js中
  Vue.directive('指令名', {
    //	inserted 会在指令所在的元素，被插入到页面时触发
    //	el 就是指令所插入的元素
    "inserted" (el) {
      // 可以对 el 标签，扩展额外功能
      el.focus()
    }
  })
  ```

- 局部注册

  ```vue
  //在Vue组件的配置项中
  directives: {
    "指令名": {
      inserted () {
        // 可以对 el 标签，扩展额外功能
        el.focus()
      }
    }
  }
  ```

使用指令

注意：在使用指令的时候，一定要先注册，再使用，否则会报错
使用指令语法： v-指令名。如：<input type="text"  v-focus/>  

注册指令时不用加v-前缀，但使用时一定要加v-前缀

指令中的配置项介绍

inserted：被绑定元素插入父节点时调用的钩子函数

el：使用指令的那个 DOM 元素

需求：当页面加载时，让元素获取焦点（ `autofocus 在 safari 浏览器有兼容性`）

App.vue

```vue
<template>
  <div>
    <h1>自定义指令</h1>
    <input v-focus ref="inp" type="text">
  </div>
</template>

<script>
  export default {
    //	局部注册指令
    directives: {
      //	指令名：指令配置项
      focus: {
        inserted (el) {
          el.focus()
        }
      }
    }
  }
</script>
```

main.js

~~~js
//	全局注册指令
Vue.directive('focus', {
  //	inserted 会在指令所在的元素被插入到页面中时触发
  "inserted" (el) {
    // el 指令所绑定的元素
    el.focus()
  }
})
~~~

### 指令的值

inserted：提供的是元素被添加到页面中时的逻辑

update：指令的值修改的时候触发，提供值变化后，dom 更新的逻辑

语法

1.在绑定指令时，可以通过“等号”的形式为指令绑定`具体的参数值`

```html
<div v-color="color">我是内容</div>
```

2.通过 `binding.value` 可以拿到指令值，指令值修改会`触发 update 函数`

```js
directives: {
  color: {
    inserted (el, binding) {
      el.style.color = binding.value
    },
    update (el, binding) {
      el.style.color = binding.value
    }
  }
}
```

App.vue

```vue
<template>
  <div>
     <!--显示红色--> 
    <h2 v-color="color1">指令的值1测试</h2>
     <!--显示蓝色--> 
    <h2 v-color="color2">指令的值2测试</h2>
     <button>
        改变第一个h1的颜色
    </button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      color1: 'red',
      color2: 'blue'
    }
  },
  directives: {
    color: {
      //	inserted 提供的是元素被添加到页面中时的逻辑
      inserted (el, binding) {
        el.style.color = binding.value
      },
      //	update 指令的值修改的时候触发，提供值变化后，dom 更新的逻辑
      update (el, binding) {
        el.style.color = binding.value
      }
    }
  }
}
</script>
```

### v-loading指令的封装

场景：实际开发过程中，发送`请求需要时间`，在请求的数据未回来时，页面会处于`空白状态`  =>  `用户体验不好`，我们可以封装一个 v-loading 指令，实现加载中的效果

`inserted` 钩子中，binding.value 判断指令的值，设置`默认`状态

`update` 钩子中，binding.value 判断指令的值，设置`类名`状态

分析：

1.本质 loading 效果就是一个蒙层，盖在了盒子上

2.数据请求中，开启 loading 状态，添加蒙层

3.数据请求完毕，关闭 loading 状态，移除蒙层

实现：

1.准备一个 loading 类，通过伪元素定位，设置宽高，实现蒙层

2.开启关闭 loading 状态（添加移除蒙层），本质只需要添加移除类即可

3.结合自定义指令的语法进行封装复用

```css
.loading:before {
  content: "";
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: #fff url("./loading.gif") no-repeat center;
}
```

```html
<template>
  <div class="main">
    <div class="box" v-loading="isLoading">
      <ul>
        <li v-for="item in list" :key="item.id" class="news">
          <div class="left">
            <div class="title">{{ item.title }}</div>
            <div class="info">
              <span>{{ item.source }}</span>
              <span>{{ item.time }}</span>
            </div>
          </div>
          <div class="right">
            <img :src="item.img" alt="">
          </div>
        </li>
      </ul>
    </div> 
    <div class="box2" v-loading="isLoading2"></div>
  </div>
</template>

<script>
// 安装axios =>  yarn add axios || npm i axios
import axios from 'axios'

// 接口地址：http://hmajax.itheima.net/api/news
// 请求方式：get
export default {
  data () {
    return {
      list: [],
      isLoading: true,
      isLoading2: true
    }
  },
  async created () {
    // 1. 发送请求获取数据
    const res = await axios.get('http://hmajax.itheima.net/api/news')
    
    setTimeout(() => {
      // 2. 更新到 list 中，用于页面渲染 v-for
      this.list = res.data.data
      this.isLoading = false
    }, 2000)
  },
  directives: {
    loading: {
      inserted(el, binding) {
        binding.value ? el.classList.add('loading') : el.classList.remove('loading')
      },
      update(el, binding) {
        binding.value ? el.classList.add('loading') : el.classList.remove('loading')
      }
    }
  }
}
</script>

<style>
.loading:before {
  content: '';
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: #fff url('./loading.gif') no-repeat center;
}
</style>
```

## 插槽

### 默认插槽

作用：让组件内部的一些`结构`支持`自定义`

组件的内容部分，`不希望写死`，希望能使用的时候`自定义`时可以使用插槽

插槽的基本语法：

1. 组件内需要定制的结构部分，改用**<slot></slot>**占位
2. 使用组件时, **<MyDialog></MyDialog>**标签内部, 传入结构替换slot
3. 给插槽传入内容时，可以传入纯文本、html标签、组件

MyDialog.vue

```vue
<template>
  <div class="dialog">
    <div class="dialog-header">
      <h3>友情提示</h3>
      <span class="close">✖️</span>
    </div>

    <div class="dialog-content">
      <slot></slot>
    </div>
    <div class="dialog-footer">
      <button>取消</button>
      <button>确认</button>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {

    }
  }
}
</script>
```

App.vue

```vue
<template>
  <div>
    <MyDialog>需要删除吗？</MyDialog>
  </div>
</template>

<script>
import MyDialog from './components/MyDialog.vue'
export default {
  data () {
    return {

    }
  },
  components: {
    MyDialog
  }
}
</script>

<style>
body {
  background-color: #b3b3b3;
}
</style>
```

### 后备内容（默认值）

通过插槽完成了内容的定制，传什么显示什么, 但是如果不传，则是空白，我们可以给插槽设置`默认显示内容`

封装组件时，可以为预留的 `<slot>` 插槽提供`后备内容`（默认内容）。

语法：

在 <slot> 标签内，放置内容, 作为默认显示内容

效果：

- 外部使用组件时，不传东西，则slot会显示后备内容 
- 外部使用组件时，传东西了，则slot整体会被换掉

~~~vue
<slot>我是默认的文本内容</slot>
~~~

### 具名插槽

一个组件内有多处结构，需要外部传入标签，进行定制 

弹框中有三处不同，但是默认插槽只能定制一个位置，这时我们可以使用具名插槽

语法：

- 多个 slot 使用 name 属性区分名字 

~~~vue
<div class="dialog-header">
  <slot name="head"></slot>
</div>
<div class="dialog-content">
  <slot name="content"></slot>
</div>
<div class="dialog-footer">
  <slot name="footer"></slot>
</div>
~~~

- template 配合 v-slot: 名字来分发对应标签

~~~vue
<MyDialog>
  <template v-slot:head>
  	大标题
  </template>
  <template v-slot:content>
  	内容文本
  </template>
  <template v-slot:footer>
  	<button>按钮</button>
  </template>
</MyDialog>
~~~

- `v-slot:插槽名`可以简化成`#插槽名`

> 一旦插槽起了名字就是具名插槽，具名插槽只支持定向分发
>
> 引用需要通过 template 标签包裹需要分发的结构，包成一个整体

### 作用域插槽

插槽分类：

- 默认插槽
- 具名插槽

插槽只有两种，`作用域插槽`不属于插槽的一种分类，只是插槽的一个传参`语法`

作用：定义 slot 插槽的同时，是可以`传值`的。给`插槽`上可以`绑定数据`，将来`使用组件时可以用`

场景：封装表格组件

1. 父传子，动态渲染表格内容
2. 利用默认插槽，定制操作列
3. 删除或查看都需要用到`当前项的 id`，属于`组件内部的数据`，通过`作用域插槽`传值绑定，进而使用

作用域插槽使用步骤：

1. 给 slot 标签, 以 添加属性的方式传值

   ```vue
   <slot :id="item.id" msg="测试文本"></slot>
   ```

2. 所有添加的属性, 都会被收集到一个对象中

   ```vue
   { id: 3, msg: '测试文本' }
   ```

3. 在 template 中, 通过  ` #插槽名="obj"` 接收，默认插槽名为 `default`

   ```vue
   <MyTable :list="list">
     <template #default="obj">
       <button @click="del(obj.id)">删除</button>
     </template>
   </MyTable>
   ```

MyTable.vue

```vue
<template>
  <table class="my-table">
    <thead>
      <tr>
        <th>序号</th>
        <th>姓名</th>
        <th>年纪</th>
        <th>操作</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(item, index) in data" :key="item.id">
        <td>{{ index + 1 }}</td>
        <td>{{ item.name }}</td>
        <td>{{ item.age }}</td>
        <td>
          <slot :row="item" msg="测试文本">删除</slot>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  props: {
    data: Array
  }
}
</script>
```

App.vue

```vue
<template>
  <div>
    <MyTable :data="list">
  		<template #default="obj">
				<button @click="del(obj.row.id)">
          删除
  			</button>
			</template>
  	</MyTable>
    <MyTable :data="list2">
			<template #default="{ row }">
				<button @click="show(row)">
          删除
  			</button>
			</template>
		</MyTable>
  </div>
</template>

<script>
  import MyTable from './components/MyTable.vue'
  export default {
    data () {
      return {
     	list: [
            { id: 1, name: '张小花', age: 18 },
            { id: 2, name: '孙大明', age: 19 },
            { id: 3, name: '刘德忠', age: 17 },
          ],
          list2: [
            { id: 1, name: '赵小云', age: 18 },
            { id: 2, name: '刘蓓蓓', age: 19 },
            { id: 3, name: '姜肖泰', age: 17 },
          ]
      }
    },
    methods: {
      del(id) {
        this.list = this.list.filter(item => item.id !== id)
      },
      show(row) {
        alert(`姓名：${row.name}，年龄：${row.age}`)
      }
    },
    components: {
      MyTable
    }
  }
</script>
```

## 单页应用程序介绍

概念：

单页应用程序：SPA【Single Page Application】是指所有的功能都在`一个 html 页面`上实现

具体示例：

单页应用网站： 网易云音乐  <https://music.163.com/>

多页应用网站：京东  https://jd.com/

单页应用 VS 多页面应用

单页应用类网站：系统类网站 / 内部网站 / 文档类网站 / 移动端站点

多页应用类网站：公司官网 / 电商类网站

|          |        单页        |       多页       |
| :------: | :----------------: | :--------------: |
| 实现方式 |   一个 html 页面   |  多个 html 页面  |
| 页面性能 | `按需更新，性能高` | 整页更新，性能低 |
| 开发效率 |        `高`        |       中等       |
| 用户体验 |      `非常好`      |       一般       |
| 学习成本 |         高         |       中等       |
| 首屏加载 |         慢         |        快        |
|   SEO    |         差         |        优        |

## 路由

单页面应用程序，之所以开发效率高，性能好，用户体验好

最大的原因就是：`页面按需更新`

比如当点击【发现音乐】和【关注】时，只是更新下面部分内容，对于头部是不更新的

要按需更新，首先就需要明确：`访问路径`和`组件`的对应关系！

访问路径 和 组件的对应关系如何确定呢？`路由`

路由的介绍

生活中的路由：设备和 ip 的`映射`关系

Vue中的路由：`路径`和`组件`的`映射`关系

### 路由的基本使用

认识插件 VueRouter，掌握 VueRouter 的基本使用步骤

作用：`修改`地址栏`路径`时，`切换显示`匹配的`组件`

说明：Vue 官方的一个路由插件，是一个第三方包

官网：<https://v3.router.vuejs.org/zh/>

### VueRouter的使用（5+2）

固定5个固定的步骤（不用死背，熟能生巧）

1. 下载 VueRouter 模块到当前工程，版本3.6.5（v2版本）

   ```bash
   yarn add vue-router@3.6.5
   ```

2. main.js中引入VueRouter

   ```vue
   import VueRouter from 'vue-router'
   ```

3. 安装注册

   ```vue
   Vue.use(VueRouter)
   ```

4. 创建路由对象

   ```vue
   const router = new VueRouter()
   ```

5. 注入，将路由对象注入到new Vue实例中，建立关联

   ```vue
   new Vue({
     render: h => h(App),
     router:router
   }).$mount('#app')

   ```

当我们配置完以上5步之后 就可以看到浏览器地址栏中的路由 变成了 /#/ 的形式。表示项目的路由已经被Vue-Router管理了

main.js

```vue
// 路由的使用步骤 5 + 2
// 5个基础步骤
// 1. 下载 v3.6.5
// yarn add vue-router@3.6.5
// 2. 引入
// 3. 安装注册 Vue.use(Vue插件)
// 4. 创建路由对象
// 5. 注入到new Vue中，建立关联


import VueRouter from 'vue-router'
Vue.use(VueRouter) // VueRouter插件初始化

const router = new VueRouter()

new Vue({
  render: h => h(App),
  router
}).$mount('#app')
```

两个核心步骤：

1. 创建需要的组件 (views目录)，配置路由规则（路径组件的`匹配关系`）

main.js

~~~js
import Find from './views/Find.vue'
import My from './views/My.vue'
import Friend from './views/Friend.vue'

const router = new VueRouter({
  //  路由规则
  //  route 一条路由规则 { path: 路径, component: 组件 }
  routes: [
    { path: '/find', component: Find },
    { path: '/my', component: My },
    { path: '/friend', component: Friend },
  ]
})
~~~

2. 配置导航，配置路由出口(路径匹配的`组件显示的位置`)

App.vue

```vue
<div>
	<div class="footer_wrap">
    <a href="#/find">发现音乐</a>
    <a href="#/my">我的音乐</a>
    <a href="#/friend">朋友</a>
  </div>
  <div class="top">
    //	路由出口 → 匹配的组件所展示的位置
    <router-view></router-view>
  </div>
</div>
```
## 组件的存放目录问题

注意：`.vue文件本质无区别`

`组件分类`

 .vue文件分为2类，都是 .vue文件（本质无区别）

- 页面组件 （配置路由规则时使用的组件）
- 复用组件（多个组件中都使用到的组件）

存放目录：

分类开来的目的就是为了`更易维护`

1. src/views文件夹

   `页面组件` - 页面展示 - 配合路由用

2. src/components文件夹

   `复用组件` - 展示数据 - 常用于复用

## 路由的封装抽离

问题：所有的路由配置都在main.js中合适吗？

目标：将路由模块抽离出来，写在 sre/router/index.js 中，引用到 main.js 中

好处：`拆分模块，利于维护`

路径简写：

脚手架环境下 `@指代src目录`，可以用于快速引入组件

main.js

~~~js
import rouer from './router/index.js'

new Vue({
  render: h => h(App),
  router
}).$mount('#app')
~~~

## 声明式导航

### 导航链接

实现导航高亮效果，如果使用a标签进行跳转的话，需要给当前跳转的导航加样式，同时要移除上一个a标签的样式，太麻烦！！！

vue-router 提供了一个全局组件 router-link (取代 a 标签)

- `能跳转`，配置 to 属性指定路径(`必须`) 。本质还是 a 标签，`to 无需 #`
- `能高亮`，默认就会提供`高亮类名`，可以直接设置高亮样式

语法： `<router-link to="path的值">发现音乐</router-link>`

```vue
  <div>
    <div class="footer_wrap">
      <router-link to="/find">发现音乐</router-link>
      <router-link to="/my">我的音乐</router-link>
      <router-link to="/friend">朋友</router-link>
    </div>
    <div class="top">
      <!-- 路由出口 → 匹配的组件所展示的位置 -->
      <router-view></router-view>
    </div>
  </div>
```

通过 router-link 自带的两个样式进行高亮

使用 router-link 跳转后，我们发现。当前点击的链接默认加了两个class的值 `router-link-exact-active`和`router-link-active`

我们可以给任意一个class属性添加高亮样式即可实现功能

### 两个类名

当我们使用<router-link></router-link>跳转时，自动给当前导航加了`两个类名`

1. router-link-active

`模糊匹配（用的多）`

to="/my"  可以匹配 /my    /my/a    /my/b    ....  

只要是以 /my 开头的路径 都可以和 to="/my" 匹配到

2. router-link-exact-active

`精确匹配`

to="/my" 仅可以匹配  /my

在地址栏中输入二级路由查看类名的添加

### 自定义类名（了解）

router-link 的两个高亮类名太长了，我们能`定制`

我们可以在创建路由对象时，额外配置两个配置项即可。 `linkActiveClass`和`linkExactActiveClass`

```js
const router = new VueRouter({
  routes: [...],
  linkActiveClass: "类名1",
  linkExactActiveClass: "类名2"
})
```

### 跳转传参

在跳转路由时，进行传参

比如：现在我们在搜索页点击了热门搜索链接，跳转到详情页，`需要把点击的内容带到详情页`，改怎么办呢？

跳转传参：我们可以通过两种方式，在跳转的时候把所需要的参数传到其他页面中

- 查询参数传参
- 动态路由传参

#### 查询参数传参

- 传参语法：

  `<router-link to="/path?参数名=值"></router-link>`

- 接受参数：

  固定用法：`$route.query.参数名`

Home.vue

```vue
<template>
  <div class="home">
    <div class="logo-box"></div>
    <div class="search-box">
      <input type="text">
      <button>搜索一下</button>
    </div>
    <div class="hot-link">
      热门搜索：
      <router-link to="/search?key=黑马程序员">黑马程序员</router-link>
      <router-link to="/search?key=前端培训">前端培训</router-link>
      <router-link to="/search?key=如何成为前端大牛">如何成为前端大牛</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FindMusic'
}
</script>
```

Search.vue

```vue
<template>
  <div class="search">
    <p>搜索关键字: {{ $route.query.key }}</p>
    <p>搜索结果: </p>
    <ul>
      <li>.............</li>
      <li>.............</li>
      <li>.............</li>
      <li>.............</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'MyFriend',
  created () {
    // 在created中，获取路由参数
    //	this.$route.query.参数名 获取
    console.log(this.$route.query.key)
  }
}
</script>
```

#### 动态路由传参

- 配置动态路由

  > 动态路由后面的参数可以随便起名，但要有语义

  ```js
  const router = new VueRouter({
    routes: [
      ...,
      { 
        path: '/search/:words', 
        component: Search 
      }
    ]
  })
  ```

- 配置导航链接

  to="/path`/参数值`"

- 对应页面组件接受参数

  $route`.params.参数名`

  > params后面的参数名要和动态路由配置的参数保持一致

Home.vue

```vue
<template>
  <div class="home">
    <div class="logo-box"></div>
    <div class="search-box">
      <input type="text">
      <button>搜索一下</button>
    </div>
    <div class="hot-link">
      热门搜索：
      <router-link to="/search/黑马程序员">黑马程序员</router-link>
      <router-link to="/search/前端培训">前端培训</router-link>
      <router-link to="/search/如何成为前端大牛">如何成为前端大牛</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FindMusic'
}
</script>
```

Search.vue

```vue
<template>
  <div class="search">
    <p>搜索关键字: {{ $route.params.words }}</p>
    <p>搜索结果: </p>
    <ul>
      <li>.............</li>
      <li>.............</li>
      <li>.............</li>
      <li>.............</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'MyFriend',
  created () {
    // 在created中，获取路由参数
    //	this.$route.params.参数名 获取
    console.log(this.$route.params.words)
  }
}
</script>
```

#### 查询参数传参 VS 动态路由传参

1. 查询参数传参  (比较适合传`多个参数`) 

   1. 跳转：to="/path`?参数名=值&参数名2=值`"
   2. 获取：$route`.query.参数名`

2. 动态路由传参 (`优雅简洁`，传单个参数比较方便)

   1. 配置动态路由：path: "/path`/:参数名`" 
   2. 跳转：to="/path`/参数值`"
   3. 获取：$route`.params.参数名 `

   注意：动态路由也可以传多个参数，但一般只传一个

#### 动态路由参数的可选符(了解)

配了路由 path:"/search/:words"  为什么按下面步骤操作，会未匹配到组件，显示空白？

原因：

/search/:words  表示，`必须要传参数`。如果不传参数，也希望匹配，可以加个可选符"`?`"

```js
const router = new VueRouter({
  routes: [
 	...
    { path: '/search/:words?', component: Search }
  ]
})
```

## Vue路由

### 重定向

网页打开时， url 默认是 / 路径，未匹配到组件时，会出现空白

解决方案

重定向 → 匹配 path 后, 强制跳转 path 路径

语法：`{ path: 匹配路径, redirect: 重定向到的路径 }`

```js
const router = new VueRouter({
  routes: [
    { path: '/', redirect: '/home'},
 	 ...
  ]
})
```

### 404

作用：当路径找不到匹配时，给个提示页面

位置：

404的路由，虽然配置在任何一个位置都可以，但一般都配置在其他路由规则的`最后面`

语法：path: "*"   (任意路径) – 前面不匹配就命中最后这个

```js
import NotFind from '@/views/NotFind'

const router = new VueRouter({
  routes: [
    ...
    { path: '*', component: NotFound } //最后一个
  ]
})
```

NotFound.vue

```vue
<template>
  <div>
    <h1>404 Not Found</h1>
  </div>
</template>

<script>
export default {

}
</script>
```

router/index.js

```js
...
import NotFound from '@/views/NotFound'
...

// 创建了一个路由对象
const router = new VueRouter({
  routes: [
     ...
    { path: '*', component: NotFound }
  ]
})

export default router
```

### 模式设置

路由的路径看起来不自然, 有#，我们可以切成真正路径形式

- hash路由(默认)        例如:  http://localhost:8080/#/home
- history路由(常用)     例如: http://localhost:8080/home   (以后上线需要服务器端支持，开发环境webpack给规避掉了history模式的问题)

语法

```js
const router = new VueRouter({
    mode:'histroy', //默认是hash
    routes:[]
})
```

## 编程式导航

### 两种路由跳转方式

点击按钮跳转实现

编程式导航：用 JS 代码来进行跳转

两种语法：

- path 路径跳转 （简易方便）
- name 命名路由跳转 (适合 path 路径长的场景)

#### path路径跳转语法

特点：简易方便

```js
//简单写法
this.$router.push('路由路径')

//完整写法
this.$router.push({
  path: '路由路径'
})
```

#### name命名路由跳转

特点：适合` path 路径长`的场景

语法：

- 路由规则，必须配置name配置项

  ```js
  { name: '路由名', path: '/path/xxx', component: XXX },
  ```

- 通过name来进行跳转

  ```js
  this.$router.push({
    name: '路由名'
  })
  ```

### path路径跳转传参

点击搜索按钮，跳转需要把文本框中输入的内容传到下一个页面实现

两种传参方式

1.查询参数 

2.动态路由传参

两种跳转方式，对于两种传参方式都支持：

① path 路径跳转传参

② name 命名路由跳转传参

#### query传参

```js
//简单写法
this.$router.push('/路径?参数名1=参数值1&参数2=参数值2')
//完整写法，更适合传参
this.$router.push({
  path: '/路径',
  query: {
    参数名1: '参数值1',
    参数名2: '参数值2'
  }
})
```

接受参数的方式依然是：`$route.query.参数名`

#### 动态路由传参

```js
//简单写法
this.$router.push(`/路径/参数值`)
//完整写法
this.$router.push({
  path: `/路径/参数值`
})
```

接受参数的方式依然是：`$route.params.参数值` 

**注意：**path不能配合params使用

### name命名路由传参

#### query传参

```js
this.$router.push({
  name: '路由名字',
  query: {
    参数名1: '参数值1',
    参数名2: '参数值2'
  }
})
```

#### 动态路由传参

```js
this.$router.push({
  name: `路由名字`,
  params: {
    参数名: '参数值',
  }
})
```

## 二级路由配置

二级路由也叫嵌套路由，当然也可以嵌套三级、四级...

当在页面中点击链接跳转，只是部分内容切换时，我们可以使用嵌套路由

语法

- 在一级路由下，配置children属性即可
- 配置二级路由的出口

 1.在一级路由下，配置children属性

>  一级的路由path 需要加 `/`   二级路由的path不需要加 `/`

```js
const router = new VueRouter({
  routes: [
    {
      path: '/',
      component: Layout,
      children:[
        //children中的配置项 跟一级路由中的配置项一模一样 
        {path:'xxxx',component:xxxx.vue},
        {path:'xxxx',component:xxxx.vue},
      ]
    }
  ]
})
```

技巧：这些二级路由对应的组件渲染到哪个一级路由下，children就配置到哪个路由下边

2.配置二级路由的出口 <router-view></router-view>

**注意：** 配置了嵌套路由，一定配置对应的路由出口，否则不会渲染出对应的组件

Layout.vue

```vue
<template>
  <div class="h5-wrapper">
    <div class="content">
      <router-view></router-view>
    </div>
  ....
  </div>
</template>
```

router/index.js

```js
...
import Article from '@/views/Article.vue'
import Collect from '@/views/Collect.vue'
import Like from '@/views/Like.vue'
import User from '@/views/User.vue'
...

const router = new VueRouter({
  routes: [
    {
      path: '/',
      component: Layout,
      redirect: '/article',
      children:[
        {
          path:'/article',
          component:Article
        },
        {
          path:'/collect',
          component:Collect
        },
        {
          path:'/like',
          component:Like
        },
        {
          path:'/user',
          component:User
        }
      ]
    },
    ....
  ]
})

```

Layout.vue

```vue
<template>
  <div class="h5-wrapper">
    <div class="content">
      <!-- 内容部分 -->
      <router-view></router-view>
    </div>
    <nav class="tabbar">
      <a href="#/article">面经</a>
      <a href="#/collect">收藏</a>
      <a href="#/like">喜欢</a>
      <a href="#/user">我的</a>
    </nav>
  </div>
</template>
```

## 接口文档

```vue
请求地址: https://mock.boxuegu.com/mock/3083/articles
请求方式: get
```

## 组件缓存 keep-alive

从面经列表 点到 详情页，又点返回，数据重新加载了 →  希望回到原来的位置

原因

当路由被跳转后，原来所看到的组件就被销毁了（会执行组件内的beforeDestroy和destroyed生命周期钩子），重新返回后组件又被重新创建了（会执行组件内的beforeCreate,created,beforeMount,Mounted生命周期钩子），所以数据被加载了

解决方案

利用keep-alive把原来的组件给缓存下来

keep-alive 是 Vue 的内置组件，当它包裹动态组件时，会缓存不活动的组件实例，而不是销毁它们。

keep-alive 是一个抽象组件：它自身不会渲染成一个 DOM 元素，也不会出现在父组件中。

优点：

在组件切换过程中把切换出去的组件保留在内存中，防止重复渲染DOM，

减少加载时间及性能消耗，提高用户体验性。

App.vue

```vue
<template>
  <div class="h5-wrapper">
    <keep-alive>
      <router-view></router-view>
    </keep-alive>
  </div>
</template>
```

### keep-alive的三个属性

① `include`  ： 组件名数组，只有匹配的组件会被缓存

② exclude ： 组件名数组，任何匹配的组件都不会被缓存

③ max       ： 最多可以缓存多少组件实例

App.vue

```vue
<template>
  <div class="h5-wrapper">
    <keep-alive :include="['LayoutPage']">
      <router-view></router-view>
    </keep-alive>
  </div>
</template>
```

## 额外的两个生命周期钩子

keep-alive 的使用会触发两个生命周期函数

activated 当组件被激活（使用）的时候触发 →  进入这个页面的时候触发

deactivated 当组件不被使用的时候触发      →  离开这个页面的时候触发

组件缓存后就不会执行组件的 created，mounted，destroyed 等钩子了

所以其提供了actived 和deactived钩子，帮我们实现业务需求。

## VueCli 自定义创建项目

1.安装脚手架 (已安装)

```
npm i @vue/cli -g
```

2.创建项目

```
vue create hm-exp-mobile
```

- 选项

```js
Vue CLI v5.0.8
? Please pick a preset:
  Default ([Vue 3] babel, eslint)
  Default ([Vue 2] babel, eslint)
> Manually select features     选自定义
```

- 手动选择功能


- 选择vue的版本

```jsx
  3.x
> 2.x
```

- 是否使用history模式 no


- 选择css预处理


- 选择eslint的风格 （eslint 代码规范的检验工具，检验代码是否符合规范）
- 比如：const age = 18;   =>  报错！多加了分号！后面有工具，一保存，全部格式化成最规范的样子


- 选择校验的时机 （直接回车）


- 选择配置文件的生成方式 （直接回车）


- 是否保存预设，下次直接使用？  =>   不保存，输入 N


- 等待安装，项目初始化完成


- 启动项目

```
npm run serve

```

## ESlint代码规范及手动修复

代码规范：一套写代码的约定规则。例如：赋值符号的左右是否需要空格？一句结束是否是要加;？... 

> 没有规矩不成方圆  

ESLint:是一个代码检查工具，用来检查你的代码是否符合指定的规则(你和你的团队可以自行约定一套规则)。在创建项目时，我们使用的是 [JavaScript Standard Style](https://standardjs.com/readme-zhcn.html) 代码风格的规则。

### JavaScript Standard Style 规范说明

建议把：https://standardjs.com/rules-zhcn.html 看一遍，然后在写的时候,  遇到错误就查询解决。

下面是这份规则中的一小部分：

- *字符串使用单引号* – 需要转义的地方除外
- *无分号* – [这](http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding)[没什么不好。](http://inimino.org/~inimino/blog/javascript_semicolons)[不骗你！](https://www.youtube.com/watch?v=gsfbh17Ax9I)
- *关键字后加空格* `if (condition) { ... }`
- *函数名后加空格* `function name (arg) { ... }`
- 坚持使用全等 `===` 摒弃 `==` 一但在需要检查 `null || undefined` 时可以使用 `obj == null`
- ......

代码规范错误

如果你的代码不符合standard的要求，eslint会跳出来刀子嘴，豆腐心地提示你。

下面我们在main.js中随意做一些改动：添加一些空行，空格。

```js
import Vue from 'vue'
import App from './App.vue'

import './styles/index.less'
import router from './router'
Vue.config.productionTip = false

new Vue ( {
  render: h => h(App),
  router
}).$mount('#app')


```

按下保存代码之后：

你将会看在控制台中输出错误：

> eslint 是来帮助你的。心态要好，有错，就改。

#### 手动修正

根据错误提示来一项一项`手动`修正。

如果你不认识命令行中的语法报错是什么意思，你可以根据错误代码（func-call-spacing, space-in-parens,.....）去 ESLint 规则列表中查找其具体含义。

打开 [ESLint 规则表](https://zh-hans.eslint.org/docs/latest/rules/)，使用页面搜索（Ctrl + F）这个代码，查找对该规则的一个释义。

#### 通过eslint插件来实现自动修正

> 1. eslint会自动`高亮错误`显示
> 2. `通过配置`，eslint会`自动`帮助我们`修复`错误

- 如何安装


- 如何配置

```js
// 当保存的时候，eslint自动帮我们修复错误
"editor.codeActionsOnSave": {
    "source.fixAll": true
},
// 保存代码，不自动格式化
"editor.formatOnSave": false
```

- 注意：eslint的配置文件必须在根目录下，这个插件才能才能生效。打开项目必须以根目录打开，一次打开一个项目
- 注意：使用了eslint校验之后，把vscode带的那些格式化工具全禁用了 Beatify

settings.json 参考

```jsx
{
    "window.zoomLevel": 2,
    "workbench.iconTheme": "vscode-icons",
    "editor.tabSize": 2,
    "emmet.triggerExpansionOnTab": true,
    // 当保存的时候，eslint自动帮我们修复错误
    "editor.codeActionsOnSave": {
        "source.fixAll": true
    },
    // 保存代码，不自动格式化
    "editor.formatOnSave": false
}
```

## Vuex 概述

[Vuex](https://vuex.vuejs.org/zh/)目标：明确[Vuex](https://vuex.vuejs.org/zh/)是什么，应用场景以及优势

Vuex 是一个 Vue 的`状态管理工具`，状态就是数据。

大白话：Vuex 是一个插件，可以帮我们`管理 Vue 通用的数据 (多组件共享的数据)`。例如：购物车数据、个人信息数

使用场景：

- 某个状态 在`很多个组件`来使用 (个人信息)


- 多个组件`共同维护`一份数据 (购物车)

优势：

- 共同维护一份数据，`数据集中化管理`
- `响应式变化`
- 操作简洁 (vuex提供了一些辅助函数)

注意：

官方原文：

- 不是所有的场景都适用于vuex，只有在必要的时候才使用vuex
- 使用了vuex之后，会附加更多的框架中的概念进来，增加了项目的复杂度  （数据的操作更便捷，数据的流动更清晰）

Vuex就像《近视眼镜》, 你自然会知道什么时候需要用它~

## 构建 vuex 【多组件共享数据】环境

目标：基于脚手架创建项目，构建 vuex 多组件数据共享环境

效果是三个组件共享一份数据:

- 任意一个组件都可以修改数据
- 三个组件的数据是同步的

### 创建一个空仓库

目标：安装 vuex 插件，初始化一个空仓库

1.安装 vuex

安装vuex与vue-router类似，vuex是一个独立存在的插件，如果脚手架初始化没有选 vuex，就需要额外安装。

```bash
yarn add vuex@3 或者 npm i vuex@3
```

2.新建 `store/index.js` 专门存放 vuex

​	为了维护项目目录的整洁，在src目录下新建一个store目录其下放置一个index.js文件。 (和 `router/index.js` 类似)

3.创建仓库 `store/index.js`

```jsx
// 导入 vue
import Vue from 'vue'
// 导入 vuex
import Vuex from 'vuex'
// vuex也是vue的插件, 需要use一下, 进行插件的安装初始化
Vue.use(Vuex)

// 创建仓库 store
const store = new Vuex.Store()

// 导出仓库
export default store
```

4 在 main.js 中导入挂载到 Vue 实例上

```js
import Vue from 'vue'
import App from './App.vue'
import store from './store'

Vue.config.productionTip = false

new Vue({
  render: h => h(App),
  store
}).$mount('#app')
```

此刻起, 就成功创建了一个 **空仓库!!**

5.测试打印Vuex

App.vue

```js
created(){
  console.log(this.$store)
}
```

## Vuex 核心概念

###state 状态

目标：明确如何给仓库`提供`数据，如何`使用`仓库的数据

####提供数据

State提供唯一的公共数据源，所有共享的数据都要统一放到Store中的State中存储。

打开项目中的store.js文件，在state对象中可以添加我们要共享的数据。

```jsx
// 创建仓库 store
const store = new Vuex.Store({
  // state 状态, 即数据, 类似于vue组件中的data,
  // 区别：
  // 1.data 是组件自己的数据, 
  // 2.state 中的数据整个vue项目的组件都能访问到
  state: {
    count: 101
  }
})
```

#### 使用数据

#####通过 store 直接访问

获取 store：

1. this.$store
2. import 导入 store

模板中：     {{ $store.state.xxx }}
组件逻辑中：  this.$store.state.xxx
JS模块中：   store.state.xxx

1. 模板中使用

组件中可以使用  **$store** 获取到vuex中的store对象实例，可通过**state**属性属性获取**count**， 如下

```vue
<h1>state的数据 - {{ $store.state.count }}</h1>
```

2. 组件逻辑中使用

将state属性定义在计算属性中 https://vuex.vuejs.org/zh/guide/state.html

```js
<h1>state的数据 - {{ count }}</h1>

// 把state中数据，定义在组件内的计算属性中
  computed: {
    count () {
      return this.$store.state.count
    }
  }
```

3. js文件中使用

```vue
//main.js

import store from "@/store"

console.log(store.state.count)
```

##### 通过辅助函数（简化）

mapState是辅助函数，帮助我们把 store 中的数据`自动`映射到 组件的计算属性中

1.导入mapState (mapState是vuex中的一个函数)

```js
import { mapState } from 'vuex'
```

2.采用数组形式引入state属性

```js
mapState(['count', 'title']) 
```

上面的代码类似于

```js
count () {
    return this.$store.state.count
}
```

3.利用`展开运算符`将导出的状态映射给计算属性

```js
  computed: {
    ...mapState(['count', 'title'])
  }
```

```vue
 <div> state的数据：{{ count }}</div>
```

### mutations

目标：明确 vuex 同样遵循单向数据流，组件中不能直接修改仓库的数据

通过 `strict: true` 可以开启严格模式，开启严格模式后，直接修改 state 中的值会报错

> state 数据的修改只能通过 mutations，并且 mutations 必须是同步的

1. 定义 mutations 对象，对象中存放修改 state 的方法

```js
const store  = new Vuex.Store({
  state: {
    count: 0
  },
  // 定义mutations
  mutations: {
     //	第一个参数是当前 store 的 state 属性
    addCount (state) {
      state.count += 1
    }
  }
})
```

2. 组件中提交调用 mutations

```jsx
this.$store.commit('addCount')
```

#### 传参

提交 mutation 是可以传递参数的  `this.$store.commit('xxx',  参数)`

1. 提供 mutation 函数（带参数 - 提交载荷 payload ）

```js
mutations: {
  ...
  addCount (state, n) {
    state.count += n
  }
},
```

2. 页面中提交调用 mutation

```jsx
handle (n) {
  this.$store.commit('addCount', n)
}
```

> 提交的参数只能是一个，如果有多个参数要传，可以传递一个对象

```jsx
this.$store.commit('addCount', {
  count: 10
})
```

####辅助函数 - mapMutations

mapMutations 和 mapState 很像，它把位于`mutations中的方法`提取了出来，映射到`组件 methods`中

```js
import  { mapMutations } from 'vuex'
methods: {
    ...mapMutations(['addCount'])
}
```

上面代码的含义是将mutations的方法导入了methods中，等价于

```js
methods: {
      // commit(方法名, 载荷参数)
      addCount () {
          this.$store.commit('addCount')
      }
 }
```

此时，就可以直接通过this.addCount调用了

```jsx
<button @click="addCount(1)">值+1</button>
```

> `mutations 必须是同步的（便于监测数据变化，记录调试）`，如果有异步的ajax请求，应该放置在actions中

###actions

目标：明确 actions 的基本语法，处理异步操作

> state 是存放数据的
>
> mutations 是同步更新数据 (便于监测数据的变化, 更新视图等, 方便于调试工具查看变化)
>
> actions 则负责进行异步操作

需求：一秒钟之后，修改 state 的 count 成 666

1. 提供 actions 方法

```js
mutations: {
  changeCount (state, newCount) {
    state.count = newCount
  }
}

actions: {
  //	context 上下文（此处未分模块，可以当成 store 仓库）
  setAsyncCount (context, num) {
    //	这里是 setTimeout 模拟异步，以后大部分场景是发请求
    // 一秒后, 给一个数, 去修改 num
    setTimeout(() => {
      context.commit('changeCount', num)
    }, 1000)
  }
}
```

2. 页面中 dispatch 调用

```js
setAsyncCount () {
  this.$store.dispatch('setAsyncCount', 666)
}
```

####辅助函数 - mapActions

目标：掌握辅助函数 mapActions，映射方法

mapActions 是把位于`actions中的方法`提取了出来，映射到`组件methods`中

Son2.vue

```js
import { mapActions } from 'vuex'
methods: {
   ...mapActions(['changeCountAction'])
}

//mapActions映射的代码 本质上是以下代码的写法
//methods: {
//  changeCountAction (n) {
//    this.$store.dispatch('changeCountAction', n)
//  },
//}
```

直接通过 this.方法 就可以调用

```vue
<button @click="changeCountAction(666)">+异步</button>
```

###getters

目标：掌握核心概念 getters 的基本语法（类似于计算属性）

除了 state 之外，有时我们还需要从state中`派生出一些状态`，这些数据是依赖 state 的，此时会用到 getters

例如，state 中定义了 list，为 1-10 的数组，组件中需要显示所有大于 5 的数据

```js
state: {
    list: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
}
```

1. 定义getters

```js
getters: {
  // getters函数的第一个参数是 state
  // getters函数必须要有返回值
  filterList (state) {
    return state.list.filter(item => item > 5)
  }
}
```

####访问 getters

#####通过 store 访问 getters

```vue
<div>{{ $store.getters.filterList }}</div>
```

#####通过辅助函数 mapGetters 映射

```js
computed: {
    ...mapGetters(['filterList'])
}
```

```vue
 <div>{{ filterList }}</div>
```

###模块 module（进阶语法）

目标：掌握核心概念 module 模块的创建

由于 vuex 使用`单一状态树`，应用的所有状态`会集中到一个比较大的对象`。当应用变得非常复杂时，store 对象就有可能变得相当臃肿。（当项目变得越来越大的时候，Vuex 会变得越来越难以维护）

1. 模块拆分：

user 模块：store/modules/user.js

```jsx
const state = {
  userInfo: {
    name: 'zs',
    age: 18
  }
}

const mutations = {}
const actions = {}
const getters = {}

export default {
  state,
  mutations,
  actions,
  getters
}

```

setting 模块：store/modules/setting.js

```jsx
const state = {
  theme: 'dark'	//	主题色
  desc: '描述真呀真不错'
}

const mutations = {}
const actions = {}
const getters = {}

export default {
  state,
  mutations,
  actions,
  getters
}
```

2. 在`store/index.js`文件中的modules配置项中，注册这两个模块

```js
import user from './modules/user'
import setting from './modules/setting'

const store = new Vuex.Store({
    modules:{
        user,
        setting
    }
})
```

####获取模块内的state数据

目标：掌握模块中 state 的访问语法

尽管已经分模块了，但其实子模块的状态，还是会挂到根级别的 state 中，属性名就是模块名

使用模块中的数据：

1. 直接通过模块名访问 `$store.state.模块名.xxx`  =>  `$store.state.setting.desc`

2. 通过 mapState 映射

   默认根级别的映射 `mapState(['xxx'])`

   子模块的映射 `mapState('模块名',  ['xxx'])` - 需要开启命名空间

```jsx
export default {
  namespaced: true,
  state,
  mutations,
  actions,
  getters
}
```

$store直接访问

```js
$store.state.user.userInfo.name
```

mapState辅助函数访问

```js
...mapState('user', ['userInfo']),
...mapState('setting', ['theme', 'desc']),
```

####获取模块内的getters数据

目标：掌握模块中 getters 的访问语法

使用模块中 getters 中的数据： 

1. 直接通过模块名访问` $store.getters['模块名/xxx ']`
2. 通过 mapGetters 映射      
   1. 默认根级别的映射  `mapGetters([ 'xxx' ]) `
   2. 子模块的映射  `mapGetters('模块名', ['xxx'])` -  需要开启命名空间

modules/user.js

```js
const getters = {
  // 分模块后，state指代子模块的state
  UpperCaseName (state) {
    return state.userInfo.name.toUpperCase()
  }
}
```

Son1.vue 直接访问getters

```html
<!-- 测试访问模块中的getters - 原生 -->
<div>{{ $store.getters['user/UpperCaseName'] }}</div>
```

Son2.vue 通过命名空间访问

```js
computed:{
  ...mapGetters('user', ['UpperCaseName'])
}
```

####获取模块内的mutations方法

目标：掌握模块中 mutation 的调用语法

> 默认模块中的 mutation 和 actions 会被挂载到全局，`需要开启命名空间`，才会挂载到子模块。

调用子模块中 mutation：

1. 直接通过 store 调用   `$store.commit('模块名/xxx ',  额外参数)`
2. 通过 mapMutations 映射    
   1. 默认根级别的映射  `mapMutations([ 'xxx' ])     `
   2. 子模块的映射 `mapMutations('模块名', ['xxx']) ` -  需要开启命名空间

modules/user.js

```js
const mutations = {
  setUser (state, newUserInfo) {
    state.userInfo = newUserInfo
  }
}
```

modules/setting.js

```js
const mutations = {
  setTheme (state, newTheme) {
    state.theme = newTheme
  }
}
```

Son1.vue

```vue
<button @click="updateUser">更新个人信息</button> 
<button @click="updateTheme">更新主题色</button>


export default {
  methods: {
    updateUser () {
      // $store.commit('模块名/mutation名', 额外传参)
      this.$store.commit('user/setUser', {
        name: 'xiaowang',
        age: 25
      })
    }, 
    updateTheme () {
      this.$store.commit('setting/setTheme', 'pink')
    }
  }
}
```

Son2.vue

```vue
<button @click="setUser({ name: 'xiaoli', age: 80 })">更新个人信息</button>
<button @click="setTheme('skyblue')">更新主题</button>

methods:{
// 分模块的映射
...mapMutations('setting', ['setTheme']),
...mapMutations('user', ['setUser']),
}
```

####获取模块内的actions方法

目标：掌握模块中 action 的调用语法 (同理 - 直接类比 mutation 即可)

> 默认模块中的 mutation 和 actions 会被挂载到全局，`需要开启命名空间`，才会挂载到子模块。

调用子模块中的action：

1. 直接通过 store 调用   `$store.dispatch('模块名/xxx ',  额外参数)`
2. 通过 mapActions 映射     
   1. 默认根级别的映射  `mapActions([ 'xxx' ])     `
   2. 子模块的映射 `mapActions('模块名', ['xxx'])`  -  需要开启命名空间

modules/user.js

```js
const actions = {
  setUserSecond (context, newUserInfo) {
    // 将异步在action中进行封装
    setTimeout(() => {
      // 调用mutation   context上下文，默认提交的就是自己模块的action和mutation
      context.commit('setUser', newUserInfo)
    }, 1000)
  }
}
```

Son1.vue  直接通过store调用

```vue
<button @click="updateUser2">一秒后更新信息</button>

methods:{
    updateUser2 () {
      // 调用action dispatch
      this.$store.dispatch('user/setUserSecond', {
        name: 'xiaohong',
        age: 28
      })
    },
}
```

Son2.vue mapActions映射

```js
<button @click="setUserSecond({ name: 'xiaoli', age: 80 })">一秒后更新信息</button>

methods:{
  ...mapActions('user', ['setUserSecond'])
}
```

####Vuex模块化的使用小结

#####直接使用

1. state --> $store.state.**模块名**.数据项名
2. getters --> $store.getters['**模块名**/属性名']
3. mutations --> $store.commit('**模块名**/方法名', 其他参数)
4. actions --> $store.dispatch('**模块名**/方法名', 其他参数)

#####借助辅助方法使用

1.import { mapXxxx, mapXxx } from 'vuex'

computed、methods: {

​     // **...mapState、...mapGetters放computed中；**

​    //  **...mapMutations、...mapActions放methods中；**

​    ...mapXxxx(**'模块名'**, ['数据项|方法']),

​    ...mapXxxx(**'模块名'**, { 新的名字: 原来的名字 }),

}

2.组件中直接使用 属性 `{{ age }}` 或 方法 `@click="updateAge(2)"`

## json-server

目标：基于 json-server 工具，准备后端接口服务环境

1. 安装全局工具 json-server （全局工具仅需要安装一次）

   `yarn global add json-server`或`npm i json-server -g`

2. 代码根目录新建一个 db 目录

3. 将资料 index.json 移入 db 目录

4. 进入 db 目录，执行命令，启动后端接口服务

   `json-server index.json`

5. 访问接口测试 http://localhost:3000/cart

## 智慧商城 - 授课大纲

接口文档：https://apifox.com/apidoc/shared-12ab6b18-adc2-444c-ad11-0e60f5693f66/doc-2221080

演示地址：http://cba.itlike.com/public/mweb/#/

## 调整初始化目录结构

> 强烈建议大家严格按照老师的步骤进行调整，为了符合企业规范

为了更好的实现后面的操作，我们把整体的目录结构做一些调整。

目标:

1. 删除初始化的一些默认文件
2. 修改没删除的文件
3. 新增我们需要的目录结构

### 1.删除文件

- src/assets/logo.png
- src/components/HelloWorld.vue
- src/views/AboutView.vue
- src/views/HomeView.vue

### 2.修改文件

`main.js` 不需要修改

`router/index.js`

删除默认的路由配置

```js
import Vue from 'vue'
import VueRouter from 'vue-router'

Vue.use(VueRouter)

const routes = [
]

const router = new VueRouter({
  routes
})

export default router

```

`App.vue`

```html
<template>
  <div id="app">
    <router-view/>
  </div>
</template>
```

### 3.新增目录

- src/api 目录
  - 存储接口模块 (发送ajax请求接口的模块)
- src/utils 目录
  - 存储一些工具模块 (自己封装的方法)



## vant组件库及Vue周边的其他组件库

> 组件库：第三方封装好了很多很多的组件，整合到一起就是一个组件库。
>
> https://vant-contrib.gitee.io/vant/v2/#/zh-CN/

比如日历组件、键盘组件、打分组件、下拉筛选组件等

组件库并不是唯一的，常用的组件库还有以下几种：

pc:  [element-ui](https://element.eleme.cn/#/zh-CN)    [element-plus](https://element-plus.gitee.io/zh-CN/)  [iview](https://iview.github.io/)      **[ant-design](https://antdv.com/components/overview-cn)**

移动：[vant-ui](https://vant-contrib.gitee.io/vant/v2/#/zh-CN/)     [Mint UI](http://mint-ui.github.io/docs/#/zh-cn2) (饿了么)    [Cube UI](https://didi.github.io/cube-ui/#/zh-CN/) (滴滴)

###全部导入和按需导入的区别

目标：明确全部导入和按需导入的区别

区别：

1.全部导入会引起项目打包后的体积变大，进而影响用户访问网站的性能

2.按需导入只会导入你使用的组件，进而节约了资源

### 全部导入

- 安装vant-ui

```
yarn add vant@latest-v2
```

- 在main.js中

```js
import Vant from 'vant';
import 'vant/lib/index.css';
// 把vant中所有的组件都导入了
Vue.use(Vant)
```

- 即可使用

```jsx
<van-button type="primary">主要按钮</van-button>
<van-button type="info">信息按钮</van-button>
```

vant-ui提供了很多的组件，全部导入，会导致项目打包变得很大。

### 按需导入

- 安装vant-ui

```
yarn add vant@latest-v2
```

- 安装一个插件

```jsd
yarn add babel-plugin-import -D
```

- 在`babel.config.js`中配置

```js
module.exports = {
  presets: [
    '@vue/cli-plugin-babel/preset'
  ],
  plugins: [
    ['import', {
      libraryName: 'vant',
      libraryDirectory: 'es',
      style: true
    }, 'vant']
  ]
}
```

- 按需加载，在`main.js`

```js
import { Button, Icon } from 'vant'

Vue.use(Button)
Vue.use(Icon)
```

- `app.vue`中进行测试

```js
<van-button type="primary">主要按钮</van-button>
<van-button type="info">信息按钮</van-button>
<van-button type="default">默认按钮</van-button>
<van-button type="warning">警告按钮</van-button>
<van-button type="danger">危险按钮</van-button>
```

- 把引入组件的步骤抽离到单独的js文件中比如 `utils/vant-ui.js`

```js
import { Button, Icon } from 'vant'

Vue.use(Button)
Vue.use(Icon)
```

main.js中进行导入

```js
// 导入按需导入的配置文件
import '@/utils/vant-ui'
```



## 项目中的vw适配

目标：基于 postcss 插件实现项目 vw 适配

官方说明：https://vant-contrib.gitee.io/vant/v2/#/zh-CN/advanced-usage

1. 安装插件

```js
yarn add postcss-px-to-viewport@1.1.1 -D
```

2. 根目录新建postcss的配置文件`postcss.config.js`，填入配置

```jsx
// postcss.config.js
module.exports = {
  plugins: {
    'postcss-px-to-viewport': {
      viewportWidth: 375,
    },
  },
};
```

viewportWidth:设计稿的视口宽度

1. vant-ui中的组件就是按照375的视口宽度设计的
2. 恰好面经项目中的设计稿也是按照375的视口宽度设计的，所以此时 我们只需要配置375就可以了


## 路由设计配置

目标：分析项目页面，设计路由，配置一级路由

但凡是单个页面，独立展示的，都是一级路由


## request模块 - axios封装

接口文档：https://apifox.com/apidoc/shared-12ab6b18-adc2-444c-ad11-0e60f5693f66/doc-2221080

演示地址：http://cba.itlike.com/public/mweb/#/

基地址：http://cba.itlike.com/public/index.php?s=/api/

**目标：将 axios 请求方法，封装到 request 模块**

使用 axios 来`请求后端接口`, 一般都会对 axios 进行`一些配置` (比如: 配置基础地址,请求响应拦截器等等)

所以项目开发中, 都会对 axios 进行基本的`二次封装`, 单独封装到一个 request 模块中，`便于维护使用`

1. 安装 axios

```
npm i axios
```

1. 新建 `utils/request.js` 封装 axios 模块

   利用 axios.create 创建一个自定义的 axios 来使用

   http://www.axios-js.com/zh-cn/docs/#axios-create-config

```js
/* 封装axios用于发送请求 */
import axios from 'axios'

// 创建一个新的axios实例
const request = axios.create({
  baseURL: 'http://cba.itlike.com/public/index.php?s=/api/',
  timeout: 5000
})

// 添加请求拦截器
request.interceptors.request.use(function (config) {
  // 在发送请求之前做些什么
  return config
}, function (error) {
  // 对请求错误做些什么
  return Promise.reject(error)
})

// 添加响应拦截器
request.interceptors.response.use(function (response) {
  // 对响应数据做点什么
  return response.data
}, function (error) {
  // 对响应错误做点什么
  return Promise.reject(error)
})

export default request
```

1. 获取图形验证码，请求测试

```js
import request from '@/utils/request'
export default {
  name: 'LoginPage',
  async created () {
    const res = await request.get('/captcha/image')
    console.log(res)
  }
}
```

## 图形验证码功能完成

目标：基于请求回来的 base64 图片，实现图形验证码功能

说明：

1. 图形验证码，本质就是一个`请求回来的图片`
2. 用户将来输入图形验证码，用于强制人机交互，可以`抵御机器自动化攻击`（例如：避免批量请求获取短信）

需求：

1. 动态将请求回来的 base64 图片，解析渲染出来
2. 点击验证码图片盒子，要刷新验证码

1. 准备数据，获取图形验证码后存储图片路径，存储图片唯一标识

```jsx
async created () {
  this.getPicCode()
},
data () {
  return {
    picUrl: '',
    picKey: ''
  }
},
methods: {
  // 获取图形验证码
  async getPicCode () {
    const { data: { base64, key } } = await request.get('/captcha/image')
    this.picUrl = base64
    this.picKey = key
  }
}
```

1. 动态渲染图形验证码，并且点击时要重新刷新验证码

```jsx
<img v-if="picUrl" :src="picUrl" @click="getPicCode">
```



## 封装api接口 - 图片验证码接口

目标：将请求封装成方法，`统一存放到 api 模块`，与页面分离

以前的模式：

- 页面中充斥着请求代码，可阅读性不高
- 请求没有统一管理
- 相同的请求没有复用

封装 api 模块的好处：

- 请求与页面逻辑分离
- 相同的请求可以直接复用请求
- 请求进行了统一管理

具体实现

新建 `api/login.js` 提供获取图形验证码 Api 函数

```jsx
import request from '@/utils/request'

// 获取图形验证码
export const getPicCode = () => {
  return request.get('/captcha/image')
}
```

`login/index.vue`页面中调用测试

```jsx
async getPicCode () {
  const { data: { base64, key } } = await getPicCode()
  this.picUrl = base64
  this.picKey = key
},
```

## toast 轻提示

https://vant-contrib.gitee.io/vant/v2/#/zh-CN/toast

注册安装：

```js
import { Toast } from 'vant';
Vue.use(Toast)
```

两种使用方式

1. 导入调用 (组件内或非组件中均可) 

```jsx
import { Toast } from 'vant';
Toast('提示内容');
```

2. 通过this直接调用 (必须组件内)

   本质：将方法注册挂载到了 Vue 原型上 `Vue.prototype.$toast = xxx`

```jsx
this.$toast('提示内容')
```

## 短信验证倒计时

目标：实现短信验证倒计时功能

步骤分析：

1. 点击按钮，实现`倒计时`效果
2. 倒计时之前的`校验处理`（手机号、验证码）
3. 封装`短信验证请求接口`，发送请求添加提示

## 响应拦截器统一处理错误提示

目标：通过响应拦截器，统一处理接口的错误提示

响应拦截器是咱们拿到数据的第一个数据流转站，可以在里面`统一处理错误`，只要不是 200 默认给提示，抛出错误

utils/request.js

```jsx
import { Toast } from 'vant'

...

// 添加响应拦截器
request.interceptors.response.use(function (response) {
  const res = response.data
  if (res.status !== 200) {
    Toast(res.message)
    return Promise.reject(res.message)
  }
  // 对响应数据做点什么
  return res
}, function (error) {
  // 对响应错误做点什么
  return Promise.reject(error)
})
```

## 登录权证信息存储

目标：vuex 构建 user 模块存储登录权证（token & userId）

token 存入 vuex 的好处，`易获取，响应式`

vuex 需要分模块 → user 模块

## 搜索 - 历史记录管理

目标：构建搜索页的静态布局，完成历史记录的管理

需求：

1. 搜索历史基本渲染

2. 点击搜索（添加历史）

   点击搜索按钮或底下历史记录，都能进行搜索

   若之前`没有`相同搜索关键字，则直接`追加到最前面`

   若之前`已有`相同搜索关键字，将该`原有关键字移除，再追加`

3. 清空历史：添加清空图标，可以清空历史记录

4. 持久化：搜索历史需要持久化，刷新历史不丢失

## storage 存储模块 - vuex持久化处理

目标：封装 storage 存储模块，利用本地存储，进行 vuex 持久化处理

utils/storage.js

```js
//  约定通用键名
const INFO_KEY = 'shop_info'

//  获取个人信息
export const getInfo = () => {
  const defultObj = { token: '', userId: '' }
  const res = localStorage.getItem(INFO_KEY)
  return res ? JSON.parse(res) : defultObj
}

//  设置个人信息
export const setInfo = (obj) => {
  localStorage.setItem(INFO_KEY, JSON.stringify(obj))
}

//  移除个人信息
export const removeInfo = () => {
  localStorage.removeItem(INFO_KEY)
}
```

## 添加请求 loading 效果

目标：统一在每次请求后台时，添加 loading 效果

有时候因为网络原因，一次请求的结果可能需要一段时间后才能回来，此时，需要给用户`添加 loading 提示`

添加 loading 提示的好处：

1. 节流处理：防止用户在一次请求还没回来之前，多次进行点击，发送无效请求
2. 友好提示：告知用户，目前是在加载中，请耐心等等，用户体验会更好

步骤：

1. `请求拦截器`中，每次请求，`打开 loading`
2. `响应拦截器`中，每次响应，`关闭 loading`

## 登录访问拦截 - 路由前置守卫

**目标：基于全局前置守卫，进行页面访问拦截处理**

说明：智慧商城项目，大部分页面，`游客都可以直接访问`，如遇到需要登录才能进行的操作，提示并跳转到登录

但是：对于支付页，订单页等，必须是登录的用户才能访问的，游客不能进入该页面，`需要做拦截处理`

路由导航守卫 - [全局前置守卫](https://v3.router.vuejs.org/zh/guide/advanced/navigation-guards.html)

1.所有的路由一旦被匹配到，都会先经过全局前置守卫

2.只有全局前置守卫放行，才会真正解析渲染组件，才能看到页面内容

访问权限页面时，`用户是否有登录权证 token` 是拦截或放行的关键点

```jsx
router.beforeEach((to, from, next) => {
  // 1. to   往哪里去， 到哪去的路由信息对象  
  // 2. from 从哪里来， 从哪来的路由信息对象
  // 3. next() 是否放行
  //    如果next()调用，就是放行
  //    next(路径) 拦截到某个路径页面
})
```



```jsx
const authUrl = ['/pay', '/myorder']
router.beforeEach((to, from, next) => {
  const token = store.getters.token
  if (!authUrl.includes(to.path)) {
    next()
    return
  }

  if (token) {
    next()
  } else {
    next('/login')
  }
})
```

## 判断token及登录回跳

prodetail.js

```js
//  判断 token 是否存在
if (!this.$store.getters.token) {
  //  弹确认框
  this.$dialog.confirm({
    title: '温馨提示',
    message: '此时需要先登录才能继续操作哦',
    confirmButtonText: '去登陆',
    cancelButtonText: '再逛逛'
  }).then(() => {
    //  确认按钮操作
    //  跳转登录 => 登陆后会跳需要跳转时携带参数
    //  this.$route.fullPath => 带参数
    this.$router.replace({
      path: '/login',
      query: {
        backUrl: this.$route.fullPath
      }
    })
  }).catch(() => {
    //  取消按钮操作
  })
  return
}
```

login.js

```js
//  判断地址栏有无回跳地址
const url = this.$route.query.backUrl || '/'
this.$router.replace(url)
```

puth：打开页面历史进行累加，返回会逐渐返回

replace：覆盖页面，历史不会累加

## 购物车模块

购物车`数据联动关系`较多，且通常会封装一些`小组件`，所以为了便于维护，一般都会将购物车的数据基于 vuex `分模块管理`

1. 基本静态结构
2. 构建 vuex `cart 模块`，获取数据存储
3. 基于数据`动态渲染`购物车列表
4. 封装 `getters` 实现动态统计
5. 全选反选功能
6. 数字框修改数量功能
7. 编辑切换状态，删除功能
8. 空购物车处理

## mixins文件夹

编写的是 Vue 组件实例的配置项，可以直接混入到组件内容使用，例如：data、methods、computed、生命周期函数...

> 1. 如果此处和组件内提供了同名的 `data` 或 `methods`，则`组件内优先级更高`
> 2. 如果编写了`生命周期函数`，则 mixins 中的生命周期函数和页面的生命周期函数会用数组管理`统一执行`

mixins/mixins.js

```js
export default {
  methods: {
    //  根据登录状态确认是否需要弹出登录确认框
    loginConfirm () {
      //  判断 token 是否存在
      if (!this.$store.getters.token) {
        //  弹确认框
        this.$dialog.confirm({
          title: '温馨提示',
          message: '此时需要先登录才能继续操作哦',
          confirmButtonText: '去登陆',
          cancelButtonText: '再逛逛'
        }).then(() => {
          //  确认按钮操作
          //  跳转登录 => 登陆后会跳需要跳转时携带参数
          //  this.$route.fullPath => 带参数
          this.$router.replace({
            path: '/login',
            query: {
              backUrl: this.$route.fullPath
            }
          })
        }).catch(() => {
          //  取消按钮操作
        })
        return true
      }
      return false
    }
  }
}

```

protedail.js

```js
<script>
import loginConfirm from '@/mixins/loginConfirm'

methods: {
  //  跳转结算页面
  goPay () {
    //  未登录处理
    if (this.loginConfirm()) {
      return
    }

    this.$router.push({
      path: '/pay',
      query: {
        mode: 'buyNow',
        goodsId: this.goodsId,
        goodsNum: this.addCount,
        goodsSkuId: this.list.skuList[0].goods_sku_id
      }
    })
  }
}
</script>
```

## 项目打包优化

vue脚手架只是开发过程中，协助开发的工具，当真正开发完了 => 脚手架不参与上线

参与上线的是 => 打包后的源代码

打包：

- 将多个文件压缩合并成一个文件
- 语法降级
- less sass ts 语法解析, 解析成css
- ....

打包后，可以生成，浏览器能够直接运行的网页 => 就是需要上线的源码！

1.打包命令

vue脚手架工具已经提供了打包命令，直接使用即可。

```bash
yarn build
```

在项目的根目录会自动创建一个文件夹`dist`,dist中的文件就是打包后的文件，只需要放到服务器中即可。

2.配置publicPath

vue.config.js

```js
module.exports = {
  // 设置获取.js,.css文件时，是以相对地址为基准的。
  // https://cli.vuejs.org/zh/config/#publicpath
  publicPath: './'
}
```

3.路由懒加载

路由懒加载 & 异步组件， 不会一上来就将所有的组件都加载，而是访问到对应的路由了，才加载解析这个路由对应的所有组件

官网链接：https://router.vuejs.org/zh/guide/advanced/lazy-loading.html#%E4%BD%BF%E7%94%A8-webpack

> 当打包构建应用时，JavaScript 包会变得非常大，影响页面加载。如果我们能把不同路由对应的组件分割成不同的代码块，然后当路由`被访问的时候才加载对应组件`，这样就更加`高效`了。

```js
const ProDetail = () => import('@/views/prodetail')
const Pay = () => import('@/views/pay')
const MyOrder = () => import('@/views/myorder')
```









































