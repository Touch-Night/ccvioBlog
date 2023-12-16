---
order: 40
date: 2023-12-15
---

# 第四章 信号的调理与显示记录

## 电桥（直流电桥）

### 直流电桥的输出特性

$$
u_{y} = \frac{1}{4} u_{x}\left( \frac{\Delta R_{1}}{R_{1}} - \frac{\Delta R_{2}}{R_{2}}+\frac{\Delta R_{3}}{R_{3}}-\frac{\Delta R_{4}}{R_{4}} \right)
$$
$$
u_{0} = \frac{\Delta R_{1} + \Delta R_{3} - \Delta R_{2} - \Delta R_{4}}{4R}
$$

### 直流电桥输出特点

1. 输出电压和各桥臂电阻变化量的代数和成正比 
2. 和差特性（加减特性）
3. 供桥电压增大，容易引起蠕变和零漂
4. 增大电阻应变片的灵敏度可以提高电桥的输出电压

### 几种典型的直流电桥

灵敏度计算掌握：
- 半桥单臂
- 半桥双臂
- 全桥差动

### 和差特性的应用

::: tip
什么是电桥的和差特性？

- 若相邻桥臂应变极性一致，则输出电压为两者之差；反之为两者之和。
- 若相对桥臂应变极性一致，则输出电压为两者之和；反之为两者之差。
:::

- 提高灵敏度
- 进行温度补偿，消除测量误差
- 复杂应力状态下测取单独由某一因素产生的应变

### 电桥温度补偿原理

半桥测量时进行温度补偿使用桥路补偿法，$R_{1}$、$R_{2}$ 完全相同，处于相同温度场中，并且接入相邻臂。

$$
u_{y} = \frac{u_{0}}{4} \left[ \left( \frac{\Delta R_{1}}{R_{1}} \right)_{\varepsilon} + \left( \frac{\Delta R_{1}}{R_{1}} \right)_{t} - \left( \frac{\Delta R_{2}}{R_{2}} \right)_{t} \right]
$$

::: tip
例 4-1
:::
## 调制与解调

### 调制基本概念

- 调制的目的：解决微弱缓变信号的放大以及信号的传输问题
- 调制的概念：利用某种低频信号来控制或改变某一高频信号的某个参数的过程
	- 载波：高频振荡信号
	- 调制信号：控制高频振荡的低频信号
	- 已调制信号：调制后的高频振荡信号
- 解调：从已调制信号中恢复出原有低频调制信号的过程
- 调制种类：调幅、调频、调相

### 调幅数学分析

调幅是将一个高频余弦信号与调制信号相乘，使载波信号幅值随调制信号的变化而变化

#### 卷积

定义

$$
x(t) * h(t) = \int _{-\infty}^{\infty} x(\tau) \cdot h(t - \tau) \, d \tau
$$

卷积定理

$$
\begin{cases}
x(t) \leftrightarrow  X(\omega) \\
h(t) \leftrightarrow H(\omega)
\end{cases} \to x(t) * h(t) \leftrightarrow X(f) * H(f)
$$

#### $\delta$ 函数

$\delta$ 函数是一个理想函数，是物理不可实现信号，幅值为无限，持续时间为 0 的脉冲。

$$
\delta(t) = \begin{cases}
\infty  & t = 0 \\
0 & t \not = 0
\end{cases}
$$

$$
\int_{-\infty}^{\infty} \delta(t) \, dt  = 1
$$
1. 乘积特性：$f(t)\delta(t) = f(0)\delta(t)$, $f(t)\delta(t - t_{0}) = f(t_{0})\delta(t - t_{0})$
2. 积分特性（抽样特性）：$\int _{-\infty}^{\infty} f(t)\delta (t) \, dt$, $\int _{-\infty}^{\infty} f(t) \delta(t - t_{0}) \, dt = f(t_{0})$，即 $x(t) * \delta(t - t_{0}) = x(t - t_{0})$
3. 拉氏变换：$\Delta(s) = \int _{0-}^{\infty} \delta(t)e^{-st} \, dt = 1$
4. 傅氏变换：$\Delta(f) = \int _{-\infty}^{\infty}\delta(t) e^{-j 2\pi ft} \, dt = 1$

一个函数与单位脉冲函数卷积的结果，就是将其图像由坐标原点平移至该脉冲函数处。

