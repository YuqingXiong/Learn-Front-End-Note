## 数据类型

- 基本数据类型：`String` `Number` `Boolean` `null` `undefined`  ES6: `Symbol` `Bigint` 
  - 定义但未被赋值的变量为 undefined
  - null 表示一个空的对象，`typeof null`  为 Object
  - Symbol 用来表示某个属性是唯一的
- 引用数据类型：Object **Array** Function ES6: Date`、`RegExp`、`Map`、`Set
- 存储区别：
  - 基本数据类型的变量的值存储在栈空间，赋值的时候，一个变量发生改变不会影响另一个
  - 引用数据类型的变量的值存储在对空间中，栈空间中存储的是指向堆空间的起始地址，赋值时两个对象指向堆空间的同一个对象

## 类型判断

`var p = {}`

- `typeof` ：`typeod p` ==> 字符串 `'Object'` 
  - 无法判断 null，typeof null  输出 Object
  - 无法判断 Array 和 Object，typeof array 输出 Object
- `instanceof` ：`p instanceod Object` ===> Boolean `true`

## 数组方法

`push()`末尾添加

`unshift()`开头添加

`splice()` 开始位置，删除元素数量，插入元素 影响原数组

`concat()` **不影响原数组**，合并多个数组，返回新数组

---

`pop()` 删除末尾元素

`shift() `删除开头元素

`slice(beg, end)：`**不影响原数组** 字符串切割 `[beg, end)` 

----

`arr.indexOf() `查找元素第一次出现的位置，没找到返回 -1

`arr.includes()` 找到返回 true,

`arr.find((item, index, arr) = >{ item > 18})` 返回第一个匹配的元素

-----

`reverse()` 数组反转

`arr.sort((a, b) =>{return a-b})` 排序，传入排序规则函数，a - b 从小到大，b-a从大到小

------

`join("分隔符")` 返回该分隔符分割的字符串

-----

`arr.forEach((item, index, array) =>{})`

`arr.filter((item, index, array) = {过滤条件})` **返回新数组**，不会对原数组影响

`some() every() map()`

## 字符串方法

**不改变原有字符串，返回一个副本**

`str.contact()`  拼接字符串

`slice(beg, end)` / `substr(beg, end)` : `[beg, end)` 字符串切割

`substring(beg, num)` 开始位置，截取数量

---

`trim()` /`trimLeft()` /`triemRight()`  删除空格

`repeat(n)` ：复制字符串，返回副本

`toLowerCase()` / `toUpperCase()`

-----

`indexOf()`

`charAt(idx)` 返回索引位置的字符

`startWith()` / `includes()` 

----

`split(分隔符)` 按照分隔符，拆分成数组的每一项

---

`mathch()` `search()`

 **`replace('匹配内容','替换元素')`**

## DOM 操作

`creatElement("div")`

`createTextNode("content")` 

`createAttribute("myAtrr")`

-------

`querySelector('css 选择器')` 返回首个选中的 DOM 元素

`querySelectorAll("css 选择器")` 返回所有选中的 DOM 元素列表

`getElementById('id')` 

`getElementsByClassName('类名') `

`getElementsByTagName('标签')`

`getElementsByName('name属性')`

`parentNode` `childNodes` `firstChild` `lastChild` `nextSibling` `previousSibling`

----

`innerHTML`  修改文本内容，且会改变DOM 节点

`innerText` / `textContent` ：修改文本内容，但是不会设置 `html` 标签

`style` 设置节点样式

----

`innerHTML` 可以添加节点

`appendChild` 子节点添加到父节点的最后一个子节点

`parentElement.insertBefore(newElement, referenceElement)` 将newElement插入到referenceElement前面

`setAttribute('属性名', '属性值')` 添加一个属性节点或者修改属性值

----

删除节点需要有删除节点的父节点，调用父节点的 `removeChild` 删除

## 事件

- 阻止冒泡

  ```js
  div.addEventListener('click', function(e){
      e.stopPropagation();
  })
  div.onclick = (e) = >{
  	e.cancelBubble = true
  }
  ```

