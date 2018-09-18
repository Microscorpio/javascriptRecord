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

var someResult = numbers.some(function(item.index.array){
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
