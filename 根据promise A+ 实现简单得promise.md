
- 解决（fulfill）：指一个 promise 成功时进行的一系列操作，如状态的改变、回调的执行。虽然规范中用 fulfill 来表示解决，但在后世的 promise 实现多以 resolve 来指代之。
- 拒绝（reject）：指一个 promise 失败时进行的一系列操作。
- 终值（eventual value）：指 promise 被解决时传递给解决回调的值，由于 promise 有一次性的特征，因此当这个值被传递时，标志着 promise 等待态的结束，故称之终值，有时也直接简称为值（value）。
- 据因（reason）：也就是拒绝原因，指在 promise 被拒绝时传递给拒绝回调的值。


### Promise
> promise 是一个拥有 ``then``方法得对象或函数

### thenable
> 定义了一个 ``then`` 方法得对象或函数

### 值（value）
> 指任何 JavaScript 的合法值（包括 ``undefined`` , thenable 和 promise）

### 异常（exception）
> 是使用 ``throw`` 语句抛出的一个异常值

### 据因（reason）
> 表示为什么 promise 被拒绝得原因。


## then 方法

> 一个 promise 必须提供一个 then 方法以访问其当前值、终值和据因

```
promise.then(onFulfilled, onRejected)
```

- 返回 then 方法必须返回一个 promise 对象 

```
promise2 = promise1.then(onFulfilled, onRejected)
```

- 不论 promise1 被 reject 还是被 resolve 时 promise2 都会被 resolve，只有出现异常时才会被 rejected








```
额外得收获
macro-task: script（整体代码）, setTimeout, setInterval, setImmediate, I/O, UI rendering
micro-task: process.nextTick, Promises（原生 Promise）, Object.observe, MutationObserver
```