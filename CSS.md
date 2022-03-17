## CSS 选择器

类选择器：`.class {}`

id选择器：`#id {}`

元素选择器：`div {}`

伪类选择器：

-  `:nth-child(_)` 
  - n第 0 ~ 正无穷
  - 2n/even：偶数子元素
  - 2n+1/odd：奇数子元素
- first-child，last-child
- `:first-of-type` ：同类型的第一个子元素

伪元素选择器：

- `::before` 元素的开始

- `::after` 元素的末尾

  - ```css
    div::after{
        width:100px;
       	height: 100px;
        display: block;
        content:'';
    }
    ```

  - 要想设置高宽，必须设置  display 属性为 block 或 inline block

## 选择器权重

1. 行内样式 1000
2. id选择器：0100
3. 类选择器：0010
4. 元素选择器：0001
5. 通配符*和继承的样式没有权值

## 单位

- 像素：px
- em：`1em = <self>.font-size*10`
- rem：`1rem = <root>.font-size*10`

## 边框

`border: solid 1px black` ：无顺序要求，style+width+color

`border-radius`: 圆角，左上开始顺时针，50%可以设置圆和椭圆

## 盒子模型

`box-sizing`: 设置盒子的计算方式

- `content-box`: 盒子大小由content padding margin 决定
- `border-box`: 高宽为整个盒子可见框的带下，width和height 包含 border padding 和content

## 浮动

浮动的特点：

- 脱离文档流
- 浮动元素不会从父元素移出
- 不会超过前面浮动的元素

clear：清除浮动，本质上是浏览器自动计算添加 `margin-top` 的属性

## 脱离文档流

- 块元素不再独占页面一行，没有高宽变为被内容撑开
- 行内元素变为块元素，可以设置高宽，不独占一行
- 与行内块元素很像，但是没有默认的边距

## 高度塌陷

父元素的高度被子元素撑开，子元素浮动后脱离文档流，没有办法撑起父元素的高度，下面的元素会上移，引起布局混乱

## BFC

块级格式化环境（Block Formatting Context）

特点

- 不会被浮动元素覆盖
- 可以包含浮动元素
- 父子元素外边距不会重叠

高度塌陷的解决方式，为元素开启BFC

- 父元素：overflow：hidden

- 父元素末尾，添加一个空元素，clear:both

- 父元素:: after

  ```css
  .box::after{
      content:"";
      display:block;	/*块元素才能撑起box高度，设置margin-top*/
      clear:both;
  }
  ```

## 外边距重叠

子元素设置外边距，父元素没有border会一起移动，margin相邻会重叠

在父子元素之间使用before选择器将**两元素隔开** 

- float：left或者right
- position: absolute/fixed
- content和display:inline-block开启BFC	会有行内元素默认的边距
- **`display:table`**  开启 BFC

同时解决：

before 解决外边距重叠，after 清除浮动解决高度塌陷

```css
.clearfix::before,
.clearfix::after{
    content:"";
    display:table;
    clear:both;
}
```

## 定位

- 相对定位 relative
  - 参照自己在文档中的原始位置进行定位
  - 会提高元素的层级（如果移动到了其他元素商法，可以覆盖其他元素）
  - 不会改变元素性质（块还是块，行内还是行内）
- 绝对定位 absolute
  - 相对于**包含块**定位
  - 提高元素层级
  - 元素会从**文档中脱离**
  - 改变元素的性质：行内编程块（块的宽高被内容撑开）
- 包含快
  - 距离当前元素最近的开启了定位的祖先块元素
- 固定定位：fixed
  - 参照浏览器的视口进行定位，不跟随网页的滚动条滚动
- 元素层级 z-index
  - 开启了**定位的元素，** **才可以**使用 z-index指定元素层级

## 弹性盒

开始方式 `display: flex`

主轴的对齐方式 `flex-direction`

- `row` / `row-reverse` 水平和反向水平
- `column` / `column-reverse` 纵向排列

主轴空白 `justify-content`

- `flex-start`
- `center`
- `flex-end`
- `space-around` 两侧
- `space-between` 元素间
- `space-evenly` 单侧

辅轴对齐方式  `align-items`

- `stretch` 元素长度相同
- `flex-start` 
- `flex-end`
- `center`
- `baseline` 

