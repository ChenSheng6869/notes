## 5 浮动

### 5.1

```
h1~h6 p div 独占一行 列表
```

行内元素不独占一行

```
span a img strong...
```

行内元素可以被包含在块级元素中,反之不可以

### 5.2 display

### 5.3 float

### 5.4 父级边框塌陷的问题

解决方案:

1.增加父级元素高度

2.增加一个空的div标签,清除浮动

```html
.clear{
            clear: both;
            margin: 0;
            padding: 0;
        }
        
 <div class="layer">
        浮动的盒子可以向左浮动，也可以向右浮动，直到它的外边缘碰到包含框或另一个浮动盒子为止。
    </div>
    <div class="clear"></div>
```

3.overflow

```
在父级元素中增加一个 overflow:hidden
```

4.父类添加一个伪类

```css
#father:after{
            content: '';
            display: block;
            clear: both;
        }
```

小结:

1.浮动元素后面增加空div

​	简单,代码中尽量避免空div

2.设置父元素的高度

​	简单,元素假设有了固定的高度,就会被限制

3.overflow

4.父类添加一个伪类:after(推荐)

写法稍微复杂,但是没有副作用

### 5.5 对比

display

方向不可以控制

float

浮动起来会脱离父级边框,所以要解决父级边框

## 6 定位

### 6.1 相对定位

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!--
    相对定位
    相对于自己原来的位置进行偏移
    -->
    <style>
        body{
            padding: 20px;
        }
        div{
            margin: 10px;
            padding: 5px;
            font-size: 12px;
            line-height: 25px;
        }
        #father{
            border: 1px solid #666;
        }
        #first{
            background-color: #0c6630;
            border: 1px dashed #0c6630;
            position: relative; /*相对定位*/
            top: -20px;
            right: 20px;
        }
        #second{
            background-color: #662d4a;
            border: 1px dashed #662d4a;
        }
        #third{
            background-color: #4158D0;
            border: 1px dashed #0f4266;
            position: relative;
        }
    </style>
</head>
<body>
<div id="father">
    <div id="first">第一个盒子</div>
    <div id="second">第二个盒子</div>
    <div id="third">第三个盒子</div>
</div>
</body>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        #box{
            width: 300px;
            height: 300px;
            border: 1px solid red;
        }

        a{
            width: 100px;
            height: 100px;
            text-decoration: none;
            background: hotpink;
            line-height: 100px;
            text-align: center;
            color: white;
            display: block;
        }

        a:hover{
            background: deepskyblue;
        }

        .a2, .a4{
            position: relative;
            left: 200px;
            top: -100px;
        }
        .a5 {
            position: relative;
            left: 100px;
            top: -300px;
        }

    </style>
</head>
<body>
<div id="box">
    <a class="a1" href="#">链接1</a>
    <a class="a2" href="#">链接2</a>
    <a class="a3" href="#">链接3</a>
    <a class="a4" href="#">链接4</a>
    <a class="a5" href="#">链接5</a>
</div>
</body>
</html>
```



### 6.2 绝对定位

1.没有父级元素定位的情况下,相对于浏览器定位

2.假设父级元素存在定位,通常会相对于父级元素进行偏移

### 6.3 z-index

z-index:默认是0,最高无限~999

