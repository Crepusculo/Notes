一句话而言, JavaScript 在设计时根本没有有意划分所谓"primitive type"
# ECMA 的划分标准
Undefined
Null
Boolean
String
Number
Object

# `typeof` 的六种取值
```js
var a = 1, b = '2', c = true, d, e = null, f = function(){}
typeof a === 'number'; // true
typeof b === 'string';    // true
typeof c === 'boolean'; // true
typeof d === 'undefined'; // true
typeof e === 'object'; // true
typeof f === 'function'; // true
```
但是其中,
 `null === 'object'` 是一个众所周知的历史性错误
 `function` 实质是 `Object` 的子类, 只是 JavaScript 中 function 地位比较特殊而已
# 原始值
三种原始值分别是 数字, 字符串, 布尔值

# 不可改的源生构造函数
源生构造函数是只读的, 被用于创造 boolean 值 (`true/false`), 数字(`1/3e2`,不包括`Number`构造器)和字符串(`"test"`), 这些源生构造函数创建的值通常就被称为原始值。
此外, 如`Function`,`Array`,`Number`等构造函数, 统统是不可靠的。

# 《JavaScript 高级程序设计》

Undefined、Null、Boolean、Number、String、(1st Edition)
simple data type (2ed,3rd Edition)

#《JavaScript 权威指南（第 6 版）》
primitive types
分为基本类型（primitive types）和对象类型，基本类型又分为数字，字符串，布尔，及两个特殊 null，undefined

# 九个原生对象构造函数
Number()
String()
Boolean()
Object()
Array()
Function()
Date()
RegExp()
Error()

其中 `Number()` `Boolean()` `String` 不仅能够构建对象，而且能为字符串、数字和布尔值提供原始值。
JavaScript 主要是由这 9 个对象（以及字符串、数字和布尔原始值）来创建的。

原始值由原生构造函数创建时, 其 prototype.constructor 是只读的。
# Ref
http://www.cnblogs.com/snandy/archive/2013/01/02/2841899.html
