### javascript整理
***
#### addLoadEvent
页面加载完成后执行 `func` 函数
```javascript
function addLoadEvent(func) {
  var oldonload = window.onload;
  if (typeof window.onload != 'function') {
    window.onload = func;
  } else {
    window.onload = function() {
      oldonload();
      func();
    }
  }
}

addLoadEvent(func)
```
#### insertBefore
把一个新元素插入到一个现有元素的前面
* 新元素：想插入的元素 `newElement`
* 目标元素：想把这个新元素插入到哪个元素 `targetElement` 之前
* 父元素：目标元素的父元素 `parentElement`
```javascript
parentElement.insertBefore(newElement, targetElement);
```

#### insertAfter
把一个新元素插入到一个现有元素的前面 (自定义方法)
```javascript
function insertAfter(newElement, targetElement) {
  var parent = targetElement.parentNode;
  if (parent.lastChild == targetElement) {
    parent.appendChild(newElement);
  } else {
    //nextSibling：目标元素的下一个兄弟元素
    parent.insertBefore(newElement, targetElement.nextSibling);
  }
}
```
#### getNextElement
获取下一个元素节点
```javascript
function getNextElement(node) {
  if (node.nodeType == 1) {
    return node;
  }
  if (node.nextSibling) {
    return getNextElement(node.nextSibling);
  }
  return null;
}
```
#### addClass
添加class
```javascript
function addClass(element, class) {
  //className 替换原有的class，而不是追加class
  if (!element.className) {
    element.className = class;
  } else {
    element.className = element.className + " " + class;
  }
}
```
#### label语句
加标签的语句一般都要与 for 语句等循环语句配合使用。由 break 或 continue 语句引用
```javascript
label: statement

var num = 0;
outermost:
for (var i = 0; i < 10; i++) {
  for (var j = 0; j < 10; j++) {
    if (i == 5 && j == 5) {
      break outermost;
    }
  }
}
console.log(num)  //55
--------------------------------------------
var num = 0;
outermost:
for (var i = 0; i < 10; i++) {
  for (var j = 0; j < 10; j++) {
    if (i == 5 && j == 5) {
      continue outermost;
    }
  }
}
console.log(num) //95
```
#### Array
```javascript
//监测数组 instanceof  Array.isArray()
/*
instanceof操作符的问题在于，它假定只有一个全局执行环境。如果网页中包含多个框架，那实
际上就存在两个以上不同的全局执行环境，从而存在两个以上不同版本的 Array 构造函数。如果你从
一个框架向另一个框架传入一个数组，那么传入的数组与在第二个框架中原生创建的数组分别具有各自
不同的构造函数。
Array.isArray()确定某个值到底是不是数组，而不管它是在哪个全局执行环境中创建
*/
if (value instanceof Array) {  //ECMAScript3
  //对数组执行某些操作
}
if (Array.isArray(value)) {  //ECMAScript5
  //对数组执行某些操作
}

--------------------------------------------

//join() 返回所有数组项的字符串
var colors = ['red','green','blue'];
console.log(colors.join(','))  //red,green,blue
console.log(colors.join('||')) //red||green||blue

--------------------------------------------

//push() 添加到数组末尾，并返回数组长度
var colors = new Arrar();
var count = colors.push('red','green');
console.log(count);   //2
console.log(colors);  //['red','green']

--------------------------------------------

//pop() 从数组末尾移除最后一项，并返回当前移除的项
var colors = ['red','green','black'];
var item = colors.pop();
console.log(item);  //black
console.log(colors.length)  //2

--------------------------------------------

//shift() 移除数组中的第一个项，并返回当前移除的项
var colors = ['red','green','black'];
var item = colors.shift();
console.log(item)  //red
console.log(colors.length)  //2

--------------------------------------------

//unshift() 在数组前端添加任意个项，并返回新数组的长度
var colors = ['black'];
var count = colors.unshift('red','green');
console.log(count)  //3
console.log(colors)  //['red','green','black']

--------------------------------------------

//reverse() 反转数组项的顺序
var values = [1,2,3,4,5];
values.reverse();
console.log(values)  //[5,4,3,2,1]

--------------------------------------------

//sort() 排序(默认按升序(从小到大)排列数组)
//sort()方法可以接受一个比较函数作为参数
function compare(value1,value2) {
  if (value1 < value2) {
    return -1;
  } else if (value > value2) {
    return 1;
  }else{
    0
  }
}
var values = [0,10,5,1,15];
value.sort(compare);
console.log(values);  //[0,1,5,10,15]

--------------------------------------------

//concat() 方法会先创建当前数组一个副本，
//然后将接收到的参数添加到这个副本的末尾，最后返回新构建的数组
var colors = ['red','green','blue'];
var colors2 = colors.concat('yellow',['black','brown']);
console.log(colors2)  //['red','green','blue','yellow','black','brown']

--------------------------------------------

//slice() 能够基于当前数组中的一或多个项创建一个新数组
//slice()方法可以接受一或两个参数，即要返回项的起始和结束位置
//slice()方法不会影响原始数
var colors = ["red", "green", "blue", "yellow", "purple"];
var colors2 = colors.slice(1);
var colors3 = colors.slice(1,4);
var colorsCopy = colors.slice();
console.log(colors2)  //['green','blue','yellow','purple']
console.log(colors3)  //['green','blue','yellow']
console.log(colorsCopy)  //["red", "green", "blue", "yellow", "purple"]

--------------------------------------------

//splice() 向数组的中部插入项
//splice()方法始终都会返回一个数组，该数组中包含从原始数组中删除的项（如果没有删除任何项，则返回一个空数组）
//删除:可以删除任意数量的项，只需指定 2 个参数：要删除的第一项的位置和要删除的项数
var colors = ['red','green','blue'];
var removed = colors.splice(0,1);
console.log(colors)  //['green','blue']
console.log(removed)  //['red']
//插入:可以向指定位置插入任意数量的项，只需提供 3 个参数：起始位置、 0（要删除的项数）
//和要插入的项。如果要插入多个项，可以再传入第四、第五，以至任意多个项
var colors = ['red','green','blue'];
var removed = colors.splice(1,0,'yellow','orange');
console.log(colors)  //["red", "yellow", "orange", "green", "blue"]
console.log(removed)  //[] 空数组
//替换：可以向指定位置插入任意数量的项，且同时删除任意数量的项，只需指定 3 个参数：起
//始位置、要删除的项数和要插入的任意数量的项。插入的项数不必与删除的项数相等。
var colors = ['red','green','blue'];
var removed = colors.splice(1,1,'white','black');
console.log(colors)  //['red','white','black','blue']
console.log(removed)  //["green"]

--------------------------------------------

//indexOf()和 lastIndexOf() 这两个方法都接收两个参数：要查找的项和（可选的）表示查找起点位置的索引。
//indexOf()方法从数组的开头（位置 0）开始向后查找
//lastIndexOf()方法则从数组的末尾开始向前查找。
var numbers = [1,2,3,4,5,4,3,2,1];
console.log(numbers.indexOf(4))  //3
console.log(numbers.lastIndexOf(4))  //5

--------------------------------------------

//迭代方法
//every()：对数组中的每一项运行给定函数，如果该函数对每一项都返回 true，则返回 true。
//filter()：对数组中的每一项运行给定函数，返回该函数会返回 true 的项组成的数组。
//forEach()：对数组中的每一项运行给定函数。这个方法没有返回值。
//map()：对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组。
//some()：对数组中的每一项运行给定函数，如果该函数对任一项返回 true，则返回 true。
//以上方法都不会修改数组中的包含的值。
var numbers = [1,2,3,4,5,4,3,2,1];
var everyResult = numbers.every(function(item,index,array){
  return item > 2;
});
console.log(everyResult)  //false  每一项都返回 true，则返回 true。

var someResult = numbers.some(function(item,index,array){
  return item > 2;
});
console.log(someResult)  //true  对任一项返回 true，则返回 true。

var filterResult = numbers.filter(function(item,index,array){
  return item > 2;
});
console.log(filterResult)  //[3,4,5,4,3]

var mapResult = numbers.map(function(item, index, array){
  return item * 2;
});
alert(mapResult);  //[2,4,6,8,10,8,6,4,2]

//forEach没有返回值，类似for循环迭代数组
numbers.forEach(function(item, index, array){
  //执行某些操作
});

--------------------------------------------

//归并方法
//reduce() reduceRight() 都会迭代数组的所有项，然后构建一个最终返回的值
var values = [1,2,3,4,5];
var reduceSum = values.reduce(function(prev, cur, index, array){
  return prev + cur; //(prev:1,cur:2) (prev:3,cur:3) (prev:6,cur:4) (prev:10,cur:5)
});
console.log(reduceSum);  //15

var reduceRightSum = values.reduceRight(function(prev, cur, index, array){
  return prev + cur; //(prev:5,cur:4) (prev:9,cur:3) (prev:12,cur:2) (prev:14,cur:1)
});
console.log(reduceRightSum);  //15
```
### 函数内部属性
函数内部，有两个特殊对象`arguments`和`this`
```javascript
//arguments 的主要用途是保存函数参数，但这个对象还有一个名叫 callee 的属性，该属性是一个指针，指向拥有这个 arguments 对象的函数
//阶乘函数
function factorial(num) {
  if (num <= 1) {
    return 1;
  } else {
    return num * factorial(num-1);
  }
}
等同于
function factorial(num) {
  if (num <=1 ) {
    return 1;
  } else {
    return num * arguments.callee(num-1);
  }
}

//this引用的是函数据以执行的环境对象——或者也可以说是 this 值（当在网页的全局作用域中调用函数时，this 对象引用的就是 window）
window.color = "red";
var o = { color: "blue" };
function sayColor(){
  console.log(this.color);
}
sayColor();  //red   this指向window
o.sayColor = sayColor;
o.sayColor();  //blue
```
### 函数属性和方法
每个函数都包含两个属性：`length`和`prototype`
`length`属性表示函数希望接受的命名参数的个数
```javascript
function sayName(name) {
  console.log(name);
}
function sum(num1, num2) {
  console.log(num1 + num2);
}
function sayHi() {
  console.log("hi");
}
console.log(sayName.length);  //1
console.log(sum.length);  //2
console.log(sayHi.length);  //0
```
`prototype`是保存所有实例方法的真正所在
每个函数都包含两个非继承而来的方法：`apply()`和`call()`
#### apply
`apply()`方法接受两个参数：一个是在其中运行函数的作用域，另一个是参数数组。
其中，第二个参数可以是`Array`的实例，也可以是`arguments`对象
```javascript
function sum(num1 + num2) {
  return num1 + num2;
}
function callSum1(num1 + num2) {
  return sum.apply(this, arguments);
}
function callSum2(num1 + num2) {
  return sum.apply(this, [num1, num2]);
}
console.log(callSum1(10,10));  //20
console.log(callSum2(10,10));  //20
```
#### call
`call()`与`apply()`的作用相同，区别仅在于接收参数的方式不同。对于`call()`方法而言，第一个参数是 this 值没有变化，变化的是其余参数都直接传递给函数
```javascript
function sum(num1 + num2) {
  return num1 + num2;
}
function callSum(num1 + num2) {
  return sum.call(this, num1, num2);  //必须明确地传入每一个参数
}
console.log(callSum(10,10));  //20
```
`call()`和`apply()`真正强大的地方是能够扩充函数赖以运行的作用域。
```javascript
window.color = 'red';
var o = {color: 'blue'};
function sayColor() {
  console.log(this.color);
}
sayColor();  //red
sayColor.call(this);  //red
sayColor.call(window);  //red
sayColor.call(o);  //blue  此时函数体内的 this 对象指向了 o
```
#### bind
`bind()`方法会创建一个函数的实例，其 this 值会被绑定到传给 bind()函数的值。
```javascript
window.color = "red";
var o = { color: "blue" };
function sayColor(){
  console.log(this.color);
}
var objectSayColor = sayColor.bind(o);
objectSayColor();  //blue
```
#### string
字符串操作方法：`concat()` `slice()` `substr()` `subString()`
```javascript
//concat()将一或多个字符串拼接起来，返回拼接得到的新字符串。
var stringValue = "hello ";
var result = stringValue.concat("world");
var result2 = stringValue.concat("world", "!");
console.log(result);  //"hello world"
console.log(result2);  //"hello world!"
console.log(stringValue);  //"hello"

//slice()、 substr()和 substring() 都会返回被操作字符串的一个子字符串，而且也都接受一或两个参数。
//slice()和substring()的第二个参数指定的是子字符串最后一个字符后面的位置。而 substr()的第二个参数指定的则是返回的字符个数。
var stringValue = "hello world";
console.log(stringValue.slice(3));  //"lo world"
console.log(stringValue.substring(3));  //"lo world"
console.log(stringValue.substr(3));  //"lo world"
console.log(stringValue.slice(3, 7));  //"lo w"
console.log(stringValue.substring(3,7));  //"lo w"
console.log(stringValue.substr(3, 7));  //"lo worl"  substr第二个参数指定的是要返回的字符个数
//参数是负值
var stringValue = "hello world";
console.log(stringValue.slice(-3));  //"rld"
console.log(stringValue.substring(-3));  //"hello world"
console.log(stringValue.substr(-3));  //"rld"
console.log(stringValue.slice(3, -4));  //"lo w"
console.log(stringValue.substring(3, -4));  //"hel"
console.log(stringValue.substr(3, -4));  //""（空字符串）
```
`trim()`方法。创建一个字符串的副本，删除前置及后缀的所有空格，然后返回结果。
```javascript
var stringValue = " hello world ";
var trimmedStringValue = stringValue.trim();
console.log(stringValue); //" hello world "
console.log(trimmedStringValue); //"hello world"
```
#### Math对象
`min()` 和 `max()` 方法

