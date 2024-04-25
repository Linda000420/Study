# JavaScript进阶

## 作用域

> 了解作用域对程序执行的影响及作用域链的查找机制，使用闭包函数创建隔离作用域避免全局变量污染。

作用域（scope）规定了变量能够被访问的“范围”，离开了这个“范围”变量便不能被访问，作用域分为全局作用域和局部作用域。

### 局部作用域

局部作用域分为函数作用域和块作用域。

#### 函数作用域

在函数内部声明的变量只能在函数内部被访问，外部无法直接访问。

```html
<script>
  // 声明 counter 函数
  function counter(x, y) {
    // 函数内部声明的变量
    const s = x + y
    console.log(s) // 18
  }
  // 设用 counter 函数
  counter(10, 8)
  // 访问变量 s
  console.log(s)// 报错
</script>
```

总结：

1. 函数内部声明的变量，在函数外部无法被访问
2. 函数的参数也是函数内部的局部变量
3. 不同函数内部声明的变量无法互相访问
4. 函数执行完毕后，函数内部的变量实际被清空了

#### 块作用域

在 JavaScript 中使用 `{}` 包裹的代码称为代码块，代码块内部声明的变量外部将【`有可能`】无法被访问。

```html
<script>
  {
    // age 只能在该代码块中被访问
    let age = 18;
    console.log(age); // 正常
  }
  
  // 超出了 age 的作用域
  console.log(age) // 报错
  
  let flag = true;
  if(flag) {
    // str 只能在该代码块中被访问
    let str = 'hello world!'
    console.log(str); // 正常
  }
  
  // 超出了 age 的作用域
  console.log(str); // 报错
  
  for(let t = 1; t <= 6; t++) {
    // t 只能在该代码块中被访问
    console.log(t); // 正常
  }
  
  // 超出了 t 的作用域
  console.log(t); // 报错
</script>
```

JavaScript 中除了变量外还有常量，常量与变量本质的区别是【常量必须要有值且不允许被重新赋值】，常量值为对象时其属性和方法允许重新赋值。

```html
<script>
  // 必须要有值
  const version = '1.0.0';

  // 不能重新赋值
  // version = '1.0.1';

  // 常量值为对象类型
  const user = {
    name: '小明',
    age: 18
  }

  // 不能重新赋值
  user = {};

  // 属性和方法允许被修改
  user.name = '小小明';
  user.gender = '男';
</script>
```

总结：

1. `let` 声明的变量会产生块作用域，`var` 不会产生块作用域
2. `const` 声明的常量也会产生块作用域
3. 不同代码块之间的变量无法互相访问
4. 推荐使用 `let` 或 `const`

注：开发中 `let` 和 `const` 经常不加区分的使用，如果担心某个值会不小被修改时，则只能使用 `const` 声明成常量。

### 全局作用域

`<script>` 标签和 `.js` 文件的【最外层】就是所谓的全局作用域，在此声明的变量在函数内部也可以被访问。

```html
<script>
  // 此处是全局
  
  function sayHi() {
    // 此处为局部
  }

  // 此处为全局
</script>
```

全局作用域中声明的变量，任何其它作用域都可以被访问，如下代码所示：

```html
<script>
    // 全局变量 name
    const name = '小明'
  
  	// 函数作用域中访问全局
    function sayHi() {
      // 此处为局部
      console.log('你好' + name)
    }

    // 全局变量 flag 和 x
    const flag = true
    let x = 10
  
  	// 块作用域中访问全局
    if(flag) {
      let y = 5
      console.log(x + y) // x 是全局的
    }
</script>
```

总结：

1. 为 `window` 对象动态添加的属性默认也是全局的，不推荐！
2. 函数中未使用任何关键字声明的变量为全局变量，不推荐！！！
3. 尽可能少的声明全局变量，防止全局变量被污染

JavaScript 中的作用域是程序被执行时的底层机制，了解这一机制有助于规范代码书写习惯，避免因作用域导致的语法错误。

### 作用域链

在解释什么是作用域链前先来看一段代码：

```html
<script>
  // 全局作用域
  let a = 1
  let b = 2
  // 局部作用域
  function f() {
    let c
    // 局部作用域
    function g() {
      let d = 'yo'
    }
  }
</script>
```

函数内部允许创建新的函数，`f` 函数内部创建的新函数 `g`，会产生新的函数作用域，由此可知作用域产生了嵌套的关系。

如下图所示，父子关系的作用域关联在一起形成了链状的结构，作用域链的名字也由此而来。

作用域链本质上是底层的`变量查找机制`，在函数被执行时，会`优先查找当前函数`作用域中查找变量，如果当前作用域查找不到则会依次`逐级查找父级作用域`直到全局作用域，如下代码所示：

```html
<script>
  // 全局作用域
  let a = 1
  let b = 2

  // 局部作用域
  function f() {
    let c
    // let a = 10;
    console.log(a) // 1 或 10
    console.log(d) // 报错
    
    // 局部作用域
    function g() {
      let d = 'yo'
      // let b = 20;
      console.log(b) // 2 或 20
    }
    
    // 调用 g 函数
    g()
  }

  console.log(c) // 报错
  console.log(d) // 报错
  
  f();
</script>
```

总结：

1. 嵌套关系的作用域串联起来形成了作用域链
2. 相同作用域链中按着从小到大的规则查找变量
3. 子作用域能够访问父作用域，父级作用域无法访问子级作用域

### 垃圾回收机制

垃圾回收机制（Garbage Collection）简称 GC，JS 中`内存`的分配和回收都是`自动完成`的，内存在不使用的时候会被`垃圾回收器`自动回收

**内存的生命周期**

1. `内存分配`：当我们声明变量、函数、对象的时候，系统会自动为他们分配内存
2. `内存使用`：即读写内存，也就是使用变量、函数等
3. `内存回收`：使用完毕，由垃圾回收器自动回收不再使用的内存

**说明**：

- 全局变量一般不会回收（关闭页面回收）
- 一般情况下`局部变量的值`不用了会被`自动回收`掉

**内存泄露**：程序中分配的`内存`由于某种原因程序`未释放`或`无法释放`叫做`内存泄露`

常见的浏览器垃圾回收算法：`引用计数法`和`标记清楚法`

#### 引用计数法

IE 采用的引用技术算法，定义“`内存不再使用`”，就是看一个`对象`是否有指向它的引用，没有引用了就回收对象

算法：

1. 跟踪记录被`引用的次数`
2. 如果被引用了一次，那么就记录次数1，多次引用会`累加 ++`
3. 如果减少一个引用就`减1 --`
4. 如果引用次数是`0`，则释放内存

引用计数法是个简单有效的算法，但它存在一个致命的问题：`嵌套引用`（循环引用），如果两个对象`相互引用`，尽管他们已不再使用，垃圾回收器不会进行回收，导致内存泄露。

```js
function fn() {
  let o1 = {}
  let o2 = {}
  o1.a = o2
  o2.a = o1
  return '引用计数无法回收'
}
fn()
```

因为他们的引用次数永远不会是0，这样的相互引用如果说很大量的存在就会导致大量的内存泄露。

#### 标记清除法

现代的浏览器已经不再使用引用计数算法了，通用的大多是基于`标记清除法`的某些改进算法，总体思想都是一致的。

核心：

1. 标记清除算法将“不再使用的对象”定义为“`无法达到的对象`”
2. 就是从`根部`（在 JS 中就是全局对象）出发定时扫描内存中的对象。凡是能从`根部到达`的对象，都是还`需要使用`的。
3. 那些`无法`从根部出发触及到的对象被标记为`不再使用`，稍后进行`回收`。

### 闭包

闭包是一种比较特殊和函数，使用闭包能够访问函数作用域中的变量。从代码形式上看闭包是一个做为返回值的函数，如下代码所示：

