对于一些共用的模块功能，vue提供了组件方法予以复用

## 组件复用
```html
<div id="demo01">
    <counter></counter>
    <counter></counter>
</div>

<script>

Vue.component('counter',{
data:function(){
    return {
        count: 0
    }
},
template: '<button v-on:click="count++">click {{count}} times</button>'
})

var vue01 = new Vue({
el: '#demo01'
})
</script>
```

## 组件传参
组件可以传传单或多个参数，如果属性过多也可以传对象
```html
<div id="demo02">
        <news title='今日头条新闻' reporter='小明' content='小区野狗咬人'></news>
        <news title='昨日头条新闻' reporter='小王' content='这个夏天真热'></news>
</div>

<div id="demo03">
        <news2 v-bind:ndata="ndata" ></news2>
</div>

<script>
Vue.component('news',{
    props:['title','reporter','content'],
    template: `<div>
                <h1>标题:{{title}}</h1> <h3>{{reporter}}</h3> <p>{{content}}</p>
                </div>
                `
})

Vue.component('news2',{
    props:['ndata'],
    template:`<div>
                <h1>标题:{{ndata.title}}</h1> <h3>{{ndata.eporter}}</h3> <p>{{ndata.content}}</p>
                </div>
                `
})

var vue02 = new Vue({
    el: '#demo02'
})

var vue03 = new Vue({
    el: '#demo03',
    data:{
        ndata:{
            title:'今日头条新闻2',reporter:'小明2',content:'小区野狗咬人2'
        }
    }
})
</script>

```

## 组件的事件传递
有时候组件内部的触发某个方法时希望组件外部监听到，这时候需要在组件内部使用$emit方法，外部使用v-on方法监听
```html
<div id="demo04" :style="{ backgroundColor: color,fontSize: size + 'px' }">
        <news3 v-bind:ndata="ndata" v-on:change-color="color = $event" v-on:change-size="onChangeSize"></news3>
</div>
<script>
Vue.component('news3',{
props:['ndata'],
template:`<div>
            <h1>标题:{{ndata.title}}</h1> <h3>{{ndata.eporter}}</h3> <p>{{ndata.content}}</p>
            <button v-on:click="$emit('change-color','yellow')">点击改变组件外层的颜色</botton>
            <button v-on:click="$emit('change-size',5)">点击改变字体大小</botton>
            </div>
            `
})

var vue04 = new Vue({
    el: '#demo04',
    data:{
        ndata:{
            title:'今日头条新闻3',reporter:'小明3',content:'小区野狗咬人3'
        },
        color: '#bdbdbd',
        size: 30
    },
    methods:{
        onChangeSize:function(fontSize){
            this.size += fontSize;
        }
    }
})

</script>

```

## 组件双向绑定
双向绑定其实是同时input标签同时实现了v-bind:value方法和v-on:input方法，因此希望组件也支持v-model方法就需要在组件内部props申明value，同时使用$emit指令
```html
<div id="demo05">
    <input v-model="searchText">
    <input v-bind:value="searchText" v-on:input="searchText = $event.target.value">
    <my-input v-model="searchText"></my-input>
    <p>{{searchText}}</p>

</div>

<script>
Vue.component('my-input',{
props:['value'],
template:`<input
    v-bind:value="value"
    v-on:input="$emit('input', $event.target.value)"
>`
})

var vue05 = new Vue({
    el: '#demo05',
    data:{
        searchText:'hello'
    }
})
</script>
```

## 组件插槽
组件嵌套插入标签是会报错的，需要在组件内部设置一个slot标签，这时候在组件内嵌套一个标签就会内嵌至插槽的位置
```html
<div id="demo06">
    <my-user name='小明' age='18'>
        <p>性别：男<p>
    </my-user>
</div>

<script>
Vue.component('my-user',{
    props:['name','age'],
    template:`
        <div>
            <p>用户名:{{name}}</p>
            <p>年龄:{{age}}</p>
            <slot></slot>
        </div>
    `
})

var vue06 = new Vue({
el: '#demo06'
}) 
</script>
```

## 动态组件
```html
<div id="demo07">
    <button v-on:click="switchComponent(1)">切换到动态组件1</button>
    <button v-on:click="switchComponent(2)">切换到动态组件2</button>
    <button v-on:click="switchComponent(3)">切换到动态组件3</button>
    <component v-bind:is="currentComponent"></component>
</div>

<script>
Vue.component('dynamic-component1',{
    template:'<h1>动态组件组件1</h1>'
})

Vue.component('dynamic-component2',{
    template:'<h1>动态组件组件2</h1>'
})

Vue.component('dynamic-component3',{
    template:'<h1>动态组件组件3</h1>'
})

var vue07 = new Vue({
    el: '#demo07',
    data:{
        currentComponent:'dynamic-component1'
    },
    methods:{
        switchComponent:function(index){
            this.currentComponent = 'dynamic-component' + index
        }
    }
})
</script>
```

[github代码](https://github.com/carvetime/study-vue/blob/master/08-Component/index.html)