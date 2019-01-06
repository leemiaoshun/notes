# CSS Transition
- 基本用法
> 在CSS 3引入Transition（过渡）这个概念之前，CSS是没有时间轴的。也就是说，所有的状态变化，都是即时完成。
```
img{
    height:15px;
    width:15px;
}

img:hover{
    height: 450px;
    width: 450px;
}

```
> 上述代码中当 hover 被触发时候，缩略图会迅速变大。==transition==的作用在指定变化所需要的时间。如下述代码

```
img{
    transition: 1s;
}

```

- transition-delay
>delay的真正意义在于，它指定了动画发生的顺序，使得多个不同的transition可以连在一起，形成复杂效果。

```
img{
    transition: 1s height, 1s 1s width;
}
```

- transition-timing-function
transition的状态变化速度（又称timing function），默认不是匀速的，而是逐渐放慢，这叫做ease。  
```
img{
    transition: 1s ease;
}

```
#####  其他模式还包括
    1.linear：匀速
    2.ease-in：加速
    3.ease-out：减速
    4.cubic-bezier函数： [自定义网站](http://cubic-bezier.com/#.17,.67,.83,.67)
    
    
- transition的各项属性

```
img{
    transition: 1s 1s height ease;
}

可以单独写为

img{
    transition-property: height;
    transition-duration: 1s;
    transition-delay: 1s;
    transition-timing-function: ease;
}

```

-  transition的局限
1.transition的优点在于简单易用，但是它有几个很大的局限。

1. transition需要事件触发，所以没法在网页加载时自动发生。

1. transition是一次性的，不能重复发生，除非一再触发。

1. transition只能定义开始状态和结束状态，不能定义中间状态，也就是说只有两个状态。

1. 一条transition规则，只能定义一个属性的变化，不能涉及多个属性。