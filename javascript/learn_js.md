对象
---

### 创建对象

* 对象直接量

  ```
  var empty = {};
  var point = {x:0,y:9};
  var book = {
    "main title":"Kevin woo", //属性名有空格，必须用引号
    "sub-title":"JS",         //属性名有连接符，必须用引号
    "for":"programming",      //属性名是保留字，必须用引号
    authors:{                 //属性值也可以是一个对象
      firstname:"Kevin",
      secName:"woo"
    }
  };
  ```

    在ES5中保留字做属性名，可以不加引号，ES3中必须要添加，ES5中，对象直接量的最后一个属
    性的逗号可以忽略，ES3中大部分实现也可以忽略，但在IE中会报错。

* 通过`new`创建对象

    ```
    var o = new Object();
    var a = new Array();
    var d = new Date();
    var r = new RexExp("js");
    ```

* 通过原型

* 通过 `Object.create()`

  ```
  var o1 = Object.create({x:1,y:2});            //o1继承了属性x和y
  var o2 = Object.create(null);                 //o2不继承任何属性和方法
  var o3 = Object.create(Object.prototype);     //o3和{}和new Object()
  ```

    ES5中定义了一个`create()`方法，它可以创建一个新对象，其中第一个参数是这个对象的原型。
    第二个参数是对象的属性


### 继承

JS中的对象具有“自有属性(own property)”,也有一些属性是从原型对象继承而来的
对象的原型属性构成了一个链，通过这个链可以实现属性的继承。
* 属性的赋值操作首先检查原型链，以此判断是否允许赋值操作。如果允许属性赋值操作，也总是在
原始对象上创建属性或赋值，而不会修改原型链
* 属性访问错误  
  属性的访问并不总是返回或设置一个值，查询一个不存在的属性并不会报错，则访问属性时返回
  undefined。  
  如果对象不存在，那么试图查询这个不存在的对象的属性时就会报错

  ```
  book.subtitle                 //如果book对象没有subtitle属性时，返回 undefined;
  var len book.subtitle.length  //如果再访问length时，就会抛出异常
  ```
  避免访问出错的方法
  ```
  //一种冗余简单易懂的方法
  var len = undefined;
  if(book){
    if(book.subtitle) len = book.subtitle.length;
  }

  //一种简单常用的方法
  var len = book && book.subtitle && book.subtitle.length;
  ```
  有一些属性是只读的，不能重新赋值

* 删除属性
  `delete`运算符可以删除对象的属性，`delete`只是断开属性和宿主对象的联系，而不会去操作属性中
  的属性
  ```
  var a = {p:{x:1}};b = a.p;delete a.p; b.x的值依然是1;
  ```
  `delete`运算符只能删除自有属性，不能删除继承属性(要删除继承属性必须从定义这个属性的原型
    对象上删除它，而且这会影响所有继承自这个原型的对象)

* 检测属性
  检测集合中成员的所属关系--判断某个属性是否存在于某个对象中，可以通过`in`运算符，
  `hasOwnProperty()`和`propertyIsEnumerable()`方法来完成
  ```
  var o = {x:1};
  "x" in o;           //true,"x"是o的属性
  "y" in o;           //false,"y"不是o的属性
  "toString" in o;    //true,o继承toString的属性
  ```
  `in`运算符，如果对象的自有属性或继承属性中包含这个属性则返回true;

  对象的`hasOwnProperty()`方法用来检测给定的名字是否是对象的 **自有属性**，对于继承属性
  会返回false;
  ```
  var o = {x:1};
  o.hasOwnProperty("x");            //true; o有一个自有属性x
  o.hasOwnProperty("y");            //false;o中不存在属性y
  o.hasOwnProperty("toString")      //false;toString是继承属性
  ```

  还可以使用 `!==`判断一个属性是否是undefined;
  ```
  var o = {x:1};
  o.x !== undefined;          //true;
  o.y !== undefined;          //false;
  o.toString !== undefined;   //true,o继承toString属性
  ```
