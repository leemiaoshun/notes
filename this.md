# this
```
function foo () {
	return this.num;
}
let a = {
	num:1
}
console.log(foo.call(a))
```
> this让我们更加优雅的隐式"传递"了一个对象的引用，易于设计api使用this时，会让this自动关联到调用的时候的上下文此处如果不使用this ，就需要显示的把对象传入给当前函数。上下文对象越来越多会使得代码越来越混乱

### 误解
1. this指向自身
2. this指向函数作用域（this在任何情况下都不指向函数的词法作用域）

### 绑定规则
1.默认绑定
```
function foo (){
    console.log(this.a)
}
var a = 2
foo()  // 2
```
> 本例中函数调用时候默认this的默认绑定，此时this指向全局对象（this调用时是没有进行任何修饰的函数引用进行调用的）严格模式下this指向是undefined

2.隐式绑定
```
function(){
    console.log(this.a)
}
var obj = {
    a:2,
    foo:foo
}
obj.foo() // 2
```
> 考虑调用时的位置是否存在上下文对象，或者说被某个对象包含
> 上面的代码中，foo函数在obj对象内部，this就默认指向了存在的上下文对象

3.显示绑定
```
function foo(){
    console.log(this.a)
}
var obj = {
    a:2
}
foo.cal(obj) //2 
```
> 使用关键字call apply 把this绑定到当前的对象上面
> call apply 接受的参数不同
> 硬绑定 bind

==硬绑定 bind==
```
function bind(fn,obj){
    return function(){
        return fn.call(obj,arguments)
    }
}
```
> bind 函数会返回一个新函数，会把指定的参数设置为this的上下文并调用原函数

### 箭头函数

> 根据外层（函数或者全局对象）决定this

```
function foo(){
    return (a)=>{
        console.log(this.a)
    }
}
var obj1={
    a:2
}
var obj2={
    a:3
}
var bar = foo.call(obj1)
bar.call(obj2)  //2  箭头函数的绑定无法被修改
```

