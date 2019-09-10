
vue可以直接在html标签中嵌入if-else和for循环对于列表的渲染是非常方便

## 条件判断
```html
<div id="app" v-if="show">
    I am here
</div>

<div id="app2" v-if="1+1==2">
    You are right
</div>
<script>
        var app = new Vue({
            el: '#app',
            data:{
                show: true
            }
        })
</script>
```
<!-- more -->

## 数组及对象遍历

通过v-for语句可以直接遍历数组的元素和index以及对象的value和key
```html
<div id="app3">
    <ul>
        <li v-for="food in foods" >
                    {{food.name}} 
        </li>
        <li v-for="food of foods" >
                {{food.name}} 
        </li>
        <li v-for="(food,index) in foods" >
                {{index}} : {{food.name}} 
        </li>
        <li v-for="value in student" >
            {{value}}
        </li>
        <li v-for="(value,name) in student" >
                {{name}} : {{value}}
        </li>
        <li v-for="(value,name,index) in student" >
                {{index}} : {{name}}  {{value}}
        </li>
        </ul>
</div>

<script>

var app3 = new Vue({
    el: '#app3',
    data:{
        foods:[
            {name: 'potato',wareId:1},
            {name: 'tomato',wareId:2},
            {name: 'watermelon',wareId:3}
        ],
        student:{
            name: 'wendell',
            age: 1,
            score: 100,
        }
    }
})
</script>

```

## 数组列表修改
数组列表的元素的变动通过数组的push、shift、splice、sort、reverse等方法可以直接响应到列表视图上，但是针对某个元素直接替换不会生效需要调用Vue.set或$.set方法
```html
<div id="app4">
        <ul>
            <li v-for="food in foods" >
                        {{food.name}} 
            </li>
</div>
<div id="app5">
        <ul>
            <li v-for="food in foods" >
                        {{food.name}} 
            </li>
</div>
<script>
    var app4 = new Vue({
            el: '#app4',
            data:{
                foods:[
                    {name: 'potato',wareId:1},
                    {name: 'tomato',wareId:2},
                    {name: 'watermelon',wareId:3}
                ]
            }
        })
        setTimeout(() => {
        app4.foods.push({name:'pork',key:4})
        }, 1000);
        setTimeout(() => {
        app4.foods.shift()
        }, 2000);
        setTimeout(() => {
            app4.foods = [
                    {name: 'tomato',wareId:2}
                ]
        }, 3000);

        var app5 = new Vue({
            el: '#app5',
            data:{
                foods:[
                    {name: 'potato',wareId:1},
                    {name: 'tomato',wareId:2},
                    {name: 'watermelon',wareId:3}
                ]
            }
        })
        setTimeout(() => {
        app4.foods[0] = {name:'grape'}
        }, 1000);
        setTimeout(() => {
            Vue.set(app5.foods,1,{name:'peach'});
            app5.$set(app5.foods,2,{name:'grape'});
        }, 3000);
</script>
```


## 对象属性增减
同样对象的属性的增减也是需要调用Vue.set或$.set方法
```html
<div id="app6">
        <ul>
            <li v-for="(value,name) in person" >
                        {{name}}:{{value}} 
        </li>
</div>
<script>
    var app6 = new Vue({
            el: '#app6',
            data:{
                person:{job: 'student'}
            }
        })
        setTimeout(() => {
            app6.score = 100;
            app6.$set(app6.person,'name','Lily');
            Vue.set(app6.person,'age',18);
        }, 1000);

        setTimeout(() => {
            app6.score = 100;
            app6.person = Object.assign(app6.person,{sex:'women',height:'170'});
            app6.person = Object.assign({},app6.person,{hobby:'music', city:'shanghai'});
        }, 2000);
</script>
```

[github代码]()
