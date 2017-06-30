+ 写在前面
前一篇太乱了, 重新梳理一篇

# 大纲

# 目录
<!-- MDTOC maxdepth:6 firsth1:1 numbering:0 flatten:0 bullets:1 updateOnSave:1 -->

- [大纲](#大纲)
- [目录](#目录)
- [继承与原型链](#继承与原型链)
   - [`[[prototype]]` 与 `__proto__`](#prototype-与-__proto__)
   - [`[[prototype]]` 和 `prototype`](#prototype-和-prototype)
- [原型链与原型](#原型链与原型)
   - [原型链与闭包](#原型链与闭包)
   - [函数与原型](#函数与原型)
   - [原型链传播](#原型链传播)
   - [Object.prototype, Function.prototype 与原型链的结束](#objectprototype-functionprototype-与原型链的结束)
   - [继承的法理依据](#继承的法理依据)
      - [手工拼接原型链](#手工拼接原型链)
   - [Object 与原型](#object-与原型)
      - [ES 5 继承的实现](#es-5-继承的实现)
      - [Object.create()](#objectcreate)
      - [B.prototype.constructor = B](#bprototypeconstructor-b)
      - [After any case onceif you changed 'prototype'](#after-any-case-onceif-you-changed-prototype)
      - [B.call(this)](#bcallthis)
      - [混入继承](#混入继承)
      - [Object.assign (ES6)](#objectassign-es6)
      - [`prototype` and `Object.getPrototypeOf()`](#prototype-and-objectgetprototypeof)
   - [函数与构造函数](#函数与构造函数)
- [`instanceof`](#instanceof)
- [ES6 原型链语法糖](#es6-原型链语法糖)
- [Traps](#traps)
- [Ref](#ref)

<!-- /MDTOC -->
# 继承与原型链
Java 等语言是 __基于类__ 的, 与之相对, JavaScript 是 __基于原型__ 的。
> JavaScript 是一种动态语言,
> JavaScript 本身没有提供类的实现
> JavaScript 只有"对象"(object)这一种结构
> 上面这句话准确的说是错的... 详见 primitive type 和 wrapper object 部分, 本文默认把所有东西当成对象, 其实反正额外情况也不多,

当我们在谈论 JavaScript 的 "继承" 时, 实际上是在谈论 JavaScript 中每个对象都拥有的私有属性`[[prototype]]`和 `prototype` 对象为基础的方法实现的"继承"。

> ## `[[prototype]]` 与 `__proto__`
> `[[prototype]]`这个内置属性在 ECMA 标准中并没有给出明确的获取方式, 在大多数 JavaScript 的实现方案中（如 Node、大部分浏览器等）都提供了一个`__proto__`属性来指代这一`[[Prototype]]`

## `[[prototype]]` 和 `prototype`
每个对象都拥有私有属性`[[prototype]]`, 这个属性持有一个连接到另一个称之为 该对象的原型(prototype) 的对象的链接。
这个原型对象也有它自己的原型, 如此向上递归, 直到一个对象的原型为`null`。

根据定义, `null` 是没有原型的, 可以得出结论, __`null` 是原型链(prototype chain)的最后一个环节__

> 实际上并不是所有对象都有 `prototype` 属性, 比如 null 和 undefined 就没有


# 原型链与原型
原型 prototype
原型链 prototype chain

可以说原型链是一个 `[[prototype]]` 疯狂指向 `prototype` 连成链状不明物体的过程, 所以我们的问题基本也就可以简化为经典的 5W 了,
+ 怎么连
+ 为什么连
+ 什么时候连
+ 谁连谁
+ 连什么

## 原型链与闭包
> JavaScript objects are dynamic "bags" of properties (referred to as own properties).

当我们访问一个 object 时, JavaScript 会按序搜索整个闭包, 直到搜索到结果。而我们之前说过, 每个 object 都有 `[[prototype]]` 属性来指向其原型, 这意味着搜索时会遍历 object 原型链上的所有对象。这带来了少数几个影响:
+ 所以这个东西被称为"原型__链__"
+ 在原型链过长时, 会影响性能
+ 对数组对象等使用 forin foreach 在链上的搜索导致 for 循环意外的失效

如果你看过 MDN 上的例子的话... 那么这是一个简化版的改写
```{js cmd:"node", id:"chj4ek1qxf"}
// 让我们假设我们有一个对象 o, 其有自己的属性 a 和 b：
// {a: 1, b: 2}

// o 的原型 o.__proto__ 有属性 b 和 c：
// {b: 3, c: 4}
let O = function(){}
O.prototype.a = 1;
O.prototype.b = 2;
let o = {b:3,c:4}
let x = o.__proto__ = O.prototype;

// o -> O.prototype  -> Object.prototype -> null
//      O {a:1, b:2} -> {}               -> null
do {
    console.log("__proto__",x);
    x = x.__proto__;
    console.log("prototype",x);

} while (x !== null);

console.log(o.a,o.b,o.c,o.d);
```

## 函数与原型
那么 `[[prototype]]`指向的原型到底是谁呢？

JavaScript 中 function 的特殊地位就不再表示了, 在 JavaScript 中, 万物皆是 object, __但是只有 function 拥有 prototype 属性__

当我们在使用 `function` 时, 其实是调用了 `Function` 构造器, 生成了一个类型为 ‘function’ 的对象。而生成的对象的`[[prototype]]`属性指向的就是其__构造函数__的`prototype`属性。
* 注意, `Function` 本身也是一个函数, `Function`的原型被指定为 `Function.prototype`, 因此, `Function.prototype` 不能被修改

## 原型链传播
现在我们知道了, JavaScript 中的 object 通过`[[prototype]]` 指向构造函数的原型('`prototype`')
那么如何依赖原型来实现继承呢?
之前提过, JavaScript 的 object 是闭包的, `[[prototype]]`作为 obejct 的固有方法, 能搜索和使用它原型链对象的所有的方法。比如原型对象的原型对象(的原型对象的原型对象...)的所有方法..

把 object 想成蛋的话, 找到生这个蛋的鸡(function), 这只鸡的原型(`prototype`)也是一颗蛋(object), 指向生它的鸡(`prototype.__proto__`), 按照这个模式循环下去, 我们就有了一条鸡生蛋蛋生鸡的"原型链"

## Object.prototype, Function.prototype 与原型链的结束
原型链不是无限的, 原型链会指向一个终点 null

我们在 JavaScript 中建立构造函数时, 始终调用了 Function 方法; 同样, 我们在建立对象时, 无论用什么方法, 始终调用了 Object 方法。

所以, 所有对象都能使用 Object.prototype 里的方法 ( 比如 toString ), 因为它们的原型链最终都指向 Object 中的 prototype 属性。
同样的, 所有 function 其本身也是一个对象, 所以 function 也拥有 `[[prototype]]` 指向 `Function.prototype`,

> 所有 function 都持有 `length` 和 `prototype` 两个属性

> 建立对象的更多, 参考本文后面 Object 的部分

```{js cmd:"node", id:"chj4h75bec"}
console.log((function(){}).__proto__); // Function.prototype
console.log((function(){}).prototype); // (object)
```

所以对于一个正常的对象,
+ 其`[[prototype]]`会指向它的构造函数,
+ 而它的构造函数的`[[prototype]]`会指向`Function.prototype`,
+ 构造函数的`prototype`中会存储"类"的方法和变量,
+ 构造函数的`prototype`的`[[prototype]]`(即原型的原型)会指向Objec.prototype
    + 这一条是最重要的

在看这个例子前, 牢牢记住, function 对象都调用 Function 方法创建, 而所有的变量(包括函数)本身就是一个 object, 它们的创建都调用了 Object 方法。
```js
function O(){}; // var O = function(){}

O.prototype.x = 1;
var o = new O();
// o.__proto__ => O.prototype
// o.prototype => undefined

// O.__proto__ => Function.prototype
// O.prototype => {x=1}
// O.prototype.__proto__ => Object.prototype

// Function.__proto__ => 被指向 Function.prototype
// Function.prototype => 被指定, 不可更改

// Function.prototype.__proto__ => Object.prototype
// Object.prototype.__proto__ => null
```
这个东西在你还不明白的时候看起来...非常诡异...
![](https://i.stack.imgur.com/4pCXC.png)

我们可以看到, 原型链最终会导向 `Object.prototype.__proto__`, 也就是 null

## 继承的法理依据
从上面的话题, 我们提炼出两点疑问,
+ 既然万物皆是对象(object), 那么创建的函数(function)同时还是 function, 它们之间的关系是什么
+ 上面那张看懂以后赞美人类智慧但是看懂之前狗屁不通的图到底是怎么把`Function`和`Object`扯到一起的

基本上解决这两个问题那么就能明白在 JavaScript 中是如何实现继承的了。毕竟, Object 和 Function 就是 ECMA 给的一个不太友好的示例。

"万物皆是对象", 那么很容易得出 "函数是一种特殊的对象" 这个结论, 聪明的你一定猜到了, `function` 是 `object` 的 "子类"。

链接两者的关键在于`prototype`。
如果我们还没有忘记 `prototype`是一个 "object" 的话, 那么是不是说明 `Function.prototype` 也是被 `Object` 创立, 那么 `Function.prototype.__proto__` 是否是指向了"构造函数的原型",也就是 `Object.prototype`?
至此我们来到了原型链的终点, `Object.prototype` 名义上应该指向自己(object的原型=>Object.prototype), 但是为了闭包我们选择使用了 null 来结束这个痛苦的循环。
> 结束这个死循环的方法是让 Object.prototype 不由 Object 函数来创建 ..

在平时, 我们由 function 关键字调用 Function 类 创建的 object 的 `foo.__proto__`(`Foo.prototype`) 都是默认的, 那么`Foo.prototype.__proto__`就指向了 Object.prototype。
> 实际上, 所有内建对象(Array, Function etc.)构造函数的原型, 除了 Object.prototype 以外, 都是由 Object 创建的

当我们改写其构造函数原型的 `Foo.prototype.__proto__`, 就改变了原型链的默认结构, 实现了继承。

接下来我们先来演示一下暴力拼接原型链
### 手工拼接原型链
```{js cmd:"node",id:"chj4ha673p"}
// let A to be a based-class, B will extend A

// This writing type makes think of that `function` is also a `object`
let A = function(){this.a2 = "this is A.a2\n"}
// let A = function(){A.prototype.a2 = "this is A.a2\n"}
A.prototype.a = "this is A.a\n"

let B = function(){}
// type B.prototype.[[prototype]] to A manually
// cm1:
// B.prototype = new A();
B.prototype.__proto__ = A.prototype;
// cm2:
// B.prototype.constructor = B;
// cm3:
B.prototype.b = "this is B.b\n"

let a = new A();
let b = new B();
console.log(b instanceof B);
console.log(b instanceof A);
console.log(b instanceof Object);
console.log("-----------var---------");
console.log(a.a,a.a2);
console.log(b.a,b.b,b.a2);
console.log("-----------proto---------");
console.log(a.__proto__);
console.log(a.__proto__.__proto__);
```
通过直接手工指定子类构造器的原型, 强行设定了继承关系。
不过我们也发现这种方法有一定的问题,
+ 比如构造器 B 并没有向其它 OO 技术一样调用父类 A 的构造方法(`b.a2=>undefined`)(解除注释 `cm1` 来消除这个错误)
+ 比如在继承链的情况下, B 的对象无法分辨自己的爹是 B 还是 A (...真是..鬼畜)(解除注释 `cm2` 来消除这个错误)
+ 比如 如果你更换了 `cm3` 的位置, 那么会遇见 B.b === undefined 的状况
> 在这里 如果构造函数里写的是
    ```
    let A = function(){
        A.prototype.a2 = "this is a2"
    }
    ```
    那么恭喜你, 你遇上大坑了, 你会发现 b.a2 有时是 undefined, 有时是字符串???
> 出现这种喜闻乐见的事情的原因还是在于 B 没能正确调用其父类 A 的构造器, 在 JavaScript 中对象的原型链是公共的, 任何对原型链的更改会反馈给所有相关的闭包。
> 在我们只调用了构造器 B 时, A 未被正确调用, 没有任何方法定义了 a2 , a2 是一个未定义值。 而当我们调用了构造器 A, 原型链受到了更改, 所有实例原型链上的方法都被更改了 -- 这时候的 a2 就被挂在了原型链上, a2 在这时候可以正常显示被 A 初始化的值了。
```{js cmd:"node", id:"chj4hb1hut"}
// Public prototype chain
let A = function(){};
A.prototype.a = 2;
let a1 = new A();
let a2 = new A();
console.log(a2.__proto__.a);
a1.__proto__.a = 3;
console.log(a2.__proto__.a);
```
> "这根本就不是继承" -- 爱因斯坦

如果我们需要手撕继承, 还需要在这个简单的例子上做更多限定和扩展..呃.. 简单来说就是把上面的注释去掉并且不要把顺序搞乱
```js
/* core step 1: */
B.prototype = new A();
// B.prototype.__proto__ === A.prototype => 这一步不需要手工做了
/* core step 2: */
B.prototype.constructor = B;
/* core step 3: */
// add your custom prototype method
```
当然, 要继续拆下去的话,
```js
// 你以为你执行的是
B.prototype = new A();
// 你其实执行的是 Dio 哒
var o = new Object();
o.__proto__ = A.prototype;
A.call(o);
```

ES5之前, 南方古猿就是这么生成对象的 ( 尼安德特人选择手工操作`__proto__`,抱歉他们没能活下来 )。 所以接下来, 还是我们看一看标准的实现方法(ES5)。
## Object 与原型

### ES 5 继承的实现
```{js cmd:"node", id:"chj4hallqp"}
// same A, same B, diff Story
let A = function(){
    A.prototype.a2 = "This is A2! \n"
    this.a3 = "This is A3! \n"
};
A.prototype.a = "This is A! \n"

let B = function(){
    A.call(this);
    this.b2 = "This is B2! \n"
}

B.prototype.b1 = "This is B1! \n"
B.prototype = Object.create(A.prototype);
B.prototype.b = "This is B! \n"

B.prototype.constructor = B;

let b = new B();
console.log(b.b2, b.b, b.b1);
console.log(b.a,b.a2,b.a3);
console.log("----------obj---------");
console.log("b:\t",b);
console.log("B:\t",b.__proto__);
console.log("A:\t",b.__proto__.__proto__);
console.log("Object:\t",b.__proto__.__proto__.__proto__);
console.log("is instanceof B?:",b instanceof B);
console.log("is instanceof A?:",b instanceof A);
```
这里有些和之前不一样的东西, 删掉那些多余的输出和调试语句, 最后我们的核心代码有这么三句
+ `B.prototype = Object.create(A)`
+ `B.prototype.constructor = B`
+ `A.call(this)`
让我们一条一条来说说
### Object.create()
`Object.create()`最大的好处在于提供了一种简易引入和继承其它类的方法, 在 ES 5 以前, 继承并不是那么容易的事情。
在使用 `Object.create()`的时候, 我们应该将其封装起来, 为其第二个参数提供 Properties, 来建立对象的属性,(而不是在父类或子类里面胡写。)这么做的好处在于我们可以创造定制化的需要的对象, 而不会把构造函数搞的异常复杂, 使用 prototype 是无法做到这一点的 (prototype 中的变量是全局的)。
```{js cmd:"node", id:"chj4ilwrzi"}
global = {
    nextId:function(){return 12;}
}

const create_person = function(name){
    const Person = function(){}
    Person.prototype = {
        constructor: Person,
        sayHello: function(){console.log("Hello "+this.name)}
    }
    let ret = Object.create(Person.prototype,{
        'id' :{
            value: global.nextId(),
            enumerable:true
            // writable:false, configurable(deletable):false by default
        },
        'name':{
            value: name,
            enumerable:true
        }
    });
    return ret;
}

let bob = create_person('bob');
bob.sayHello();
console.log(bob);
```
> `properties` 的三个值`enumberable`(可枚举) `writable`(可写) `configurable`(可配置)默认均为`false`

不过要注意, 在这种写法下, 类的构造器对外是不可见的, 我们不能直接调用类的构造函数。

> 在这里演示的是继承自 Object 的函数, 如果是继承自别的类, 在构造函数里依然要 `Base.call(this)`

### B.prototype.constructor = B
### After any case onceif you changed 'prototype'

这一条相对简单, 之前也提到过多次,
无论是
```js
Foo.prototype.__proto__ = new Bar(); // 从基类继承
```
还是
```js
Foo.prototype = {
    foo:12450,
    var:"93e",
} // 重新定义 Foo.prototype
```
这样的行为都会 __导致 Foo.prototype 被重写__, prototype 的结构被破坏, 这时候我们需要重新指定 Foo.prototype.constructor 让 Foo 创建的对象能找到正确的构造函数。

同理, 所有对 prototype 的自定义行为需要在重写 prototype 后进行, 不然写半天又自己覆盖掉, 白忙活一场。

> 事实上, 基本类型对象的 constructor 值也可以被改写, 依赖一个对象的 constructor 属性并不是安全的
> 唯一的例外来源于由 native constructors (源生构造函数) 创建的对象。

### B.call(this)
来源于 `Function.prototype.call()`
该方法和 `Function.prototype.apply()` 类似, 唯一的区别是 `call()` 接受若干个__参数的列表__, `apply()` 接受一个__包含多个参数的数组__
```
fun.call(thisArg[, arg1[, arg2[, ...]]])
```
+ thisArg
    + 在fun函数运行时指定的this值。
    + __指定 this 值__
    + __指定 this 值__
    + __指定 this 值__
    + 指定的this值并不一定是该函数执行时真正的this值
        + 在非严格模式下, 指定为null和undefined的this值会自动指向全局对象 (浏览器中就是 window 对象)
        + 在非严格模式下, 值为原始值 (数字，字符串，布尔值) 的this会指向该原始值的自动包装对象。
    + 也可以为匿名函数指定 this 值
+ arg1, arg2, ...
    + 参数列表

可以让 call() 中的对象调用当前对象所拥有的 function。你可以使用 call() 来实现继承：写一个方法，然后让另外一个新的对象来继承它（而不是在新对象中再写一次这个方法）。

### 混入继承
有时候我们需要继承多个类...呃...为什么没有"接口"这样美好的事物呢..
```js
function MyClass() {
     SuperClass.call(this);
     OtherSuperClass.call(this);
}

MyClass.prototype = Object.create(SuperClass.prototype); //inherit
mixin(MyClass.prototype, OtherSuperClass.prototype); //mixin

MyClass.prototype.myMethod = function() {
     // do a thing
};
```
mixin 函数会把超类原型上的函数拷贝到子类原型上，这里 mixin 函数没有给出, 需要由你自己来实现。
### Object.assign (ES6)
( MDN 在这里讲的非常好.. 我就基本照抄了 )
在 ES 6 中, 新提供了 Object.assign 函数来辅助对象的复制
> Object.assign() 方法用于将所有可枚举的属性的值从一个或多个源对象复制到目标对象。它将返回目标对象。
```js
Object.assign(target, ...sources)
```
其中, `target` 是被植入值的目标对象, 是最后的返回值。`sources`是要混入的源对象。
如果 target(目标对象)中的属性具有相同的键，则属性将被源中的属性覆盖。后来的源的属性将类似地覆盖早先的属性。

` Object.assign` 方法只会拷贝源对象__自身的__并且__可枚举的(enumerable:true)__属性到目标对象身上。
> 该方法使用源对象的 `[[Get]]` 和目标对象的 `[[ Set ]]`，所以它会调用相关 getter 和 setter。因此，它分配属性而不是复制或定义新的属性。如果合并源包含了 getter，那么该方法就不适合将新属性合并到原型里。假如是拷贝属性定义到原型里，包括它们的可枚举性，那么应该使用 `Object.getOwnPropertyDescriptor()` 和 `Object.defineProperty()` 。

+ String类型和 Symbol 类型的属性都会被拷贝。
    + Symbol 也是 ES 6 引入的, 所以在 ES 5 实现 Object.assgin 的时候无须考虑 Symbol 的处理
+ 注意，在属性拷贝过程中可能会产生异常，比如目标对象的某个只读属性和源对象的某个属性同名，这时该方法会抛出一个 TypeError 异常，拷贝过程中断，已经拷贝成功的属性不会受到影响，还未拷贝的属性将不会再被拷贝。

+ 注意， Object.assign 会跳过那些值为 null 或 undefined 的源对象。
+ 继承属性和不可枚举属性是不能拷贝的
    + 继承属性在构造器的 prototype 上, 不可枚举属性没有 getter
+ 原始类型会被包装为 object
    + 只有字符串的包装对象才可能有自身可枚举属性。
    + 也就是说 true/false 和 数字类型无法被正确拷贝, 字符串则会被切割包装, 逐个枚举。

### 深度拷贝
Object.assign() 拷贝的是属性值

针对深度拷贝，需要使用其他方法，因为 Object.assign() 拷贝的是属性值。假如源对象的属性值是一个指向对象的引用，它也只拷贝那个引用值。

> 一种简单的深拷贝方法是利用 `JSON.parse(JSON.stringify(obbj))` 来拷贝对象

```js
// 下面这个函数会拷贝所有自有属性的属性描述符
function completeAssign(target, ...sources) {
  sources.forEach(source => {
    let descriptors = Object.keys(source).reduce((descriptors, key) => {
      descriptors[key] = Object.getOwnPropertyDescriptor(source, key);
      return descriptors;
    }, {});

    // Object.assign 默认也会拷贝可枚举的Symbols
    Object.getOwnPropertySymbols(source).forEach(sym => {
      let descriptor = Object.getOwnPropertyDescriptor(source, sym);
      if (descriptor.enumerable) {
        descriptors[sym] = descriptor;
      }
    });
    Object.defineProperties(target, descriptors);
  });
  return target;
}
```

### `prototype` and `Object.getPrototypeOf()`
之前提到过, 原型中定义的元素将被所有实例共享, 甚至可以在稍后对原型进行修改, 这种变更将影响到所有现存实例。
我们使用 `Constructor.prototype` 来找到构造函数的 `prototype`,
而 `Object.getPrototypeOf()` 的作用是提供给 object 一个获取构造器 `prototype` 的方法
也就是说, 简而言之， `prototype` 是用于类型的，而 `Object.getPrototypeOf()` 是用于实例的（instances），两者功能一致。
> 为了养成良好的习惯，实际项目最好使用 `getPrototypeOf` 取原型链, 别用`__proto__`

## 函数与构造函数
```{js cmd:"node", id:"chj4gwnoep"}
function Example() {
    this instanceof Example ? console.log('以构造函数形式调用') : console.log('非构造函数形式调用');
}

new Example(); // '以构造函数形式调用'
Example();     // '非构造函数形式调用'
```


# `instanceof`
用于检查构造器的原型是否在对象的原型链上。

# ES6 原型链语法糖
ECMAScript6 引入了一套新的关键字用来实现 class。使用基于类语言的开发人员会对这些结构感到熟悉，但它们是不一样的。 JavaScript 仍然是基于原型的。这些新的关键字包括 class, constructor, static, extends, 和 super.
```js
class A{
  constructor(name) {
    this.name= name
  }
  toString() {
    return this.name
  }
}

class B extends A {
  toString(){
    return this.name + 'b'
  }
}
```
Babel 编译出来长这样:
```js
function _inherits(subClass, superClass) {
    // 密
}

var A = (function () {
    function A(name) {
        this.name = name;
    }

    A.prototype.toString = function toString() {
        return this.name;
    };

    return A;
})();

var B = (function (_A) {
    function B() {
        if (_A != null) {
            _A.apply(this, arguments);
        }
    }

    _inherits(B, _A);

    B.prototype.toString = function toString() {
        return this.name + 'b';
    };

    return B;
})(A);
```


# Traps
1. 牢记只有 `function` 类型拥有 `prototype` 属性。
    + 一个常见的错误认知产生于
    ```{js cmd:"node",id:"console_prototype"}
    console.log(Object.prototype);
    console.log(Array.prototype);
    console.log(String.prototype);
    ```
    从而产生 "`object`" 类型也有自己的 prototype 的错误认识。
    问题在于, 这里打印的实际上 作为__构造函数__的 Object/Array/... 等 __函数__ 的 `prototype`
2. 不要去对之前提到的那群并不可靠的"内置对象原型"动任何刀子, 比如不要去尝试对 Object.prototype 做任何修改, 这会破坏原型链的密封性。
    + 该技术被称为 monkey patching
    + 我们去扩展内置对象原型的唯一理由是引入新的 JavaScript 引擎的某些新特性，比如 Array.forEach。
3. `Object.create()`除了接受 object 作为参数, 还接受 null 作为参数 (这里我们突然想起来 null 其实不应该是一个对象了), 在 `Object.create(null)` 的情况下, 对象__不会继承__任何 `Object.prototype` 的方法
    + `{}` 与 `Object.create(Object.prototype)` 相等。

# 虽然..但是..
JavaScript 提供了多种方法来模拟 class, 而在常见的框架库通常使用 原型链 来模拟并实现继承,
但是《Programming JavaScript Applications》,《Design Patterns: Elements of Reusable Object Oriented Software》提出, 别用继承, 特别是在 JavaScript 中。

他们建议使用 组合(compose) 来建立更简单, 灵活的对象。

# Ref
http://www.cnblogs.com/snandy/archive/2013/01/02/2841899.html
https://github.com/creeperyang/blog/issues/9
https://blog.oyanglul.us/javascript/understand-prototype.html
https://developer.mozilla.org/
