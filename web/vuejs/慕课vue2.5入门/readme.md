## 慕课网vue2.5入门

网址：https://www.imooc.com/learn/980

- 挂载点(与vue绑定的节点)、模板（节点下的内容）、实例（template） 
- 数据展示、事件绑定、方法定义
  ```
  <div id="root">
            <div v-text="msg"></div>
            <div v-html="msg"></div>
            <div v-on:click="handleClick">{{content}}</div>//插值表达式{{val}}
            <div @click="handleClick">{{content}}</div>//v-on: 简写 @
    </div>
    <script>
        new Vue({
            el: "#root",
            data: {
                msg: "<h1>hello</h1>",
                number: 123,
                content: "hello"
            },
            methods: {
                handleClick: function(){
                    this.content = "world";
                }
            }
        })
    </script>
  ```

- 属性绑定和双向数据绑定
  
```
<div id="root">
        <!-- 属性绑定 v-bind: 缩写 ： -->
        <div v-bind:title="'dell lee '+title">hello world</div>
        <div :title="'dell lee '+title">hello world</div>
        <!-- 双向数据绑定 -->
        <input type="text" :value="content">
        <input type="text" v-model="content">
        <div>{{content}}</div>
    </div>
    <script>
        new Vue({
            el: "#root",
            data: {
                title: "this is hello world",
                content: "this is content"
            }
        })
    </script>
```

- 计算属性与侦听器

```
<div id="root">
        <!-- 计算属性 -->
        firstName:<input type="text" v-model="firstName">
        lastName:<input type="text" v-model="lastName">
        <div>{{fullName}}</div>
        <!-- 侦听器 -->
        <div>{{count}}</div>
    </div>
    <script>
        new Vue({
            el: "#root",
            data: {
                firstName: '',
                lastName: '',
                count: 0
            },
            computed: {//computed - 一个属性由其它属性计算而来，依赖数据发生变化才会计算，不然读取缓存值
                fullName: function(){
                    return this.firstName+" "+this.lastName;
                }
            },
            watch: {//侦听器 里面的数据一旦发生变化，执行函数
                // firstName: function(){
                //     this.count++
                // },
                // lastName: function(){
                //     this.count++
                // }
                fullName: function(){
                    this.count++
                }
            }
        })
    </script>
```

- v-if,v-show,v-for 指令

```
<div id="root">
        <!-- DOM存在与否 v-if 为true时，div存在,false时 div节点去除  删除节点 DOM中移除-->
        <div v-if="show">hello world</div>
        <button @click="handleClick">toggle</button>
        <!-- DOM显示与否 v-show 为true时，div显示,false时 div节点不显示 display设为none 隐藏   使用频率大时用show，不更改DOM，性能好-->
        <div v-show="show">hello show</div>
        <!-- 循环显示DOM v-for -->
        <ul>
            <li v-for="item of list" :key="item">{{item}}</li>
            <!-- key属性提高每一项渲染的效率，key值每一项不能相同，如果数组为[1,1,2] 就不行了 可以用下面这个 -->
        </ul>
        <ul>
            <li v-for="(item,index) of list" :key="index">{{item}}</li>
            <!-- 每项值放入item，索引放入index  利用索引值作key值，在不对数组排序等操作时没问题，如进行进阶操作，最好不使用，基础课程暂不解释-->
        </ul>
    </div>
    <script>
        new Vue({
            el: "#root",
            data: {
                show: true,
                list: [1,2,3]
            },
            methods: {
                handleClick: function(){
                    this.show = !this.show
                }
            }
        })
    </script>
```

- 每一个组件都是一个vue实例
- 父组件通过属性的方式向子组件传递值
- 子组件和父组件通过发布订阅的方式建立通信

#### vue-cli

- 新建项目爬坑指南见4.1文件夹readme
- 项目文件夹
    - build：项目的webpack配置文件-不动
    - config：针对开发环境和线上环境的配置文件
    - node_modules：项目依赖
    - src：源代码放置目录 编写代码处
        - main.js项目入口文件
    - static：静态资源
    - index.html：网页最外层html文件 里面有挂载点
- .vue文件-一个完整组件
- .vue组件中data是一个函数
- 组件里的单行注释用// 内容  (注意//和内容之间有空格)
- 子组件中&lt;script&gt;标签中的scoped属性会限制样式作用的作用域，如果没有这个属性，样式会影响父组件
- 注意空格，多余的空格会报警告