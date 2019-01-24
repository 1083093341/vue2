#### 1.v-text

 用来控制显示文本内容

```html
<p v-text="msg"></p>
```
和以下效果一样

```html
<p>{{msg}}</p>
```

<!-- 默认 v-text 是没有闪烁问题的 -->
<!-- v-text会覆盖元素中原本的内容，但是插值表达式只会替换自己的这个占位符，不会把整个元素的内容清空 -->

#### 2.v-html

 插入HTML 和js的innerHTML一样，v-html会将其当html标签解析后输出

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





