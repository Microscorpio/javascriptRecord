###javascript整理
***
####addLoadEvent
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
####insertBefore
把一个新元素插入到一个现有元素的前面
* 新元素：想插入的元素 `newElement`
* 目标元素：想把这个新元素插入到哪个元素 `targetElement` 之前
* 父元素：目标元素的父元素 `parentElement`
```javascript
parentElement.insertBefore(newElement, targetElement);
```

####insertAfter
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
####getNextElement
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
####addClass
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
####label语句
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
