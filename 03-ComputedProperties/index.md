

## 模板表达式
之前学了模板表达式子，简单回顾下写法
```html
 <div id="app">
        {{message.split('').reverse().join('')}}
</div>

var app = new Vue({
        el: '#app',
        data:{
            message:"HelloComputedProperties"
        }
})
```

<!-- more -->

## 函数表达式
我们之前了解到模板表达式只能写简单的单行表达式，复杂的多行都不支持，这时候我们可以在表达式内调用方法

```html
 <div id="app2">
    {{reverseMessage()}}
    {{dataFormat()}}
</div>

var app2 = new Vue({
    el: '#app2',
    data:{
        message:'HelloComputedProperties',
    },
    methods:{
        reverseMessage:function(){
            var date = new Date()
            return this.message.split('').reverse().join('') + date;
        },
        dataFormat: function(){
            // alert('execute method')
            return  new Date()
        }
    }
})

setTimeout(() => {
    app2.message = 'hello'
}, 2000);
```
看上去使用函数表达式可以解决负责的属性修改运算，但是仔细发现看视图显示的或者打开注释的alert方法，我们发现在修改message的时候，不仅调用了reverseMessage的方法，同时还调用了dataFormat方法，这也许不是我们希望的结果，那么这时候就需要用到计算属性

## 计算属性

```html
<div id="app3">
        {{reverseMessage}}
        {{dataFormat}}
</div>

var app3 = new Vue({
    el: '#app3',
    data:{
        message:'HelloComputedProperties',
    },
    computed:{
        reverseMessage:function(){
            return this.message.split('').reverse().join('');
        },
        dataFormat: function(){
            // alert('execute cuompute method')
            return  new Date()
        }
    }
})

setTimeout(() => {
    app3.message = 'hello'
}, 2000);
```
这时候我们发现修改message只会熏染与message相关的计算属性方法，而不会引起dataFormate方法调用及渲染。

[github代码](https://github.com/carvetime/study-vue/blob/master/03-ComputedProperties/index.html)