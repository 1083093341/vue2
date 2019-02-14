#### 1.v-text

 用来控制显示文本内容：

```html
<p v-text="msg"></p>
```
和以下效果一样：

```html
<p>{{msg}}</p>
```

<!-- 默认 v-text 是没有闪烁问题的 -->
<!-- v-text会覆盖元素中原本的内容，但是插值表达式只会替换自己的这个占位符，不会把整个元素的内容清空 -->

#### 2.v-html

 插入HTML 和js的innerHTML一样，v-html会将其当html标签解析后输出：

```html
<div id="app">
    <p v-html="html"></p>
</div>
<script>
    let app = new Vue({
        el: "#app",
        data: {
            html: "<h1>我是H1</h1>"
        }
    });
</script>
```

#### 3.v-if   v-else  v-else-if

一看就知道这是vue中的 if条件表达式

v-if是根据表达式的真假来渲染元素的

如果属性值isGirl为true，就显示

```html
<p v-if="isGirl">女装大佬</p>
```

v-else 搭配v-if使用

```html
<p v-if="isGirl">女装大佬</p>
<p v-else>非女装大佬</p>
```

#### 4.v-show

v-show也是根据表达式的真假来渲染元素

```html
<p v-show="isGirl">女装大佬</p>
```

v-if 和 v-show的区别：

1.v-if 的特点：每次都会重新删除或创建元素  
2.v-show 的特点： 每次不会重新进行DOM的删除和创建操作，只是切换了元素的 display:none 样式 
3.如果元素涉及到频繁的切换，最好不要使用 v-if, 而是推荐使用 v-show
4.如果元素可能永远也不会被显示出来被用户看到，则推荐使用 v-if 

#### 5.v-for

1. v-for循环普通数组：

```html
<div id="app">
    <p v-for="(item, i) in list">索引值：{{i}} --- 每一项：{{item}}</p>
</div>
<script>
    var vm = new Vue({
      el: '#app',
      data: {
        list: [1, 2]
      },
      methods: {}
    });
</script>
```

**界面效果：**

**索引值：0 --- 每一项：1**

**索引值：1 --- 每一项：2**

2. v-for循环对象数组：

```html
<div id="app">
 <p v-for="(user, i) in list">Id：{{user.id}} --- 名字{{user.name}} --- 索引：{{i}}</p>
</div>
  <script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        list: [
          { id: 1, name: 'zs1' },
          { id: 2, name: 'zs2' },
          { id: 3, name: 'zs3' },
          { id: 4, name: 'zs4' }
        ]
      },
      methods: {}
    });
  </script>
```

3. v-for循环对象：

```html
<div id="app">
   <!-- 在遍历对象身上的键值对的时候， 除了 有  val  key  ,在第三个位置还有 一个 索引  -->
   <p v-for="(val, key, i) in user">值是： {{ val }} --- 键是： {{key}} -- 索引： {{i}}</p></div>
<script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        user: {
          id: 1,
          name: '大佬',
          gender: '男'
        }
      },
      methods: {}
    });
</script>
```

4. v-for循环数字:

```html
<div id="app">
  <!-- in 后面我们放过  普通数组，对象数组，对象， 还可以放数字 -->
  <!-- 注意：如果使用 v-for 迭代数字的话，前面的 count 值从 1 开始 -->
  <p v-for="count in 10">这是第 {{ count }} 次循环</p>
</div>
```

5. v-for 中的key关键字:

```html
<!-- 注意： v-for 循环的时候，key 属性只能使用 number或者string，最好使用唯一的ID值 -->
<!-- 注意： key 在使用的时候，必须使用 v-bind 属性绑定的形式，指定 key 的值 -->
<!-- 在组件中，使用v-for循环的时候，或者在一些特殊情况中，如果 v-for 有问题，必须 在使用 v-for 的同时，指定 唯一的 字符串/数字 类型 :key 值 -->
<p v-for="item in list" :key="item.id">
  <input type="checkbox">{{item.id}} --- {{item.name}}
</p>
```

#### 6.v-bind

1. Vue提供的属性绑定机制 ,  常用于动态绑定class和style和href

```html
<!-- 完整语法 -->
<a v-bind:href="url"></a>
<!-- 缩写 只写一个 : -->
<a :href="url"></a>
```

2. 使用数组语法绑定 class:

```html
<!-- 第一种使用方式，直接传递一个数组，注意： 这里的 class 需要使用  v-bind 做数据绑定 -->
<h1 :class="['thin', 'italic']">这是一个很大很大的H1，大到你无法想象！！！</h1>

渲染结果为：
<h1 class="thin italic">这是一个很大很大的H1，大到你无法想象！！！</h1>
```
3. 在数组中使用三元表达式:

```html
<h1 :class="['thin', flag?'italic':'']">这是一个很大很大的H1</h1>
<script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        flag: true,
      },
      methods: {}
    });
</script>
```

4. 使用对象语法绑定 class

```html
<div id="app">
    <!--当activity为true div才添加activity-class-->
    <!--当Inactive为true div才添加Inactive-class-->
    <!--可以控制 active和Inactive的true false来进行类的切换 达到高亮和非高度状态-->
    <div :class="{'active-class':active, 'Inactive-class':Inactive}"></div>
</div>
<script>
    var app = new Vue({
        el: '#app',
        data: {
            active: true,  
            Inactive: false
        }
    })
</script>

渲染结果为：
<h1 class="active-class">这是一个很大很大的H1</h1>
```

