
按照官网文档写了一点简单入门实例，以下为了方便我们直接使用script引入Vue
```html
<head>
    <script src="https://cdn.jsdelivr.net/npm/vue"></script>    
</head>
```

## 声明渲染
```js
<div id="app">
        {{ message }}
</div>
 <script>
        var app = new Vue({
            el: '#app',
            data: {
                message: 'Hello Vue!'
            }
        })
 </script>
```

##  属性绑定
```js
 <div id="app2">
        <span v-bind:title="message">
                鼠标悬停几秒钟查看此处动态绑定的提示信息！
        </span>
 </div>

  var app2 = new Vue({
            el: '#app2',
            data: {
                message: 'Hello Vue 2'
            }
})
```

## 条件语句
```js
<div id="app3">
        <p v-if="show">显示</p>
</div>

 var app3 = new Vue({
            el: '#app3',
            data: {
                show: false
            }
        })

setTimeout(() => {
    app3.show = true
}, 1000);

```

## 循环语句
```js
<div id="app4">
        <ol>
            <li v-for="item in list">
                {{ item }}
            </li>
        </ol>
</div>

 var app4 = new Vue({
            el: '#app4',
            data: {
                list: ["javascript","css","html","vue"]
            }
        })
```

## 点击事件
```js
<div id="app5">
        <p>{{number}}</p>
        <button v-on:click="increase">点击增加</button>
        <button v-on:click="reduce">点击减少</button>
</div>

var app5 = new Vue({
            el:'#app5',
            data:{
                number:1
            },
            methods:{
                increase: function(){
                    this.number += 1;
                },
                reduce: function(){
                    this.number -= 1;
                }
            }
        })
```

## 双向绑定
```js
<div id="app6">
        <p>{{message}}</p>
        <input type="text" v-model="message">
</div>

 var app6 = new Vue({
            el: '#app6',
            data: {
                message: 'Hello Vue!'
            }
        })
setTimeout(() => {
            app6.message = "Changed"
}, 2000);

```

## 自定义组件
```js
<div id="app7">
        <ol>
            <custom-item v-for="item in wareList" v-bind:data="item" v-bind:key="item.id">
            </custom-item>
        </ol>
</div>

Vue.component('custom-item',{
            props:['data'],
            template: '<li>{{data.text}}</li>'
        })

        var app7 = new Vue({
            el:'#app7',
            data:{
                wareList:[
                    {id:0,text:'vegetable'},
                    {id:1,text:'biscuit'}
                ]
            }
        })
```

以上是简单的入门示例，感觉和React及小程序的写法大同小异。

[github代码]()