函数
---

### 函数

#### 函数定义

函数定义从`function`关键字开始，其后跟随的组成部分如下：
 - 函数名称标识符
 - 一对圆括号
 - 一对花括号

```
function printprops(o){
  for(var p in o){
    console.log(p+":"+o[p]+"\n");
  }
}

//表达式方式定义的函数
var square = function(x){return x * x;}
```
**表达式定义的函数，函数的名称是可选的**  

**嵌套函数**  
在javascript中，函数可以嵌套在其他函数里  

```
function hypothenuse(a,b){
  function square(x) {return x * x;}
  return Math.sqrt(square(a) + square(b));
}
```
嵌套函数可以访问嵌套它们的函数的参数和变量。  

#### 函数调用  
有4中方式来调用JavaScript中的函数  
  - 作为函数  
    作为普通的函数调用
  - 作为方法  
    一个方法就是保存在一个对象的属性中的函数  
    ```
    o.m = f;  //给对象o定义了一个m()的方法
    o.m()     //调用时
    ```

    对方法调用的参数和的返回值的处理，和普通函数调用完全一致，方法和函数调用的一个重要
    区别是：调用上下文，方法调用时 对象是调用上下文，函数调用时调用上下文是this  

    **关键字this**  
    this是一个关键字，不是变量 也不是属性名，不能给this赋值  
    和变量不同，this没有作用域的限制  
    如果嵌套函数作为方法调用，其this的值指向调用它的对象  
    如果作为函数调用时，其this值不是全局对象就是undefined  

    **很多人误以为调用嵌套函数时this会指向调用外层函数的上下文**  
    ```
    var o = {                     //对象o
      m:function(){               //对象中的方法m()
        var self = this;          //将this的值保存至一个变量self
        console.log(this === o);  //输出为true，this就是对象o
        f();                      //调用辅助函数f();

        function f(){             //定义一个嵌套函数
          console.log(this === o);//false，this的值是全局对象或undefined;
          console.log(self === o);//true,self指的就是对象o
        }
      }
    };

    o.m();                        //调用方法m();
    ```
  - 作为构造函数
  - 通过它们的call()和apply()方法间接调用  


#### 函数的实参和形参

* 可选形参  
  当调用函数的时候传入的实参比函数声明时制定的形参个数要少，剩下的形参都将为undefined值  
* 可变长的实参列表:实参对象


#### 函数的属性、方法和构造函数

函数是特殊的对象，也可以拥有属性和方法，和普通的对象一样。
* length属性  
  在函数体中，arguemnts.length表示传入函数的实参的个数，而函数本身的length则有着不同的
  含义。函数的length属性是只读属性，表示形参的个数，即函数定义时给出的参数的个数

* prototype属性
  每一个函数都包含一个protoytype属性，这个属性指向一个对象的引用，这个引用称为“原型对象”

* call()方法和apply()方法
  call()和apply()方法的第一个参数是调用函数的母对象，它是调用上下文，
