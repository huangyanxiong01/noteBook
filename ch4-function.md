javascript设计得最出色的就是它的函数的实现，几乎接近完美


## 函数对象
javascript函数就是对象，它拥有一个连接到原型的隐藏链接。对象字面量产生的对象连接到`Object.prototype`，函数对象连接到`Function.protoptype`（该原型对象本身连接到`Object.prototype`），每个函数在创建时会附加两个属性：函数的上下文和实现函数行为的代码。


## 函数字面量
创建一个字面量的函数
```js
var add = function(a,b){
  return a+b;
}

```
add是函数名，可以被省略，省略的函数被成为匿名函数，`(a,b)`括号中的a,b称为参数，他们不普通的变量那被初始化为undefined，而是在该函数被调用时初始化为是实际提供的参数的值。函数字面量可以出现在任何允许表达式出现的地方，函数也可以定义在其它函数中，一个内部函数除了可以访问自己的参数和变量，同时他也能自由的访问把它嵌套其中的父函数中参数和变量，通过函数字面量创建的函数对象包含一个连接到外部上下文的连接，这被称为闭包(closure)。他是javascript强大表现力的来源


## 调用
调用函数会暂停当前函数的执行，传递控制权和参数给新函数，除了声明时定义的形式参数，每个函数还接收两个附加的参数：this和arguments，参数this在面向对象编程时非常重要，它的值取决于调用模式，在javascript中有函数四种调用模式

1.方法调用模式
当一个和函数被保存为对象的一个方法时，我们称它为一个方法，当一个方法被调用时，this被绑定到该对象上。如果调用的表达式包含一个提取属性的动作，那么就是被当作方法调用
```js
var obj = {
  add(a,b){
    return a+b;
  }
}
obj.add(1,2);
```
方法可以使用this访问自己的所属的对象，所以它能从对象中取值或者对对象进行修改，this到对象额绑定发发生在调用的时候，这个‘超级’延迟绑定，使得函数可以对this高度复用，通过this可以取得上下文的方法称为公共方法

2.函数调用模式
当一个函数不是对象的属性，那么它就是被作为一个函数调用
```js
var sum = add(1,2);
```
此模式调用函数时，this被绑定到全局对象。这是语言设计上的错误，倘若语言设计正确，那么当内部函数调用时，this应该指向外部函数的this变量，这个错误设计的后果就是方法不能利用内部函数来帮助他工作，因为内部函数被绑定了错误的值，解决这个问题，我们可以使用在函数外部声明一个变量并给它赋值为this，那么内部函数就可以通过变量访问到this，很多人都习惯将这个变量命名__this，that
```js
function c(){
  let that = this;
  function d(){
    console.info(this) //在浏览器中this指向的是window
    console.info(that) //可以访问到外部函数的this
  };
  d()
}

c.call({name:'test'}); 
```
3.构造器调用模式
javascript是一门基于原型继承的语言，这意味着对象可以直接从其它对象继承属性，该语言是无类的。如果在一个函数的前面带上new来调用，那么就会创建一个prototype连接到新对象上，new也会改变return的行为
```js
function Person(name){
  this.name = name;
}
Person.prototype.getName = function(){
   return this.name;
}

let curly =  new Person('curly');
curly.getName(); //curly
```
一个函数如果在创建时就希望和通过new关键字调用，那它被称为构造器函数。按照约定们被保存在以大写开头的变量里，如果没有通过new关键字调用构造函数，this就会指向window(在浏览器)，this的属性就会暴露全局中，污染全局环境
4.apply调用模式
因为javascript是一门函数式的面向对象编程语言，所以函数也拥有方法，apply方法在调用函数可以改变内部`this`上下文，并传递一个数组作为参数
```js
function showName(args){
  console.info('context',this.name)
  console.info('args',args);
}

test.showName({name:'yourName'},[1,2]);
``




