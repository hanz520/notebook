
### 1.js监听输入框值发生变化事件 普通浏览器支持input, ie支持propertychange
```
$("#amount").bind('input propertychange',function(){ 
  
});
```
### 2.js延迟对外部JS的调用
```
defer="defer"
```
### 3.uc禁用左右滑动页面
```
(function(){ 
  var control = navigator.control || {}; 
  if(control.gesture){ 
    control.gesture(false); 
  } 
})();
```
### 4.正则匹配css3样式
```
var str='transform:scale(1) translate(100px,200px)' 
var str2=str.match(/scale\([^\)]+\)/g)[0]; 
console.log(str2.match(/\-?[0-9]+\.?[0-9]*/g))
```
### 5.手机去除拨号
`format-detection`翻译成中文的意思是“格式检测”，顾名思义，它是用来检测html里的一些格式的，那关于`meta`的`format-detection`属性主要是有以下几个设置： 
```
meta name="format-detection" content="telephone=no" 
meta name="format-detection" content="email=no" 
meta name="format-detection" content="adress=no" 
/// 也可以连写：
meta name="format-detection" content="telephone=no,email=no,adress=no"
```

