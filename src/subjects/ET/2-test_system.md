---
order: 20
date: 2023-12-15
---

# 第二章 测试系统的基本特征

::: tip 什么是测试系统？
为了完成某种物理量的测量而由具有某一种或多种变化特性的物理装置构成的总体。
:::

::: tip 信号与系统之间的作用
系统对信号的作用
:::

## ==线性系统基本特征==

线性系统：输入输出呈线性关系

| 特性               | 说明 |
| :------------------: | ---- |
| ==叠加性==             |    系统对各输入之和的输出等于各单个输入的输出之和  |
| 比例性             |   常数倍输入所得的输出等于原输入所得输出的常数倍   |
| 微分性             | 系统对原输入信号的微分的响应等于原输出信号的微分     |
| 积分性             |    当初始条件为零时，系统对原输入信号的积分的响应等于原输出信号的积分  |
| ==频率保持性== | 若系统的输入为某一频率的谐波信号，则系统的稳态输出将为同一频率的谐波信号。     |

## 测试系统静态特性
::: note 这个知识点的考试要求
能够判断例子体现的指标是哪个指标，能够计算指标的值
:::

| 特性           | 说明                                                                                                                           | 图片示意 |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------ | -------- |
| 重复性（精度） | 表示由同一观察者采用相同的测量条件、方法以及仪器对统一被测量所做的一组测量之间的接近程度。表征测试仪器随机误差接近于零的程度。 |     ![](_images/截屏2023-12-17%2011.19.26.png)     |
| 漂移           | 仪器输入未产生变化时其输出所发生的变化。由仪器的内部温度变化和元件的不稳定性引起。                                             |       ![](_images/截屏2023-12-17%2011.19.52.png)   |
| 精确度         | 测试系统的指示值和被测量真值的符合程度。精确度是诸如非线性、迟滞、温度变化、漂移等一系列因素所导致的不确定度之和。             |    |
| 灵敏度         | 测试系统在稳态下输出量的增量和输入量的增量之比                                                                                 | ![](_images/截屏2023-12-17%2011.20.11.png)               |
| 分辨率         | 当一个被测量从一个任意值开始连续增加时，使指示值产生一定变化量所需的输入量的变化量                                             |          |
| 线性度         | 测试系统输入输出曲线与理想直线的偏离程度，即非线性误差                                                                         |     ![](_images/截屏2023-12-17%2011.20.29.png)     |
| 回程误差       | 测试系统在正行程和反行程的输入输出曲线不重合的程度，即空程误差、滞后                                                           |      ![](_images/截屏2023-12-17%2011.21.16.png)    |
| 零点稳定性     | 在被测量回到零值且其他变化因素被排除之后，仪器回到零指示值的能力。                                                             |          |

### 线性度的计算

理想直线是一般不存在或者很难获得的准确结果，利用测试数据我们可以通过计算获得拟合直线代替。

#### 端点连线法

简单、方便、偏差大

#### 最小二乘法

残差  $\Delta_{i} = y_{i} - (a + bx_{i})$，其中
$$
b = \frac{n\sum x_{i}y_{i} - \sum x_{i}\sum y_{i}}{n \sum x_{i}^{2} - (\sum x_{i})^{2}}
$$

$$
a = \frac{\sum x_{i}^{2} \sum y_{i} - \sum x_{i} \sum x_{i}y_{i}}{n \sum x_{i}^{2} - \left( \sum x_{i} \right)^{2}}
$$

精度高

## 测试系统动态特性

### 测试系统数学模型

#### 拉普拉斯变换


$$F(s) = L[f(t)] = \int_{0_-}^{\infty} f(t)e^{-st}  \, dt$$

$$f(t) = L^{-1} [F(s)] = \frac{1}{2\pi j} \int _{\sigma - j \infty} ^{\sigma + j \infty} F(s) e^{st} \, ds, t > 0$$

详见 [机械控制工程基础 课时一、拉氏变换](../CE/1-laplace_transfer.md)。

#### 传递函数

$$
G(s) = \frac{X_o(s)}{X_i(s)} = \frac{b_{0}s^m+b_{1}s ^{m-1}+\dots+b_{m-1}s+b_{m}}{a_{0}s^n+a_{1}s^{n-1}+\dots+a_{n-1}s+a_{n}} = \frac{b_{0}(s-z_{1})(s-z_{2})\dots(s-z_{m})}{a_{0}(s-p_{1})(s-p_{2})\dots(s-pn)}
 = \frac{N(s)}{D(s)}
 $$

::: tip 典型环节传递函数
- 一阶微分环节： $\tau s+1$ 
- 二阶微分环节： $\tau^2s^2+2\zeta Ts + 1$ 
:::


