#### Vue的基本代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <!-- 1. 导入Vue的包 -->
  <script src="../lib/vue-2.4.0.js"></script>
</head>
<body>
  <!-- Vue是MVVM框架 -->
  <!-- Vue 实例所控制的这个元素区域，就是我们的 V  -->
  <div id="app">
    <p>{{ msg }}</p>
  </div>
  <script>
    // 2. 创建一个Vue的实例
    // 我们 new 出来的这个 vm 对象，就是我们 MVVM中的VM调度者
    var vm = new Vue({
      // el表示当前我们 new 的这个 Vue 实例，要控制页面上的哪个区域
      el: '#app', 
      //data 就是 MVVM中的 M，专门用来保存 每个页面的数据的
      // data 属性中，存放的是 el 中要用到的数据
      data: { 
        msg: 'Hello Vue'
      }
    })
  </script>
</body>
</html>
```

