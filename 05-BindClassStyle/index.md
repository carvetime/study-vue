
vue提供了各种样式绑定方式，可以根据不同是使用场景来选中使用,在此我们先引入vue并声明几个样式方便后面测试效果
```html
<head>
    <script src="https://cdn.jsdelivr.net/npm/vue"></script>
    <style type="text/css">
        .active{
            background-color: red;
        }
        .maxSize{
            font-size: 50px;
        }
        .center{
            text-align: center;
        }
        div{
            margin-bottom: 10px;
        }
    </style>
</head>
```
<!-- more -->

## 对象语法

我们先看下普通的对象样式绑定，可以通过对象的属性来切换样式的有无，同时还可以和正常的样式一起并存。

```html
<div id="app" v-bind:class="{active: isActive}">
    style1
</div>

<div id="app2" class="center" v-bind:class="{active: isActive, 'maxSize': isMax}">
        style2
</div>

<div id="app3" v-bind:class="classObject">
        style3
</div>

<script>
    var app = new Vue({
        el: '#app',
        data:{
            isActive: true
        }
    })

    var app2 = new Vue({
            el: '#app2',
            data:{
                isActive: true,
                isMax: true
            }
    })

    var app3 = new Vue({
            el: '#app3',
            data:{
                classObject:{
                    active:true,
                    'maxSize': true
                }
            }
    })
</script>
```

然后我们再看看对象语法中使用计算属性来切换属性的例子
```html
<div id="app4" v-bind:class="classObject">
        style4
</div>
<script>
var app4 = new Vue({
    el: '#app4',
    data:{
        num1:1,
        num2:1,
    },
    computed:{
        classObject: function(){
            return {
                active: this.num1 > 10,
                maxSize: this.num2 > 10
            }
        }
    }
})

setTimeout(() => {
    app4.num1 = 11
}, 1000);

setTimeout(() => {
    app4.num2 = 11
}, 2000);
</script>
```

## 数组语法

数组语法可以直接绑定一个class列表同时还可以使用三元表达式
```html
<div id="app5" v-bind:class="[active,maxSize]">
        style5
</div>

<div id="app6" v-bind:class="[flag == 2 ? active : '' ]">
        style6
</div>
<script>
var app5 = new Vue({
    el: '#app5',
    data:{
        active:'active',
        maxSize:'maxSize'
    }
})

var app6 = new Vue({
    el: '#app6',
    data:{
        flag: 2,
        active:'active'
    }
}) 
</script>
```

[github代码](https://github.com/carvetime/study-vue/blob/master/05-BindClassStyle/index.html)