> 简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息

## 含义
### 特点
1.对象的状态不受外界影响。``Promise``对象代表一个异步操作，有三种状态：``pending``（进行中）、``fulfilled``（已成功）和``rejected``（已失败）。只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。这也是``Promise``这个名字的由来，它的英语意思就是“承诺”，表示其他手段无法改变。

2.一旦状态改变，就不会再变，任何时候都可以得到这个结果。Promise对象的状态改变，只有两种可能：从 `` pending``变为``fulfilled``和从``pending``变为``rejected``。只要这两种情况发生，状态就凝固了，不会再变了，会一直保持这个结果，这时就称为 ``resolved``（已定型）。如果改变已经发生了，你再对``Promise``对象添加回调函数，也会立即得到这个结果。这与事件（Event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。

### 缺点
1.无法取消（一旦新建就会立即执行，无法中途取消）

2.如果不设置回调函数，``promise`` 内部反应的错误无法反映到外部

3.当处于 ``pending``（进行中）状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）

## 用法
> Promise对象是一个构造函数，用来生成Promise实例

```
const promise = new Promise(function(resolve, reject) {
  // 
  if (ERR_OK){
    resolve(value);
  } else {
    reject(error);
  }
});
```

- ``resolve``函数的作用是，将``Promise``对象的状态从“未完成”变为“成功”（即从 pending 变为 resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去；``reject``函数的作用是，将``Promise``对象的状态从“未完成”变为“失败”（即从 pending 变为 rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。

```
promise.then(function(res){},function(err){})
```

- Promise实例生成以后，可以用**then**方法分别指定``resolved``状态和``rejected``状态的回调函数。**then**方法可以接受两个回调函数作为参数。第一个回调函数是``Promise``对象的状态变为``resolved``时调用，第二个回调函数是``Promise``对象的状态变为``rejected``时调用。其中，第二个函数是可选的，不一定要提供。这两个函数都接受``Promise``对象传出的值作为参数。

- ==Promise.protototype.then()== 
> ``then``方法返回的是一个新的``Promise``实例（不是原来那个``Promise``实例）。因此可以采用链式写法，即``then``方法后面再调用另一个``then``方法。

- ==Promise.protototype.catch()== 
> ``Promise.prototype.catch``方法是``.then(null, rejection)``的别名，用于指定发生错误时的回调函数。

- ==Promise.protototype.finally()== 
> ``finally``方法用于指定不管 ``Promise`` 对象最后状态如何，都会执行的操作。该方法是 ``ES2018`` 引入标准的。(所以我写了es8了已经？？？？) ``finally``方法的回调函数不接受任何参数，无法得知前面的 ``Promise`` 状态到底是``fulfilled``还是``rejected``。这表明，``finally``方法里面的操作，应该是与状态无关的，不依赖于 ``Promise`` 的执行结果。(我一般用来关闭 loading )

- ==Promise.all()==
> 用于将多个 Promise 实例，包装成一个新的 Promise 实例。
```
const p = Promise.all([xhr1, xhr2, xhr3]);
```
    1.只有xhr1、xhr2、xhr3的状态都变成==fulfilled==，p的状态才会变成==fulfilled==，此时xhr1、xhr2、xhr3的返回值组成一个数组，传递给p的回调函数。
    2.只要xhr1、xhr2、xhr3之中有一个被rejected，p的状态就变成rejected，此时第一个被reject的实例的返回值，会传递给p的回调函数。
    
-  ==Promise.race()==
> 同 promise.all 不同的是，顾名思义，只要有参数中的 promise 实例有一个发生了改变 就会传递给 p 进行赋值

-  ==Promise.resolve()==
> 将现有对象转为 Promise 对象

-  ==Promise.reject()==
> ``Promise.reject(reason)``方法也会返回一个新的 Promise 实例，该实例的状态为``rejected``。

-  ==Promise.reject()==
> ``Promise.reject(reason)``方法也会返回一个新的 Promise 实例，该实例的状态为``rejected``。

- ==Promise.try()==
> 