5. 在数组中使用 对象来代替三元表达式，提高代码的可读性

```html
<h1 :class="['thin', 'italic', {'active':flag} ]">这是一个很大很大的H1</h1> 
```

6. v-bind 绑定style

```html
<div id="app">
    <!-- 对象就是无序键值对的集合 -->
    <!-- <h1 :style="styleObj1">这是一个h1</h1> -->
    <h1 :style="[ styleObj1, styleObj2 ]">这是一个h1</h1>
</div>
<script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        styleObj1: { color: 'red', 'font-weight': 200 },
        styleObj2: { 'font-style': 'italic' }
      },
      methods: {}
    });
</script>
```

#### 7.v-on

Vue提供的事件绑定机制 主要用来监听dom事件

```html
<!-- 完整语法 -->
<button v-on:click="btnClick"></button>
<!-- 缩写 只写一个 @ -->
<button @click="btnClick"></button>
```

1. 使用  .stop  阻止冒泡

```html
<div id="app">
   <div class="inner" @click="div1Handler">
   <input type="button" value="戳他" @click.stop="btnHandler">
</div> 
结果：点击按钮只会触发btnHandler方法
```

2. 使用 .prevent 阻止默认行为

```html
<a href="http://www.baidu.com" @click.prevent="linkClick">有问题，先去百度</a>
结果：会调用linkClick方法，但点击 a标签 不在进行跳转
```

3. 使用  .capture 实现捕获触发事件的机制。即元素自身触发的事件走自己的方法，然后才交由内部元素进行处理

```html
<div class="inner" @click.capture="div1Handler">
   <input type="button" value="戳他" @click="btnHandler">
</div>
点击按钮打印 这是触发了 inner div 的点击事件
            这是触发了 btn 按钮 的点击事件
```

4. 使用 .self 实现只有点击当前元素时候，才会触发事件处理函数

```html
<div class="inner" @click.self="div1Handler">
   <input type="button" value="戳他" @click.self="btnHandler">
</div>  
结果：点击div 只调用div1Handler
      点击input 只调用btnHandler
```

5. 使用.once值触发一次事件处理函数

```html
<input type="button" value="戳他" @click.once="btnHandler">
结果：方法只调用一次
```

6. .self 和.once区别

   .self 只会阻止自己身上冒泡行为的触发，并不会真正阻止 冒泡的行为 

```html
(1)点击按钮 只会打印：：这是触发了 btn 按钮 的点击事件
<div class="outer" @click="div2Handler">
   <div class="inner" @click="div1Handler">
      <input type="button" value="戳他" @click.stop="btnHandler">
  </div>
</div>

(2)打印：这是触发了 btn 按钮 的点击事件
        这是触发了 outer div 的点击事件
<div class="outer" @click="div2Handler">
 <div class="inner" @click.self="div1Handler">
    <input type="button" value="戳他" @click="btnHandler">
 </div>
</div>
</div>
<script>
  // 创建 Vue 实例，得到 ViewModel
  var vm = new Vue({
   el: '#app',
   data: {},
    methods: {
      div1Handler() {
        console.log('这是触发了 inner div 的点击事件')
      },
      btnHandler() {
         console.log('这是触发了 btn 按钮 的点击事件')
      },
      linkClick() {
        console.log('触发了连接的点击事件')
      },
      div2Handler() {
        console.log('这是触发了 outer div 的点击事件')
      }
     }
  });
</script>
```

7. vue事件修饰符的v-on:click.prevent.self与v-on:click.self.prevent区别：

   请看：https://blog.csdn.net/qq_39105508/article/details/83008604

#### 8.v-model

v-bind 只能实现数据的单向绑定，从 M 自动绑定到 V， 无法实现数据的双向绑定

使用  v-model 指令，可以实现 表单元素和 Model 中数据的双向数据绑定

注意： v-model 只能运用在 表单元素中

```html
<div id="app">
    <h4>{{ msg }}</h4>
    <input type="text" style="width:100%;" v-model="msg">
</div>
<script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        msg: '我是msg'
      },
      methods: {
      }
    });
</script>
<!--这样 界面上值的也会影响到内存数据，内存数据改变也会体现在界面上-->
```

**v-model修饰符**

```html
<!-- 先转变为在change事件再同步输入框的值和数 -->
<input v-model.lazy="message">
<!-- 将输入值转化为数值类型-->
<input v-model.number="message">
<!-- 去除两端空格-->
<input v-model.trim="message">
```

#### 9.v-pre

v-pre主要用来此元素和它的子元素编译过程, 加快编译速度

```html
<div id="app">
    <p v-pre>{{message}}</p>  <!--//这条语句不进行编译-->
    <p>{{message}}</p>
</div>
```

#### 10.v-once

v-once 的作用就是 当前元素和子元素，只会被渲染一次，后面即使对内存数据进行了更改，也不会更改界面效果（不会进行二次渲染）

```html
<span v-once> {{message}} </span>
```