辅轴空白空间 `align-content` （无法作用于**单行**弹性元素）

- `flex-start`
- `flex-end`
- `center`
- `space-around` 两侧
- `space-between` 元素间
- `space-evenly` 单侧

**弹性元素属性**

- `flex-grow` 生长系数，**默认为0**，父元素有多余空间时，按比例分配
- `flex-shrink` 收缩系数。**默认为1**，父元素空间不足时，对子元素收缩，
- `flex-basis` 元素在主轴上的基础长度。默认auto，参考自身高度宽度

简写方式

- flex：增长 缩减 基础
- `initial`: `flex: 0 1 auto`
- `auto` : `flex: 1 1 auto`
- `none` : `flex: 0 0 auto` 没有弹性

**常问：flex: 1 的含义**

- flex: 1 = flex 1 1 0

- flex: 2 = flex 1 2 0

排列顺序

- order: x

覆盖主轴属性 `align-self` 

## 双列布局

- 浮动

  - 父元素开启 BFC 避免高度塌陷  `overflow: hidden` （方式很多）
  - 子元素左浮动

- 绝对定位

  - 父元素开启定位 `position: relative `
  - 子元素绝对定位
    - left 元素 左浮动，设置 `left: 0`
    - right 元素右浮动，设置 `right: 0` 和 left 值为left元素的width

- flex实现

  - 父元素开启 display: flex
  - right子元素 `flex: 1` 

- grid实现

  - 父元素设置：

    ```css
    display: grid;
    grid-template-columns: 100px 1fr;
    ```

## 三列布局

- 浮动

  - 父元素开启 BFC, overflow: hidden
  - left 左浮动，设置width，right设置右浮动，设置width
  - 中间元素设置 margin: 0 10px

- 绝对定位

  - 父元素 `position: relative`
  - left元素设置 position: absolute，left: 0 width: 100px
  - right元素设置 position: absolute，right: 0 width: 100px
  - center元素设置 position: absolute，left: 100px  right: 100px

- flex

  - 父元素 display: flex
  - left 和 right 元素设置宽度
  - center 元素设置 `flex: 1` 占满剩余空间

- grid

  - 父元素 display: grid；grid-template-columns：100px auto 100px
  - 表示一共三列，宽度分别为 100px 自适应 100px

- 圣杯布局

  - ```html
    <section class="container">
        <article class="center">
            <main class="main"><br /><br /><br /></main>
        </article>
        <article class="left"><br /><br /><br /></article>
        <article class="right"><br /><br /><br /></article>
    </section>
    ```

  - **center 在前，可以有限渲染 center 的数据**

  - 父元素设置 overflow: hidden开启bfc，防止高度塌陷，然后设置padding为左右栏流出位置 padding: 0 100px
  - left 设置左浮动，覆盖 center, 
    - float: left; width: 100px;
    - margin-left: 100% 相对于父元素而言
    - 开启相对定位，移进预留的padding: position: relative; left: -100px
  - right 设置右浮动 
    - float: right; width: 100px;
    - margin-left: -100px;
    - 开启相对定位，移进预留的padding: position: relative; left: 100px
  - center 设置 float: left 和 width: 100% 占满空间

- 双飞翼布局

  - 父元素设置 overflow: hidden 
  - left 设置
    - float: left; width: 100px
    - margin-left: 100%
  - right
    - float: left, width: 100px
    - margin-left: -100px
  - center 中的 main 设置 margin : 0 100px
    - 通过设置外边距，将内容封锁在两边浮动元素中间

  

## 其他

