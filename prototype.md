### prototype
1.实例的构造函数（constructor）属性指向
```
function Person(){}
var person = new Person()
console.log(person.conotructor === Person) // true
```

2.每个函数对象都有 prototype 属性

3.原型对象，即 prototype ，通常都包含着一个默认属性  constructor ，该属性指向 prototype 所在的函数 （喵喵喵这不就是第一条？）

```
function Person(){}
console.log(Person.prototype.constructor === Person)
```
4.原型对象是构造函数的一个实例，即

```
function Person(){}
var person = new Person()
Person.prototype = person
```
> 因此得出一个结论，为什么Function.prototype 是一个函数对象因为

```
var func = new Function()
Function.prototype = func
```

### 如何查看prototype上包含那些值
##### Object.getOwnPropertyNames(Function.prototype)

5.每个对象（null除外）都有_proto_ 属性，它指向创建对象时的构造函数的原型对象。

```
var person = new Person()
console.log(person._proto_ === Peroson.prototype)
```

6.所有函数对象的_proto_都指向 Function.prototype