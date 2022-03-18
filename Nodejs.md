## 文件读取

1. 导入 `fs`模块

```js
const fs = require('fs')
```

2. 调用 `fs.readFile` 方法读取文件

参数：文件名， 编码格式，回调函数（err, data)

- 如果读取成功，`err` 为 null
- 如果读取失败， `err` 为 错误对象， data 为 undefined

```js
fs.readFile('./files/test.txt', 'utf8', function(err, data){
    if(err) throw err;
    console.log(data);
})
```

### Promise 封装文件读取 `fs` 模块

```js
const fs = require('fs');
let p = new Promise((resolve, reject) => {
    fs.readFile('./files/test.txt', 'utf8', (err, data) => {
        if(err) reject(err);
        resolve(data);
    });
});

p.then(value => {
    console.log(value.toString());
}, reason =>{
    console.log(reason);
})
```

## 文件写入

1. 导入 `fs` 模块

2. 调用 `fs.writeFile()` 方法

参数：写入文件名，写入的内容，回调函数

- 如果写入成功，err 为 null
- 写入失败，err 为错误对象

```js
fa.writeFile('./files/test.txt', 'write data test', function(err){
    if(err) return err.message;
    console.log('write success!')
})
```

## 路径问题和文件名与后缀

`__dirname` 表示当前文件所处的目录

引入 path 模块

```js
const path = require('path')
```

`path.join()` 可以拼接路径

结合使用：`../` 会抵消前面的路径

`path.join(__dirname, './files/1.txt', ...,...)` 

-------

获取文件名：

```js
const fullName = path.basename('/a/b/c/d/index.html')
// fullName = 'index.html'
```

去掉后缀：

```js
const nameWithoutExt = path.basename('/a/b/c/d/index.html', '.html')
// nameWithoutExt = 'index'
```

获取文件后缀：

```js
const fileExt = path.extname('/a/b/c/d/index.html');
// fileExt = '.html'
```

## `http`  模块创建服务器

使用 `http` 模块的 `createServer()` 函数创建 web 服务器实例

```js
// 1.导入http模块
const http = require('http');
// 2. 创建 web 服务器实例
const server = http.createServer()
// 3. 为服务器绑定 request 事件，监听客户端请求
server.on('request', function(req, res){
          console.log('Someone visit my web server!')
          });
// 4. 启动服务器
server.listen(8080, function(){
    console.log('server running at http://127.0.0.1:8080');
})
```

### `req` 请求对象

`req` 是客户端的请求对象，包含了与客户端相关的数据和属性

`req.url` 是客户端请求的地址

`req.method`  是客户端请求的 method 类型

`res.end(数据)` 方法，向客户端响应数据

```js
const http = require('http');
const server = http.createServer();
server.on('request', function(req, res) => {
		const url = req.url;
         const method = req.method;
         const str = `你的请求 url 是${url}, 请求的类型是：${method}`;
		res.end(str);
});
server.listen(8080, funtion(){
	console.log('server running at http://127.0.0.1:8080');
})
```

![image-20220318191837791](C:\Users\RAINSUN\AppData\Roaming\Typora\typora-user-images\image-20220318191837791.png)

**中文乱码**

设置响应头：

```js
server.on('request', (req, res) => {
  // 定义一个字符串，包含中文的内容
  const str = `您请求的 URL 地址是 ${req.url}，请求的 method 类型为 ${req.method}`
  //调用 res.setHeader() 方法，设置 Content-Type 响应头，解决中文乱码的问题
  res.setHeader('Content-Type', 'text/html; charset=utf-8')
  // res.end() 将内容响应给客户端
  res.end(str)
})

```

![image-20220318192133271](C:\Users\RAINSUN\AppData\Roaming\Typora\typora-user-images\image-20220318192133271.png)

### 根据不同的 `url` 响应不同的 `html` 内容

## 自定义模块

## express 创建服务器

### express.static 提供静态资源

## 路由

### 模块化路由

## 中间件

### 局部中间件

### 全局中间件

### 解析表单数据

## 跨域问题

## 操作 mysql 数据库

## 身份认证

### session

### jwt
