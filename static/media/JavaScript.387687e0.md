## 3. JavaScript

### 3.1 JS基础知识部分

#### 3.1.1 原始数据类型？null是对象吗？原始数据类型和复杂数据类型的存储区别？

1. JS中的数据类型分为原始值和引用值：

- 原始值有6种：Number、String、Boolean、Undefined、Null、Symbol(ES6新增)

- 引用值有：Array、Object、Function、Date、RegExp

2. typeof null返回的是object，但null不是对象，是基本数据类型的一种

3. 原始数据类型和复杂数据类型的存储区别：

- 原始数据存储在栈内存，存储的是值

- 复杂数据类型的地址存储在栈内存，然后地址指向存储在堆内存的值。当我们将对象赋值给另外一个变量的时候，复制的是地址，指向同一个内存空间，其中一个内存改变的时候，另一个对象也会变化。

#### 3.1.2 typeof 和 instanceof

1. typeof返回基本数据类型：number、string、boolean、undefined、function、object（泛在的引用值，array/null/object返回的都是object）

2. instanceof的用法：

```javascript
A instanceof B
```
可以用来判断复杂的数据类型，但是不能用来判断基本数据类型。

其实现原理为：通过原型链来判断。 A instanceof B 则在A和B的原型链上查找，如到原型链的顶端都没有，则返回false

#### 3.1.3 for of, for in 和 forEach, map 的区别