```html
<body>
  <script>
    // 1. 闭包 : 内层函数 + 外层函数变量
    // function outer() {
    //   const a = 1
    //   function f() {
    //     console.log(a)
    //   }
    //   f()
    // }
    // outer()

    // 2. 闭包的应用： 实现数据的私有。统计函数的调用次数
    //	count是全局变量，容易被修改
    // let count = 1
    // function fn() {
    //   count++
    //   console.log(`函数被调用${count}次`)
    // }

    // 3. 闭包的写法  统计函数的调用次数
    function outer() {
      let count = 1
      function fn() {
        count++
        console.log(`函数被调用${count}次`)
      }
      return fn
    }
    const re = outer()
    // const re = function fn() {
    //   count++
    //   console.log(`函数被调用${count}次`)
    // }
    re()
    re()
    // const fn = function() { }  函数表达式
    // 4. 闭包存在的问题： 可能会造成内存泄漏
  </script>
</body>
```

总结：

概念：一个函数对周围状态的引用捆绑在一起，内层函数中访问到其外层函数的作用域

1.怎么理解闭包？

- 闭包 = 内层函数 + 外层函数的变量

2.闭包的作用？

- 封闭数据，实现数据私有，外部也可以访问函数内部的变量
- 闭包很有用，因为它允许将函数与其所操作的某些数据（环境）关联起来

3.闭包可能引起的问题？

- 内存泄漏

### 变量提升

变量提升是 JavaScript 中比较“奇怪”的现象，它允许在变量声明之前即被访问（仅存在于 var 声明变量）

1. 把所有 var 声明的变量提升到当前作用域的最前面
2. 只提升声明，不提升赋值

```html
<script>
  // 访问变量 str
  console.log(str + 'world!');

  // 声明变量 str
  var str = 'hello ';
</script>
```

总结：

1. 变量在未声明即被访问时会报语法错误
2. 变量在声明之前即被访问，变量的值为 `undefined`
3. `let` 声明的变量不存在变量提升，推荐使用 `let`
4. 变量提升出现在相同作用域当中
5. 实际开发中推荐先声明再访问变量

