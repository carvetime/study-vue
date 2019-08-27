
vue和react小程序的模板语法基本都差不多，下面来简单写几个模板语法的demo

## 数据绑定

通过声明data每次修改data里面的值，视图层都会跟着渲染。
```html
<div id="app">
        <span>message: {{message}}</span>
</div>

var app = new Vue({
    el: '#app',
    data:{
        message: 'hello'
    }
})
```

通过声明添加v-once后，视图只会渲染一次，以后data变化都不会改变视图
```html
<div id="app2">
        <span v-once>message: {{message}}</span>
</div>

var app2 = new Vue({
    el: '#app2',
    data:{
        message: ''
    }
})

setTimeout(() => {
    app2.message = 'hi' // 这时候修改视图层不会响应
}, 1000);
```

<!-- more -->

有时候需要直接渲染html标签，那么可以使用v-html，但是使用需谨慎，渲染不安全的html字符串容易导致XSS攻击。
```html
<div id="app3">
        <span v-html="headHtml"></span>
</div>

var app3 = new Vue({
    el: '#app3',
    data:{
        headHtml:'<h1>h1 title</h1>'
    }
})
```

有时候我们需要对html标签的某些属性进行直接绑定，这时候可以使用v-bind指令
```html
<div id="app4">
    <span v-bind:id="dynamicId">dynamic id</span>
    <span v-bind:style="dynamicStyle">dynamic style</span>
    <button v-bind:disabled="btnDisable">disable button</button>
</div>

var app4 = new Vue({
    el: '#app4',
    data:{
        dynamicId:1,
        dynamicStyle:'background-color: green',
        btnDisable: true
    }
})
```
## 表达式

使用双括号可以使用javascript的表达式，但是只能用单个表达式。
```html
<div id="app5">
    {{number + 1}}
    {{number == 1 ? 'true' : 'false'}}
    {{message.slice(5)}}
</div>

var app5 = new Vue({
    el: '#app5',
    data:{
        number:1,
        message: 'hellovue'
    }
})
```

## 指令

使用v-on指令可以为标签添加点击方法
```html
<div id="app6">
    <div v-on:click="onClick" style="background-color: yellow; display: inline-block">click me</div>
</div>

var app6 = new Vue({
    el: "#app6",
    methods:{
        onClick:function(){
            alert('click event');
        }
    }
})
```

使用v-bind:[]指令可以动态的修改绑定的属性名
```html
<div id="app7">
    // 注意这里attributeName会被转成小写attributename
    <input type="text" v-bind:[attributeName]="123" />
</div>

var app7 = new Vue({
    el: "#app7",
    data:{
        attributename:'value'
    }
})

```
指令还可以加修饰符，比如添加一个.prevent修饰符可以阻止原来标签的动作
```html
<div id="app8">
    <a href="http:www.baidu.com" v-on:click="click1" >universally click </a>
    <a href="http:www.baidu.com" v-on:click.prevent="click2" > prevent click </a>
</div>

var app8 = new Vue({
    el: "#app8",
    methods:{
        click1:function(){
            alert("jump to website");
        },
        click2:function(){
            alert("use prevent don't jump to website");
        }
    }
})
```

为了简洁方便指令还可以使用@和:的简写方式来表示
```html
<div id="app9">
    <div @click="onClick" style="background-color: yellow; display: inline-block">shorthand of v-on</div>
    <input type="text"  :value="message" />
</div>

var app9 = new Vue({
    el: "#app9",
    data:{
        message:'shorthand of v-bind:'
    },
    methods:{
        onClick:function(){
            alert("shorthand");
        }
    }
})

```

[github代码](https://github.com/carvetime/study-vue/blob/master/02-TemplateSyntax/TemplateSyntax.html)


