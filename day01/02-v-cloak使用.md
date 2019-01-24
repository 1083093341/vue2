#### v-cloak使用

使用v-cloak 能够解决 插值表达式闪烁的问题：

比如你在界面上使用了如下表达式
```html 
<!-- 插值表达式：只是替换自己的这个占位符-->
<p> {{msg}} </p>
```

又在Vue的data中写了

```javascript
var vm = new Vue({
      el: '#app',
      data: {
        msg: '123'
      }
    })
```

可能在界面加载的时候会先到{{msg}},再看到123。这就是插值表达式闪烁的问题

解决方法： 

```css
/*在style中加入*/
<style>
 [v-cloak] {
    display: none; 
 }
 /*
  [v-cloak] {
     display: none!important; 
   }
  */
</style>

/*在标签上加上*/
<p v-cloak> {{msg}} </p> 
```

完整栗子：

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    [v-cloak] {
        display: none; 
    }
  </style>
</head>
<body>
  <div id="app">
    <p v-cloak>{{ msg }}  </p>
  </div>
  <script src="../lib/vue-2.4.0.js"></script>
  <script>
    var vm = new Vue({
      el: '#app',
      data: {
        msg: '123'
      }
    })
  </script>
</body>
</html>
```