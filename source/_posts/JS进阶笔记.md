---
title: JS进阶笔记
---

# JS进阶
## 新增变量命名

let  //变量，防止重复定义，块级作用域 let a = 5;

const  //常量，定义后不可随意更改 const PI = 3.14

> ES5和之前版本的var定义变量是函数级的，即在函数中任意地方定义，都会作用于整个函数，例如在for循环中定义的var = i变量，会作用于整个函数。有时需要闭包来解决  
而ES6中的let定义变量则不会出现此问题

<!-- more -->

## 解构赋值

```
//解构json，使用{}
let obj = {name:"jojo",age:18}
let name = obj.name;
let age = obj.age;
//等价于
let {name,age} = {name:"jojo",age:18}
//注意变量名需一一对应

//解构数组
let [a,b,c]= [4,8,98]
//解构数组时变量名随便定义，不需要一一对应
//取非0下标开始的数时，使用","占位[,,a]为取第三个数即下标为2的数
console.log(a,b,c)
```
1.解构赋值时左右两边必须结构相同，即左边为json时，右边必须也为json

也可以用来交换两个数
```
let a = 5;
let b = 10;
[a, b]= [b, a];

console.log(a);  // 10
console.log(b);  // 5
```

2.解构赋值

赋值与解构需要同时完成


## 函数
**箭头函数**

作用：1，简写函数   
2，固定this

有且仅有一个参数时()可不写，函数中仅有一个条语句并且为return时，{}也可不写

常规定义函数:

```
function ( ){
}
箭头函数:
( )=>{   }
```

## 参数展开

**数组展开**

1，可用于收集

```
function show(a,b,...c){
    console.log(a,b,c);
}
show(3,5,7,13,6);
```

控制台输出为3,5,{7,13,6}

剩余参数被存到c中为一个数组

2，展开

用...arr的方式展开数组

```
var arr=[4,5,6];
function show(a,b,c){
    alert(a+b+c);
}
show(...arr);

Json展开
var json={a:12,b:3,c:17}
var json2={
    ...josn,
    d:18,
}
```

以上方法可以将json展开，传给下一个json

## 新增原生对象

**Array数组方法**

**map用于映射数组**

```
var arr=[65,30,46,98];
var arr2=arr.map(function(item){
   return item>=60?'及格':'不及格';
})
//arr2输出为［及格,不及格,不及格,及格］
```

**reduce最终输出单个数据**

三个参数tmp为临时存储，第一次时为数组第一个数，item为tmp后一个数，index是计算次数

```
var result=arr.reduce(function(tmp,item,index){
  if(index==arr.length-1){
      //最后一次时求平均数
      return (tmp+item)/arr.length;
  }else{
      return tmp+item;
  }
})
//result输出值为平均数
```


**filter数组过滤**
```
var arr2=arr.filter(function(item){
  //过滤掉数组中的奇数
  if(item%2==1){
      return false;
  }else{
      return true;
  }
  //或者简写为
  return item%2==0;
})
```
      
**forEach循环**

forEach() 方法用于调用数组的每个元素，并将元素传递给回调函数。

```
//currentValue当前元素，必须
//index当前元素索引值，可选
//arr当前元素所属数组对象，可选
/*可选。传递给函数的值一般用 "this" 值。
如果这个参数为空， "undefined" 会传递给 "this" 值*/
array.forEach(function(currentValue, index, arr), thisValue)

<button onclick="numbers.forEach(myFun)">点我</button>
<p>数组元素总和：<span id="demo"></span></p>

var sum = 0;
var numbers = [65, 44, 12, 4];
function myFun(item) {
    sum += item;
    demo.innerHTML = sum;
}
```


**JSON对象**

```
JSON.stringify({需转换为字符串的JSON});
//json转为字符串
JSON.parse({需转换为JSON的字符串});
//字符串转为json
```

## 异步操作

async //标识符，提示该方法带有异步操作

await //标识符，提示async函数到该处时暂停处理异步操作

```
async function show(){
    xxx;
    xxx;
    let data1=await $.ajax();
    xxx;
}
```

普通函数一直执行

async函数可以一直暂停


## 面向对象
*新增class关键字创建类*

*新增constructor关键字表示构造函数*

```
class Person{
    constructor(name,age){
        this.name=name;
        this.age=age;
    }
    showName(){
        alert(this.name);
    }
    showAge(){
        alert(this.age);
   }
}

let man = new Person('sam',16);
man.showName();
man.showAge();
```

**extends继承**
```
class Worker extends Person{
    constructor(name,age,job){
        super(name,age);
        this.job=job;
    }
    showJob(){
        alert(this.job);
    }
}
let w=new Worker('jack',15,'搬砖');
w.showName();
w.showAge();
w.showJob();
```