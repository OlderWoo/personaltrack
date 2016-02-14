数组
---

### 创建数组

* 数组直接量
```
var empty = [];
var p = [1,2,3,4,5,7];
var m = [1.1,true,"a",]
```
数组中的直接量不一定是常量，可以是任意的表达式

* `Array`
```
var a = new Array();
var a = new Array(10);
var a = new Array(4,2,34,4,"test");
```

### 数组长度
每个数组都有一个`length`属性，代表数组中元素的个数

### 添加和删除

### 数组遍历
使用for循环遍历数组，
```
var keys = Object.keys(o);
var values = [];
for(var i = 0;i<keys.length;i++){
  var key = keys[i];
  values[i] = o[key];
}

//优化版
for(var i = 0,len = keys.length;i<len;i++){
  //循环体仍然不变
}

//排除null,undefined和不存在的元素
for(var i = 0;i<a.length;i++){
  if(!a[i]) continue;   //跳过null,undefined和不存在的元素
  //循环体
}

//只跳过undefined和不存在的元素
for(var i = 0;i<a.length;i++){
  if(a[i] === undefined) continue;  //跳过undefined+不存在的元素
  //循环体
}

//跳过不存在的元素
for(var i = 0;i<a.length;i++){
  if(!(i in a)) continue;       //跳过不存在的元素
  //循环体
}

for(var i in a){
  if(!a.hasOwnProperty(i)) continue;    //跳过继承的属性
}

```

### 数组方法

* `join`  
`Array.join()`方法将数组中所有元素都转化为字符串并连接在一起，返回最后生成的字符串
```
var a = [1,2,3]
a.join();                 // => "1,2,3"
a.join(" ");              // => "1 2 3"
a.join("");               // => "123"
var b = new Array(10);    
b.join("-");              // => "---------" 9个连字符
```

* `reverse`  
`Array.reverse()`方法将数组中的元素颠倒顺序，返回逆序的数组。
