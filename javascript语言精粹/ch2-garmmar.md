## 对象
javascript数据类型包括数字，字符串，布尔值，undefinded,null。其它所有数据类型均是对象。数字，布尔值，字符串,"像是"对象，因为他们都有方法，但是他们是不可变的，对象类型包括有正则表达式，函数，当然对象也是对象
javascript包含一种原型链的特性，允许对象继承另一个对象的属性，正确使用它能减少对象初始化的时间和内存，对象通过引用传递，他们永远不会被复制


## 引用
对象通过引用传递，永远不会被复制
```js
var x = stooge;
x.name = 'Curly';
var nick = stooge.nickname; //Curly
//因为stooge，x都是指向同一个对象的引用，所以nick为Curly

var a = {}, b = {}, c = {};
//a,b,c都引用一个不同的空对象
var a = b = c = {};



```

## 原型
每个对象都可以连接到一个原型对象，并且可以从中继承属性，所有通过字面量创建的对象都会连接到`Object.prototype`,它是javascript标配对象，当你创建对象时你可以选择任意一个对象作为它的原型

使用原型简化对象的创建
```js
if(Object.beget !== 'function'){
  Object.create = function(o){
    var f = function(0){};
    f.prototype = o;
    return new F
  }
}
var other_stoogge = Object.create(stooge);
```

原型在更新时是不起作用的，也就是说在更新对象的属性时不会影响到原型

```js
other_stoogge.name = 'Curly'; //在对象上添加的属性在原型上是找不到的
```

原型链在检索值的时候才会用到，如果我们尝试获取某个对象的属性，但该对象没有该属性，那么javascript就会从原型连中查找，如果在原型上也没有找到，那么在从其它的原型连上查找，一次类推，直到该过程最后到达终点`Object.prototype`，如果想要的属性没有被找到，那么结果就是undefinded。这个过程称为`委托`

原型是动态的，如果我们添加属性到该原型上，那么该属性对想继承该原型对象可见
## 反射
使用typeof可以检查对象属性的类型，hasOwnProperty方法可以检查属性是否是该对象独有的
## 枚举
for-in语句可与遍历对象的属性名，该过程将会列出所有属性，包括函数和原型中你不关心的属性，所以有必要过滤掉一些值

## 删除
delete运算符可以用来删除对象的属性，如果该对象包含该属性，那么属性就会被移除，他不会触及原型连中的任何对象，删除对象上的属性后会是使原型链的属性显现出来

```js
stooge.nickname; //Moe
delete stooge.nickname;
stooge.nickname //Clury
```
## 全局变量

javascript可以随意的定义全局变量，全局变量会是程序灵活性降低，因该尽量避免使用全局变量，最小化使用全局变量的方式之一是只创建一个全局变量
```js
var MYAPP = {};
```