```javascript
var max = Math.max(3, 54, 32, 16);
console.log(max); //54
var min = Math.min(3, 54, 32, 16);
console.log(min); //3
//也可以使用apply()方法
var values = [1,2,3,4,5,6,7];
var max = Math.max.apply(Math, values); //把 Math 对象作为 apply()的第一个参数，从而正确地设置 this 值
console.log(max);  //7
```
`Math.ceil()` `Math.floor()`和`Math.round()`方法
* Math.ceil()执行向上舍入，即它总是将数值向上舍入为最接近的整数；
* Math.floor()执行向下舍入，即它总是将数值向下舍入为最接近的整数；
* Math.round()执行标准舍入，即它总是将数值四舍五入为最接近的整数。

```javascript
console.log(Math.ceil(25.9));  //26
console.log(Math.ceil(25.5));  //26
console.log(Math.ceil(25.1));  //26

console.log(Math.round(25.9));  //26
console.log(Math.round(25.5));  //26
console.log(Math.round(25.1));  //25

console.log(Math.floor(25.9));  //25
console.log(Math.floor(25.5));  //25
console.log(Math.floor(25.1));  //25
```
`random()`方法返回大于等于 0 小于 1 的一个随机数

#### location对象
`location` 对象是很特别的一个对象，因为它既是 `window` 对象的属性，也是 `document` 对象的属性；
`window.location` 和 `document.location` 引用的是同一个对象。

