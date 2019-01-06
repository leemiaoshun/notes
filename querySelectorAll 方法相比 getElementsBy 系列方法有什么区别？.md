querySelectorAll 相比下面这些方法有什么区别？
- getElementsByTagName
- getElementsByClassName
- getElementsByName

#### 1.W3C标准
querySelectorAll 属于 W3C 中的 [Selectors API](https://www.w3.org/TR/selectors-api2/)规范。而 getElementsBy 系列则属于 W3C 的 [DOM](https://www.w3.org/TR/DOM-Level-3-Core/core.html)规范。

#### 2. 浏览器兼容
querySelectorAll 已被 IE 8+、FF 3.5+、Safari 3.1+、Chrome 和 Opera 10+ 良好支持 。getElementsBy 系列，以最迟添加到规范中的 getElementsByClassName 为例，IE 9+、FF 3 +、Safari 3.1+、Chrome 和 Opera 9+ 都已经支持该方法了。

#### 3. 接收参数
querySelectorAll 方法接收的参数是一个 CSS 选择符。而 getElementsBy 系列接收的参数只能是单一的className、tagName 和 name。代码如下

```
var c1 = document.querySelectorAll('.b1 .c');
var c2 = document.getElementsByClassName('c');
var c3 = document.getElementsByClassName('b2')[0].getElementsByClassName('c');

```
需要注意的是，querySelectorAll 所接收的参数是必须严格符合 CSS 选择符规范的。所以下面这种写法，将会抛出异常。代码如下

```
try {
  var e1 = document.getElementsByClassName('1a2b3c');
  var e2 = document.querySelectorAll('.1a2b3c');
} catch (e) {
  console.error(e.message);
}
console.log(e1 && e1[0].className);
console.log(e2 && e2[0].className);

```
==（CSS 选择器中的元素名，类和 ID 均不能以数字为开头。）==

#### 4. 返回值
大部分人都知道，querySelectorAll 返回的是一个 Static Node List，而 getElementsBy 系列的返回的是一个 Live Node List。

```
// Demo 1
var ul = document.querySelectorAll('ul')[0],
    lis = ul.querySelectorAll("li");
for(var i = 0; i < lis.length ; i++){
    ul.appendChild(document.createElement("li"));
}

// Demo 2
var ul = document.getElementsByTagName('ul')[0], 
    lis = ul.getElementsByTagName("li"); 
for(var i = 0; i < lis.length ; i++){
    ul.appendChild(document.createElement("li")); 
}

```
因为 Demo 2 中的 lis 是一个动态的 Node List， 每一次调用 lis 都会重新对文档进行查询，导致无限循环的问题。而 Demo 1 中的 lis 是一个静态的 Node List，是一个 li 集合的快照，对文档的任何操作都不会对其产生影响。

在 W3C 规范中对 querySelectorAll 方法有明确规定

> The NodeList object returned by the querySelectorAll() method must be static ([DOM], section 8).

NodeList 

> he NodeList interface provides the abstraction of an ordered collection of nodes, without defining or constraining how this collection is implemented. NodeList objects in the DOM are live.

###### NodeList 本质上是一个动态的 Node 集合，只是规范中对 querySelectorAll 有明确要求，规定其必须返回一个静态的 NodeList 对象。

在 chrome 下得返回情况

```
document.querySelectorAll('a').toString();    // return "[object NodeList]"
document.getElementsByTagName('a').toString();    // return "[object HTMLCollection]"

```
这里出现了 HTMLCollection 那么 HTMLCollection  是什么呢？在 w3c 定义如下

```
An HTMLCollection is a list of nodes. An individual node may be accessed by either ordinal index or the node's name or id attributes.Note: Collections in the HTML DOM are assumed to be live meaning that they are automatically updated when the underlying document is changed.

```
实际上，HTMLCollection 和 NodeList 十分相似，都是一个动态的元素集合，每次访问都需要重新对文档进行查询。两者的本质上差别在于，HTMLCollection 是属于 Document Object Model HTML 规范，而 NodeList 属于 Document Object Model Core 规范。

###### NodeList 对象会包含文档中的所有节点，如 Element、Text 和 Comment 等。HTMLCollection  对象只会包含文档中的 Element 节点。另外，HTMLCollection 对象比 NodeList 对象 多提供了一个 namedItem 方法。所以在现代浏览器中，querySelectorAll 的返回值是一个静态的 NodeList 对象，而 getElementsBy 系列的返回值实际上是一个 HTMLCollection 对象 。