- 阻止默认事件发生

  ```js
  div.addEventListener('click', function(e){
      e.preventEDefault()
  })
  div.onclick = (e) =>{
      e.preventDefault()
  }
  ```

## BOM

浏览器对象模型

- window 浏览器窗口
- Navigator 浏览器信息，识别不同的浏览器
- Location 地址栏信息
  - location.href 当前页面的 url
  - location.assign(targetUrl) 跳转页面
  - location.reload() 重新加载页面，location.reload(true) 清空缓存刷新页面
  - location.hostname web 主机名
  - location.protocol 使用的 web 协议
- history
  - history.length 访问的链接数量
  - history.back() 退回上一个页面
  - history.forword()
  - history.go(n)

## 原型与原型链

- constructor 相关

1. 每一个构造函数都有一个 prototype 属性，指向一个空的 Object 对象成为原型对象
2. 每个原型对象上有一个 constructor 方法，指向构造函数
3. 当构造函数的 prototype 属性被设置为一个以字面量形式创建的对象时，constructor 将不再指向构造函数

![image-20220316230630084](C:\Users\RAINSUN\AppData\Roaming\Typora\typora-user-images\image-20220316230630084.png)

- 显式原型和隐性原型

1. 每个构造函数上都有一个显示原型属性 prototype，prototype 指向一个原型对象
2. 每个构造函数的实例对象上都有一个隐式原型属性 `__proto__`
3. 实例对象的隐式原型属性指向构造函数的显式原型对象

![image-20220316231535307](C:\Users\RAINSUN\AppData\Roaming\Typora\typora-user-images\image-20220316231535307.png)

- **原型链**

1. 函数的显式原型指向空的Object实例对象（Object的显式原型指向一个内置对象，内置对象的隐式原型为null)
2. 所有函数都是 Function 的实例（包括Function自己）
3. Object 的显式原型是 原型链的尽头

![image-20220316233554057](C:\Users\RAINSUN\AppData\Roaming\Typora\typora-user-images\image-20220316233554057.png)

- instanceof

child instanceof parent 判断 child 是否是 parent 的实例

原理是通过判断 child 的原型链上是否有 parent 的显式原型

手写instanceof

```js
function instance_of(child, parent){
    let parentPrototype = parent.prototype;
    while(child.__proto__ !== null){
        if(child.__proto__ === parentPrototype){
            return true;
        }
        child = child.__proto__;
    }
    return false;
}
```

## 变量提升与函数提升

1. 变量提升就是
   - 通过 **var 定义**的变量再定义语句之前就可以访问到
   - 值为 undefined
2. 函数提升就是
   - 通过 **function 声明**的函数，在声明之前就可以调用
   - 值为函数对象
3. 变量提升和函数提升产生的原因是？
   - **涉及执行上下文和执行上下文栈**

常见面试题：

```js
var a = 3;
function fn(){
    console.log(a); // undefined
    var a = 4;
}
fn()
fn3()

console.log(b)
fn2()
// fn3() 不能调用，遵循的是变量提升，通过函数声明的才可以是函数提升
var b = 3;
function fn2(){
	console.log('fn2()')
}
var fn3 = function(){
	console.log('fn3()')
}
```

## 执行上下文和执行上下文栈

### 执行上下文

1. 在创建阶段，也就是编译完成之后，函数被调用还没有执行内部代码之前
   - 创建词法环境，存储函数声明和变量（let const)绑定
   - 创建变量环境，存储变量(var)绑定
   - 确定this的值