**[面试官| web前端面试 - 面试官系列 (CSS](https://vue3js.cn/interview/css/box.html)**

### 如何让元素在可视范围内不可见？

- `display: none`  
  - 元素在文档流中消失，但是还存在DOM树当中
  - 绑定的事件不会触发
  - 重新显示需要页面重绘
- `visibility: hidden` 
  - 元素还占据页面的物理空间
  - 绑定的事件不会触发
  - 重新显示不需要页面重绘
- `opacity: 0` 
  - 元素还占据页面的物理空间
  - 绑定的事件会触发
- `overflow: hidden` + `height: 0; width: 0; padding: 0; margin: 0; border: 0`
- `position: absolute;` + `left: 100000px; top: 10000px` 移出可视区域
- `position: relative/absolute` + `z-index: -999` 

### 如何实现元素水平垂直居中？如果不定宽度和高度？

1. 父元素 position: relative; 子元素：position: absolute; 设置 top:0 ; bottom:0;left:0;right:0;

   然后 margin: auto

```css
#fa {
    width: 400px;
    height: 400px;
    position: relative;
    background-color: blue;
}
#son {
    width: 100px;
    height: 100px;
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    margin: auto;
    background-color: red;
}
```

2. 使用定位和margin负值，需要知道子元素宽高

父元素相对定位，子元素绝对定位

top和left为50%，将子元素的左顶点移动到父元素中心

然后子元素使用 margin-left和margin-top 负自身大小的50%

```css
#fa {
    width: 400px;
    height: 400px;
    position: relative;
    background-color: blue;
}
#son {
    width: 100px;
    height: 100px;
    position: absolute;
    top: 50%;
    left: 50%;
    margin-top: -50px;
    margin-left: -50px;
    background-color: red;
}
```

3. 定位和transform: translate(50%, 50%)

transform 代替了使用 margin负自身元素的一半调整到中心的操作，使得不需要知道高宽

```css
#fa {
    width: 400px;
    height: 400px;
    position: relative;
    background-color: blue;
}
#son {
    width: 100px;
    height: 100px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: red;
}
```

4. 使用table-cell 和 inline-block

父元素设置 table-cell，子元素设置inline-block

然后给父元素设置：text-align: center, vertical-align: middle

```css
#fa {
    width: 400px;
    height: 400px;
    display: table-cell;
    text-align: center;
    vertical-align: middle;
    background-color: blue;
}
#son {
    width: 100px;
    height: 100px;
    display: inline-block;
    background-color: red;
}
```

5. flex 布局

父元素 display: flex；

子元素在主轴上空白分配方式为 center，元素对齐方式为 center

```css
#fa {
    width: 400px;
    height: 400px;
    display: flex;
    background-color: blue;
    justify-content: center;
}
#son {
    width: 100px;
    height: 100px;
    align-self: center;
    background-color: red;
}
```

6. grid 网格布局

```css
#fa {
    width: 400px;
    height: 400px;
    display: grid;
    background-color: blue;
    justify-content: center;
}
#son {
    width: 100px;
    height: 100px;
    align-self: center;
    background-color: red;
}
```

- 行内元素居中
  - 水平居中
    - `text-align: center` 
    - flex 布局下的行内元素，给父元素设置 `justify-content: center`
  - 垂直居中
    - 单行文本：`line-height: 父元素height`
    - 多行文本：父元素：`display: table-cell` 子元素：`vertiacl-align: middle`
    - flex 布局下的行内元素，子元素设置：`align-self: center`

### 如何实现单行文本和多行文本的溢出省略？

1. 单行文本溢出

首先设置 `white-space: nowarp` 不能换行

然后设置：`overflow: hidden` 这是 `text-overflow` 生效的基础

最后设置：`text-overflow : ellipsis` 省略标记； clip：溢出裁剪

2. 多行文本溢出

- 基于高度阶段：伪元素+绝对定位

  ```css
  .demo{
      position: relative;
      line-height: 20px;
      height: 40px;
      overflow: hidden;
  }
  .demo::after{
  	content: '...';
      position: absolute;
      bottom: 0;
      right: 0;
      padding: 0 20px 0 10px;
  }
  ```

  `word-break: break-all` : 英文单词换行拆分

- 基于行数截断

  。。。。对不起，没用过，不了解

### 视差滚动

- background-attachment: fixed

  ```css
  .g-img{
      background-image: url(...);
      background-size: cover;
      background-position: center, center;
      background-attachment: fixed;
  }
  ```

- transform: translate3D

### 响应式设计

- 媒体查询

- 百分比

- vw/vh

- rem

  - 默认情况下浏览器字体大小为 16px，如果设置 1rem = 16px*62.% = 10px

  - 配合媒体查询

  - ```css
    @media screen and (max-width: 414px){
        html{
            font-size: 18px;
        }
    }
    @media screen and (max-width: 375px){
        html{
            font-size: 16px;
        }
    }
    ```

