### 1考察var和let以及this指向问题
```
let userName = 'the window'
let objk = {
	userName : 'obj',
	getUserName:function (argument) {
		// body...
		return function (){
			return this.userName
		}
	}
}
console.log(objk.getUserName()());  // undefined

```
> this 指向 window 但是由于 username 使用 `` let `` 声明

### 2. 考察深拷贝
```
var arr = [
	{a:1},
	{b:3},
]
var obj = arr.slice();
console.log(obj);
arr[0].a = 0;
console.log(arr)

```
> ``slice`` 复制的数组为浅拷贝，如果是对象数组需要使用深拷贝，当对象中不存在引用类型时候，可以使用 ``Object.assign()`` 进行复制操作

### this 指向问题

```
function foo(){
    return ()=>{
        return ()=>{
            return ()=>{
                console.log('this',this.id)
            }
        }
    }
}
var f = foo.call({id:1})

var t1 = f.call({id:2})()();
var t2 = f().call({id:3})();
var t3 = f()().call({id:4});


function foo(){
    setTimeout(()=>{
        console.log(this.id)
    })
}
var id = 'window'
foo.call({id:42})
```
> 注意：不能混淆箭头函数所在的函数与箭头函数本身。

