

# PID表示

## 位置式PID表示

表示方法1：

P控制：
![P control expression1](imgs/PID/P_controller_expression1.gif "P control expression1")

PI控制：
![PI control expression1](imgs/PID/PI_controller_expression1.gif "PI control expression1")

PID控制：
![PID control expression1](imgs/PID/PID_controller_expression1.gif "PID control expression1")



## 增量式PID表示

## 关于P - Proportion

比例控制可以快速地减少误差，但是当误差小于一定值时，也就是控制量小于一定值，螺旋桨提供的升力不足以让无人机上升而只能保持现有的高度。


## 关于I - Integral

积分控制提供了一定的**惯性**

### 说下积分时间常数



## 关于D - Derivation

微分控制提供了一定的**阻尼**，微分控制器是来阻挡变化的。

比如无人机快速地下降，也就是高度的变化率加大，微分的控制量也就加大，无人机的升力加大，阻挡了无人机高度的下降。另一方面，当无人机在PI控制器的作用下快速地向目标高度靠近时，误差快速地降低，故误差的导数为负，微分控制项在整个PID控制项中将减小控制量，进而使得无人机的转速减小，以防止其上升冲过30m这一目标高度。

## 场景

### 场景1 - 控制无人机飞行到距离地面30m位置

<img src="imgs/PID/Scene/Scene1.PNG" alt="drawing" width="260" height="131"/>

所用传感器：气压高度传感器，获取当前的高度

控制量：无人机螺旋桨转速的大小

仅使用比例控制，可以快速地减小误差，但当误差量小于一定值时，也就是控制量小于一定值时，螺旋桨提供的升力不足以让无人机上升而只能保持现有的高度。

<img src="imgs/PID/Scene/Scene1_2.PNG" alt="drawing" width="262" height="149"/>

仅使用比例控制，会造成稳态误差，如下，

<img src="imgs/PID/Scene/Scene1_3.PNG" alt="drawing" width="262" height="149"/>

稳态误差不会随着时间推移而被比例控制消除。

理想情况下，引入积分控制后，也就是PI控制器，可以消除稳态误差。

## 外部环境的变化

```
控制无人机上升时，突然从上方刮来一阵风，无人机的高度急剧下降，如果只有PI控制器的话，此时会怎样？误差突然加大，PI控制器的控制量也会增大，但仍然可以通过PI控制器让无人机回到目标高度。
```

实际控制过程中，会有外部环境的变化，试想突然从上方刮来一阵风，无人机的高度急剧下降，微分控制器计算误差的变化率。当无人机快速地下降时，微分控制量将随着误差的变化率的增大而增大。
