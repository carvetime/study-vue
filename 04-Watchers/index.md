
之前我们尝试过计算属性，现在我们也可以使用监听属性来达到同样的效果
```html
<div id="app">
        <div>{{sum}}</div>
</div>
<script>
var app = new Vue({
    el:'#app',
    data:{
        valueA:1,
        valueB:2,
        sum: 3
    },
    watch:{
        valueA: function(val){
            this.sum = val + this.valueB
        },
        valueB: function(val){
            this.sum = val + this.valueA;
        }
    }
})
setTimeout(() => {
    app.valueA = 2
}, 1000);
</script>
```
一般简单的计算场景适合使用计算属性，复杂的场景比如存在某些异步处理的情况适合使用监听处理
```html
<head>
    <script src="https://cdn.jsdelivr.net/npm/vue"></script> 
    <script src="https://cdn.jsdelivr.net/npm/lodash@4.13.1/lodash.min.js"></script>
</head>

<div id="app2">
        <input v-model:value="search" />
        <span>answer:{{answer}}</span>
</div>
<script>
    var app2 = new Vue({
            el:'#app2',
            data:{
                search:'',
                answer:''
            },
            created: function(){
                this.debouncedGetAnswer = _.debounce(this.getAnswer,500)
            },
            watch:{
                search: function(val){
                    this.debouncedGetAnswer();
                }
            },
            methods:{
                getAnswer: function(){
                    this.answer = 'loading ...'
                    setTimeout(() => {
                        this.answer = 'hello vue'
                    }, 1000);
                }
            }
        })
</script>
```
[github代码]()