详见 [机械控制工程基础 课时二、传递函数和数学模型](../CE/2-transfer_function.md)

#### 频率响应函数

::: tip
物理意义：体现了系统对不同频率信号的作用
:::

$H(j\omega)$ 在频域中描述系统，称为测试系统的频率响应函数，是传递函数的特例。

$$
H(j\omega) = \frac{Y(j\omega)}{X(j\omega)} = A(\omega)e^{j\varphi(\omega)}
$$

其中：
- 幅频特性 $A(\omega) = \frac{|Y(\omega)|}{|X(\omega)|} = |H(j\omega)|$
- 相频特性 $\varphi(\omega) = \arctan H(j\omega) = \varphi_{y}(\omega) - \varphi_{x}(\omega)$

::: tip 传递函数和频率响应函数的区别
用频率响应函数 $H(j\omega)$ 不能反映过渡过程，必须用传递函数 $H(s)$ 才能反映全过程。
:::

详见 [机械控制工程基础 课时六、控制系统的频率特性](../CE/6-frequency_characteristic.md)

###  利用频率保持性求解系统的稳态输出

当我们知道系统的传递函数和信号输入，要求系统的稳态输出时，可以对输入信号进行拉氏变换得到输入函数，随后和传递函数相乘得到输出函数， 再通过拉氏反变换得到系统的稳态输出信号。

但是这种方法往往比较复杂，需要比较多的运算，我们可以直接计算出系统的频率响应函数，求得其幅值特性和相位特性，然后求得输入信号的频率，通过频率保持性得到输出信号的频率，直接代入即可得到相应的幅值和相位，得到答案。

::: details 例题
某测试系统传递函数为 $H(s) = \frac{1}{1 + 0.5s}$，当输入信号分别为 $x_{1} = \sin \pi t$ 和 $x_{2} = \sin4 \pi t$ 时，分别求系统的稳态输出。

解：由系统的传递函数得到系统的频率响应函数：

$$
H(j\omega) = \frac{1}{1 + 0.5j\omega } = \frac{1 - 0.5j\omega}{(1 + 0.5j\omega)(1 - 0.5j\omega)} = \frac{1 - 0.5j\omega}{1 - 0.25 \omega^{2}}
$$ 

由 $f = \frac{\omega}{2\pi}$，即 $\omega = 2\pi f$ 可得：

$$
H(jf) = \frac{1 - j\pi f}{1 + \pi^{2}f^{2}}
$$

故 $A(f) = \frac{1}{\sqrt{ 1 + \pi^{2}f^{2} }}$，$\varphi(f) = -\arctan(\pi f)$

当输入为 $x_{1} = \sin \pi t$ 时，频率 $f_{1} = 0.5Hz$，根据频率保持性可得输出频率 $f_{1} = 0.5Hz$

故 $A(f_{1}) = \frac{1}{\sqrt{ 1 + \pi^{2}f^{2} }} = \frac{1}{\sqrt{ 1 + \pi^{2}(0.5^{2}) }} = 0.537$，$\varphi(f) = -\arctan(\pi f) = -\arctan(\pi \cdot 0.5) = -57.73^{\circ}$

稳态输出 $y_{1}(t) = 0537 = \sin(\pi t - 57.52^{\circ})$

同理，当输入为 $x_{2} = \sin 4 \pi t$ 时，频率 $f_{2} = 2Hz$，稳态输出 $y_{2}(t) = 0.157 \sin(4\pi t - 80.96^{\circ})$
:::

###  一阶、二阶系统的动态特性

详见 [机械控制工程基础 课时四、时域瞬态响应分析](../CE/4-time_domain.md) 


