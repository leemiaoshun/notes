## 属性描述符号
```
var obj = {
    a:2,
}
Object.getOwnPropertyDescriptor(obj,'a');
{
    value:2,
    writable:true,
    enumerable:true,
    configurable:true,
    
}
获取对象的 key 的描述字符
```
> 普通的对象属性对应的属性描述符除了 value 之外，还包含 writable （可写） enumerable （可枚举） 和 configurable （可配置） 在创建普通的属性时属性描述符会使用默认值，可以使用Object.defineProperty() 来添加修改属性 （修改 configurable 必须为true ）

- writeable
> 决定是否可以修改属性的值，当值为false 的时候，修改操作会失败，严格模式下会抛出错误。
- configurable
> 只要属性是可配置的，就可以使用 defineProperty() 方法来修改属性描述符

==configurable修改为false时单向操作，无法撤销==

- enumerable
> 控制对象的属性，是否会出现在对象枚举属性中，当值为 false 时，for in 循环将拿不到该 key 

```
Object.defineProperty(obj,"k"{
    value:2,
    writable:true,
    enumerable:true,
    configurable:true,
})
与开头的方法相对应，defineProperty  可以改变对象中 key 的属性
```

#### 设置常量
1.结合使用 writable:false 和 configurable：false 可以创建一个真正的常量

2.如果你想禁止一个对象添加新属性并且保留已有属性，可以使用Object.preventExtensions();
```
var obj = {a:2}
Object.preventExtension(obj)
obj.b = 3;
obj.b = 3; // undefined


// 密封之后不仅仅不能添加新属性，也不能重新配置或者删除任何属性（可以修改属性的值）
```
==失败 严格模式下会抛出错误==

3.密封
> Object.seal() 会 '密封' 一个对象，这个方法实际会在现有一个 对象上调用 Object.preventExtensions() 并把所有属性标记为 configurable false
不能添加新属性，不能重新配置后删除任何现有属性

4.冻结
> Object.freeze() 会创建一个冻结对象，现有对象上调用 Object.seal() 并把所有 '数据访问' 属性标记为 writable false


### [[GET]]
```
var obj = {a:2}
obj.a //2
```
> 上述代码并不仅仅时在 obj 中查找名字为 a 的属性
语言规范中，obj.a 在 obj 上实际是实现了 [[GET]] 操作 。对象默认的内置的 [[GET]] 操作首先在对象中查找是否有名称相同的 属性，如果找到就会返回这个属性的值。然而如果没有找到名称相同的属性，按照[[ GET ]] 算法的定义会 遍历对象所在原型链
如果没有找到，就会返回 undefined

[[ PUT ]]
    1.属性是否在访问描述符，如果并且存在setter调用setter
    2.属性的数据描述符中 writable 是否是 false 如果是，在非严格模式下静默失败，在严格模式下抛出错误
    3.如果不是以上情况，将值设置为属性的值


### Getter 和 Setter
> 对象默认的 [[put]] he [[get]] 操作分别可以控制属性值的设置和获取

==在es5中可以使用getter和setter部分改写默认操作，但无法应用在整个对象上，getter是一个隐藏函数，会在获取属性值时调用，setter会在设置属性值的调用==

> 当一个属性定义 getter setter 或者两者都有时，这个属性会被定义成为 “访问描述符” 对于访问描述符来说，Js会忽略他们的value 和 writable 会关心get 和 set 操作