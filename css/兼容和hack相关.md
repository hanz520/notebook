# 兼容和hack相关

## 兼容

### 1.解决ie下的浮动，margin重叠等一些问题
```
zoom：1;
```
### 2.ie6双倍行距
```
display:inline  _ ie7 * ie6
```

## hack

### 1.clearfix
```
.clearfix:after{visibility:hidden;display:block;font-size:0;content: " ";clear:both;height:0;}
.clearfix{zoom:1;}    // 兼容ie
```

### 2.文本溢出  [外链](https://www.html.cn/archives/5206)
- 单行溢出
```
overflow: hidden;
text-overflow: ellipsis;
white-space: nowrap;
```
- 多行溢出
```
overflow : hidden;
text-overflow: ellipsis;
display: -webkit-box;
-webkit-line-clamp: 2;
-webkit-box-orient: vertical;
```

### 3.去除select初始样式
```
-webkit-appearance:none;
appearance:none;
border:none;
font-size:12px;
padding:0px 5px;
display:block;
width:100%;
-webkit-box-sizing:border-box;
box-sizing:border-box;
background-color: #FFFFFF;
color:#555;
border-radius:4px
```