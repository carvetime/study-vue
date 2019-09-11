
vue可以通过v-on或简写@指令来处理事件

## 事件处理

事件处理可以直接在运行javascript代码，调用javascript方法以及传参。
```html
<div id="demo01" >
        <p>{{counter}}</p>
        <button v-on:click="counter += 1">click me</button>
        <button v-on:click="add">click me</button>
        <button v-on:click="showHello('hello')">click me</button>
        <button v-on:click="showHi('hi',$event)">click me</button>
</div>
<script>
    var app = new Vue({
        el: '#demo01',
        data:{
            counter: 0
        },
        methods:{
            add:function(event){
                this.counter += 2;
            },
            showHello:function(message){
                alert(message);
            },
            showHi:function(message,event){
                alert(message+JSON.stringify(event));
            }
        }
    })
</script>
```

<!-- more -->

## 事件修饰符
vue同时为事件增加了一些修饰符stop、prevent、capture、once等，用来处理点击事件冒泡、多次点击等各种行为。
```html
<div id="demo02" v-on:click="click0">
        <button v-on:click.once="click1">click me</button>
        <button v-on:click.prevent="click2">click me</button>
</div>

<script>
var app = new Vue({
    el: '#demo02',
    methods:{
        click0:function(event){
            alert('parent click event');
        },
        click1:function(event){
            alert('alert once');
        },
        showHello:function(message){
            alert(message);
        },
        showHi:function(message,event){
            alert(message+JSON.stringify(event));
        }
    }

})
</script>
```