2. 执行上下文分为全局执行上下文和函数执行上下文
   - 全局执行上下文中的词法环境是全局环境，有一个全局对象window，this 指向这个全局对象
     - 对全局的数据进行预处理
       - var 定义的全局变量赋值为undefined，添加为 windows 属性
       - function 声明的全局函数添加为window的方法
       - 把 this 赋值为 window
   - 在执行函数体之前，创建对应的函数执行上下文对象，函数执行上下文中的词法环境是函数环境
     - 对局部数据进行预处理
       - 将实参赋值给形参，添加为函数执行上下文的属性
       - 将实参列表赋值给 arguments
       - var 定义的局部变量赋值为 undefined
       - 将 function 声明的函数添加为函数执行上下文的方法
       - this 赋值为调用函数的对象（window, apply, call, bind, new)

### 执行上下文栈

1. 在全局代码执行之前，JS引擎会创建一个栈来存储管理所有的执行上下文对象
2. 在全局执行上下文（window)确定后，将其添加到栈中
3. 在调用函数创建了函数执行上下文后，将其添加到栈中
4. 在当前函数执行完成后，将栈顶的上下文对象出栈
5. 当所有代码执行完成后，栈中只剩下 window

常见面试题

```js
console.log('gb: ', i);
var i = 1;
foo(1);

function foo(i) {
    if (i === 4) return;
    console.log('fb: ', i)
    foo(i + 1)
    console.log('fe: ', i)
}
console.log('ge', i);
/*
    输出：
        gb: undefined
        fb: 1
        fb: 2
        fb: 3
        fb: 3
        fb: 2
        fb: 1
        ge: 1
*/
```

测试题：

```js
// 先变量提升，再函数提升，函数提升会覆盖变量提升
// 函数提升的优先级高于变量提升
function a() {}
var a;
console.log(typeof a); // function
//---------------------------------
// var b 那么window上就有b 属性了但是未被赋值
if (!(b in window)) {
    var b = 1;
}
console.log(b); // undefined
//----------------------------------
var c = 1;
function c(c){
    console.log(c);
}
c(2);   // 报错 c 不是一个 function
// 因为函数 c 将变量 c 覆盖了，但是在所有提升完成后，c 被赋值为1后，c就不是函数了，等于下面的代码
var c;
function c(c){
    console.log(c);
}
c = 1	// c 在这里赋值
c(2)
```

## 作用域 与 作用域链

### 作用域

执行上下文是执行（函数调用）的时候才产生的，作用域在编码的时候就确定了

在 ES5 中是没有块作用域的，但是ES6中增加了 let 和 const 具有块作用域

- 全局作用域：所有不在函数中或者大括号中声明的变量都在全局作用域下，可以在任意位置访问
- 函数作用域：在函数内部声明的变量，只能在函数内部访问
- 块作用域：在大括号中声明的 let 和 const 变量不能在大括号内部访问

```js
var a = 2;
function foo(){
    console.log(a)	// 输出 2
}
function bar(){
    var a = 3;
    foo();
}
bar()

var x = 10;
function fn(){
	console.log(x); // 输出10
}
function show(f){
	var x = 20;
    f()
}
show(fn);

```

### 作用域链

当JavaScript 中使用一个变量的时候，手写JS引擎会在当前作用域下寻找，如果没找到，就到它的上层作用域寻找，知道找到该变量或者已经找到了全局作用域。如果全局作用域仍然找不到就会报错：变量 is not defined

```js
var a = 10,
    b = 20;

function fn(x) {
    var a = 100,
        c = 300;
    console.log('fn()', a, b, c, x); // 100, 20, 300, 10
    function bar(x) {
        var a = 1000,
            d = 400;
        console.log('bar()', a, b, c, d, x);
    }
    bar(100); // 1000, 20, 300, 400, 100
    bar(200); // 1000, 20, 300, 400, 200
}
fn(10)
```

```js
var fn = function () {
    console.log(fn);
}
fn()    // 输出 fn 函数
// -------------------------------
var boj = {
    fn2: function () {
        console.log(fn2()); // 报错
    }
}
obj.fn2();
```

## 闭包

### 什么是闭包?

- 闭包是嵌套的内部函数
- 内部函数引用了外部函数的数据（变量/函数）
- 内部函数执行了定义就产生了闭包（不用调用内部函数）

### 常见的闭包

