## 基本用法

> CSS Animation需要指定动画一个周期持续的时间，以及动画效果的名称。
```
div:hover {
  animation: 1s rainbow;
}
 // 当鼠标悬停在div元素上时，会产生名为rainbow的动画效果，持续时间为1秒。为此，我们还需要用keyframes关键字，定义rainbow效果。
@keyframes rainbow {
  0% { background: #c00; }
  50% { background: orange; }
  100% { background: yellowgreen; }
}
// rainbow效果一共有三个状态，分别为起始（0%）、中点（50%）和结束（100%）。如果有需要，完全可以插入更多状态。效果如下。

```
- 动画只播放一次。加入infinite关键字，可以让动画无限次播放。

```
div:hover {
  animation: 1s rainbow infinite;
}
```

## animation-fill-mode

> 动画结束以后，会立即从结束状态跳回到起始状态。如果想让动画保持在结束状态，需要使用animation-fill-mode属性。

```
div:hover {
  animation: 1s rainbow forwards;
}

```
 - 参数
 
（1）none：默认值，回到动画没开始时的状态。

（2）backwards：让动画回到第一帧的状态。

（3）both: 根据animation-direction（见后）轮流应用forwards和backwards规则。

## animation-direction
> 动画循环播放时，每次都是从结束状态跳回到起始状态，再开始播放。animation-direction属性，可以改变这种行为。
- 参数
（1）normal：默认值

（2）alternate：交替
（3）reverse: 根据animation-direction（见后）轮流应用forwards和backwards规则。
（4）alternate-reverse：交替翻转

## animation的各项属性

```
div:hover {
  animation: 1s 1s rainbow linear 3 forwards normal;
}

=====

div:hover {
  animation-name: rainbow;
  animation-duration: 1s;
  animation-timing-function: linear;
  animation-delay: 1s;
    animation-fill-mode:forwards;
  animation-direction: normal;
  animation-iteration-count: 3;
}

```
## keyframes的写法
> keyframes关键字用来定义动画的各个状态

```
@keyframes rainbow {
  0% { background: #c00 }
  50% { background: orange }
  100% { background: yellowgreen }
}

```
**0%可以用from代表，100%可以用to代表**

## animation-play-state
> 有时，动画播放过程中，会突然停止。这时，默认行为是跳回到动画的开始状态。


```
div {
    animation: spin 1s linear infinite;
    animation-play-state: paused;
}

div:hover {
  animation-play-state: running;
}

```