|     系统     |                                                                   一阶惯性系统                                                                   |                                                                                                                                                     二阶惯性系统                                                                                                                                                      |
|:------------:|:------------------------------------------------------------------------------------------------------------------------------------------------:|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|     描述     |                                                 $a_{1} \frac{dy(t)}{dt} + a_{0}y(t) = b_{0}x(t)$                                                 |                                                                                                                  $a_{2} \frac{d ^{2} y(t)}{dt^{2}} + a_{1} \frac{dy(t)}{dt} + a_{0}y(t) = b_{0}x(t)$                                                                                                                  |
|   传递函数   |                                                         $H(s) = \frac{K}{(\tau s + 1)}$                                                          |                                                                                                                  $H(s) = \frac{K}{\frac{s^{2}}{\omega_{n^{2}}} + \frac{2\zeta s}{\omega_{n} } + 1}$                                                                                                                   |
|     说明     |                             $K = \frac{b_{0}}{a_{0}}$ 为静态增益<br/>$\tau = \frac{a_{1}}{a_{0}}$ 为时间常数                             |                                                                    $K = \frac{b_{0}}{a_{0}}$ 为静态灵敏度<br/>$\omega_{n} = \sqrt{ \frac{a_{0}}{a_{2}} }$ 为无阻尼固有频率<br/>$\zeta = \frac{a_{1}}{2 \sqrt{ a_{0}a_{2} }}$ 为阻尼比                                                                     |
| 频率响应函数 | $A(\omega) = \lvert H(j\omega)\rvert = \frac{1}{\sqrt{ 1 + (\tau\omega)^{2} }}$<br/>$\varphi(\omega) = \angle H(j\omega) = -\arctan \omega \tau$ | $A(\omega) = \lvert H(j\omega) \rvert = K \frac{1}{\sqrt{ \left[ 1 - \left( \frac{\omega}{\omega_{n}} \right)^{2} \right]^{2} + 4\zeta^{2}\left( \frac{\omega}{\omega_{n}} \right)^{2} }}$<br/>$\varphi(\omega) = -\arctan \frac{2\zeta \frac{\omega}{\omega_{n}}}{1 - \left( \frac{\omega}{\omega_{n}} \right)^{2}}$ |

::: tip 为何只研究一、二阶系统？
任何一个系统均可视为是多个一阶、二阶系统的并联。也可将其转换为若干个一阶、二阶系统的串联。
:::

###  一阶、二阶系统对典型输入的响应

::: note 灵敏度的归一处理
为了方便系统响应的计算，我们通常对灵敏度进行归一处理，即 $K = 1$
:::

#### 一阶系统的响应

| 响应类型\系统类型 | 一阶系统 | 二阶系统（欠阻尼） | 二阶系统（临界阻尼） |
| :----------------: | :------: | :----------------: | :------------------: |
| 单位脉冲响应 | $$\frac{1}{T} e^{-t/T}$$ | $$\frac{\omega_{n}}{\sqrt{ 1 - \zeta^{2} }}e^{-\zeta\omega_{n}t} \sin(\sqrt{ 1 - \zeta^{2} }\omega_{n}t)$$ | $$\omega_{n}^{t}te^{-\omega_{n}t}$$ |
| 单位阶跃响应 | $$1 - e^{-t/T}$$ | $$1 - \frac{e^{-\zeta\omega_{n}t}}{\sqrt{ 1 - \zeta^{2} }} \sin(\sqrt{ 1 - \zeta^{2} }\omega_{n}t + \varphi)$$ | $$1 - (1 + \omega_{n}t)e^{-\omega_{n}t}$$ |

::: tip 一阶系统时间常数的选择
为了获得较好的工作性能，时间常数 $\tau$ 应该越小越好。

当 $\omega$ 一定的时候，$\tau$ 越小，系统输出的幅值误差越小。

当 $\omega \tau$ 一定的时候，$\tau$ 越小，系统能测量的频率越高。
:::

::: tip 二阶系统阻尼比的选择
阻尼比 $\zeta$ 直接影响系统超调量和振荡次数，若 $\zeta$ 选择在 $0.6 \sim 0.8$ 之间，最大超调量约在 $2.5 \% \sim 10 \%$ 之间，对于 $5 \% \sim 2\%$ 的允许误差而认为达到稳态的所需调整时间也最短，约为$\frac{3\sim 4}{\zeta}\omega_{n}$。

因此，许多测量装置在设计参数时，常常将阻尼比选择在 $0.6 \sim 0.8$ 之间，如 $0.707$
:::

## 测试系统不失真测试条件

精确测试（即不失真测试）即测试系统的输出信号能够真实，准确的反映出被测对象的信息。

设原函数为 $x(t)$，测试函数为 $y(t) = A_0x(t - t_{0})$，则其傅里叶变换为 $Y(j\omega) = A_0x(j\omega)e^{-j\omega t_{0}}$

频率响应函数为

$$
H(j\omega) = \frac{Y(j\omega)}{X(j\omega)} = A_0 e^{-j\omega t_{0}}
$$

幅频特性和相频特性为：

$$
\begin{align}
A(\omega) &  = A_0 \\
\varphi(\omega) &  = -\omega t_{0}
\end{align}
$$

故条件为幅频特性为常数 $A(\omega) = A_{0}$，相频特性为一次函数 $\varphi(\omega) = -\omega t_{0}$。

此时测试信号幅值放大了 $A_{0}$ 倍，在时间上延迟了 $t_{0}$，信号不失真。

![](_images/截屏2023-12-17%2021.48.38.png)


::: tip 信号的所有频率成分相位滞后相同吗？
实际中由于任何测量都伴有时间上的滞后，在信号的频率范围上要同时实现接近与零的相位滞后几乎是不可能的。
:::