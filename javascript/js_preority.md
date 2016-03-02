JavaScript的属性和方法
---

* 私有变量 - 在对象内部使用'var'关键字声明，而且它是能被私有函数和特权方法访问
* 私有方法 - 在对象的构造函数里声明(或通过var functionName = function(){}定义的)
* 特权方法 - 通过this.methodName = function(){}来声明
* 公有属性 - 通过this.variableName 来定义
* 公有方法 - 通过ClassName.prototype.methodName = function(){}来定义的
* 原型属性 - 通过ClassName.prototype.propertyName = someValue来定义的
* 静态属性 - 通过ClassName.propertyName = someValue 来定义的
* 静态方法 - 通过ClassName.functionName = function(){}来定义的


## 封装

* 用命名规范区别私有成员
  在方法和属性的名称前加上下划线以示其私用性


## 继承
* 类式继承

```
/*Class Person*/

function Person(name){
  this.name = name;
}

Person.prototype.getName = function(){
  return this.name;
}

var render = new Person('Kevin');
render.getName();
```

创建继承Person的类
```
/*Class Author*/
function Author(name,books){
  Person.call(this,name);         //调用Person的构造函数
  this.books = books;
}

Author.prototype = new Person();      //将Author的prototype设置为Person的一个实例
Author.prototype.constructor = Author;  //将prototype的constructor属性重新设置为Author
Author.prototype.getBooks = function(){
  return this.books;
}
```

extend函数

```
function extend(subClass,superClass){
  var F = function(){};
  F.prototype = superClass.prototype;
  subClass.prototype = new F();
  subClass.prototype.constructor = subClass;
}
```

改造后的Author

```
function Author(name,books){
  Person.call(this,name);
  this.books = book;
}
extend(Author,Person);

Author.prototype.getBooks = function(){
  return this.books;
}
```

进一步改造extend函数

```
function extend(subClass,superClass){
  var F = function(){};
  F.prototype = superClass.prototype;
  subClass.prototype = new F();
  subClass.prototype.constructor = subClass;

  subClass.superclass = superClass.prototype;
  if(superClass.prototype.constructor == Object.prototype.constructor){
    superClass.prototype.constructor = superClass;
  }
}
```

进一步改造之后的Author
```
function Author(name,books){

  Author.superclass.constructor.call(this,name);
  this.books = books;
}

extend(Author,Person);

Author.prototype.getBooks = function(){
  return this.books;
}
```

* 原型式继承

```
function clone(object){
  function F(){};
  F.prototype = object;
  return new F;
}
```