- [遍历器Iterator](http://es6.ruanyifeng.com/#docs/iterator)——ES6文档的Iteration部分

1. for...of循环：具有iterator（遍历器）接口，可以用for...of循环遍历成员。for...of循环可使用的范围包括数组、Set和Map结构、某些类数组的结构、Generator对象及字符串。其调用遍历器接口。对普通对象，for...of不可直接使用，会报错。需要部署Iterator接口后才可用，可中断循环。

2. for...in循环：遍历对象自身和继承的可枚举属性，不能直接获取属性值，可以中断循环

3. forEach：只能遍历数组，不能中断，没有返回值（返回值为undefined）

4. map：只能遍历数组，不可中断，返回的值是修改后的数组

#### 3.1.4 判断变量是否为数组

1. **使用Object.prototype.toString.call()**判断返回[object Array]，则为数组

2. A instanceof Array, 如果返回的是true，则表示为数组

3. constructor，通过构造来判断，数组的constructor为Array，对象的constructor为Object

```javascript
arr.constructor === Array
```

4. arr.isArray, 如果返回的为true，则表示为数组

#### 3.1.5 类数组和数组的区别是什么？

1. 类数组：

- **类数组有length属性**，其他属性（索引）为非负整数（对象中的索引会被当作字符串来处理）

- 类数组不具有数组所具有的方法pop、push等

- **类数组是一个普通的对象，而真实的数组是Array类型**

- 常见的类数组有：函数的参数arguments，DOM对象列表（如通过document.querySelectorAll得到的列表），jQuery对象（比如$("div")）

2. 类数组转为数组的方式：

```javascript
// Way 1
Array.prototype.slice.call(arrayLike, start);
// Way 2
[...arrayLike];
// Way 3
Array.from(arrayLike)
```
**注：Array.from方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象。**

#### 3.1.6 ==和=\==有什么区别

1. ===不需要进行类型的转换，只有类型相同且值相等时，才返回true

2. ==如果两个类型不同，则需要进行类型转换。具体流程包括：

- 如果比较的是null和undefined，则直接返回true；

- 判断两者类型是否为string(boolean)和number，如是的话，则将字符串(boolean)转变为number

- 如其中一方为object，且另一方为string、number或symbol，如果是，将object转为原始类型再进行判断

```javascript
console.log([] == ![])
// true
```

#### 3.1.7 ES6中的class和ES5的类有什么区别？

- ES6 class 内部所有定义的方法都是不可枚举的

- ES6 class 必须使用new调用

- ES6 class 不存在变量提升

- ES6 class 默认即为严格模式

- ES6 class 子类必须在父类的构造函数中调用super(), 这样才有this对象；ES5中类继承的关系是相反的，先有子类的this，然后用父类的方法应用在this上

#### 3.1.8 数组的哪些API会改变原数组？

1. 修改原数组的API有：splice（插入数据）/

```javascript
splice(index, howMany, item1,..., itemX)
// index表示位置，howMany表示删除多少个，item1～itemX表示添加的新项目
```
push/pop/reverse/sort/shift（删除第一个值）/unshift（添加到数组的开头部分，可添加多个）/fill（固定值替换数组元素）/copyWithin（拷贝元素到另一元素位置）

2. 不修改原数组的API有：concat（连接字符串）/toString/join/split/slice（截取部分数组[a, b)）/map/forEach/every/filter/reduce/entry/entries/find

#### 3.1.9 let、const和var的区别

1. let和const定义的变量不出现变量提升，而var定义的变量会出现变量提升

2. let和const是JS的块级作用域；

3. let和const你不允许重复声明，且let和const定义的变量在声明之前使用会报错（出现暂时性死区），而var不会

4. const只声明一个只读变量。一旦声明，常量的值就不能够改变（如果声明的只是一个对象，那么不能改变的是对象的引用地址）

#### 3.1.10 call、apply有什么区别？call、apply和bind的内部如何实现？

1. call、apply的区别：call与apply的功能相同，其区别在于传参方式不同：

- fn.call(obj, arg1, arg2,...), 调用一个函数，具有一个指定的this值和分别提供的参数

- fn.apply(obj, [argsArray]), 调用一个函数，具有一个指定的this值，以及作为一个数组（或类数组对象）提供的参数

2. call核心：

- 将函数设为传入参数的属性

- 指定this到函数，并传入给定参数，执行函数

- 如果不传入参数，或参数为null，默认指向为window / global

- 删除参数上的函数

```javascript
Function.prototype.call = function (context) {
    /** 如果第一个参数传入的是 null 或者是 undefined, 那么指向 this 指向 window/global */
    /** 如果第一个参数传入的不是 null 或者是 undefined, 那么必须是一个对象 */
    if (!context) {
        //context 为 null 或者是 undefined
        context = typeof window === 'undefined' ? global : window;
    }
    context.fn = this; //this 指向的是当前的函数 (Function 的实例)
    let args = [...arguments].slice(1);// 获取除了 this 指向对象以外的参数, 空数组 slice 后返回的仍然是空数组
    let result = context.fn(...args); // 隐式绑定, 当前函数的 this 指向了 context.
    delete context.fn;
    return result;
}

// 测试代码
var foo = {
    name: 'Selina'
}
var name = 'Chirs';
function bar(job, age) {
    console.log(this.name);
    console.log(job, age);
}
bar.call(foo, 'programmer', 20);
// Selina programmer 20
bar.call(null, 'teacher', 25);
// 浏览器环境: Chirs teacher 25; node 环境: undefined teacher 25
```

3. apply实现与call类似，但需注意传参不同

4. bind实现原理

- bind和call/apply的重要区别：一个函数被call/apply的时候，会被直接调用，但是bind会创建一个新函数。

- 新函数被调用时，bind()的第一个参数将作为它运行时的this，之后的一序列参数将会在传递的实参前传入作为它的参数。

```javascript
Function.prototype.bind = function(context) {
    if(typeof this !== "function"){
        throw new TypeError("not a function");
    }
    let self = this;
    let args = [...arguments].slice(1);
    function Fn() {};
    Fn.prototype = this.prototype;
    let bound = function() {
        let res = [...args, ...arguments]; //bind 传递的参数和函数调用时传递的参数拼接
        context = this instanceof Fn ? this : context || this;
        return self.apply(context, res);
    }
    // 原型链
    bound.prototype = new Fn();
    return bound;
}

var name = 'Jack';
function person(age, job, gender){
    console.log(this.name , age, job, gender);
}
var Yve = {name : 'Yvette'};
let result = person.bind(Yve, 22, 'enginner')('female');
```

### 3.2 JS知识重难点部分

#### 3.2.1 在JS中什么是变量提升？什么是暂时性死区？

1. 变量提升就是变量在声明之前就可以使用，值为undefined

2. 暂时性死区

- 在代码块内使用let/const命令声明变量之前，该变量都是不可用的状态（会抛出错误），语法上称为“暂时性死区”

```javascript
typeof x;    // ReferenceError（暂时性死区）
let x;

typeof y;  // 值为undefined，不会抛出错误
```

- 暂时性死区的本质是，只要一进入当前的作用域，所要使用的变量就已经存在，但是不可获取，只有等声明变量那一行代码出现，才可以获取和使用变量

#### 3.2.2 如何正确判断this？箭头函数的this是什么？

[你真的了解this吗？](https://github.com/YvetteLau/Blog/issues/6)——this相关的详细知识点

1. this的绑定规则有四种：new绑定，显式绑定，隐式绑定，默认绑定

- **new绑定**，函数是否在new中调用（new绑定），如果是，那么this绑定的是新创建的对象

- **显式绑定**，函数是否通过call，apply调用，或者使用bind（硬绑定），如果是，this绑定的就是制定的对象

- **隐式绑定**，函数是否在上下文对象中调用（隐式绑定），如果是的话，this绑定的是那个上下文对象。一般是obj.foo();

- **默认绑定**，如不是以上的情况的话，则为默认绑定。在严格模式下，绑定到undefined，否则绑定到全局对象

- 如果把null或者undefined作为this绑定对象传入call、apply或bind中，这些值在调用时会被忽略，实际应用的是默认绑定规则。

2. 箭头函数没有自己的this，它的this继承于上一层代码块的this

#### 3.2.2 词法作用域和this的区别

- 词法作用域是由写代码时，将变量和块作用域写在哪里决定的

- this是在调用时被绑定的，this指向什么，完全取决于函数的调用位置

#### 3.2.3 JS执行上下文栈和作用域链

1. 执行上下文就是当前JavaScript代码被解析和执行所处的环境，JS执行上下文是一个存储函数调用的栈结构，遵循先进后出的原则

- JavaScript执行在单线程上，为了防止不同线程对同一个对象进行操作造成混乱。

- 浏览器在执行全局的代码时，首先创建全局的执行上下文，压入执行栈的顶部。

- 每当进入一个函数的执行就会创建函数的执行上下文，并且把它压入执行栈的顶部，当前函数执行完后，当前函数的执行上下文出栈，等待垃圾回收。

- 浏览器的JS执行引擎总是访问栈顶的执行上下文

- 全局的执行上下文只有一个，在浏览器关闭的时候出栈

2. 作用域链：无论LHS或RHS查询，都会在当前的作用域查找，如果没有找到，就顺着作用域链继续查找目标标识符，每次上升一个作用域，直到上升到全局作用域

#### 3.2.4 什么是闭包？闭包的作用？闭包额使用场景？

1. 闭包的概念

- 闭包是指在一个函数内部构建另外一个函数，并将内部的函数保存到外部时候，产生闭包。

- 闭包将导致原有的作用域链不释放，导致内存泄漏。

- 闭包指有权访问另一个函数作用域的变量的函数。

2. 闭包的作用：

- 封装私有变量，模块化开发。防止污染全局变量，如大型开发项目的命名规则

- 模仿块级作用域（ES5中没有块级作用域）

#### 3.2.5 new

1. new的创建流程

（1）创建一个新对象

（2）这个对象会被执行[[原型]]连接；

（3）将构造函数的作用域赋值给新对象，即this指向这个新对象；

（4）如果函数没有返回其他对象，那么new表达式中的函数调用会自动返回这个新对象

```javascript
function new(func) {
    let target = {};
    target.__proto__ = func.prototype;
    let res = func.call(target);
    if (typeof(res) == "object" || typeof(res) == "function") {
        return res;
    }
    return target;
}
```
字面量创建对象，不会调用Object构造函数，简洁且性能更好。

new Object()方式创建对象本质上是方法调用，涉及到在proto链中遍历该方法，当找到该方法后，又会生产方法调用必须的堆栈信息，方法调用结束后，还要释放该堆栈，性能不如字面量的方式。

通过对象字面量定义对象时，不会调用Object构造函数。

#### 3.2.6 原型的理解

- 在JS中，定义一个对象，都会有一些预定义的方法

- 同时，对于函数对象都有一个prototype属性，属性指向函数的原型对象。

- 原型对象的好处是所有对象实例共享它所包含的属性和方法

#### 3.2.7 原型链及其应用

1. 原型链主要解决继承的问题。

2. 每个对象拥有一个原型对象，通过proto指针指向其原型对象，并从中继承方法和属性，同时原型对象也可能拥有原型，一层一层最终指向null(Object.prototype.\_\_proto\_\_指向的null)。这种关系被称为原型链（prototype chain），通过原型链一个对象可以拥有定义在其他对象的属性和方法。

3. 构造函数Parent、Parent.prototype和实例p的关系如下：（p.\_\_proto\_\_ === Parent.prototype）

![3-1](https://ambitionc-blog.oss-cn-hongkong.aliyuncs.com/Blog_Notes/3JavaScript/3-1.png)

#### 3.2.8 prototype和\_\_proto\_\_的区别是什么？

1. prototype是构造函数的属性

2. \_\_proto\_\_是每个实例都有的属性，可以访问[[prototype]]属性

```javascript
function Student(name) {
    this.name = name;
}
Student.prototype.setAge = function(){
    this.age=20;
}
let Jack = new Student('jack');
console.log(Jack.__proto__);
//console.log(Object.getPrototypeOf(Jack));;
console.log(Student.prototype);
console.log(Jack.__proto__ === Student.prototype);  //true
```

#### 3.2.9 继承的方式

1. 传统形式，采用原型链，会导致继承无用的属性

（借助构造函数）

2. 共享原型：也就是一个原型给了多个函数但一个函数改变原型会影响另一个

3. 圣杯模式（组合继承）：通过中间层实现原型链的继承

```javascript
function SuperType() {
    this.name = name;
    this.colors = ['red', 'blue', 'green'];
}
SuperType.prototype.sayName = function() {
    console.log(this.name);
}

function SubType(name, age) {
    SuperType.call(this, name);
    this.age = age;
}
SubType.prototype = new SuperType();
SubType.prototype.constructor = SubType;

SubType.prototype.sayAge = function() {
    console.log(this.age);
}
```

#### 3.2.10 深拷贝？与浅拷贝的区别？

1. 浅拷贝只是复制第一层对象，但是当对象的属性是引用类型时，实质复制的是其引用，当引用指向的值改变时也会跟着变化。

2. 深拷贝复制变量值，对于非基本类型的变量，则递归至基本类型变量后，再复制。深拷贝后的对象与原来的对象完全隔离，互不影响。对一个对象的修改不会影响另外一个对象。