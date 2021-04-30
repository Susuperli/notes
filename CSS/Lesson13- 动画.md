# 第十三讲 动画

## 过渡效果

- 说明：css过滤是指元素从一种样式逐渐改变成为另外一种样式的效果，transition（过渡）简写属性，用于在一个属性中设置四个过滤属性。**（对于过渡元素的声明对本元素使用）。**
- tansition-property：规定应用过滤的css属性的名称（比如：width、height）。
- transiton-duration：定义过滤效果花费的时间，默认是0，单位s。
- transiton-timing-function：规定过渡效果所使用的时间曲线。默认是ease。
  - linear：线性的过渡效果。
  - ease：默认值，慢开始然后快最后慢结束。
  - ease-in：慢开始。
  - ease-out：慢结束。
  - ease-in-out：慢开始慢结束。
- transition-delay：延时，从多长时间后开始执行样式，单位s。

## 帧效果

### 关键帧动画

语句1：

@keyframes name{

​                               from{样式1}

​                               to{样式2}

​                       }

设置样式1从样式2的过程，两个关键帧，css会自动补齐过程帧。

语句2：

@keyframes name{

​                      0%{css样式}

​                      25%{css样式}

​                      50%{css样式}

​                      75%{css样式}

​                      100%{css样式}

​                  }

### 调用关键帧

我们设置好了关键帧动画，就可以通过如下的语句来调用他们了。

- animation-name:name;指定动画名称。

- animation-duration:xs;指定完成动画需要的时间。

- animation-timing-function:ease;指定完成动画所用的变化函数。

  包括如下函数：liner、ease（默认）、ease-in、ease-out、ease-in-out。

- animation-delay:xs;定义动画从什么时间开始，单位为s和ms。

- animation-iteration-count:number|infinite;设置动画的重复次数，可以设置数字默认为1，或者infinite一直重复。其中iteration：重复，ifinite：无限的，无穷的。

- animation-direction:normal|reveres|alternate;设置下次动画的方向。normal默认正常，reverse相反的，即反向转，alternate交替的，即奇数次正向，偶数次反向。

- animation-fill-mode:指定动画在播放之前或之后，其动画效果是否可见。默认是none，不改变默认行为；forwards，当前动作完成后保持最后一个属性值（在最后一个关键帧定义）。

- animation-play-state:指的是动画是否在运行或是暂停，默认值running，暂停是paused。