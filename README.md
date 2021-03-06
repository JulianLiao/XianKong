

# 汽车组成部件

节气门，火花塞，喷油嘴的实物图片如下，

![throttle + piston](imgs/components/car_components.jpg "throttle + piston")

## 节气门总成

现代汽车的节气门总成如下：

![Hyundai throttle](imgs/components/Hyundai_motor_throttle.jpg "Hyundai throttle")

别克汽车的节气门总成如下：

![Buick throttle](imgs/components/Buick_throttle.jpg "Buick throttle")

三菱/猎豹汽车的节气门总成如下：

![Mitsubishi/Jaguar throttle](imgs/components/Mitsubishi_Jaguar_throttle.jpg "Mitsubishi/Jaguar throttle")

# XianKong

一共有3个电机，驱动电机（绿通），转向电机（松灵后加），驻车电机（松灵后加）。

汽车线控系统需要的相关传感器有：

- 角位移传感器
- 转矩传感器
- 车速传感器
- 侧向加速度传感器
- 横摆角速度传感器

# 线控历史

最早源于飞行控制系统。它将飞行员执行的操作动作转变成弱电信号，再通过弱电信号控制强电执行机构的方式来实现相应的飞行控制。

# 车体坐标系

![Vehicle Coordinate](imgs/vehicle_coordinates_3d.png "Vehicle Coordinate")

一辆车要能够跑起来，最基本的是横向控制和纵向控制。横向控制指的是车能够在y方向上移动，纵向控制指的是车能够在x方向上移动。

# 线控的功能框图

![Sbw Function diagram](imgs/Sbw_function_diagram.png "Sbw Function diagram")

每一个系统并不是独立在工作，而是相互之间有依存关系，例如，单独把转向系统剥离出整车，它是不会工作的，必须接入到整车环境中。

## 线控加速

纵向控制分为3个核心控制：加速控制，减速控制和档位调换。

节气门那里需要接一个伺服电机(servemotor)

The "Position sensor" senses how much you press the "Gas Pedal".

线控油门的实现示意图，

![Throttle by wire](imgs/Drive_by_wire_example.PNG "Throttle by wire")

"Position sensor"的实物图如下：

![Position Sensor for gas pedal](imgs/position_sensor_for_gas_pedal.png "Position Sensor for gas pedal")

ECU，电机的实物图如下：

![ECU and Motor for throttle body](imgs/ECU_and_motor_for_throttle_body.png "ECU and Motor for throttle body")


## 线控转向

Steer-by Wire，简称"SbW"，线控转向

让车辆仅通过电子信号实现安全可靠的转向。

耐世特实现了“随需转向系统”和“静默方向盘系统”。

1. 转向助力系统(EPS)
当驾驶员在进行转向动作时，车辆会捕捉驾驶员的转向动作并持续输出一个辅助转向力让转向变得更加轻便。转向力输出主要依靠助力系统来完成，助力系统包括：

!["EPS"](imgs/EPS.png "EPS")

传统的“机械转向系统”的示意图如下：

!["traditional mechanical turn"](imgs/mechanical_turn_system.jpg "traditional mechanical turn")

“液压助力转向”的示意图如下：

!["EPS_1"](imgs/EPS_1_sample.jpg "EPS_1")

“电子助力转向”的示意图如下：

!["EPS_3"](imgs/EPS_3_sample.webp "EPS_3")

横向控制系统主要包括机械转向部分和电子助力部分。

- 机械转向部分

通过机械传动将方向盘转动量变成车轮的转角量。机械传动部分包括转向杆，万向轴，转向机和拉杆。

- 电子助力部分

将人类纯机械的动能输入转换成通过电机转动来实现转向机的动能输入，主要包括转向电机，转向传感器和转向控制器。

在乘用车中，液压助力和电控液压助力逐渐被电子助力系统取代，因此这里讨论的线控改装是基于电子助力转向来实现的。


## 线控制动



舍弗勒自己做了个模块，叫做“舍弗勒智能转向驱动模块”。这个模块是一个高度集成的车轮悬架单元，将包括轮内电机在内的所有驱动和底盘零部件都集成在一个紧凑的模块内。


## 线控供应商

公司英文名 | 公司中文名 | 所在国家 | 在华研发中心数量 | 在华主要城市 | 在华主要合作伙伴 | 其他
-----|-----|------|------|------|------|------
Nexteer  |  耐世特  |  德国  |  2  |  1. 上海市嘉定区安亭镇 2. 湖南湘江新区  |  湖南政府  |  无
Schaeffler  |  舍弗勒  |  德国  |  2  |  1. 上海市嘉定区安亭镇 2. 湖南湘江新区  |  湖南政府  |  无
其他  |  verb  |  放水时间  |  其他  |  其他  |  其他
其他  |  verb  |  水桶大小  |  其他  |  其他  |  其他


### 好的参考资料

#### 好的Youtube视频介绍

这下面几个视频都是在Youtube上找到的比较好的介绍线控的视频。

https://www.youtube.com/watch?v=QGdEM2TRajw


https://www.youtube.com/watch?v=IYm2C7zr82Q

https://www.youtube.com/watch?v=Pgln9L5Y7sQ

https://www.youtube.com/watch?v=7SnpLfCF-r4

#### 好的文章列表



## 硬件说明

## 实际车体测试中遇到问题集锦

### 问题1 - chassis上报Frame_161/151/141/131/121/111/171 timeout

该问题仅在POD4上出现，POD4主控vcu用的是比较旧的固件，POD5/6所用的主控vcu固件已解决了该问题。

