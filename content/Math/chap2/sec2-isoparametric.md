# 等参变换

[前文](./intro.md)提到，物理单元上的计算关键在于单元 $E$ 上的积分运算和场变量分布运算。然而，由于 $\left.\phi\right|_{E}$ 与单元 $E$ 的几何形状密切相关，其构造过程复杂且难以统一处理。为了解决这一问题，引入了参考单元和形函数，将物理单元上的计算变换到参考单元上进行

在有限元方法中，物理单元与参考单元通过**参数化映射**实现积分运算

$$
\int_{E}\frac{\partial \left.\phi_{i}\right|_{E}}{\partial x}\frac{\partial \left.\phi_{j}\right|_{E}}{\partial x}\,\mathrm{d}E
$$

与场变量分布运算

$$
u_{h}(x,y) = \sum_{i=1}^{n}u_{i}\left.\phi_{i}(x,y)\right|_{E_{(x,y)}}
$$

的规范化处理

## 几何映射

几何映射通过形函数将物理单元坐标 $(x,y)$ 映射到参考单元坐标 $(\xi, \eta)$：

```{margin}
$(x_{i},y_{i})$ 是物理单元节点的坐标
```

$$
\begin{equation}
x = \sum_{i} N_{i}(\xi,\eta)x_{i},\quad y = \sum_{i} N_{i}(\xi,\eta)y_{i}.
\end{equation}
$$ (sec2-eq:coordinate-transformation)

几何映射的核心目的是将不规则物理单元的积分运算转化为参考单元上的规则域积分

通过坐标变换，物理单元上的积分通过参考单元计算

$$
\int_{E_\text{物理}}f(x,y)\,\mathrm{d}x\mathrm{d}y=\int_{E_\text{参考}}f(\xi,\eta)\cdot\left|\det \mathbf{J}\,\right|\ \mathrm{d}\xi\mathrm{d}\eta,
$$

其中 Jacobian 矩阵

$$
\begin{equation}
\mathbf{J} = \left[
\begin{matrix}
\frac{\partial x}{\partial \xi} & \frac{\partial x}{\partial \eta} \\
\frac{\partial y}{\partial \xi} & \frac{\partial y}{\partial \eta} 
\end{matrix}
\right].
\end{equation}
$$

:::{admonition} 积分变换公式
:class: tip, dropdown

在二维情形下，考虑坐标变换 $T$

$$
T:(\xi,\eta) \rightarrow (x(\xi,\eta),y(\xi,\eta))
$$

该变换将区域 $\mathcal{D}$ 映射为区域 $\mathcal{D}'$。
如图所示，设点 $P$ 被映射到了 $P'$

```{figure} ../../../images/Math/chap2/IntegralTransform.png
---
width: 800px
name: sec5-fig:IntegralTransform
---
二维情形下面积变换公式
```

于是，忽略高阶项，$A',B',C'$ 的坐标位置为

