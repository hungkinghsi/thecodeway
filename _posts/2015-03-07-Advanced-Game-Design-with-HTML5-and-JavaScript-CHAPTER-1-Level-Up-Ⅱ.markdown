---
layout: post
title:  "HTML5和JavaScript高级游戏设计 章一 提升 Ⅱ"
date:   2016-03-07
author: Houngking Hsi
category: other
tags: [HTML5, JavaScript , JavaScript 2015, ES6]
---



[本章翻译作者 : ] [Houngking Hsi](http://indeex.org/thecodeway) Email:<imisslovelove@live.com>



### forEach循环




　　ES5引进了专门遍历数组的方法：forEach。使用索引计数器可以遍历数组里的所有值。还可以调用回调函数做其他的事情。(你可以看到回调函数是如何工作的。)这意味着只要你需要你可以重用相同的代码遍历其他数组。下面是如何使用forEach来显示四颗行星的名字的例子:



```Javascript
let planets = ["jupiter", "venus", "saturn", "mars"];
planets.forEach(displayElements);
function displayElements(element) {
  console.log(element);
}
```


　　结果和我们的第一个例子一模一样:控制台输出了每个行星的名字。你可以看到forEach参数是一个叫做displayElements的函数:



```Javascript
planets.forEach(displayElements);
```



　　这意味着数组的四个元是一次一个发送每个displayElements函数。displayElements就是一个回调函数。它是一个函数的“回复”,让另一个函数去做一些其他的工作。就好像forEach说,“嘿!displayElements,过来帮我显示这些行星的名字!“  
displayElements函数有一个参数,它表示正在处理的当前元素:


```Javascript
function displayElements(element) {
    console.log(element);
}
```


　　第一次循环时,元素的值是木星。第二次是金星,一次循环下去。



　　数组中有多少元素就循环运行多少次。你不需要声明像i这样的循环计数器变量。   
另一个优点是,如果你有另一个数组您可以重用displayElements函数。下面是如何使用它来显示第二个数组的内容,叫mountains:



```Javascript
let planets = ["jupiter", "venus", "saturn", "mars"];
let mountains = ["everest", "k2", "kanchanjunga", "lhotse"];
planets.forEach(displayElements);
mountains.forEach(displayElements);
function displayElements(element) {
  console.log(element);
}
```



　　这将显示所有的planets和所有的mountains。我们只需要写一个displayElements函数,它就可以遍历两个数组的元素。  
　　关于索引计数器变量,我们亲爱的老朋友i?我们可以通过回调函数中使用。方法如下:



```Javascript
let planets = ["jupiter", "venus", "saturn", "mars"];
planets.forEach(displayElements);
function displayElements(element, i) {
  console.log(i + ": " + element);
}
```


结果:



```Javascript
0: jupiter
1: venus
2: saturn
3: mars
```




　　forEach数组的回调函数中第三个可选参数是一个对数组本身的引用。这里有一个例子:



```Javascript
function displayElements (element, i, array) {
    console.log(array.toString());
}
```



　　它会把数组里的元素都输出显示,例如:




```Javascript
jupiter, venus, saturn, mars
```



　　在大多数情况下,你可能只需要使用遍历循环而不需要回调函数。在这种情况下,您可以使用forEach的匿名回调函数,如下:



```JavaScript
let planets = ["jupiter", "venus", "saturn", "mars"];
planets.forEach((planet) => {
  console.log(planet);
});
```



　　之所以称为匿名函数是因为没有指定函数的名字。当然为了简洁还可以这么写:



```JavaScript
planets.forEach(planet => console.log(planet));
```


　　当你处理数组时，这个写将可以提高效率，但是可读性会降低。




### for循环



```JavaScript
for (let planet of planets) {
  console.log(planet);
}
```



**//Displays: "jupiter", "venus", "saturn", "mars"**




　　for循环还允许你在处理一个数组时动态处理另一个数组。这里有一个例子如何处理numbers里的元素到另一个squared数组中存储这些数字的平方:




```JavaScript
let numbers = [1, 2, 3, 4, 5];
let squared = [for (x of numbers) x * x];
console.log(squared);
```



**//Displays: [1, 4, 9, 16, 25]**




　　注意,你不需要使用花括号。阵列解析提供了一个方便紧凑的语法用于写数学表达式。



### 遍历Object对象




　　JavaScript有许多方法,让你在循环对象的时候就像循环数组一样简单。如果你想得到一个对象的所有属性,您可以使用Object.keys()函数。它把对象的所有属性以字符串的形式存到一个数组里。(一个object的“key”就是它的属性名。)可以这样使用它:




```JavaScript
Object.keys(anyObject);
```



　　这段代码返回一个存储着object的属性名的数组,包含anyObject所有的属性名。



 ***
■ **注意** Object.keys将只返回的对象的**枚举属性**。可枚举属性可以是你可以在一个对象中看到的任何普通属性。这些通常是最你关心的。但是一个object也可以有隐藏的属性,被称为**不可枚举属性**。Object.keys不会显示他们,如果你想知道怎样何写一个房地产不可枚举属性,你可以看后面的章节。查看nonenumerable属性只需要用Object.getOwnPropertyNames就可以了
 ***






 　　这里有个实际的例子告诉你如何使用对象的键。想象你在一场冒险游戏中,使用room对象。你的room对象里在游戏中需要维持一个room的状态,像这样:






```JavaScript
 let room = {
  door: "open",
  light: "on",
  contents: ["carpet", "mouse", "katana"]
};
```




　　你可以看到room有三个属性。你可以把这些属性作为一个包含字符串的数组:



```JavaScript
console.log(Object.keys(room));
```



　　将显示：


["door", "light", "contents"]



　　这很有趣,但不实用,但是当你把它与forEach一起使用时，Object.keys就变得非常实用:




```JavaScript
Object.keys(room).forEach(key => {
  let value = room[key];
  console.log("key: " + key + ", value: " + value);
});
```




　　这段代码将显示如下:



```JavaScript
key: door, value: open
key: light, value: on
key: contents, value: carpet,mouse,katana
```





　　你可以访问键访问属性的值。它可以把你的游戏逻辑应用到你的任何room里,它的状态或者内容。



 ***
■ **注意** 如果你要检查一个对象里是否包含某个属性,使用hasOwnProperty(),像这样:



```JavaScript
if(room.hasOwnProperty("light")) { ... }
```
 ***



　　如果你喜欢,你可以使用一个循环来做同样的事情:



```JavaScript
let roomProperties = Object.keys(room);
for (let key of roomProperties) {
  let value = room[key];
  console.log("key: " + key + ", value: " + value);
}
```




　　输出是和第一个例子完全相同的。还有一个方法!我们可以用JavaScript 1.0的循环方式。下面是如何使用它来生成与前面的例子相同的输出:




```JavaScript
for(let key in room) {
  let value = room[key];
  console.log("key: " + key + ", value: " + value);
}
```



　　如果你使用一个循环,有两个要注意的地方。首先,它遍历出来的对象的键是无序的。如果顺序对你很重要,你要注意。其次,它将遍历对象的键和它的原型(请参阅本章后面的“对象”关于对象的原型的更多信息)。如果您只需要保证对象的属性被访问时,您必须测试对象的hasOwnProperty方法在另外的一个If语句里。



```JavaScript
for(let key in room) {
  if (room.hasOwnProperty(key) {
    let value = room[key];
    console.log("key: " + key + ", value: " + value);
  }
}
```



　　这些看起来很满发,根据你知道的对象属性去遍历Object。但是如果你想要确保安全,Object.keys 和forEach组合更方便。



### 遍历数组的某些元素




　　你可能只是想遍历一个数组里你正在寻找的某一个元素。当你找到它的时候,循环应该停止。你可以用某些方法。你可以用一个**some**方法做到这一点。some方法将检查数组中的所有元素，直到回调函数返回true。一旦返回true，它就立即退出循环。





下面的数组列出了五种乐器。


```JavaScript
let instruments = ["guitar", "piano", "tabla", "ocarina", "tabla"];
```


　　你看到tabla出现了两次吗?,这将有助于说明same方法是如何工作的。现在让我们使用some方法是否能找到这个数组的tabla:



```JavaScript
instruments.some(find);
function find(instrument) {
  if (instrument === "tabla") {
    console.log("Tabla found!");
    return true;
  } else {
    console.log("No tabla found...");
    return false;
  }
}
```


　　运行时，some方法遍历instruments这个数组，当它找到的第一个tabla退出。因为函数返回true。在控制台将显示：



```JavaScript
No tabla found...
No tabla found...
Tabla found!
```




　　它找到第一个tabla就立即停止，并没有继续检查。这和使用for循环的break语句达到了同样的效果。  

　　您可以使用some的匿名回调,就像forEach一样。此外,false是可选的。这意味着你可以让所有代码更加紧凑:



```JavaScript
let instruments = ["guitar", "piano", "tabla", "ocarina", "tabla"];
let found = instruments.some(instrument => {
  if (instrument === "tabla") {
    return true;
  }
});
if (found) {
  console.log("tabla found!");
}
```



　　或者，你可以把它写的更简洁:



```JavaScript
let found = instruments.some(instrument => instrument === "tabla");
if (found) console.log("tabla found!");
```



　　some方法非常有用,如果你想通过一定的测试找出数组中是否有某个元素。例如，你可以用它来检查数组中的任意值是否在大于100：




```JavaScript
let numbers = [11, 43, 9, 112, 64, 15];
let tooBig = numbers.some((number) => {
  //Return true if a number is greater than 100
  return number > 100;
});
console.log(tooBig);
```



　　这段代码将在控制台输出 true。这里有一个更紧凑的版本做同样的事:



```JavaScript
let tooBig = numbers.some(number => number > 100);
```



　　由于循环只包含一个参数，一个语句，你可以省略括号和大括号。此外，return是默认的，所以你完全可以省略。  
数组还有一个方法叫 **every**，当函数返回false退出循环,这和some是完全相反的。如果你认为false更好匹配你的测试逻辑最好使用every，而不是some。



 ***
■ **注意** 如果你只需要检查一个数组是否包含一个元素，使用**indexOf**，像这样：



```JavaScript
if (instruments.indexOf("tabla") !== -1) {//Tabla found!}
```


或者你可以使用**findIndex**,在下一节中会讲到。
 ***



### 查找数组元素




　　数组的some方法实际上是ES5的特性。ES6有一系列新方法叫做**find**,find可以找到数组中的特定元素。它的用法和some一样,但它返回元素的全部值,不仅仅是true或false。下面是如何使用find:



```JavaScript
let instruments = ["guitar", "piano", "tabla", "ocarina", "tabla"];

let found = instruments.find(x => x === "tabla");

console.log(found);

//Displays: tabla
```




　　和some不同，find方法退出并返回第一个与条件相匹配的元素。如果条件不能满足,find返回undefined。



　　如果你需要知道一个元素的索引位置,使用findIndex:




```JavaScript
let index = instruments.findIndex(x => x === "tabla");

console.log(index);

//Displays: 2
```



　　这是两个有用的新方法,可以让数组变得更有趣。当然还有有很多!




### 数组映射




　　数组映射有时是很有用。JavaScript有一个**map**方法。这里有一个例子用map创建一个基于现有数组的新的、改变过的数组。



```JavaScript
let words = ["fun", "boring", "exciting"];
let betterWords = words.map(improveGrammar);
function improveGrammar(word) {
  return word + "ish";
}
console.log(betterWords);
```



　　显示如下:



funish, boringish, excitingish



　　map方法使用现有数组来创建一个新的数组betterWords,看起来像这样:





["funish", "boringish", "excitingish"]




　　我相信你能返现，这大大提高了效率!map方法与some方法使用相同的语法,让你可以使用任何你在上一节中看到的语法排列。下面是使用映射的方法以紧凑的方式达到和前面的代码相同的结果：




```JavaScript
let betterWords = words.map(x => x + "ish");
```




　　很顺利!使用map方法并不是实现这个结果的唯一方式。你可以用数组中循环做同样的事情:




```JavaScript
let betterWords = [for (word of words) word + "ish"];
```




　　结果是完全一样的。不同的仅仅是语法上的区别,所以你可以使用你喜欢的任何方式去实现。





### 数组切割




　　你要切出一个数组的某些元素，你可以使用**filter**方法。例如，你可以一组号码，并希望把所有大于100的数字复制到一个新的数组里。您可以使用filter方法来做到这一点，如下所示：





```JavaScript
let numbers = [11, 43, 9, 112, 64, 312, 92];
let bigNumbers = numbers.filter(findBigNumbers);
function findBigNumbers (number) {
  return number > 100;
}

console.log(bigNumbers);
```




　　你现在有一个新数组叫做bigNumbers:



[112, 312]




　　下面是数组的方式,做同样的事:




```JavaScript
bigNumbers = [for (number of numbers) if (number > 100) number];
```




　　filter方法另一个非常有用的应用，它可以很容易地切出一个数组的元素。这类似于使用数组的**splice**方法，但它让代码更简单。  
这样做的诀窍是分配新过滤好的数组回原来的数组。下一个例子会让你更清楚。下面是如何从数组里去掉所有大于100的数字:



```JavaScript
let numbers = [11, 43, 9, 112, 64, 312, 92];
numbers = numbers.filter(x => x < 100);
console.log(numbers);
```



　　下面是最终的数组。所有的数字大于100已被移除:





11,43,9,64,92






　　你有没有注意到数组是如何被复制回本身的?



```JavaScript
numbers = numbers.filter(x => x < 100);
```



　　悄悄的不要告诉别人！
　　下面是数组的理解版本：



```JavaScript
numbers = [for (number of numbers) if (number < 100) number];
```






　　用一个for遍历和切割数组的元素的方法，这些技术有什么优势吗?那就是你不必循环向后或手动递减计数器变量来补偿被去除的元素。不要担心,从数组中删除元素的技术与老式的for循环和切割的方法仍有它的位置,在第七章的碰撞检测中你会看到。





### 将数组元素变为单个值




　　**reduce**方法允许你将一个数组中的所有元素变成一个值。例如,你有一组数字,想知道它们的总和是多少。你可以做到这一点，如下所示：




```JavaScript
let numbers = [73, 19, 2, 144, 43, 7];
let total = numbers.reduce(addNumbersTogether);
function addNumbersTogether(a, b) {
  return a + b;
}
console.log(total);
```


　　输出：



288




　　简洁一点：




```JavaScript
total = numbers.reduce((a, b) => a + b);
```



　　reduce方法通过遍历每个元素与右边相邻的元素相加。在这个例子中,a是第一个元素,b是下次要循环到的元素。一直这样继续下去直到它减少为单一值。reduce的第二个可选参数:初始值。下面是一个初始值为100例子:




```JavaScript
total = numbers.reduce((a, b) => a + b, 100);
```




　　现在总和是388。  
　　reduce有一些令人惊叹的用途。有一个二维数组,你希望可以变成一个一维数组?这用reduce很容易完成。方法如下:



```JavaScript
let numbers2D = [[73, 19],[2, 144],[43, 7]];
let numbers1D = numbers2D.reduce(flattenArray);
function flattenArray(a, b) {
  return a.concat(b);
}

console.log(numbers1D);
```





　　最终得到的numbers1D数组是这样的:




[73, 19, 2, 144, 43, 7]





　　reduce依次减少从右到左的循环。如果你需要从末位开始循环数组,使用减少的姊妹方法**reduceRight**。你现在有很多新的方法处理数组元素。如果你想快速分配给变量一个数组中的值?



