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

