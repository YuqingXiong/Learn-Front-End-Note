## 表单类型

密码：设置的 value 值为默认值

```html
<input type="password" value="xxxxx">
```

复选框：

```html
<input type="checkbox" checked>
```

## 表格

caption 为表格标题，tr 为一行 td 为一列

```html
<table>
    <caption>表格标题</caption>
    <tr>
    	<td></td>
    	<td></td>
    	<td></td>
    </tr>
        <tr>
    	<td></td>
    	<td></td>
    	<td></td>
    </tr>
</table>
```

## 图像

img 是行内元素，不独占一行，不能设置大小

```html
<img src="图片地址" title="标题属性" alt="代替文本属性">
```

## 链接

href 指定链接的目标，target 表示在新窗口打开文档，

name 规定锚点的名称，可以在统一文档中使用 href 指向该锚点进行跳转

```html
<a href="url" target="_blank" name="anchor"></a>
```

## 列表

无序列表：

```html
<ul>
    <li></li>
    <li></li>
    <li></li>
</ul>
```

有序列表：

```html
<ol>
    <li></li>
    <li></li>
    <li></li>
</ol>
```

定义列表

```html
<dl>
    <dt>dtdtdtdtd</dt>
    <dd>dddddd</dd>
    <dt>dtdtdtdtd</dt>
    <dd>dddddd</dd>
</dl>
```

![image-20220315102417356](C:\Users\RAINSUN\AppData\Roaming\Typora\typora-user-images\image-20220315102417356.png)

## 语义化标签

header 头部标签，footer 文档底部，main 文档主要内容，article 文章，section 文档中的节

nav 导航标签，。。。

## 音频媒体

controls ：是否显示控制按钮

autoplay ：自动播放

src ：播放音乐的地址

```html
<autio controls autoplay></autio>
```

## 视频媒体

controls 控制按钮

onerror 加载视频错误执行的方法

```html
<video controls onerror="fun()"></video>
```

