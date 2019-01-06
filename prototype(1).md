# prototype
> Javascript 中的对象都有一个特殊的 [[ Prototype ]] 内置属性，其实就是对于其他对象的引用。几乎是所有的对象在创建时，prototype都会被赋予一个非空的值
- 当试图引用对象的属性，会触发 [[get]] 操作，第一步是检查对象是否有这个属性，要有的话就使用它。当属性不存在时候，就会继续访问对象的 prototype 链
- 使用 for in 遍历对象时，原理和查找 [[prototype]] 类似。任何可以通过原型链访问到的 (并且是enumerable) 的属性都会被枚举。使用 in 操作符来检查属性在对象中是否存在时，同样hi查找对象的整条原型链 (无论是否可枚举)

1.Object.prototype
> 所有普通的 prototype 链最终都会指向内置的 Object.prototype。由于所有的“普通” （内置）对象都源于Object.prototype,所以它包含很多通用功能 **toString()、valueOf()、 hasOwnproperty() isPrototypeOf()、propertyIsEnumerable()**

2.属性设置屏蔽
- 当修改对象中的值时，首先现在对象本身查找，当该值不存在于对象中时，prototype 就会被遍历。当原型链上找不到 foo
的时候，foo就会被添加给对象。
- 当foo同时存在于对象本身中，又存在于对象的 prototype 上层，那么就会发生屏蔽。对象本身的属性就会屏蔽原型链上的 foo 属性


## 类
- 通过调用 new Foo() 创建的每个对象最终将会被[[prototype]] 链接到这个 “Foo.prototype”
```
function foo (){}
var a = new foo()
Object.getPrototypeof(a) === Foo.prototype // true

```
- 原型继承
> javascript 不会将一个对象复制到另一个对象。只是关联起来，这种机制叫做原型继承


```
function Foo (){}
Foo.prototype.constrctor == Foo true
var a = new Foo()
a.constrctor ===Foo true
```
==Foo.prototype 默认有一个公有且不可被枚举的属性。.constructor，这个属性引用的是对象关联的函数 使用 new 关键字“构造函数”调用创建的对象也有一个.constructor属性，指向创建这个对象的函数==