### 调幅调制与解调过程

$$
\begin{align}
x(t) \cdot y(t)  & \Leftrightarrow X(f) * Y(f) \\
y(t) = \cos(2\pi f_{0}t)  & \Leftrightarrow \frac{1}{2}\delta(f - f_{0}) + \frac{1}{2} \delta(f + f_{0}) \\
x(t) \cdot \cos(2\pi f_{0} t)  & \Leftrightarrow \frac{1}{2}X(f) * \delta(f - f_{0}) + \frac{1}{2} X(f) * \delta(f + f_{0}) \\
 & = \frac{1}{2}X(f - f_{0}) + \frac{1}{2} X(f + f_{0})
\end{align}
$$
### 载波频率与最高频率

载波频率 $f_{0}$ 必须高于信号中的最高频率 $f_{max}$，否则会出现混叠现象（“混音”）。

实际应用中，载波频率至少在调制信号上限频率的十倍以上。

!!! tip
调幅波是否可以看作是载波与调制信号的迭加？

答：不可以。因为调幅波是载波幅值随调制信号大小程正比变化，只有相乘再能实现。
:::

### 解调的分析

同步解调：把调幅波再次与原载波信号相乘，随后用低通滤波器滤去大于 $f_{m}$ 的成分，则可以复现原信号的频谱，幅值为原来的一半。

$$
x(t) \cdot \cos 2(\pi f_{0}t) \cdot \cos ()2\pi f_{0}t)
$$

## 信号滤波

### 滤波的分类及其幅频特性

- 低通滤波器
- 高通滤波器
- 带通滤波器
- 带阻滤波器

![](https://ccviolett-1307804825.cos.ap-shanghai.myqcloud.com/img/202312140100799.png)
### 理想滤波器的特性

$$
H(f) = \begin{cases}
e^{-j\omega t_{0}} & |\omega| < \omega_{c} \\
0 & \text{其他}
\end{cases}
$$
脉冲响应函数 $H(j \Omega) \to h(t)$

### （重点）实际滤波器的基本参数

![](https://ccviolett-1307804825.cos.ap-shanghai.myqcloud.com/img/202312140102268.png)

#### 纹波幅度 $\delta$

通带中幅值特性值的起伏变化值

#### 截止频率

幅频特性值等于 $\frac{A_{0}}{\sqrt{ 2 }}(-3dB)$  所对应的频率点

#### 带宽 $B$

上下两截止频率之间的频率范围 $B = f_{c_{2}} - f_{c_{1}}$，又称 $-3dB$ 带宽

#### 品质因数 $Q$

对于一个带通滤波器，其品质因子 $Q$ 定义为中心频率 $f_{0}$ 与带宽 $B$ 之比，即 $Q = \frac{f_{0}}{B}$

#### 倍频程选择性

上截止频率 $f_{c_{2}}$ 与 $2f_{c_{2}}$ 之间或下截止频率 $f_{c_{1}}$ 与 $\frac{f_{c_{1}}}{2}$ 间幅频特性的衰减值

即频率变化一个倍频程的衰减量，以 $dB$ 表示。

倍频程选择性表征过渡带的幅频曲线倾斜的程度，即幅频特性衰减的快慢。

#### 滤波器因数（矩形系数）$\lambda$

滤波器幅频特性的 $-60dB$ 宽带与 $-3dB$ 宽带的比，即 $\lambda = \frac{B_{-60dB}}{B_{-3dB}}$

对理想滤波器有 $\lambda = 1$，对普通使用的滤波器，$\lambda = 1 \sim 5$

### RC 无源滤波电路

频率响应函数

幅频特性、相频特性
 
- 一阶 RC 低通滤波器

$$
\begin{align}
A(f) = |H(f)| = \frac{1}{\sqrt{ 1 + (\tau 2\pi f)^{2} }} \\
\varphi(f) = -\arctan(2\pi f\tau)
\end{align}
$$

- 一阶 RC 高通滤波器

$$
\begin{align}
A(f) = |H(f)| = \frac{2\pi f\tau}{\sqrt{ 1 + (\tau 2\pi f)^{2} }} \\
\varphi(f) = \arctan\left( \frac{1}{2\pi f\tau} \right)
\end{align}
$$