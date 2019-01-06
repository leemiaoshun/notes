### 定义正则表达式

- /正则表达式/修饰符
- new RegExp('正则表达式','修饰符')
```
var reg = /hello \w{2,12}/g
var reg2 = new RegExp('hello \\w {3,12}','g')
<!--第二种方法字符串转义 "\\"代表"\"-->
```
- 修饰符

属性 | 描述
---|---
global      | RegExp 对象是否具有标志 g
ignoreCase  | RexExp对象是否具有标志i
lastIndex   | 一个整数，标识开始下次匹配的字符位置
multline    | RegExp 对象是否具有标志m
soucetree   | 正则表达式源文本


### RegExp对象中的方法
- test()
> 检测字符串中指定的值，返回值为Boolean
```
var reg = /hello \w {3,12}/;
console.log(reg.test('hellow wo')); // false
console.log(reg.test('hellow world')); // true
// 匹配 hello 以及3-12位的字母
```
- exec
> 检测字符串中指定的值，匹配成功返回一个数组，数组中包含字符串的位置，匹配失败返回null
```
var reg = /hello/;
console.log(reg.exec('helloworld')) ['hello']
conosle.log(reg.exec('world') null
```
- compile()
> 用于改变reg
既可以改变检索模式，也可以添加或删除第二个参数

```
var reg=/hello/;
console.log(reg.exec('helloworld'));//['hello']
reg.compile('Hello');
console.log(reg.exec('helloworld'));//null
reg.compile('Hello','i');
console.log(reg.exec('helloworld'));//['hello']
```

### 字符类匹配

字符 | 匹配
---|---
[...]   | 方括号内的任意字符
.       | 除了换行字符跟Unicode行终止符之外的任意字符
\w      | 任何ASCII字符组成的单词 等价于 [a-zA-Z0-9]
\W      | 任何不是ASCII字符组成的单词
\s      | 任何Unicode空白符
\S      | 非Unicode 空白符
\d      | 任何ASCII 数字，[0-9]
\D      | 除了ASCII数字之外的任何字符
\b      | 边界符号

### 重复字符匹配


字符| 匹配
---|---
{n,m}   | 前一项至少n次，但不能超过m次
{n,}    | 前一项至少n次，或更多次
{n}     | 前一项n次
?       | 匹配前一项0次或1次，前一项为可选项 == {0,1}
+       | 前一项1次或多次，=={1，}
-       | 前一项0次货多次，=={0，}


### String对象使用正则表达式

- match
> 在字符串内检索制定的值，匹配成功后返回存放结果的数组，匹配不到返回 null 。(返回值类似exec)
```
var re1 = /world/i;
var re2 = /world/ig;
console.log('hello world world'.match(re1))
console.log('hello world world'.match(re2)) // 匹配多个world
/\?[a-zA-Z]=\w(&[a-zA-Z]=\w){0,}/g;
获取URL查询参数
```

- search
> 在字符串内检索制定的值匹配成功返回第一个匹配成功字符串的位置，匹配失败返回 -1 (有点类似indexOf)
```
var reg=/world/i;
console.log('hello world'.search(reg)); // 6
console.log('hello'.search(reg)); // -1
```
- replace
> 替换与正则表达式匹配的字符串，并返回替换后的字符串

```
var re = /world/i;
console.log('hello world'.replace(re,'JserWang'))

<!--敏感词过滤-->
console.log('hello world'.replace(re,i=>"***"))
```

- split
> 切割字符串变成数组

```
var re = /1[2,3]8/
var reg=/1[2,3]8/;
console.log('hello128Javascript138Javascript178Javascript'.split(reg));

```


0009515210