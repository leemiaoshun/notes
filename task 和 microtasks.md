```
console.log('script start');
setTimeout(function() {
  console.log('setTimeout');
}, 0);
Promise.resolve().then(function() {
  console.log('promise1');
}).then(function() {
  console.log('promise2');
});
console.log('script end');



script start
script end
promise1
promise2
setTimeout
```


- 每个线程都有自己的事件循环，所以每个 web worker 有自己的事件循环（==event loop==），所以它能独立地运行。而所有同源的 window 共享一个事件循环，因为它们能同步的通讯。事件循环持续运行，执行 tasks 列队。一个事件循环有多个 task 来源，并且保证在 task 来源内的执行顺序，在每次循环中浏览器要选择从哪个来源中选取 task，这使得浏览器能优先执行敏感 task，例如用户输入。
- Tasks 被列入队列，于是浏览器能从它的内部转移到 Javascript/DOM 领地，并且确使这些 tasks 按序执行。在 tasks 之间，浏览器可以更新渲染。来自鼠标点击的事件回调需要安排一个 task，解析 HTML 和 setTimeout 同样需要。
- Mircotasks 通常用于安排一些事，它们应该在正在执行的代码之后立即发生，例如响应操作，或者让操作异步执行，以免付出一个全新 task 的代价。mircotask 队列在回调之后处理，只要没有其它执行当中的（mid-execution）代码；或者在每个 task 的末尾处理。在处理 microtasks 队列期间，新添加的 microtasks 添加到队列的末尾并且也被执行。 microtasks 包括 mutation observer 回调。


### tasks 按序执行，浏览器会在 tasks 之间执行渲染。

### microtasks 按序执行，在下面情况时执行：

  1.在每个回调之后，只要没有其它代码正在运行。
  
  2.在每个 task 的末尾。