对于POD4主控所用的固件，当通过方向盘接管时，首先是转向模块的扭矩传感器感知到的，对主控VCU而言这是一个中断事件，该中断会抢占timer中断（定周期上报反馈帧），导致VCU在一段时间内（约180ms，20ms一帧，约9帧左右）无法上报反馈帧，之后会恢复，也就是chassis不会一直报Frame_1x1 timeout错误。当通过踩刹车踏板接管时，这个动作是直接通过主控VCU上的IO口感知到的，并不影响VCU上报反馈帧。

因此，该问题取决于接管的方式，拧方向盘接管有该错误信息，踩刹车踏板没有该错误信息，这个机制是实现在主控VCU里，并不是我们能够控制的。

![POD4 VCU frame timeout](imgs/vcu_controller/VCU_frame_timeout.jpg "POD4 VCU frame timeout")

### 问题2 - 松灵是否提供了调试PID接口给我们？

没有，chassis与主控VCU唯一的沟通方式就是通过CAN protocol，CAN protocol暴露了什么功能的接口，我们就能用怎样的接口，而现在的CAN protocol 并没有暴露PID接口。

英博尔驱动器是暴漏了PID接口给我们的，有一个上位机的调参软件可以修改Kp, Ki, Kd。


## 核心板

核心板是一个两层板，底板(STM32F405RGT6)与上层板是通过两个排针（一横一竖）连到一起的，每一个排针都有20个PIN角。对于横着的排针，底板(STM32F405RGT6)上写着"32060A-Y98-190517"，上层板上写着"32060A-Y99-190517"。

2020.04.15

从四川12座起，开始用新版主控，

![new VCU controller](imgs/vcu_controller/new_VCU_controller.PNG "new VCU controller")

之前的2座车和8座车，均使用旧版主控，松灵发的备用件也是旧版主控

![old vcu controller](imgs/vcu_controller/old_VCU_controller.jpg "old VCU controller")

### STM32F103系列 与 STM32F4xx 系统的区别

STM32F4xx是基于Cortex-M4的
```
    Cortex-M4的一个核心功能是具有单精度浮点运算单元，其支持所有ARM单精度（注意是ARM单精度，不是x86单精度）
    数据类型与数据运算。文档的原话是："The Cortex-M4 core features a Floating point unit(FPU) single
    precision which supports all ARM single-precision data-processing instructions and data types."
```

STM32F103系列是基于Cortex-M3的

参考文章

http://news.eeworld.com.cn/mcu/ic473892.html

http://news.eeworld.com.cn/mcu/ic476318.html

## EPS

SWD接口可以用于程序下载和调试。USART串口，用于外接USB转串口模块进行固件升级。

我的问题是：

1. SWD是否可以用来做固件升级

我自己给出的答案是：可以

2. USART串口是否可以用于程序下载和调试

我自己的答案是：不可以

《EPS使用说明书.pdf》没有说明转向直流电机4个PIN角的线序，也没有说明扭矩传感器5个PIN角的线序

![EPS interface1 turn-motor](imgs/eps/EPS_interface1_turn.png "EPS interface1 turn-motor")

![EPS interface2 power](imgs/eps/EPS_interface2_power.png "EPS interface2 power")

![EPS interface1](imgs/eps/EPS_interface1.jpg "EPS interface1")

A接的是车载原来就有的电源线，那这个电源是12v还是24v？

B接的是控制转向电机的线。


## 油门

英博尔驱动器提供了CAN接口，松灵根据英博尔协议通过CAN接口控制油门和挡位。


## 关于AB相编码器

“叉车项目，建图，路径规划，壁障等问题的讨论”这封邮件里面有详细的解释，该邮件创建于2017-09-22，11:37 AM

### 如何分析编码器

拿到一个编码器后，首先要分析，它是增量式编码器还是绝对值编码器。

#### 增量式编码器

对于增量式编码器，都存在一个线数的说法。
比如，刹车电机cz_nology所用的编码器的线数是500线的。
![cz_nology encoder](imgs/encoder/nology_encoder.PNG "cz_nology encoer")

```
再比如上海航天802所对接的叉车，有两个编码器：行驶轮编码器和转向轮编码器。

行驶轮编码器线数是48，转向轮编码器线数是256。

关于行驶轮
行驶轮减速比是21.956，就是说行驶轮走一圈，编码器要走21.956圈。行驶轮走一圈，编码器总的脉冲数：AB相脉冲 = A相脉冲 + B相脉冲。
A相脉冲 = B相脉冲 = 21.956 * 48 = 1053.888，AB相脉冲 = 2107.776
行驶轮直径：230mm，行驶轮走一圈的距离：0.23 * 3.1415926

一个上传计数值的长度（1个driverEnCnts）的长度：0.23 * 3.1415926 / 2107.776 = 0.00034281m

关于转向轮
```

代表增量式编码器分辨率的参数是PPR(pulse-per-revolution)，也就是每转的脉冲数。例如，每圈刻线360线，A,B每圈各输出360个脉冲，分辨率参数就是360PPR。


#### 绝对值编码器

暂且认为绝对值编码器没有线数这个说法。线控改装中的转向EPS，所用的编码器型号是BRT38-COM1024D50-RT1，这里的1024的含义是，一圈有1024个位置值，这不是一个单圈的绝对值编码器，而是一个多圈的绝对值编码器，圈数为50圈。另外，这个编码器它是一个有记忆的器件，

多圈编码器通过测量额外的转数，可提供超过360度的量程。

```
线控改装，转向电机所用的编码器，BRT38-COM1024D50-RT
```
