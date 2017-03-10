<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [ES 6 -> ES 5](#es-6-es-5)
- [`let`](#let)

<!-- /TOC -->

# ES 6 -> ES 5

|  | |
|---------|---|
| **命令行**:   | npm 安装 ->  |
| **browser**:  | 从6.0开始需要从构建工具构建

# `let`
0. 不允许变量提升
1. 块作用域
    + 内层变量覆盖外层变量
    ```js
    var tmp = new Date();
    function f(){
        console.log(tmp);
        if(false){
            var tmp = "Hello jerk";
        }
    }
    f() // [warning]: undefined
    ```
    var tmp被提升
    若换做 `let` 则不会发生这样的现象

    + 计数循环变量泄露为全局变量


2. Temporal dead zone (TDZ)
    简单的例子:
    ```js
    tmp = 'abc'         // [error]: ReferenceError
    console.log(tmp)    // [error]: ReferenceError

    let tmp;            // TDZ end
    console.log(tmp)    // [error]: undefined
    ```
    复杂一点的例子:
    ```js
    function bar(x=y, y=2){
        return [x,y];
    }

    bar(); // [error]: x=y, y=2 暂时死区
    ```
3. 不允许重复声明
    ```js
        let - var // [error]
        let - let // [error]
        arg(参数) - let // [error]
    ```