$$
\begin{equation}
\begin{aligned}
x_{A'}&=x(\xi+\mathrm{d}\xi,\eta)\approx x +\frac{\partial x}{\partial \xi}\mathrm{d}\xi,\\
y_{A'}&=y(\xi+\mathrm{d}\xi,\eta)\approx y +\frac{\partial y}{\partial \xi}\mathrm{d}\xi,\\
x_{B'}&=x(\xi,\eta+\mathrm{d}\eta)\approx x +\frac{\partial x}{\partial \eta}\mathrm{d}\eta,\\
y_{B'}&=y(\xi,\eta+\mathrm{d}\eta)\approx y +\frac{\partial y}{\partial \eta}\mathrm{d}\eta,\\
x_{C'}&=x(\xi+\mathrm{d}\xi,\eta+\mathrm{d}\eta)\approx x +\frac{\partial x}{\partial \xi}\mathrm{d}\xi + \frac{\partial x}{\partial \eta}\mathrm{d}\eta,\\
y_{C'}&=y(\xi+\mathrm{d}\xi,\eta+\mathrm{d}\eta)\approx y +\frac{\partial y}{\partial \xi}\mathrm{d}\xi + \frac{\partial y}{\partial \eta}\mathrm{d}\eta.
\end{aligned}
\end{equation}
$$

因此四边形 $P'A'C'B'$ 是平行四边形，其面积为

$$
\begin{equation}
S_{P'A'C'B'} = \left|\overrightarrow{P'A'}\times\overrightarrow{P'B'}\right|  = \left|\det(\mathbf{J})\right|\,\mathrm{d}\xi\mathrm{d}\eta,
\end{equation}
$$

因此

$$
\frac{S_{P'A'C'B'}}{S_{PACB}} = \left|\det(\mathbf{J})\right|.
$$

于是

$$
\begin{equation}
\begin{aligned}
\mathcal{D'} &= \int_{\mathcal{D'}}\mathrm{d}x\mathrm{d}y =
\lim_{n\rightarrow\infty}\sum_{n}\mathrm{d}\mathcal{D'}\\
&=\lim_{n\rightarrow\infty}\sum_{n}\left|\det(\mathbf{J})\right|\mathrm{d}\mathcal{D} = \int_{\mathcal{D}}\left|\det(\mathbf{J})\right|\ \mathrm{d}\xi\mathrm{d}\eta.
\end{aligned}
\end{equation}
$$

类似地

$$
\int_{\mathcal{D'}}f(x,y)\ \mathrm{d}x\mathrm{d}y = \int_{\mathcal{D'}}f(\xi,\eta)\cdot\left|\det(\mathbf{J})\right|\ \mathrm{d}\xi\mathrm{d}\eta.
$$

对于 $n$ 维的情形

$$
\int_{\mathcal{D'}}f(x,y,\cdots)\ \mathrm{d}\mathcal{D'} = \int_{\mathcal{D'}}f(\xi,\eta,\cdots)\cdot\left|\det(\mathbf{J})\right|\ \mathrm{d}\mathcal{D}
$$

其中

$$
\mathbf{J} = \left[
\begin{matrix}
\frac{\partial x}{\partial \xi} & \frac{\partial x}{\partial \eta} & \cdots \\
\frac{\partial y}{\partial \xi} & \frac{\partial y}{\partial \eta} & \cdots  \\
\vdots & \vdots & \ddots
\end{matrix}
\right].
$$
:::


## 场变量插值

在完成几何映射后，通过形函数在参考单元上对场变量插值

```{margin}
$u_{i}$ 是物理单元节点的物理量取值
```

$$
u(x,y)=\sum_{i}N_{i}(\xi,\eta)u_{i}.
$$ (sec2-eq:field-variable-interpolation)

这里其实暗含了基函数与形函数的关系，即

$$
v_{i}(x,y) =  N_{i}(x(\xi,\eta),y(\xi,\eta)),
$$

场变量插值的核心目的是建立节点值与连续场之间的数学关联，从而支持物理量（如应变、应力）的梯度计算

根据链式法则

$$
\begin{equation}
\begin{aligned}
\begin{bmatrix}
\frac{\partial u}{\partial \xi} \\
\frac{\partial u}{\partial \eta}
\end{bmatrix}
=
\begin{bmatrix}
\frac{\partial x}{\partial \xi} & \frac{\partial y}{\partial \xi} \\
\frac{\partial x}{\partial \eta} & \frac{\partial y}{\partial \eta}
\end{bmatrix}
\begin{bmatrix}
\frac{\partial u}{\partial x} \\
\frac{\partial u}{\partial y}
\end{bmatrix}
=\mathbf{J}^{T}\begin{bmatrix}
\frac{\partial u}{\partial x} \\
\frac{\partial u}{\partial y}
\end{bmatrix},
\end{aligned}
\end{equation}
$$

因此

$$
\begin{equation}
\begin{aligned}
\begin{bmatrix}
\frac{\partial u}{\partial x} \\
\frac{\partial u}{\partial y}
\end{bmatrix}
=
\mathbf{J}^{-T}
\begin{bmatrix}
\frac{\partial u}{\partial \xi} \\
\frac{\partial u}{\partial \eta}
\end{bmatrix} 
= \mathbf{J}^{-T}\sum_{i}u_{i}
\begin{bmatrix}
\frac{\partial N_{i}}{\partial \xi} \\
\frac{\partial N_{i}}{\partial \eta}
\end{bmatrix} 
.
\end{aligned}
\end{equation}
$$

```{note}
通过几何映射与场变量插值，无需显式求解 $\left.\phi\right|_{E}$ 的表达式，即可在单元 $E$ 上完成积分运算和场变量梯度的计算，从而实现对一般物理单元的规范化统一处理

如果几何映射是一一映射，则单元 $E$ 上的基函数可以写为 $N_{i}(\xi(x,y),\eta(x,y))$

通常，几何映射需保持一一对应，否则可能引发积分误差、场变量插值非唯一性、Jacobian 矩阵奇异等问题，进而导致数值不稳定和求解失败。因此，网格生成需满足一定的要求

```


## 等参变换与非等参变换

根据几何映射和场变量插值中所使用形函数阶次的差异，可分为等参变换和非等参变换

| **方法名称**       | **等参变换**                                              | **非等参变换度** | 
|:---------:|:--------------:|:--------:|
| **形函数一致性** | 几何映射与场变量插值使用相同阶数形函数 | 几何映射与场变量插值使用不同阶数形函数            | 
| **计算精度**     | 高（几何映射与场变量插值精度匹配）  |  几何映射精度可能低于场变量插值精度            |
| **适用场景**        | 曲边单元、高阶场分析（如二次单元） | 简单几何+高阶场（如线性网格+二次温度场）           |
| **计算复杂度**      | 较高（需处理高阶雅可比矩阵）  | 较低（几何映射简单）           |