注：关于变量提升的原理分析会涉及较为复杂的词法分析等知识，而开发中使用 `let` 可以轻松规避变量的提升，因此在此不做过多的探讨，有兴趣可[查阅资料](https://segmentfault.com/a/1190000013915935)。

## 函数

> 知道函数参数默认值、动态参数、剩余参数的使用细节，提升函数应用的灵活度，知道箭头函数的语法及与普通函数的差异。

### 函数提升

函数提升与变量提升比较类似，是指函数在声明之前即可被调用。

```html
<script>
  // 调用函数
  foo()
  // 声明函数
  function foo() {
    console.log('声明之前即被调用...')
  }

  // 不存在提升现象
  bar()  // 错误
  var bar = function () {
    console.log('函数表达式不存在提升现象...')
  }
</script>
```

总结：

1. 函数提升能够使函数的声明调用更灵活
2. 函数表达式不存在提升的现象
3. 函数提升出现在相同作用域当中

### 函数参数

函数参数的使用细节，能够提升函数应用的灵活度。

#### 默认值

```html
<script>
  // 设置参数默认值
  function sayHi(name="小明", age=18) {
    document.write(`<p>大家好，我叫${name}，我今年${age}岁了。</p>`);
  }
  // 调用函数
  sayHi();
  sayHi('小红');
  sayHi('小刚', 21);
</script>
```

总结：

1. 声明函数时为形参赋值即为参数的默认值
2. 如果参数未自定义默认值时，参数的默认值为 `undefined`
3. 调用函数时没有传入对应实参时，参数的默认值被当做实参传入

#### 动态参数

`arguments` 是函数内部内置的伪数组变量，它包含了调用函数时传入的所有实参。

```html
<script>
  // 求生函数，计算所有参数的和
  function sum() {
    // console.log(arguments)
    let s = 0
    for(let i = 0; i < arguments.length; i++) {
      s += arguments[i]
    }
    console.log(s)
  }
  // 调用求和函数
  sum(5, 10)// 两个参数
  sum(1, 2, 4) // 两个参数
</script>
```

总结：

1. `arguments` 是一个伪数组，只存在于函数中
2. `arguments` 的作用是动态获取函数的实参

#### 剩余参数

剩余参数允许我们将一个不定数量的参数表示为一个数组

```html
<script>
  function config(baseURL, ...other) {
    console.log(baseURL) // 得到 'http://baidu.com'
    console.log(other)  // other  得到 ['get', 'json']
  }
  // 调用函数
  config('http://baidu.com', 'get', 'json');
</script>
```

总结：

1. `...` 是语法符号，置于最末函数形参之前，用于获取`多余`的实参
2. 借助 `...` 获取的剩余实参，是个`真数组`
3. 开发中提倡多使用`剩余参数`

#### 展开运算符

展开运算符 (...)，将一个数组进行展开

典型运用场景：求数组最大值（最小值）、合并数组等

~~~js
const arr1 = [1, 5, 7, 9]
console.log(...arr1)	//	1 5 7 9
//	求数组最大值
console.log(Math.max(...arr1))	//	9
console.log(Math.min(...arr1))	//	1

//	合并数组
const arr2 = [2, 4, 6, 8]
const arr = [...arr1, ...arr2]	
console.log(...arr)	//	1,5,7,9,2,4,6,8
~~~

说明：

1. 不会修改原数组
2. 数组中使用，数组展开

### 箭头函数

箭头函数是一种声明函数的简洁语法，它与普通函数并无本质的区别，差异性更多体现在语法格式上。

引入箭头函数的目的是更简短的函数写法并且不绑定 this，箭头函数的语法比函数表达式更简洁，箭头函数更适用于那些本来`需要匿名函数的地方`。

#### 基本语法

~~~js
//	普通函数
const fn1 = function() {
  console.log('我是普通函数')
}
fn1()

//	箭头函数
const fn2 = () => {
  console.log('我是箭头函数')
}
fn2()

//	只有一个形参的时候可以省略小括号
const fn3 = x => {
  console.log(x)
}
fn3(1)

//	只有一行代码的时候可以省略大括号
const fn4 = x => console.log(x)
fn4(1)

//	只有一行代码时可以省略return
const fn5 = x => x + x
console.log(fn5(1))	//	2

//	阻止表单默认提交
const form = document.querySelector('form')
form.addEventListener('click', e => e.preventDefault())

//	加括号的函数体返回对象字面量表达式
const fn6 = uname => ({ uname: uname})
console.log(fn6('张三'))	//	{uname: '张三'}
~~~

总结：

1. 箭头函数属于表达式函数，因此不存在函数提升
2. 箭头函数只有一个参数时可以省略圆括号 `()`
3. 箭头函数函数体只有一行代码时可以省略花括号 `{}`，并自动做为返回值被返回
4. 加括号的函数体返回对象字面量表达式

#### 箭头函数参数

普通函数有 arguments 动态参数

箭头函数没有 `arguments`，但是有剩余参数 ...args，只能使用 `...` 动态获取实参

```html
<body>
  <script>
    // 1. 利用箭头函数来求和
    const getSum = (...arr) => {
      let sum = 0
      for (let i = 0; i < arr.length; i++) {
        sum += arr[i]
      }
      return sum
    }
    const result = getSum(2, 3, 4)
    console.log(result) // 9
  </script>
```

#### 箭头函数 this

`箭头函数不会创建自己的this`，它只会从自己的作用域链的上一层沿用this。

在开发中使用箭头函数前需要考虑函数中 this 的值，事件回调函数使用箭头时，this 为全局的 window，因此 `DOM 事件回调函数为了简便，还是不太推荐使用箭头函数`

```html
 <script>
    // 以前this的指向：  谁调用的这个函数，this 就指向谁
    // console.log(this)  // window
    // // 普通函数
    // function fn() {
    //   console.log(this)  // window
    // }
    // window.fn()
    // // 对象方法里面的this
    // const obj = {
    //   name: 'andy',
    //   sayHi: function () {
    //     console.log(this)  // obj
    //   }
    // }
    // obj.sayHi()

    // 2. 箭头函数的this  是上一层作用域的this 指向
    // const fn = () => {
    //   console.log(this)  // window
    // }
    // fn()
    // 对象方法箭头函数 this
    // const obj = {
    //   uname: 'pink老师',
    //   sayHi: () => {
    //     console.log(this)  // this 指向谁？ window
    //   }
    // }
    // obj.sayHi()

    const obj = {
      uname: 'pink老师',
      sayHi: function () {
        console.log(this)  // obj
        let i = 10
        const count = () => {
          console.log(this)  // obj 
        }
        count()
      }
    }
    obj.sayHi()

  </script>
```

## 解构赋值

> 知道解构的语法及分类，使用解构简洁语法快速为变量赋值。

解构赋值是一种快速为变量赋值的简洁语法，本质上仍然是为变量赋值，分为数组解构、对象解构两大类型。

### 数组解构

数组解构是将数组的单元值快速`批量赋值`给一系列变量`的简洁语法`

**基本语法**：

1. 赋值运算符 `=` 左侧的 `[]` 用于批量声明变量，右侧数组的单元值将被赋值给左侧的变量
2. 变量的顺序对应数组单元值的位置依次进行赋值操作
3. 变量的数量大于单元值数量时，多余的变量将被赋值为  `undefined`
4. 变量的数量小于单元值数量时，可以通过 `...` 获取剩余单元值，但只能置于最末位
5. 允许初始化变量的默认值，且只有单元值为 `undefined` 时默认值才会生效
6. 支持多维解构赋值，比较复杂后续有应用需求时再进一步分析

```html
<script>
  // 普通的数组
  let arr = [1, 2, 3]
  // 批量声明变量 a b c 
  // 同时将数组单元值 1 2 3 依次赋值给变量 a b c
  let [a, b, c] = arr
  console.log(a); // 1
  console.log(b); // 2
  console.log(c); // 3
  
  //	典型应用：交互 2 个变量
  let a = 1
  let b = 3;	//	必须加 ；
  [b, a] = [a, b]
  console.log(a)	//	3
  console.log(b)	//	1
  
  //	按需导入赋值
  const [a, b, , d] = [1, 2, 3, 4]
  console.log(a)	//	1
  console.log(b)	//	2
  console.log(d)	//	4
  
  //	支持多维结构
  const [a, b, [c, d]] = [1, 2, [3, 4]]
  console.log(a)	//	1
  console.log(b)	//	2
  console.log(c)	//	3
  console.log(d)	//	4
</script>
```

**js 前面必须加分号情况**：

1. 立即执行函数
2. 数组解构

### 对象解构

对象解构是将对象属性和方法快速批量赋值给一系列变量的简洁语法，如下代码所示：

```html
<script>
  // 普通对象
  const user = {
    name: '小明',
    age: 18
  };
  // 批量声明变量 name age
  // 同时将数组单元值 小明  18 依次赋值给变量 name  age
  const {name, age} = user

  console.log(name) // 小明
  console.log(age) // 18
</script>
```

**基本语法**：

1. 赋值运算符 `=` 左侧的 `{}` 用于批量声明变量，右侧对象的属性值将被赋值给左侧的变量
2. 对象属性的值将被赋值给与属性名`相同`的变量
3. 解构的变量名不要和外面的变量名冲突，否则会报错
4. 对象解构的变量名可以重新改名，语法：`旧变量名: 新变量名`
5. 解构数组对象，语法：`const [{变量名1， 变量名2}] = 数组名`
6. 对象中找不到与变量名一致的属性时变量值为 `undefined`
7. 允许初始化变量的默认值，属性不存在或单元值为 `undefined` 时默认值才会生效

注：支持多维解构赋值

```html
<body>
  <script>
    // 1. 这是后台传递过来的数据
    const msg = {
      "code": 200,
      "msg": "获取新闻列表成功",
      "data": [
        {
          "id": 1,
          "title": "5G商用自己，三大运用商收入下降",
          "count": 58
        },
        {
          "id": 2,
          "title": "国际媒体头条速览",
          "count": 56
        },
        {
          "id": 3,
          "title": "乌克兰和俄罗斯持续冲突",
          "count": 1669
        },

      ]
    }
    
    //	多级对象解构
    const {code, msg, data: [{id, title, count}]} = msg

    // 需求1： 请将以上msg对象  采用对象解构的方式 只选出  data 方面后面使用渲染页面
    // const { data } = msg
    // console.log(data)
    // 需求2： 上面msg是后台传递过来的数据，我们需要把data选出当做参数传递给 函数
    // const { data } = msg
    // msg 虽然很多属性，但是我们利用解构只要 data值
    function render({ data }) {
      // const { data } = arr
      // 我们只要 data 数据
      // 内部处理
      console.log(data)

    }
    render(msg)

    // 需求3， 为了防止msg里面的data名字混淆，要求渲染函数里面的数据名改为 myData
    function render({ data: myData }) {
      // 要求将 获取过来的 data数据 更名为 myData
      // 内部处理
      console.log(myData)

    }
    render(msg)

  </script>
```

## 数组

### forEach遍历数组

forEach() 方法用于调用数组的每个元素，并将元素传递给回调函数

语法：`被遍历的数组.forEach(function (当前数组元素, 当前元素索引号) { 函数体 })`

> 注意：  
>
> 1.forEach 主要是遍历数组的每个元素，不返回数值
>
> 2.参数当前数组元素是必须要写的， 索引号可选。

```html
<body>
  <script>
    // forEach 就是遍历  加强版的for循环  适合于遍历数组对象
    const arr = ['red', 'green', 'pink']
    const result = arr.forEach(function (item, index) {
      console.log(item)  // 数组元素 red  green pink
      console.log(index) // 索引号
    })
    // console.log(result)
  </script>
</body>
```

### filter筛选数组

filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素

主要使用场景： `筛选数组符合条件的元素`，并返回筛选之后元素的新数组，不会影响原数组

语法：`被遍历的数组.filter(function (当前数组元素, 当前元素索引号) { return 筛选条件 })`

```html
<body>
  <script>
    const arr = [10, 20, 30]
    // const newArr = arr.filter(function (item, index) {
    //   // console.log(item)
    //   // console.log(index)
    //   return item >= 20
    // })
    // 返回的符合条件的新数组

    const newArr = arr.filter(item => item >= 20)
    console.log(newArr)
  </script>
</body>
```

## 深入对象

> 了解面向对象的基础概念，能够利用构造函数创建对象。

### 创建对象的三种方式

1. 利用对象字面量创建对象
2. 利用 new Object 创建对象
3. 利用构造函数创建对象

~~~js
//	利用对象字面量创建对象
const o = {
  name: '佩奇'
}

//	利用 new Object 创建对象
const o = new Object({ name: '佩奇'})
console.log(o)	//	{name: '佩奇'}
~~~

### 构造函数

构造函数是一种特殊的函数，主要用来初始化对象，常规的 {...} 语法允许创建一个对象。比如我们创建了佩奇的对象，继续创建乔治的对象还需要重新写一遍，此时可以通过`构造函数`来`快速创建多个类似的对象`。

构造函数是专门用于创建对象的函数，如果一个函数使用 `new` 关键字调用，那么这个函数就是构造函数。

构造函数在技术上是常规函数，不过有两个约定：

1. 命名以大写字母开头
2. 只能由“new”操作符来执行

```html
<script>
  // 定义函数
  function Pig(name, age, gender) {
    this.name = name
    this.age = age
    this.gender = gender
  }
  // 调用函数
  const Peppa = new Pig('佩奇', 6, '女')
  const George = new Pig('乔治', 3, '男')
</script>
```

总结：

1. 使用 `new` 关键字调用函数的行为被称为`实例化`
2. 实例化构造函数时没有参数时可以省略 `()`
3. 构造函数内部无需写 return，返回值即为新创建的对象
4. 构造函数内部的 `return` 返回的值无效
5. new Object()、new Date() 也是实例化构造函数

注：实践中为了从视觉上区分构造函数和普通函数，习惯将构造函数的首字母大写。

**实例化执行过程**：

1. 创建新对象
2. 构造函数 this 指向新对象
3. 执行构造函数代码，修改 this，添加新的属性
4. 返回新对象

### 实例成员

通过构造函数创建的对象称为实例对象，`实例对象中`的属性和方法称为`实例成员`。

```html
<script>
  // 构造函数
  function Person() {
    // 构造函数内部的 this 就是实例对象
    // 实例对象中动态添加属性
    this.name = '小明'
    // 实例对象动态添加方法
    this.sayHi = function () {
      console.log('大家好~')
    }
  }
  // 实例化，p1 是实例对象
  // p1 实际就是 构造函数内部的 this
  const p1 = new Person()
  console.log(p1)
  console.log(p1.name) // 访问实例属性
  p1.sayHi() // 调用实例方法
</script>
```

总结：

1. 为构造函数传入参数，创建结构相同但值`不同的对象`
2. 构造函数创建的实例对象`彼此独立`互不影响
3. 构造函数内部 `this` 实际上就是实例对象，为其动态添加的属性和方法即为实例成员
4. 为构造函数传入参数，动态创建结构相同但值不同的对象

### 静态成员

在 JavaScript 中底层函数本质上也是对象类型，因此允许直接为函数动态添加属性或方法，`构造函数`的属性和方法被称为`静态成员`（静态属性和静态方法）。

```html
<script>
  // 构造函数
  function Person(name, age) {
    // 省略实例成员
  }
  // 静态属性
  Person.eyes = 2
  Person.arms = 2
  // 静态方法
  Person.walk = function () {
    console.log('^_^人都会走路...')
    // this 指向 Person
    console.log(this.eyes)
  }
</script>
```

总结：

1. 静态成员只能构造函数来访问
2. 静态成员指的是添加到构造函数本身的属性和方法
3. 一般公共特征的属性或方法静态成员设置为静态成员
4. 静态成员方法中的 `this` 指向构造函数本身

## 内置构造函数

> 掌握各引用类型和包装类型对象属性和方法的使用。

在 JavaScript 中**最主要**的数据类型有 6 种，分别是字符串、数值、布尔、undefined、null 和 对象，常见的对象类型数据包括数组和普通对象。其中字符串、数值、布尔、undefined、null 也被称为简单类型或基础类型，对象也被称为引用类型。

其实字符串、数值、布尔等基本类型也都有专门的构造函数，这些我们称为包装类型，JS 中几乎所有的数据都可以基于构造函数创建。

在 JavaScript 内置了一些构造函数，绝大部的数据处理都是基于这些构造函数实现的，JavaScript 基础阶段学习的 `Date` 就是内置的构造函数。

```html
<script>
  // 实例化
	let date = new Date();
  
  // date 即为实例对象
  console.log(date);
</script>
```

甚至字符串、数值、布尔、数组、普通对象也都有专门的构造函数，用于创建对应类型的数据。

**引用类型**：Object、Array、RegExp、Date 等

**包装类型**：String、Number、Boolean 等

### 引用类型

#### Object

`Object` 是内置的构造函数，用于创建普通对象。

```html
<script>
  // 通过构造函数创建普通对象
  const user = new Object({name: '小明', age: 15})

  // 这种方式声明的变量称为【字面量】
  let student = {name: '杜子腾', age: 21}
  
  // 对象语法简写
  let name = '小红';
  let people = {
    // 相当于 name: name
    name,
    // 相当于 walk: function () {}
    walk () {
      console.log('人都要走路...');
    }
  }

  console.log(student.constructor);
  console.log(user.constructor);
  console.log(student instanceof Object);
</script>
```

总结：

1. 推荐使用字面量方式声明对象，而不是 `Object` 构造函数
2. `Object.assign(对象名, 被拷贝的对象名)` 静态方法常用于对象拷贝，经常用于给对象添加属性
3. `Object.keys` 静态方法获取对象中所有属性，返回的是一个数组
4. `Object.values` 静态方法获取对象中所有属性值，返回的是一个数组

~~~js
const o = { name: '佩奇', age: 6}
const arr = Object.keys(o)

//	获得对象的所有键，并且返回是一个数组
console.log(Object.keys(o))	//	['name', 'age']

//	获得所有的属性值
console.log(Object.values(o))	//	['pink', 18]

//	对象的拷贝
const oo = {}
Object.assign(oo, o)

//	给对象添加属性
Object.assign(o, {gender: '女'})
console.log(o)	//	{uname: '佩奇', age: 18, gender: '女'}
~~~

#### Array

`Array` 是内置的构造函数，用于创建数组，创建数组建议使用`字面量`创建，不用 Array 构造函数创建

```html
<script>
  // 构造函数创建数组
  let arr = new Array(5, 7, 8);

  // 字面量方式创建数组
  let list = ['html', 'css', 'javascript']

</script>
```

数组赋值后，无论修改哪个变量另一个对象的数据值也会相当发生改变。

**数组常见实例方法**：

|   方法    |    作用    |                             说明                             |
| :-------: | :--------: | :----------------------------------------------------------: |
| `forEach` | `遍历`数组 |            不返回数组，经常用于`查找遍历数组元素`            |
| `filter`  | `过滤`数组 |        `返回新数组`，返回的是`筛选满足条件`的数组元素        |
|   `map`   | `迭代`数组 | `返回新数组`，返回的是`处理之后`的数组元素，想要使用返回的新元素 |
| `reduce`  |  `累计`器  |              返回累计处理的结果，经常用于求和等              |
|   join    |    拼接    |               数组元素拼接为字符串，返回字符串               |
|  `find`   |    查找    | 查找元素， 返回符合测试条件的`第一个`数组元素值，如果没有符合条件的则返回 undefined |
|  `every`  |    检测    | 检测数组所有元素是否都符合指定条件，如果**所有元素**都通过检测返回 true，否则返回 false |
|   some    |    检测    | 检测数组中的元素是否满足指定条件   **如果数组中有**元素满足条件返回 true，否则返回 false |
|  concat   |    合并    |                 合并两个数组，返回生成新数组                 |
|   sort    |    排序    |                      对原数组单元值排序                      |
|  splice   | 删除或替换 |                     删除或替换原数组单元                     |
|  reverse  |    反转    |                           反转数组                           |
| findIndex |    查找    |                       查找元素的索引值                       |
|   from    |    转换    |                      伪数组转换为真数组                      |

**reduce **

基本语法：如果有起始值，则把初始值累加到里面

1. `数组.reduce(function(){}, 起始值)`
2. `数组.reduce(function(上一次值, 当前值){}, 初始值)`
3. `数组.reduce((prev, current) => prev + current, 起始值)`

执行过程：

1. 如果`没有起始值`，则`上一次值`为数组的`第一个数组元素的值`
2. 每一次循环，把`返回值`作为下一次循环的`上一次值`
3. 如果`有起始值`，则起始值作为`上一次值`

### 包装类型

在 JavaScript 中的字符串、数值、布尔具有对象的使用特征，如具有属性和方法，如下代码举例：

```html
<script>
  // 字符串类型
  const str = 'hello world!'
 	// 统计字符的长度（字符数量）
  console.log(str.length)
  
  // 数值类型
  const price = 12.345
  // 保留两位小数
  price.toFixed(2) // 12.34
</script>
```

之所以具有对象特征的原因是字符串、数值、布尔类型数据是 JavaScript 底层使用 Object 构造函数“包装”来的，被称为`包装类型`。

#### String

`String` 是内置的构造函数，用于创建字符串。

```html
<script>
  // 使用构造函数创建字符串
  let str = new String('hello world!');

  // 字面量创建字符串
  let str2 = '你好，世界！';

  // 检测是否属于同一个构造函数
  console.log(str.constructor === str2.constructor); // true
  console.log(str instanceof String); // false
</script>
```

**常见实例方法**

|                           方法                           |                             说明                             |
| :------------------------------------------------------: | :----------------------------------------------------------: |
|                    `split('分隔符')`                     |                      将字符串拆分成数组                      |
| `substring（需要截取的第一个字符的索引[,结束的索引号]）` |           字符串截取，结束的索引号不包含在截取部分           |
|        `startsWith(检测字符串[, 检测位置索引号])`        |                     检测是否以某字符开头                     |
|        `includes(搜索的字符串[, 检测位置索引号])`        | 判断一个字符串是否包含在另一个字符串中，根据情况返回 true 或 false |
|                       toUpperCase                        |                       将字母转换成大写                       |
|                       toLowerCase                        |                       将字母转换成小写                       |
|                         indexOf                          |                      检测是否包含某字符                      |
|                         endsWith                         |                     检测是否以某字符结尾                     |
|                         replace                          |                   替换字符串，支持正则匹配                   |
|                          match                           |                   查找字符串，支持正则匹配                   |

总结：

1. 实例属性 `length` 用来获取字符串的度长(重点)

注：String 也可以当做普通函数使用，这时它的作用是强制转换成字符串数据类型。

#### Number

`Number` 是内置的构造函数，用于创建数值。

```html
<script>
  // 使用构造函数创建数值
  let x = new Number('10')
  let y = new Number(5)

  // 字面量创建数值
  let z = 20

</script>
```

总结：

1. 推荐使用字面量方式声明数值，而不是 `Number` 构造函数
2. 实例方法 `toFixed` 用于设置保留小数位的长度，四舍五入


## 编程思想

> 学习 JavaScript 中基于原型的面向对象编程序的语法实现，理解面向对象编程的特征。

### 面向过程

面向过程就是分析出解决问题所需要的步骤，然后用函数把这些步骤一步一步实现，使用的时候再一个一个的依次调用就可以了。

 举个栗子：蛋炒饭

![67679290689](E:/%E5%89%8D%E7%AB%AF/1.2023%E6%96%B0%E7%89%88%E5%89%8D%E7%AB%AFJavaScript/3.JS%E8%BF%9B%E9%98%B6/%E8%B5%84%E6%96%99/JavaScript%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9/02-%E7%AC%94%E8%AE%B0/assets/1676792906898.png)

面向过程就是按照我们分析好了的步骤，按照步骤解决问题

### 面向对象

面向对象是把事务分解成为一个个对象，然后由对象之间分工与合作。

![67679293032](E:/%E5%89%8D%E7%AB%AF/1.2023%E6%96%B0%E7%89%88%E5%89%8D%E7%AB%AFJavaScript/3.JS%E8%BF%9B%E9%98%B6/%E8%B5%84%E6%96%99/JavaScript%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9/02-%E7%AC%94%E8%AE%B0/assets/1676792930329.png)

面向对象是以对象功能来划分问题，而不是步骤

在面向对象程序开发思想中，每一个对象都是功能中心，具有明确分工。

面向对象编程具有灵活、代码可复用、容易维护和开发的优点，更适合多人合作的大型软件项目。

面向对象的特性：

- 封装性


- 继承性
- 多态性

|      |                         面向过程编程                         |                         面向对象编程                         |
| :--: | :----------------------------------------------------------: | :----------------------------------------------------------: |
| 优点 | 性能比面向对象高，适合跟硬件联系很紧密的东西，例如单片机就采用的面向过程编程 | 易维护、易复用、易扩展，由于面向对象有封装、继承、多态性的特性，可以设计出低耦合的系统，使系统更加灵活、更加易于维护 |
| 缺点 |              没有面向对象易维护、易复用、易扩展              |                       性能比面向过程低                       |

## 构造函数

对比以下通过面向对象的构造函数实现的封装：

```html
<script>
  function Person() {
    this.name = '佚名'
    // 设置名字
    this.setName = function (name) {
      this.name = name
    }
    // 读取名字
    this.getName = () => {
      console.log(this.name)
    }
  }

  // 实例对像，获得了构造函数中封装的所有逻辑
  let p1 = new Person()
  p1.setName('小明')
  console.log(p1.name)

  // 实例对象
  let p2 = new Person()
  console.log(p2.name)
</script>
```

封装是面向对象思想中比较重要的一部分，js面向对象可以通过构造函数实现的封装。

同样的将变量和函数组合到了一起并能通过 this 实现数据的共享，所不同的是借助构造函数创建出来的实例对象之间是彼此不影响的

> 总结：
>
> 1. 构造函数体现了面向对象的封装特性
> 2. 构造函数实例创建的对象彼此独立、互不影响

封装是面向对象思想中比较重要的一部分，js面向对象可以通过构造函数实现的封装。

前面我们学过的构造函数方法很好用，但是 存在`浪费内存`的问题

## 原型对象

构造函数通过原型分配的函数是所有对象所 共享的。

- 构造函数通过原型分配的函数是所有对象所`共享的`
- JavaScript 规定，`每一个构造函数都有一个 prototype 属性`，指向另一个对象，所以我们也称为原型对象
- 这个对象可以挂载函数，对象实例化不会多次创建原型上函数，节约内存
- `我们可以把那些不变的方法，直接定义在 prototype 对象上，这样所有对象的实例就可以共享这些方法`。
- `构造函数和原型对象中的this 都指向 实例化的对象`

```html
<script>
  function Person() {
    
  }

  // 每个函数都有 prototype 属性
  console.log(Person.prototype)
</script>
```

了解了 JavaScript 中构造函数与原型对象的关系后，再来看原型对象具体的作用，如下代码所示：

```html
<script>
  function Person() {
    // 此处未定义任何方法
  }

  // 为构造函数的原型对象添加方法
  Person.prototype.sayHi = function () {
    console.log('Hi~');
  }
	
  // 实例化
  let p1 = new Person();
  p1.sayHi(); // 输出结果为 Hi~
</script>
```

构造函数 `Person` 中未定义任何方法，这时实例对象调用了原型对象中的方法 `sayHi`，接下来改动一下代码：

```html
<script>
  function Person() {
    // 此处定义同名方法 sayHi
    this.sayHi = function () {
      console.log('嗨!');
    }
  }

  // 为构造函数的原型对象添加方法
  Person.prototype.sayHi = function () {
    console.log('Hi~');
  }

  let p1 = new Person();
  p1.sayHi(); // 输出结果为 嗨!
</script>
```

构造函数 `Person` 中定义与原型对象中相同名称的方法，这时实例对象调用则是构造函中的方法 `sayHi`。

通过以上两个简单示例不难发现 JavaScript 中对象的工作机制：**当访问对象的属性或方法时，先在当前实例对象是查找，然后再去原型对象查找，并且原型对象被所有实例共享。**

```html
<script>
	function Person() {
    // 此处定义同名方法 sayHi
    this.sayHi = function () {
      console.log('嗨!' + this.name)
    }
  }

  // 为构造函数的原型对象添加方法
  Person.prototype.sayHi = function () {
    console.log('Hi~' + this.name)
  }
  // 在构造函数的原型对象上添加属性
  Person.prototype.name = '小明'

  let p1 = new Person()
  p1.sayHi(); // 输出结果为 嗨!
  
  let p2 = new Person()
  p2.sayHi()
</script>
```

总结：**结合构造函数原型的特征，实际开发重往往会将封装的功能函数添加到原型对象中。**

### constructor 属性

在哪里？ 每个原型对象里面都有个constructor 属性（constructor 构造函数）

作用：该属性`指向`该原型对象的`构造函数， 简单理解，就是指向我的爸爸，我是有爸爸的孩子`

**使用场景：**

如果有多个对象的方法，我们可以给原型对象采取对象形式赋值.

但是这样就会覆盖构造函数原型对象原来的内容，这样修改后的原型对象 constructor 就不再指向当前构造函数了

此时，我们可以在修改后的原型对象中，添加一个 constructor 指向原来的构造函数。

~~~js
function Star() {
  
}

console.log(Star.prototype)	//	{constructor: f}

Star.prototype = {
  //	重新指回这个原型对象的构造函数
  constructor: Star
  sing: function() {
    console.log('唱歌')
  },
  dance: function() {
    console.log('跳舞')
  },
}
console.log(Star.prototype)	//	{constructor: f, sing: f, dance: f}
~~~

### 对象原型

对象都会有一个属性 `__proto__` 指向构造函数的 prototype 原型对象，之所以我们对象可以使用构造函数 prototype 原型对象的属性和方法，就是因为对象有 `__proto__` 原型的存在。

注意：

- `__proto__ `是JS非标准属性，只能读取，不能赋值
- [[prototype]]和`__proto__`意义相同
- 用来表明当前实例对象指向哪个原型对象prototype
- `__proto__`对象原型里面也有一个 constructor属性，`指向创建该实例对象的构造函数`

### 原型继承

继承是面向对象编程的另一个特征，通过继承进一步提升代码封装的程度，JavaScript 中大多是借助原型对象实现继承的特性。

龙生龙、凤生凤、老鼠的儿子会打洞描述的正是继承的含义。

```html
<body>
  <script>
    // 继续抽取   公共的部分放到原型上
    // const Person1 = {
    //   eyes: 2,
    //   head: 1
    // }
    // const Person2 = {
    //   eyes: 2,
    //   head: 1
    // }
    // 构造函数  new 出来的对象 结构一样，但是对象不一样
    function Person() {
      this.eyes = 2
      this.head = 1
    }
    // console.log(new Person)
    // 女人  构造函数   继承  想要 继承 Person
    function Woman() {

    }
    // Woman 通过原型来继承 Person
    // 父构造函数（父类）   子构造函数（子类）
    // 子类的原型 =  new 父类  
    Woman.prototype = new Person()   // {eyes: 2, head: 1} 
    // 指回原来的构造函数
    Woman.prototype.constructor = Woman

    // 给女人添加一个方法  生孩子
    Woman.prototype.baby = function () {
      console.log('宝贝')
    }
    const red = new Woman()
    console.log(red)
    // console.log(Woman.prototype)
    // 男人 构造函数  继承  想要 继承 Person
    function Man() {

    }
    // 通过 原型继承 Person
    Man.prototype = new Person()
    Man.prototype.constructor = Man
    const pink = new Man()
    console.log(pink)
  </script>
</body>
```

### 原型链

基于原型对象的继承使得不同构造函数的原型对象关联在一起，并且这种关联的关系是一种链状的结构，我们将原型对象的链状结构关系称为原型链

![67679338869](E:/%E5%89%8D%E7%AB%AF/1.2023%E6%96%B0%E7%89%88%E5%89%8D%E7%AB%AFJavaScript/3.JS%E8%BF%9B%E9%98%B6/%E8%B5%84%E6%96%99/JavaScript%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9/02-%E7%AC%94%E8%AE%B0/assets/1676793388695.png)

```html
<body>
  <script>
    // function Objetc() {}
    console.log(Object.prototype)
    console.log(Object.prototype.__proto__)

    function Person() {

    }
    const ldh = new Person()
    // console.log(ldh.__proto__ === Person.prototype)
    // console.log(Person.prototype.__proto__ === Object.prototype)
    console.log(ldh instanceof Person)
    console.log(ldh instanceof Object)
    console.log(ldh instanceof Array)
    console.log([1, 2, 3] instanceof Array)
    console.log(Array instanceof Object)
  </script>
</body>
```

**原型链-查找规则**：

① 当访问一个对象的属性（包括方法）时，首先查找这个`对象自身`有没有该属性。

② 如果没有就查找它的原型（也就是` __proto__`指向的` prototype 原型对象`）

③ 如果还没有就查找原型对象的原型（`Object的原型对象`）

④ 依此类推一直找到 Object 为止（`null`）

⑤ `__proto__`对象原型的意义就在于为对象成员查找机制提供一个方向，或者说一条路线

⑥ 可以使用 instanceof 运算符用于检测构造函数的 prototype 属性是否出现在某个实例对象的原型链上

## 深浅拷贝

开发中我们经常需要复制一个对象。如果直接用赋值会有下面问题：

~~~js
//	一个 pink 对象
const pink = {
  name: 'pink老师',
  age: 18
}
const red = pink
console.log(red)	//	{name: 'pink老师', age: 18}
red.name = 'red老师'
console.log(red)	//	{name: 'red老师', age: 18}
console.log(pink)	//	{name: 'red老师', age: 18}
~~~

### 浅拷贝

首先浅拷贝和深拷贝只针对引用类型

浅拷贝：拷贝的是地址

常见方法：

1. 拷贝对象：Object.assgin() / 展开运算符 {...obj} 拷贝对象
2. 拷贝数组：Array.prototype.concat() 或者 [...arr]

~~~js
const obj = {
  uname: 'pink'
}
const o = {...obj}
console.log(o)	//	{uname: 'pink'}
o.uname = 'red'
console.log(o)	//	{uname: 'red'}
console.log(obj)	//	{uname: 'pink'}

//	一个 pink 对象
const pink = {
  name: 'pink老师',
  age: 18
}
const red = {}
Object.assign(red, pink)
console.log(red)	//	{name: 'pink老师', age: 18}
red.name = 'red老师'
console.log(red)	//	{name: 'red老师', age: 18}
console.log(pink)	//	{name: 'pink老师', age: 18}
~~~

> 如果是简单数据类型拷贝值，引用数据类型拷贝的是地址 (简单理解： 如果是单层对象，没问题，如果有多层就有问题)

### 深拷贝

首先浅拷贝和深拷贝只针对引用类型

深拷贝：拷贝的是对象，不是地址

常见方法：

1. 通过递归实现深拷贝
2. lodash/cloneDeep
3. 通过JSON.stringify()实现

#### 递归实现深拷贝

函数递归：

`如果一个函数在内部可以调用其本身，那么这个函数就是递归函数`

- 简单理解:函数内部自己调用自己, 这个函数就是递归函数
- 递归函数的作用和循环效果类似
- 由于递归很容易发生“栈溢出”错误（stack overflow），所以`必须要加退出条件 return`

```html
<body>
  <script>
    const obj = {
      uname: 'pink',
      age: 18,
      hobby: ['乒乓球', '足球'],
      family: {
        baby: '小pink'
      }
    }
    const o = {}
    
    // 拷贝函数
    function deepCopy(newObj, oldObj) {
      debugger
      //	k 属性名，oldObj[k] 属性值
      for (let k in oldObj) {
        // 处理数组的问题  一定先写数组 在写 对象 不能颠倒
        if (oldObj[k] instanceof Array) {
          newObj[k] = []
          //  newObj[k] 接收 []  hobby
          //  oldObj[k]   ['乒乓球', '足球']
          deepCopy(newObj[k], oldObj[k])
        } else if (oldObj[k] instanceof Object) {
          newObj[k] = {}
          deepCopy(newObj[k], oldObj[k])
        }
        else {
          // newObj[k]  === o.uname  给新对象添加属性
          newObj[k] = oldObj[k]
        }
      }
    }
    deepCopy(o, obj) // 函数调用  两个参数 o 新对象  obj 旧对象
    console.log(o)
    o.age = 20
    o.hobby[0] = '篮球'
    o.family.baby = '老pink'
    console.log(obj)
    console.log([1, 23] instanceof Object)
    // 复习
    // const obj = {
    //   uname: 'pink',
    //   age: 18,
    //   hobby: ['乒乓球', '足球']
    // }
    // function deepCopy({ }, oldObj) {
    //   // k 属性名  oldObj[k] 属性值
    //   for (let k in oldObj) {
    //     // 处理数组的问题   k 变量
    //     newObj[k] = oldObj[k]
    //     // o.uname = 'pink'
    //     // newObj.k  = 'pink'
    //   }
    // }
    
    // 利用递归函数实现 setTimeout 模拟 setInterval 效果
    function getTime() {
      document.querySelector('div').innerHTML = new Date().toLocaleString()
      setTimeout(getTime,1000)
    }
    getTime()
    
  </script>
</body>
```

#### js库lodash里面cloneDeep内部实现了深拷贝

```html
<body>
  <!-- 先引用 -->
  <script src="./lodash.min.js"></script>
  <script>
    const obj = {
      uname: 'pink',
      age: 18,
      hobby: ['乒乓球', '足球'],
      family: {
        baby: '小pink'
      }
    }
    const o = _.cloneDeep(obj)
    console.log(o)
    o.family.baby = '老pink'
    console.log(obj)
  </script>
</body>
```

#### JSON序列化

```html
<body>
  <script>
    const obj = {
      uname: 'pink',
      age: 18,
      hobby: ['乒乓球', '足球'],
      family: {
        baby: '小pink'
      }
    }
    // 把对象转换为 JSON 字符串
    // console.log(JSON.stringify(obj))
    const o = JSON.parse(JSON.stringify(obj))
    console.log(o)
    o.family.baby = '123'
    console.log(obj)
  </script>
</body>
```

## 异常处理

> 了解 JavaScript 中程序异常处理的方法，提升代码运行的健壮性。

### throw

异常处理是指预估代码执行过程中可能发生的错误，然后最大程度的避免错误的发生导致整个程序无法继续运行

总结：

1. throw 抛出异常信息，程序也会终止执行
2. throw 后面跟的是错误提示信息
3. Error 对象配合 throw 使用，能够设置更详细的错误信息

```html
<script>
  function counter(x, y) {

    if(!x || !y) {
      // throw '参数不能为空!';
      throw new Error('参数不能为空!')
    }

    return x + y
  }

  counter()
</script>
```

总结：

1. `throw` 抛出异常信息，程序也会终止执行
2. `throw` 后面跟的是错误提示信息
3. `Error` 对象配合 `throw` 使用，能够设置更详细的错误信息

### try ... catch

我们可以通过 try / catch 捕获错误信息（浏览器提供的错误信息）try 试试 catch 拦住 finally 最后

```html
<script>
   function foo() {
      try {
        // 查找 DOM 节点，可能发送错误的代码写到 try
        const p = document.querySelector('.p')
        p.style.color = 'red'
      } catch (error) {
        // try 代码段中执行有错误时，会执行 catch 代码段
        // 查看错误信息
        console.log(error.message)
        // 终止代码继续执行
        return

      }
      finally {
        //	不管程序对不对，都会执行的代码
          alert('执行')
      }
      console.log('如果出现错误，我的语句不会执行')
    }
    foo()
</script>
```

总结：

1. `try...catch` 用于捕获错误信息
2. 将预估可能发生错误的代码写在 `try` 代码段中
3. 如果 `try` 代码段中出现错误后，会执行 `catch` 代码段，并截获到错误信息
4. `finally`不管是否有错误，都会执行

### debugger

相当于断点调试，浏览器直接跳到此代码

## 处理this

> 了解函数中 this 在不同场景下的默认值，知道动态指定函数 this 值的方法。

`this` 是 JavaScript 最具“魅惑”的知识点，不同的应用场合 `this` 的取值可能会有意想不到的结果，在此我们对以往学习过的关于【 `this` 默认的取值】情况进行归纳和总结。

### 普通函数

**普通函数**的调用方式决定了 `this` 的值，即【谁调用 `this` 的值指向谁】，如下代码所示：

```html
<script>
  // 普通函数
  function sayHi() {
    console.log(this)  
  }
  // 函数表达式
  const sayHello = function () {
    console.log(this)
  }
  // 函数的调用方式决定了 this 的值
  sayHi() // window
  window.sayHi()
	

// 普通对象
  const user = {
    name: '小明',
    walk: function () {
      console.log(this)
    }
  }
  // 动态为 user 添加方法
  user.sayHi = sayHi
  uesr.sayHello = sayHello
  // 函数调用方式，决定了 this 的值
  user.sayHi()
  user.sayHello()
</script>
```

注： 普通函数没有明确调用者时 `this` 值为 `window`，严格模式下没有调用者时 `this` 的值为 `undefined`。

### 箭头函数

**箭头函数**中的 `this` 与普通函数完全不同，也不受调用方式的影响，事实上`箭头函数中并不存在 this` ！箭头函数中访问的 `this` 不过是箭头函数所在作用域的 `this` 变量。

1. 箭头函数会默认帮我们绑定外层 this 的值，所以在箭头函数中 this 的值和外层的 this 是一样的
2. 箭头函数中的 this 引用的就是最近作用域中的 this
3. 向外层作用域中，一层一层查找 this，直到有 this 的定义

```html
<script>
    
  console.log(this) // 此处为 window
  // 箭头函数
  const sayHi = function() {
    console.log(this) // 该箭头函数中的 this 为函数声明环境中 this 一致
  }
  // 普通对象
  const user = {
    name: '小明',
    // 该箭头函数中的 this 为函数声明环境中 this 一致
    walk: () => {
      console.log(this)	//	window
    },
    
    sleep: function () {
      let str = 'hello'
      console.log(this)
      let fn = () => {
        console.log(str)
        console.log(this) // 该箭头函数中的 this 与 sleep 中的 this 一致
      }
      // 调用箭头函数
      fn();
    }
  }

  // 动态添加方法
  user.sayHi = sayHi
  
  // 函数调用
  user.sayHi()
  user.sleep()
  user.walk()
</script>
```

在开发中【使用箭头函数前需要考虑函数中 `this` 的值】，**事件回调函数**使用箭头函数时，`this` 为全局的 `window`，因此DOM事件回调函数`如果里面需要`DOM 对象的 this，则不推荐使用箭头函数，如下代码所示：

```html
<script>
  // DOM 节点
  const btn = document.querySelector('.btn')
  // 箭头函数 此时 this 指向了 window
  btn.addEventListener('click', () => {
    console.log(this)
  })
  // 普通函数 此时 this 指向了 DOM 对象
  btn.addEventListener('click', function () {
    console.log(this)
  })
</script>
```

同样由于箭头函数 `this` 的原因，**基于原型的面向对象也不推荐采用箭头函数**，如下代码所示：

```html
<script>
  function Person() {
  }
  // 原型对像上添加了箭头函数
  Person.prototype.walk = () => {
    console.log('人都要走路...')
    console.log(this); // window
  }
  const p1 = new Person()
  p1.walk()
</script>
```

总结：

1. 函数内不存在 this，沿用上一级的
2. 不适用：构造函数，原型函数，字面量对象中函数，dom 事件函数等等
3. 适用：需要使用上层 this 的地方
4. 使用正确的话，它会在很多地方带来方便，后面我们会大量使用慢慢体会

### 改变this指向

以上归纳了普通函数和箭头函数中关于 `this` 默认值的情形，不仅如此 JavaScript 中还允许指定函数中 `this` 的指向，有 3 个方法可以动态指定普通函数中 `this` 的指向：

#### call

使用 `call` 方法调用函数，同时指定函数中 `this` 的值

语法：`fun.call(thisArg, arg1, arg2, ...)`

thisArg表示 fun 函数运行时指定的 this 值，arg1、arg2 表示传递的其他参数，返回值就是函数的返回值，因为它就是调用函数

使用方法如下代码所示：

```html
<script>
  // 普通函数
  function sayHi() {
    console.log(this);
  }

  let user = {
    name: '小明',
    age: 18
  }

  let student = {
    name: '小红',
    age: 16
  }

  // 调用函数并指定 this 的值
  sayHi.call(user); // this 值为 user
  sayHi.call(student); // this 值为 student

  // 求和函数
  function counter(x, y) {
    return x + y;
  }

  // 调用 counter 函数，并传入参数
  let result = counter.call(null, 5, 10);
  console.log(result);
</script>
```

总结：

1. `call` 方法能够在调用函数的同时指定 `this` 的值
2. 使用 `call` 方法调用函数时，第1个参数为 `this` 指定的值
3. `call` 方法的其余参数会依次自动传入函数做为函数的参数

#### apply

使用 `apply` 方法**调用函数**，同时指定函数中 `this` 的值

语法：`fun.apply(thisArg,[argsSrray])`

thisArg表示在 fun 函数运行时指定的 this 值，argsArray 表示传递的值，必须包含在`数组`里面，返回值就是函数的返回值，因为它就是调用函数

apply 主要跟数组有关系，比如使用 Math.max() 求数组的最大值

使用方法如下代码所示：

```html
<script>
  // 普通函数
  function sayHi() {
    console.log(this)
  }

  let user = {
    name: '小明',
    age: 18
  }

  let student = {
    name: '小红',
    age: 16
  }

  // 调用函数并指定 this 的值
  sayHi.apply(user) // this 值为 user
  sayHi.apply(student) // this 值为 student

  // 求和函数
  function counter(x, y) {
    return x + y
  }
  // 调用 counter 函数，并传入参数
  let result = counter.apply(null, [5, 10])
  console.log(result)
</script>
```

总结：

1. `apply` 方法能够在调用函数的同时指定 `this` 的值
2. 使用 `apply` 方法调用函数时，第1个参数为 `this` 指定的值
3. `apply` 方法第2个参数为数组，数组的单元值依次自动传入函数做为函数的参数

#### bind

`bind` 方法并**不会调用函数**，而是创建一个指定了 `this` 值的新函数

语法：`fun.bind(thisArg, arg1, arg2, ...)`

thisArg 表示 fun 函数运行时指定的 this 值，arg1、arg2 表示传递的其他参数，返回由指定的 this 值和初始化参数改造的`原函数拷贝（新函数）`，因此当我们只是想改变 this 指向，并且不想调用这个函数的时候，可以使用 bind，比如改变定时器内部的 this 指向

使用方法如下代码所示：

```html
<script>
  // 普通函数
  function sayHi() {
    console.log(this)
  }
  let user = {
    name: '小明',
    age: 18
  }
  // 调用 bind 指定 this 的值
  let sayHello = sayHi.bind(user);
  // 调用使用 bind 创建的新函数
  sayHello()
</script>
```

注：`bind` 方法创建新的函数，与原函数的唯一的变化是改变了 `this` 的值。

#### 总结

**相同点**：

都可以改变函数内部的 this 指向

**区别点**：

1. call 和 apply 会调用函数
2. call 和 apply 传递的参数不一样，call 传递参数 aru1，aru2...形式，apply 必须数组形式 [arg]
3. bind 不会调用函数

**主要应用场景**：

1. call 调用函数并且可以传递参数
2. apply 经常跟数组有关系，比如借助于数学对象实现数组最大值最小值
3. bind 不调用函数，但是还想改变 this 指向，比如改变定时器内部的 this  指向

## 防抖节流

### 防抖（debounce）

所谓防抖，就是指触发事件后在 n 秒内函数只能执行一次，如果在 n 秒内又触发了事件，则会重新计算函数执行时间，单位时间内，频繁触发事件，`只执行最后一次`

举例：王者荣耀回城，只要被打断就需要重新来

使用场景：

1. `搜索框搜索输入`，只需要用户`最后`一次输入完，再发送请求
2. 手机号、邮箱验证`输入检测`

实现方式：

1. lodash 提供的防抖，语法：`_.debounce(fun, 时间)`
2. 手写一个防抖函数，核心思路：防抖的核心就是利用定时器（`setTimeout`）来实现
   - 声明一个定时器`变量`
   - 当鼠标每次滑动都先判断`是否有定时器`了，如果有定时器先`清除以前`的定时器
   - 如果没有定时器则`开启`定时器，记得`存到变量`里面
   - 在`定时器里面调用`要执行的函数

~~~html
<!-- 引入js -->
<script src="./lodash.min.js"></script>
<script>
  //  利用防抖实现性能优化
  //  需求：鼠标在盒子上移动，里面的数字就会变化 +1
  const box = document.querySelector('.box')
  let i = 1
  function mouseMove() {
    box.innerHTML = i++
    //  如存在大量小号性能的代码，比如 dom 操作、数据处理，可能造成卡顿
  }

  //  添加事件
  // box.addEventListener('mousemove', mouseMove)

  //  防抖，鼠标停止 500ms 后里面的数字才变化
  //  lodash 防抖,语法：_.debounce(fun, 时间)
  // box.addEventListener('mousemove', _.debounce(mouseMove, 500))

  // 手写防抖函数
  // 声明定时器变量
  function debounce(fn, t) {
    let timer
    // return 返回一个匿名函数
    return function() {
      // 判断是否有定时器，有则清除以前的定时器
      if(timer) clearTimeout(timer)
      // 没有则开启定时器，存入定时器变量
      timer = setTimeout(function() {
        // 定时器里面调用函数
        fn()
      }, t)
    }
  }
  box.addEventListener('mousemove',debounce(mouseMove, 500))
</script>
~~~

### 节流（throttle）

**节流**：单位时间内，频繁触发事件，`只执行一次`

举例：

1. 王者荣耀技能冷却，期间无法继续释放技能
2. 和平精英换子弹期间不能射击

使用场景：

高频事件：鼠标移动 `mousemove`、页面尺寸缩放 `resize`、滚动条滚动 `scroll` 等等

实现方式：

1. `lodash` 提供的`节流函数`，语法：`_.throttle(fun, 时间)`
2. `手写`一个节流函数，核心思路：节流的核心就是利用定时器（`setTimeout`）来实现
   - 声明一个定时器`变量`
   - 当鼠标每次滑动都先判断`是否有定时器`了，如果有定时器则`不开启`新定时器
   - 如果没有定时器则`开启`定时器，记得`存到变量`里面
   - 在`定时器里面调用`要执行的函数，并且要把定时器`清空`

~~~html
<!-- 引入js -->
<script src="./lodash.min.js"></script>
<script>
  //  利用防抖实现性能优化
  //  需求：鼠标在盒子上移动，里面的数字就会变化 +1
  const box = document.querySelector('.box')
  let i = 1
  function mouseMove() {
    box.innerHTML = i++
    //  如存在大量小号性能的代码，比如 dom 操作、数据处理，可能造成卡顿
  }

  //  添加事件
  // box.addEventListener('mousemove', mouseMove)

  //  节流，鼠标停止 500ms 后里面的数字才变化
  //  lodash 节流,语法：_.throttle(fun, 时间)
  // box.addEventListener('mousemove', _.throttle(mouseMove, 500))

  // 手写节流数
  // 声明定时器变量
  function throttle(fn, t) {
    let timer = null
    // return 返回一个匿名函数
    return function() {
      // 判断是否有定时器，如果有定时器则不开启新定时器
      if(!timer) {
        // 没有则开启定时器，存入定时器变量
        timer = setTimeout(function() {
          // 定时器里面调用函数
          fn()
          // 定时器清空
          timer = null
        }, t)
      }
    }
  }
  box.addEventListener('mousemove',throttle(mouseMove, 500))
</script>
~~~

| 性能优化 |                    说明                    |                           使用场景                           |
| :------: | :----------------------------------------: | :----------------------------------------------------------: |
|   防抖   | 单位时间内，频繁触发事件，`只执行最后一次` |           搜索框搜索输入、手机号、邮箱验证输入检测           |
|   节流   |   单位时间内，频繁触发事件，`只执行一次`   | 高频事件：鼠标移动 mousemove、页面尺寸缩放 resize、滚动条滚动 scroll 等等 |












