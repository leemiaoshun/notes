对数组中的所有元素调用指定的回调函数。该回调函数的返回值为累积结果，并且此返回值在下一次调用该回调函数时作为参数提供。

#### 语法

```
array1.reduce(callbackfn[, initialValue])
```

#### 参数

参数  | 定义
---|---
array1      | 必需。一个数组对象。
callbackfn  | 必需。一个接受最多四个参数的函数。对于数组中的每个元素，reduce 方法都会调用 callbackfn 函数一次。
initialValue | 可选。如果指定 initialValue，则它将用作初始值来启动累积。第一次调用 callbackfn 函数会将此值作为参数而非数组值提供。

#### 返回值

通过最后一次调用回调函数获得的累积结果。

#### 异常

当满足下列任一条件时，将引发 TypeError 异常：

    - callbackfn 参数不是函数对象。
    - 数组不包含元素，且未提供 initialValue。
    
### reduce方法同时实现map和filter
（[摘自](https://juejin.im/post/5b51e5d3f265da0f4861143c#heading-21v)）
假设现在有一个数列，你希望更新它的每一项（map的功能）然后筛选出一部分（filter的功能）。如果是先使用map然后filter的话，你需要遍历这个数组两次。 在下面的代码中，我们将数列中的值翻倍，然后挑选出那些大于50的数。

```
const numbers = [10, 20, 30, 40];
const doubledOver50 = numbers.reduce((finalList, num) => {
  num = num * 2;
  if (num > 50) {
    finalList.push(num);
  }
  return finalList;
}, []);
doubledOver50;            // [60, 80]

```

这周没学下什么东西。。。。。
