# **Functional Programming(FP-函数式编程)**
## FP是什么
- #### wiki：函数式编程是一种声明式的`编程范型`，也就是如何编写程序的方法论，意思是说程序逻辑不需要通过明确描述控制流程来表达。
## FP和OOP
- #### FP：面向对象编程把程序看作一系列相互作用的`对象`
- #### OOP：函数式编程中把程序看作是一个无状态的`函数`计算的序列。
## 命令式和声明式
- #### 命令式：
1. 程序花费大量代码来描述用来达成期望结果的特定步骤 —— `控制流`：即`如何做`。
2. 代码中频繁使用`语句`。语句是指一小段代码，它用来完成某个行为。通用的语句例子包括 `for`、`if`、`switch`、`throw`，等等
- #### 声明式：
1. 程序抽象了控制流过程，花费大量代码描述的是`数据流`：即`做什么`。
2. 代码更多依赖`表达式`。表达式是指一小段代码，它用来计算某个值。表达式通常是某些`函数调用`的`复合`、一些值和操作符，用来计算出结果值。
## 纯函数
 - 此函数在`相同的输入值`时，需产生`相同的输出`。函数的输出和输入值以外的其他隐藏信息或状态无关，也和由I/O设备产生的`外部输出无关`。
 - 该函数不能有语义上可观察的函数`副作用`，诸如“触发事件”，使输出设备输出，或更改输出值以外物件的内容等。

纯函数：
``` javascript
function double (num) {
    return num * 2
}
```
非纯函数：
``` javascript
var numTwo = 2
function double (num) {
    return num * numTwo
}
```
纯函数可缓存
``` javascript
function cache (fn) {
    var obj = {}
    return function (arg) {
        return obj[arg] || (obj[arg] = fn(arg))
    }
}
```
## 高阶函数
 - 接受一个或多个`函数`作为输入
``` javascript
function double (fn) {
    return fn() * 2
}
```
 - 输出一个`函数`
``` javascript
function Incrementing (num) {
    return function () {
        return num++
    }
}
var fn = Incrementing(2)
fn() // 2
fn() // 3
fn() // 4
```
## 闭包
- 内部的函数`引用了外部`的函数的变量
- 当内部函数被调用时，外部函数里的变量就`不会被销毁`
- 减少`全局`变量
- `内存泄漏`
## 柯里化
- 把接受`多个`参数的函数变换成接受一个`单一`参数的函数，并且返回接受余下的参数而且返回结果的新函数
``` javascript
var curry = (fn) => {
    var currideFn = function () {
        var args = [].slice.call(arguments)
        if (args.length < fn.length) {
            return function () {
                var _args = [].slice.call(arguments)
                return currideFn.apply(null, args.concat(_args))
            }
        }
        return fn.apply(null, args)
    }
    return currideFn
}
var fn = curry((a, b, c) => a + b + c)
console.log(fn(1)(2)(3)) // 6
console.log(fn(1, 2)(3)) // 
```
## 偏应用
- 把接受`多个`参数的函数变换成一个可以先接受`undefined`参数函数，并且返回接受替换`undefined`的参数而且返回结果的新函数
``` javascript
// 应用左边任意数量的参数
var partial = function (fn) {
    var args = [].slice.call(arguments, 1)
    return function () {
        var _args = [].slice.call(arguments)
        for (let i = 0, arg = 0; i < args.length && arg < _args.length; i++) {
            if (args[i] === undefined) {
                args[i] = _args[arg++]
            }
        }
        return fn.apply(null, args)
    }
}
let fn = partial(setTimeout, undefined, 3000)
fn(() => console.log(123))
// 3秒后输出：123
```
- ## 组合
- ## 管道
- ## 函子
- ## Monad
- ## Generator
---
## 函数式编程偏好：

- 使用纯函数而不是使用共享状态和副作用
- 让可变数据成为不可变的
- 用函数复合替代命令控制流
- 使用高阶函数来操作许多数据类型，创建通用、可复用功能取代只是操作集中的数据的方法。
- 使用声明式而不是命令式代码（关注做什么，而不是如何做）
- 使用表达式替代语句
- 使用容器与高阶函数替代多态
## 友情链接
- [underscore.js(JavaScript函数式库)](http://www.css88.com/doc/underscore/)
- [月影博客](https://www.h5jun.com/)
- [知乎文章](https://zhuanlan.zhihu.com/p/21714695)
- [JavaScript ES6函数式编程入门经典](https://book.douban.com/subject/30180100/)