- 将函数作为另一个函数的返回值

  ```js
  function fn1(){
  	var a = 2;
      function fn2(){
          a++;
          console.log(a)
      }
      return fn2
  }
  var f = fn1()
  f() // 3
  f() // 4
  ```

- 将函数作为实参传递给另一个函数调用

  ```js
  function showDelay(msg, time) {
      setTimeout(function () {
          alert(msg)
      }, time)
  }
  showDelay('cug', 1000)
  ```

### 闭包的作用

1. 延长变量的生命周期

。。。

2. 模拟私有变量

。。。

### 闭包的缺点

函数执行完以后，函数内部的局部变量没有释放，占用内存的时间会变长，容易造成内存泄漏

及时释放，让内部函数成为垃圾对象

面试题：

```js
var name = 'The window';
var obj = {
    name: "My object",
    getNameFunc : function(){
        return function(){
            return this.name;
        }
    }
}
// 没有产生闭包，内部函数没有调用外部变量
alert(obj.getNameFunc()())  // The window

var name2 = "The window"
var obj2 = {
    name: 'My obj2',
    getNameFunc: function(){
        var that = this;
        return function(){
            return that.name;
        }
    }
}
// 产生了闭包，引用了外部变量that
alert(obj2.getNameFunc()()) // my obj
```

**十分绕的题目**

```js
function fun(n,o) {
 console.log(o)
 return {
   fun:function(m){
     return fun(m,n)
   }
 }
}
var a = fun(0) //undefined
a.fun(1)  //0
a.fun(2)  //0	
a.fun(3)  //0

var b = fun(0).fun(1).fun(2).fun(3) //undefined 0 1 2

var c = fun(0).fun(1) //undefined  0
c.fun(2)//1 -->经过上方定义后 n固定为1
c.fun(3)//1 -->此处是陷阱!!!  一直没有改到n,所以一直是1
```

## JavaScript 中的内存泄漏

- 内存泄漏就是由于疏忽或错误造成程序没有释放不再使用的内存，造成了内存浪费

- JavaScript 具有垃圾回收机制，可以定期找出那些不再使用的变量，释放内存
- 常见的内存泄漏
  - 意外的全局变量
  - 没有释放的定时器
  - 没有取消的事件监听
  - 闭包

```js
// 1. 内存溢出
var obj = {}
for (var i = 0; i < 10000; ++ i){
    obj[i] = new Array(10000000);
}
// 2. 内存泄漏
// 意外的全局变量
function fn(){
    a = new Array(10000000); // 不使用 var let const 承接
    console.log(a);
}
fn()

// 没有及时清理定时器或者回调函数
var intervalId = setInterval(funtion(){
                             console.log("-------")
                             }, 1000);
// clearInterval(intervalId)

// 闭包
function fn1(){
    var a = 4; 
    function fn2(){
        ++a;
    }
    return fn2;
}
var f = fn1();
f()
// f = null
```

## 对象创建模式

1. Object构造函数模式

   ```js
   var obj1 = new Object()
   obj1.name = 'xxxx';
   obj1.setName = function(name){
       this.name = name;
   }
   ```

2. 对象字面量形式

   ```js
   var obj = {
   	name: 'xxx',
       setName: function(name){
           this.name = name;
       }
   }
   ```

3. 工厂模式

   ```js
   function createPerson(name, age){
       var obj = {
           name: name,
           age: age,
           setName: function(name){
               this.name = name;
           }
       }
       return obj;
   }
   var p1 = createPerson('Tom', 12)
   var p2 = createPerson('Bob', 12)
   console.log(p1, p2)// 类型都为 Object 没有具体类型
   ```

4. 自定义构造函数

   ```js
   function Person(name, age){
       this.name = name;
       this.age = age;
       this.setName = function(name){
           this.name = name;
       }
   }
   var p1 = new Person('Tom', 12);
   console.log(p1); // 输出为 Person 类型
   ```

