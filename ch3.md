# Functions

## Defining A Function
```
var square = function(x){
  return x*x;
}
console.log(square(12));
//->144
```

## Nested Scope

### Lexical Scoping
First, Lexical Scope (also called Static Scope), in C-like syntax:
```
void fun()
{
    int x = 5;

    void fun2()
    {
        printf("%d", x);
    }
}
```
Every inner level can access its outer levels.

There is another way, called Dynamic Scope used by first implementation of Lisp, again in C-like Syntax:
```
void fun()
{
    printf("%d", x);
}

void dummy1()
{
    int x = 5;

    fun();
}

void dummy2()
{
    int x = 10;

    fun();
}
```
Here fun can either access x in dummy1 or dummy2, or any x in any function that call fun with x declared in it.

### Odd Thing
People who have experience with other programming languages might expect that any block of code between braces produces a new local environment. But in JavaScript, functions are the only things that create a new scope. You are allowed to use free-standing blocks.
```
var something = 1;
{
  var something = 2;
  // Do stuff with variable something...
}
// Outside of the block again...
```

## Functions As Values
A variable that holds a function is still just a regular variable and can be assigned a new value.
```
var launchMissiles = function(value) {
  missileSystem.launch("now");
};
if (safeMode)
  launchMissiles = function(value) {/* do nothing */};
```

## Declaration Notation

### A Declaration
```
function square(x) {
  return x * x;
}

```
### Declaration FLow
It is not top-down.
```
console.log("The future says:", future());

function future() {
  return "We STILL have no flying cars.";
}
```

## Closure

闭包是函数式编程及其核心思想“Lambda 计算法”（Lambda Calculus）的必备基本设定。

我们都知道：

- 函数式编程有一个特点，就是所有操作都用可计算的函数（computable function，下简称“函数”）来体现。
- 函数的两个特点，就是每个函数都有一个输入值，一个输出值。
- 函数还有一个定律，就是给定一个确定的输入值，总能得到一个确定的输出值，即输入输出有严格的一一对应关系。
- （当然还有无副作用之类，此处不论。）

那么，在这样的限制条件下，请问，“加法”的函数怎么写？

```
function plus(senior) {
    return senior + 1;
}
```
聪明的人们想到了一个办法，如果函数 A 拿到参数 ① 之后能够返回另一个函数 B，而函数 B 拿到参数 ②，再把参数 ① 和 ② 糅合起来就可以了。
```

function plusAny(senior) {
   return function(second) {
        return senior + second;
   }
}

/* usage */

var senior = 2838240000;
var longLiveSeniorFunc = plusAny(senior);

longLiveSeniorFunc(1);     // +1s
longLiveSeniorFunc(3600);  // +1h
longLiveSeniorFunc(86400); // +1d
```
这个 plusAny 函数，就是一个闭包。因为它返回了一个函数，且此函数“包”进了 plusAny 函数作用域里的一个本地变量 senior，并且可以在其存续期间持续使用这个变量。

```
partialApply(targetFunction: Function, ...fixedArgs: Any[]) =>
  functionWithFewerParams(...remainingArgs: Any[])

const add = (a, b) => a + b;
const add10 = partialApply(add, 10);
add10(5);
```

什么是闭包？

简言之，闭包是由函数引用其周边状态（词法环境）绑在一起形成的（封装）组合结构。在 JavaScript 中，闭包在每个函数被创建时形成。

这是基本原理，但为什么我们关心这些？实际上，由于闭包与它的词法环境绑在一起，因此闭包让我们能够从一个函数内部访问其外部函数的作用域。

要使用闭包，只需要简单地将一个函数定义在另一个函数内部，并将它暴露出来。要暴露一个函数，可以将它返回或者传给其他函数。

内部函数将能够访问到外部函数作用域中的变量，即使外部函数已经执行完毕。

闭包的用途之一是实现对象的私有数据。数据私有是让我们能够面向接口编程而不是面向实现编程的基础。而面向接口编程是一个重要的概念，有助于我们创建更加健壮的软件，因为实现细节比接口约定相对来说更加容易被改变。

在 JavaScript 中，闭包是用来实现数据私有的原生机制。当你使用闭包来实现数据私有时，被封装的变量只能在闭包容器函数作用域中使用。你无法绕过对象被授权的方法在外部访问这些数据。在 JavaScript 中，任何定义在闭包作用域下的公开方法才可以访问这些数据。

对象不是唯一的产生私有数据的方式。闭包还可以被用来创建有状态的函数，这些函数的执行过程可能由它们自身的内部状态所决定。
