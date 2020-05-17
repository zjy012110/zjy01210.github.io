---
title: CSS-position定位
---
## position 以及参数总结
 **position: relative;不会脱离文档流，position: fixed;position: absolute;会脱离文档流**
 
 <!--more-->
 
1.position: relative;相对定位： 相对于自己在文档流中的初始位置偏移定位。

2.position: fixed; 固定定位：相对于浏览器窗口定位。

3.position: absolute; 绝对定位：是相对于父级非position:static 浏览器定位。
- 如果没有任何一个父级元素是非position:static属性，则会相对于文档定位。
- 这里它的父级元素是包含爷爷级元素、祖爷爷级元素、祖宗十八代级元素的。任意一级都可以。
- 如果它的父级元素和爷爷级元素都是非position:static 属性，则，它会选择距离最近的父元素。