5. 构造函数和原型的组合：将相同的方法放在原型上

   ```js
   function Person(name, age){
       this.name = name;
       this.age = age;
   }
   Person.prototype.setName = function(name){
       this.name = name;
   }
   var p1 = new Person('Tom', 12);
   console.log(p1); // 输出为 Person 类型
   ```

## 继承模式

1. 原型链继承：子类型的原型指向父类型的实例

   ```js
   // 父类型
   function Supper(){
       this.supProp = 'Supper property'
   }
   Supper.prototype.showSupperProp = function(){
   	console.log(this.supProp)
   }
   // 子类型
   function Sub(){
       this.subProp = 'Sub property'
   }
   // 最关键的地方：子类型的原型指向父类型的实例
   Sub.prototype = new Supper()
   // 子类型的 constructor 指向 子类型
   Sub.prototype.constructor = Sub
   Sub.prototyp.showSubProp = function(){
   	console.log(this.subProp)
   }
   var sub = new Sub()
   sub.showSupperProp();
   ```

   ![image-20220317185347774](C:\Users\RAINSUN\AppData\Roaming\Typora\typora-user-images\image-20220317185347774.png)

2. 构造函数 + call 继承 （假继承)

   ```js
   function Person(name, age){
       this.name = name;
       this.age =age;
   }
   function Student(name, age, price){
   	Person.call(this, name, age);
       this.price = price
   }
   var s = new Student('Tom', 12 ,10000);
   console.log(s.name, s.age, s.price)
   ```

3. 组合继承

   ```js
   function Person(name, age){
       this.name = name;
       this.age =age;
   }
   Person.prototype.setName = function(name){
       this.name = name;
   }
   function Student(name, age, price){
       // 为了获得属性
   	Person.call(this, name, age);
       this.price = price
   }
   // 为了获得方法
   Student.prototype = new Person()
   Student.prototype.contructor = Student
   Student.prototype.setPrice = function(price){
       this.price = price;
   }
   
   var s = new Student('Tom', 12 ,10000);
   s.setName('Bob');
   s.setPrice(12000);
   console.log(s.name, s.age, s.price)
   ```

4. obj2 = Object.create(obj1)，将 obj1 放在 `obj2.__proto__` 上

   - 原型式继承
   - 寄生式继承

5. class 的 extends 方式

## 线程机制与事件机制

### 进程与线程

- 进程

  - 程序的一次执行，占有一片独有的内存空间

- 线程

  - 进程内的一个独立执行单位
  - CPU 最小的调度单元

- 进程与线程

  1. 应用程序必须运行在某个进程的某个线程上
  2. 一个进程中至少有一个运行的线程：进程启动后自动创建一个主线程
  3. 一个进程可以运行多个线程：那么这个程序就是多线程运行的
  4. 多个进程之间的数据不能直接共享的：内存之间相互独立(隔离)
  5. 线程池(thread pool)：保存着多个线程对象的容器，实现线程对象的反复利用

- 多进程与多线程

  - 多进程运行：一个程序可以同时运行多个实例
  - 多线程：一个进程，同时有多个线程运行

- 多线程：

  - 优点：提高CPU的利用率
  - 缺点：
    - 创建多线程的开销
    - 线程之间切换的开销
    - 死锁和状态同步的问题

- 单线程:

  - 优点：顺序编程，简单易懂
  - 缺点：效率低

- **JS 是单线程运行的**

  - 只能由一个线程去操作 DOM 页面

- 浏览器是 多线程 运行的

- 浏览器有的是多进程运行，有的是单进程运行

  - firebox 是单进程运行
  - 新版IE和chrome是多进程运行的
  - 可以从任务管理器查看

- 浏览器内核：支持浏览器运行的最核心程序

  - Chrome safari: webkit
  - firebox: Gecko
  - 360, 搜狗浏览器：Trident + webkit