`location`对象所有属性

| 属性名 | 例子 | 说明 |
| ------ | ------ | ------ |
| `location.hash` | "#contents" | 返回URL中的hash(#后跟零或多个字符)，如果URL中不包含散列，则返回空字符串 |
| `location.host` | "www.baidu.com:80" | 返回服务器名称个端口号(如果有) |
| `location.hostname` | "www.baodu.com" | 返回不带端口号的服务器名称 |
| `location.href` | "http://www.baidu.com" | 返回当前加载页面完整的URL(`location.toString()`方法也返回这个值) |
| `location.pathname` | "/test/" | 返回URL中的目录和(或)文件名 |
| `location.port` | "8080" | 返回URL中指定的端口号。如果不包含端口号则返回空字符串 |
| `location.portocol` | "http:" | 返回页面使用的协议(http: 或 https:) |
| `location.search` | "?keyword=test" | 返回URL的查询字符串。这个字符串以问好开头 |
```javascript
//假设初始 URL 为 http://www.wrox.com/WileyCDA/
//将 URL 修改为"http://www.wrox.com/WileyCDA/#section1"
location.hash = "#section1";
//将 URL 修改为"http://www.wrox.com/WileyCDA/?q=javascript"
location.search = "?q=javascript";
//将 URL 修改为"http://www.yahoo.com/WileyCDA/"
location.hostname = "www.yahoo.com";
//将 URL 修改为"http://www.yahoo.com/mydir/"
location.pathname = "mydir";
//将 URL 修改为"http://www.yahoo.com:8080/WileyCDA/"
location.port = 8080;

//获取查询字符串(URL)参数
function getQueryStringArgs(){
  //取得查询字符串并去掉开头的问好
  var qs = (location.search.length > 0 ? location.search.subString(1) : "");
  //保存的对象
  var args = {};
  //取得每一项
  var items = qs.length ? qs.split("&") : [];
  var item = null, name = null, value = null, i = 0, len = items.length;
  for (i=0; i < len; i++) {
    item = items[i].split("=");
    //decodeURIComponent解码查询字符串
    name = decodeURIComponent(item[0]);
    value = decodeURIComponent(item[1]);
    if (name.length) {
      args[name] = value;
    }
  }
  return args;
}
//查询字符串是?q=javascript&num=10
var args = getQueryStringArgs();
console(args["q"]);  //"javascript"
console(args["num"]);  //"10
```

#### DOM拓展
选择符API核心方法(Selectors API Level 1)：`querySelector()`和`querySelectorAll()`,在兼容的浏
览器中，可以通过`Document`及`Element`类型的实例调用它们。

 `querySelector()`方法接受一个CSS选择符，返回与该模式匹配的第一个元素，没找到则返回`null`
 ```javascript
//取得body元素
var body = document.querySelector('body');
//取得ID为‘myDiv’的元素
var myDiv = document.querySelector('#myDiv');
//取得类为‘selected’的第一个元素
var selected = document.querySelector('.selected');
//取得类为'button'的第一个图像元素
var img = document.querySelector('img.button');
 ```
 `querySelectorAll()`返回的是一个`NodeList`的实例,没找到则`NodeList`为空
 ```javascript
 //取得某<div>中的所有<em>元素（类似于 getElementsByTagName("em")）
var ems = document.getElementById("myDiv").querySelectorAll("em");
//取得类为"selected"的所有元素
var selecteds = document.querySelectorAll(".selected");
//取得所有<p>元素中的所有<strong>元素
var strongs = document.querySelectorAll("p strong");
 ```
>(Selectors API Level 2)规范为`Element`类型新增了一个方法`matchesSelector()`,这个方法接收
一个参数，即 CSS 选择符，如果调用元素与该选择符匹配，返回 true；否则，返回 false。
