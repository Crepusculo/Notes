
<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

- [`const`](#const)
- [`internal`](#internal)
- [`readonly`](#readonly)
- [`sealed`](#sealed)
- [`out`](#out)
- [`override`](#override)
- [`params`](#params)
- [`ret`](#ret)
- [`sealed`](#sealed-1)
- [`unsafe`](#unsafe)

<!-- tocstop -->
# `const`
[`readonly`](#readonly) 为运行时常量，程序运行时进行赋值，赋值完成后便无法更改，因此也有人称其为只读变量。
`const`为编译时常量，程序编译时将对常量值进行解析，并将所有常量引用替换为相应值。
# `internal`
被 internal 修饰的东西只能在本程序集（当前项目）内被使用。
被 protected internal 修饰的属性 / 方法 可以在其他项目中, 被派生类使用

# `readonly`
`readonly`为运行时常量，程序运行时进行赋值，赋值完成后便无法更改，因此也有人称其为只读变量。
[`const`](#const)为编译时常量，程序编译时将对常量值进行解析，并将所有常量引用替换为相应值。

# `sealed`
```cs
sealed class Cow: Animal{
    ...
}
```
Diff with `final` in Java:
`final` in Java means plenty of different things depending on where you use it whereas `sealed` in C# applies only to classes and potentially virtual members (methods, properties, events).

In Java `final` can be applied to:

+ **classes**, which means that the class cannot be inherited. This is the equivalent of C#'s sealed.
+ **methods**, which means that the method cannot be overridden in a derived class. This is the default in C#, unless you declare a method as virtual and in a derived class this can be prevented for further derived classes with sealed again.
+ **fields** and **variables**, which means that they can only be initialized once. For fields the equivalent in C# is readonly.
# `out`
```cs
void foo(out int param1)
```
# `override`
# `params`
```cs
void foo(params int[] arrays)
void foo(out int sum, params int?[] arrays)
```
+ 只能置于参数列表最后
# `ret`
```cs
void foo(ref int param1)
```
# `sealed`

# `unsafe`
```cs
static unsafe void Main(string[] args)
```
+ 只有标记为`unsafe`的函数体内部才能使用指针
+ 并且需要使用`/unsafe`编译
否则会有`CS0227	不安全代码只会在使用 /unsafe 编译的情况下出现`
```
项目 -> {项目名称}属性 -> 生成 -> [ ]生成不安全代码(勾上)
```
+ 若使用指针传参则要注意主叫函数和被叫函数都需要添加`unsafe`