- 浏览器内核的模块组成

  - 主线程

  	1.  javascript 引擎模块：负责js程序的编译和运行
  	2. html css 文档解析模块：负责页面文本的解析
  	3. dom/css 模块： 负责dom/css在内存中的相关处理
  	4. 布局和渲染模块：负责页面的布局和效果绘制
  - 分线程
    1. 定时器模块：管理定时器
    2. 网络请求响应：负责服务器请求（ajax...)
    3. DOM事件响应模块：管理事件
  

js执行代码的基本流程：

- 先执行初始化代码：包含一些特别的代码：回调代码（异步执行)
  - 设置定时器
  - 绑定事件监听
  - 发送 Ajax 请求
- 在后面某个时刻执行回调代码

### 事件循环模型

- 执行栈

当调用一个方法的时候，js会生成这个方法的执行环境（context），确定方法的作用域，方法的参数，记录定义的变量和this的指向。

当一个方法被调用的时候就会压入栈中，直到这个方法指向完毕出栈，并把这个执行环境销毁，继续执行下一个方法

- 宏任务队列（macro task)

定时器回调，ajax回调，dom事件回调

- 微任务队列（micro task)

Promise 回调/muntation回调

JS引擎首先必须执行所有 `初始化同步任务代码` 

**每次准备取出一个宏任务执行前，都要将所有微任务一个一个取出来执行**

首先将初始化同步代码执行，将调用的方法压入栈中，直到执行栈为空时；主线程会查看微任务队列是否有事件存在，如果存在则依次执行微任务队列中的事件的回调，直到微任务队列为空。然后取出宏任务队列中最前面的一个事件，将事件回调加入执行栈。

![image-20220317232355735](C:\Users\RAINSUN\AppData\Roaming\Typora\typora-user-images\image-20220317232355735.png)

```js
async function cv() {
    new Promise((res, rej) => {
        setTimeout(() => {
            console.log('0');
        })
        setTimeout(() => {
            res('1');
            console.log('2');
        })
    }).then((res) => {
        console.log(res);
    })
    console.log('3');
}
cv();
// 输出结果是：3 0 2 1
```

```js
setTimeout(() => { 
      console.log('timeout callback1（）')//立即放入宏队列
      Promise.resolve(3).then(
        value => { 
          console.log('Promise onResolved3()', value)//当这个宏任务执行后 立马放入微队列,所以这个微任务执行完后下个宏任务才能执行 
        }
      )
    }, 0)

    setTimeout(() => { 
      console.log('timeout callback2（）') //立即放入宏队列,
    }, 0)

    Promise.resolve(1).then(
      value => { 
        console.log('Promise onResolved1()', value)//立即放入微队列
        setTimeout(() => {
          console.log('timeout callback3（）', value) //立即放入宏任务
        }, 0)
      }
    )

    Promise.resolve(2).then(
      value => { 
        console.log('Promise onResolved2()', value)//立即放入微队列
      }
    )
console.log('同步代码') //同步代码立即执行
/*
 '同步代码',
  'Promise onResolved1()',
  'Promise onResolved2()',
  'timeout callback1（）',
  'Promise onResolved3()',
  'timeout callback2（）',
  'timeout callback3（）'
*/
```

## 其他

### 浅拷贝与深拷贝

**浅拷贝**

对于基本数据而言，拷贝的就是基本类型的值。如果属性是引用数据，则拷贝的是地址值

所以浅拷贝只拷贝一层，深层次的引用则共享内存地址

手写浅拷贝

```js
function shallowClone(obj){
    const newObj = {};
    for(prop in obj){
        if(obj.hasOwnProperty(prop)){
            newObj[prop] = obj[prop];
        }
    }
    return newObj;
}
```

存在浅拷贝的现象：

- Object.assign(target, sourse)
- Array.prototype.slice(beg, end) 切片函数，返回一个新数组
- Array.prototype.concat(arr1, arr2....) 数组连接，返回一个新数组
- ES6中的扩展运算符

### this 对象的理解



### bind call apply的区别，手写bind



### JavaScript的本地存储方式 cookie sessionStorage localStorage indexedDB



### 防抖和节流，手写实现





