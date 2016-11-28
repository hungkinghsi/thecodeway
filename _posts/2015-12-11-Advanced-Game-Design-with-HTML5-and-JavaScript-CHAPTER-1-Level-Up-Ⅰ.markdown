---
layout: post
title:  "HTML5和JavaScript高级游戏设计 章一 提升 Ⅰ"
date:   2015-12-11
author: Houngking Hsi
category: other
tags: [HTML5, JavaScript]
---



[本章翻译作者 : ] [Houngking Hsi](http://indeex.org/thecodeway) Email:<imisslovelove@live.com>



### 提升



　　本文第一章对HTML5和JavaScript的高级游戏设计是一个快节奏的，拥挤的，把你的自助餐很酷的，有趣的，新的，实用的，有时令人费解的TE技巧，你可以开始使用你的游戏项目吧。你需要知道的一切，把你的技能的发展，到下一个水平就在这章


* 全新的JavaScript技巧，包括你做游戏时需要的一切和ES6
* 使用配置对象
* JavaScript的getter和setter
* Promises
* 使用Class和composition生成new objects从old ones
* 有组织的项目和模块
* 读写JSON文件和XHR
* 游戏全屏
* 分发游戏iframe和源代码压缩



[译者按：源代码压缩是指源代码经过特殊复杂化后用户无法查看或直接使用开发人员的源码以达到保护源码的一种加密技术]


　　你可以认为本章对于所有的基本技能的概括，你需要知道如何开始使用HTML5和JavaScript来制作游戏，并且加入现代游戏开发者新兵训练营。除了基础还有这本书的其余部分的核心技能，你能够将所有这些技术立即应用到你的游戏项目中。如果你使用HTML5和JavaScript读取基础游戏素材，这个有点像“secret last chapter”那本书。但是如果你没有读过那本书，你想学点很快上手的例子，这一章只是从基础上简略的介绍JavaScript和HTML5。其他章节有很大的不同，在这本书中，它是一种快速阅读的参考指南。尽可能多地阅读一下本章，不管你需要做什么，都要尽可能多地阅读一遍。当你准备好的时候，只要你准备好了你可以随时进入第二章。



### 一些新的JavaScript技巧



　　这本书是使用JavaScript的最新版本，称为ES6（ECMAScript 6）。如果你是JavaScript新手，你会发现这种程序语言很容易学习，因为它是大多数现代范式程序设计语言。如果你已经知道JavaScript，在此之前，约2015，你并没有接触过它，那么它会给你一个惊喜，因为ES6几乎是一个全新的语言。值得庆幸的是，它是一个更好，更简单，和比你知道的任何一个JavaScript都要友好的全新版本。而且，最好的是，它很容易学习，所以你就可以在阅读本章的时候，流利的使用它。



　　在本章第一节，我将介绍你应该知道的所有关于语言如何工作的重要概念。你将学习ES6最重要的新特性，及一些在前一个版本ES5以前版本的的JavaScript里你也许没有意识到的有用的特性和功能。



 ***
 ■ **注意**　　如果你想在就平台上编写ES6代码，你可以使用**transpiler**像Babel或者traceur。这样可以在使用ES6的同时依然可以使用ES5。我建议你这么做。不然你需要额外的工作量来移植你的代码到ES6，这样会增加你的心理负担。
 ***



### 变量： let，const和var   
使用关键字来创建一个变量：


let anyValue = 4;


　　让关键字给出**可变块范围**。这就意味着该变量在它被定义的一对大括号外是不能被访问的。下面是一个例子：



```JavaScript
let say = "hello";
let outer = "An outer variable";
if (say === "hello") {
    let say = "goodbye";
    console.log(say);
    //Displays: "goodbye"
    console.log(outer);
    //Displays: "An outer variable"
    let inner = "An inner variable";
    console.log(inner);
    //Displays: "An inner variable"
}
console.log(say);
//Displays: "hello"
console.log(inner);
//Displays: ReferenceError: inner is not defined
```


　　外部定义的变量可以在语句中看到。但任何变量如果在内部定义的话，就无法在外部看到它。这就是局部声明。如果语句的花括号中的变量是可见的。在这个例子中，你可以看到有2个变量声明。因为他们被定义不同的块，它们是不同的变量。改变一个花括号内部的变量，不会不改变外部的变量。




　　您还可以创建使用VaR和const变量：



* VAR：这是给变量的**函数声明**。这意味着该变量将在一个函数中的任何一个地方都能看到，即使在它的外部被创建。
* const：通过一个常数值声明一个块范围变量。这将创建一个变量，你不能改变它的值。如果你试图改变它的值，你会得到一个错误。如果你的代码依赖于一个没有被意外改变的值，这是有帮助的。const变量也块范围。



　　但是，在几乎所有的情况下，你应该使用它。它保护你不让各种各样的小错误导致程序崩溃。变量是你最重要的JavaScript构建块，你需要使用functions来构建你的应用程序。



### Functions



　　使用函数来运行和定义代码块，执行计算，并返回值。JavaScript有**函数声明**和**函数表达式**的类型。在JavaScript中你可以这样定义一个函数声明：


```JavaScript
function saySomething(value) {
    console.log(value);
}
```


　　函数声明在**编译时**加载。这意味着你的程序知道他们之前程序中的任何其他代码都在运行。即使你在程序结束时定义了一个函数函数声明将在程序开始运行时预先加载代码。那在你定义它之前，你可以调用这个函数，例如：



```JavaScript
saySomething("Hello from a function statement");
//Displays: "Hello from a function statement"
function saySomething(value) {
    console.log(value);
}
```



　　JavaScript也有函数表达式。你用一个**尖括号**创建它们，像这样：


```JavaScript
let saySomething = (value) => {
    console.log(value)
};
```


　　=>符号代表一个箭头指向右边，像这样：→。表面上是：“用我指着的括号中的值在接下来的代码块做一些工作”。    
　　定义一个变量，以同样的方式来定义函数表达式（或声明）。每一个大括号后需要一个分号。在使用它之前，必须先定义一个函数表达式。像这样：


```JavaScript
let saySomething = (value) => {
    console.log(value)
};
saySomething("Hello from a function statement");
```



　　这是因为函数表达式在运行时优先被调用。程序都是从上到下,代码读取两种模式的顺序相同,再读取代码的其余部分。如果你想在定义之前调用一个函数表达式,你会得到一个错误。



　　如果你想编写一个函数，返回一个值，使用return语句，如下所示：


```javascript
let square = (x) => {
    return x * x;
};

console.log(square(4));
//Displays: 16
```


　　为了方便，你可以省去花括号、参数周围的括号和返回关键字，这样你的函数仅仅就是一行代码与一个参数：


```javascript
let square = x => x * x;
console.log(square(4));
//Displays: 16
```



　　这样更整洁，紧凑和可读的方式来编写函数。




 ***
■ **注意** 箭头是一个不错的功能，他们使里面的函数范围同样作用到范围之外。这解决了困扰较早版本的JavaScript **绑定** 的大问题。简单地说，一个完整类的接口正常使用不再是问题（例如,您不再需要使用旧的var self = this;这很诡异。）。有一些极端情况下,绑定仍是个问题,当我们遇到了再解释。
 ***



　　您可以编写一个函数表达式不使用大括号,如下:



```javascript
let saySomething = function(value) {
    console.log(value)
};
```



　　这和前面的例子一样，但有一个重要的区别:函数的作用域是本地的函数，不是周围的代码。这意味着"this"的值是未定义的。这个例子说明了这种差异:




```javascript
let globalScope = () => console.log(this);
globalScope();

//Displays: Window...

let localScope = function(){
    console.log(this);
};

localScope();

//Displays: undefined
```



　　这种差异是微妙而重要的。在大多数情况下我建议你使用一个尖箭头来声明函数表达式，通常它是在函数内部共享相同范围的一种更方便的方式。但在某些罕见的情况下是很重要的从周围的范围里隔离函数的范围,而当我们遇到时，我将介绍这些罕见情况。




 ***
■ **注意** 如果你使用**ES5**，你需要让函数表达式使用本地范围，在第一行用"use strict"。



```javascript
var localScope = function(){
    "use strict";
    console.log(this);
};
```


这个"use strict"的JavaScript语句告诉编译器使用ES5严谨模式,以锁定函数的本地范围。
 ***




　　现在你已经掌握了变量和函数,让我们看看如何使用数组的存储和操作。




### 循环获取数组的值




　　作为一个游戏设计师你最常做的一件事就是循环数组。下面的代码看起来熟悉吗?



```javascript
let planets = ["jupiter", "venus", "saturn", "mars"];
for (let i = 0; i < planets.length; i++) {
    planet = planets[i];
    console.log(planet);
}
```




　　它在控制台中每行都显示一个名称:



```javascript
jupiter
venus
saturn
mars
```




　　这是一个典型的代码，它在ES6得到了不错的升级。因为我使用let定义循环索引计数器，它是局部的循环。这意味着我在许多其他的循环中可以重复使用相同的变量名，只要你喜欢，它们不会发生冲突。




　　我们亲爱的老循环在JavaScript中仍然有它的位置，它往往仍然是适合这么做的最佳工具。但随着ES6（和ES5），你可以使用遍历数组的更方便的方法，可以让你的代码更具可读性。





 ***
■ **注意** for循环倾向于进行高度优化的JavaScript引擎v8引擎和服务器，所以当你需要为每一帧的游戏遍历成千上万的对象时可以确定它们仍然是最可靠的。在这本书中我还是要强调当通常可以安全地使用较新的循环方法，你可以安全的使用for循环。如果你对不同循环方法在您正在使用的平台上的性能差异充满好奇，你可以访问 jsperf.com 来运行一些测试用例。
 ***




