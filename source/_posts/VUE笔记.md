---
title: vue习笔记
---
# VUE笔记
>el用于选择属性

>data用于定义属性和值

>methods用于定义的函数，可以通过return来返回函数值  


*双向数据绑定只存在于form表单元素中*

*首先双向数据的绑定需要通过 v-model 来将数据关联起来，
其次在 data 中一定要定义好通过 v-model 关联的数据，
Vue 在实现数据监听只能够监听到 data 中的数据，
如果在 data 中没有定义该数据，那么将无法实现监听 ，
同时也无法实现表单的双向数据绑定*

<!-- more -->

数据绑定最常见的形式就是使用双大括号的文本值插入

```
    <p>{{ message }}</p>
```

**v-bind**  
它的用法是后面加冒号，跟上html元素的属性，例如：
```
<div id="app-2">
  <span v-bind:title="message">
    鼠标悬停几秒钟查看此处动态绑定的提示信息！
  </span>
</div>
```
如果不加 v-bind 那么 message 就是个常量，没有任何动态数据参与。当加上 v-bind 之后，它的值 message 不是字符串，而是vue实例对应的 data.message 这个变量。
```
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: '页面加载于 ' + new Date().toLocaleString()
  }
})
```
**v-model双向绑定**  

在 input 输入框中我们可以使用 v-model 指令来实现双向数据绑定：

```
    <div id="app">
        <p>{{ message }}</p>
        <input v-model="message">
    </div>
    <script>
    new Vue({
    el: '#app',
        data: {
            message: 'Hello Vue!'
        }
     })
    </script>
```

双向绑定:输入框文字改变，数据内容也改变

v-model.lazy//延后绑定时间，如当用户输入完数据后失去input焦点后再更新绑定

v-model.trim//去掉输入字符串前后的空格字符

v-model.number//将输入的字符串数字直接转换为number类型

## 缩写
**v-bind 缩写**  

```
<!-- 完整语法 -->
<a v-bind:href="url"></a>
<!-- 缩写 -->
<a :href="url"></a>
```

**v-on 缩写**  

```
<!-- 完整语法 -->
<a v-on:click="doSomething"></a>
<!-- 缩写 -->
<a @click="doSomething"></a>
```

**v-if条件语句**  

```
<div id="app-3">
  <p v-if="seen">现在你看到我了</p>
</div>
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
```

**v-for循环**  

```
<div id="app-4">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: '学习 JavaScript' },
      { text: '学习 Vue' },
      { text: '整个牛项目' }
    ]
  }
})
```

**v-on 监听**  
*可以用 v-on 指令添加一个事件监听器，通过它调用在 Vue 实例中定义的方法：*  

```
<div id="app-5">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">逆转消息</button>
</div>
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Hello Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})  
```

**computed计算属性**
在vue中添加
```
var app6 = newVue({
    el:'#app-6',
    data:{
        a:34,
        b:56,
    },
    
});
computed:{
    sum: function(){
        return this.a+this.b;
    }
    avg: fuction(){
        return this.sum/2;
    }
}
```
{{sum}}
{{avg}}

与methods区别：计算完成会产生一个缓存存储计算后的数据，只要数据不改变就不会像methods每次渲染都调用一次方法

防坑：记得将输入的数据处理为number类型，否则会将数据当初字符串拼接，使用v-model.number或者在方法中对数据使用parseFloat()等方法：return parseFloat(this.a);

**components自定义组件**
在vue中添加:
```
components:{
    'new_btn':{
        template:'<button @click="on_click"></button>',
        methods:{
            on_click: function(){
                alert('hello');
            }
        }
    }
}
```

全局添加:

```
Vue.components('new_btn',{
     template:'<button @click="on_click"></button>',
        methods:{
            on_click: function(){
                alert('hello');
            }
        }
});
```