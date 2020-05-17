---
title: css样式垂直居中显示元素方案
---

# CSS定位元素水平垂直居中
## 第一种
**负边距居中：子元素相对于父元素绝对定位，设置margin百分比50，边距减去子元素一半的宽高**

<!--more-->

```
<style>
        body{margin: 0;}
        .box{
            width: 400px;
            height: 400px;
            border:1px solid red;
            position: relative;
        }
        .sbox{
            position: absolute;
            /*设置左，上方向上距离为50%*/
            top: 50%;
            left: 50%;
            /*设置元素左，上边距为该元素一半宽高*/
            margin-top: -50px;
            margin-left: -50px;
            width: 100px;
            height: 100x;
            background: yellow;
        }
</style>
<body>
    <div class="box">
        <div class="sbox"></div>
     </div>
</body>

```
*缺点：需要知道元素宽高且不支持百分比*

## 第二种
**绝对定位居中：子元素相对于父元素绝对定位，上下左右定位为0，margin值为auto**
```
<style>
        body{margin: 0;}
        .box{
            width: 400px;
            height: 400px;
            border:1px solid red;
            position: relative;
        }
        .sbox{
            position: absolute;
            /*设置元素距离上下左右都为0*/
            left: 0;
            right: 0;
            bottom: 0;
            top:0;
            /*设置元素margin值为auto*/
            margin: auto;
            width: 100px;
            height: 100x;
            /*防止内容越界溢出*/
            overflow: auto; 
            background: green;
        }
</style>
<body>
    <div class="box">
        <div class="sbox"></div>
     </div>
</body>
```
*兼容性较好，不受元素宽高限制，缺点:不支持IE7以下的浏览器*

## 第三种
**css3移动样式居中：**
```
<style>
        body{margin: 0;}
        .box{
            width: 400px;
            height: 400px;
            border:1px solid red;
            position:relative;
        }
        .sbox{
            width: 100px;
            height: 100x;
            background: green;
            position: absolute;
            left: 50%;
            top: 50%;
            /*设置css3变形*/
            transform: translate(-50%,-50%);
        }
</style>
<body>
    <div class="box">
        <div class="sbox"></div>
     </div>
</body>
```
*适合移动端，不定宽高，缺点:兼容性不好，只支持IE9+的浏览器，可能与其他transform属性冲突，需要添加浏览器厂商前缀*

## 第四种
**flex弹性布局居中：**
```
<style>
        body{margin: 0;}
        .box{
            width: 400px;
            height: 400px;
            border:1px solid red;
            /*设置flex布局*/
            display: flex;
            /*设置主轴，交叉轴居中对齐*/
            justify-content: center;
            align-items: center;
        }
        .sbox{
            width: 100px;
            height: 100x;
            background: green;
        }
</style>
<body>
    <div class="box">
        <div class="sbox"></div>
     </div>
</body>    

```
*缺点：兼容性差，最低IE10*

*设为Flex布局以后，子元素的float、clear和vertical-align属性将失效.*

*Webkit内核的浏览器，必须加上-webkit前缀*

## 第五种
**表格样式居中： diplay：table-cell，将元素转换为表格样式，使用表格样式居中**
```
<style>
        body{margin: 0;}
        .box{
            width: 400px;
            height: 400px;
            border:1px solid red;
            /*给它的父容器加一个text-align:center的样式*/
            display: table-cell
            /*把此元素放置在父元素的中部*/
            vertical-align: middle;
        }
        .sbox{
            margin:0 auto;
            width: 100px;
            height: 100x;
            background: green;
        }
</style>
<body>
    <div class="box">
        <div class="sbox"></div>
     </div>
</body>

```
*兼容好，不定宽高，缺点：html层级多*