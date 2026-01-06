# 构型与描述

```{figure} ../../../images/Continuum/chap1/configuration.png
---
width: 400px
name: sec1-fig:stress-1
---
构型与连续体映射
```

考虑连续物质体（下简称物质体） $\mathcal{B}$，在给定几何条件和外力作用下，$\mathcal{B}$ 发生宏观几何变化，称为变形。变形过程中，$\mathcal{B}$ 占据的空间区域随时间连续演化，其在任一时刻所占据的空间区域称为**构型**，记为 $\Omega$

如下图所示，物质体 $\mathcal{B}$ 在初始时刻的构型为 $\Omega_0$，称为参考构型；在当前时刻的构型为 $\Omega$，称为当前构型。映射

$$
\mathcal{X}:\Omega_{0}\rightarrow \Omega
$$

称为物质体 $\mathcal{B}$ 的变形映射（或运动映射），它给出了物质点从参考位置 $\mathbf{X}$ 到当前位置 $\mathbf{x}=\mathcal{X}(\mathbf{X})$ 的变换关系


## 物质描述与空间描述

对连续体的变形通常有两种数学描述：物质描述，也称为 **Lagrangian 描述**；空间描述，也称为 **Euler 描述**

### 物质描述

```{figure} ../../../images/Continuum/chap1/material.png
---
width: 400px
name: sec1-fig:material
---
物质描述
```

物质描述跟踪物质体中每个物质点的运动历程

$$
\mathbf{x}=\mathcal{X}(\mathbf{X}, t),\quad \mathbf{X}=\mathcal{X}(\mathbf{X},0),
$$

对于分布在物质体上的物理量 $\phi$，其物质描述为

$$
\phi=\phi(\mathbf{X}, t),
$$

即初始时刻占据位置 $\mathbf{X} \in \Omega_0$ 的物质点在 $t$ 时刻的物理量值（此时它已经运动到了 $\mathbf{x}$）。因此，物质描述采用跟随物质点运动的观察方式，关注**特定**物质点所携带物理量随时间的演化



物质描述常用于研究固体的应力和变形，因为通常关注的是物体本身及其在固定结构上的响应，而不关心它所处的具体空间位置

### 空间描述

```{figure} ../../../images/Continuum/chap1/spacial.png
---
width: 400px
name: sec1-fig:spacial
---
空间描述
```

空间描述观察固定空间位置的状态变化

$$
\phi=\phi(\mathbf{x},t),\quad \mathbf{X}=\mathbf{X}(\mathbf{x}, t),
$$

即空间位置 $\mathbf{x}\in\Omega$ 处的物理量随时间的变化。因此，空间描述关注的是场随时间的变化


而空间描述则常用于研究流体运动，此时关注的是固定空间位置上的流动状态（如密度、温度、压力等），而不是那些瞬时占据该空间位置的物质微粒

### 物质导数

对于确定的物质点 $\mathbf{X}$，其所携带的物理量 $\phi$ 随时间的变化可表示为

$$
\frac{\mathrm{d}}{\mathrm{d}t}\left[\phi(\mathbf{X},t)\right],
$$

这一时间导数被称为**物质导数**

根据链式法则，有

```{margin}
物质点 $\mathbf{X}$ 的空间位置也随时间变化 
```

$$
\begin{aligned}
\frac{\mathrm{d}}{\mathrm{d}t}\left[\phi(\mathbf{X},t)\right] &= \frac{\partial \phi}{\partial t} + \frac{\partial \phi}{\partial X_{i}}\frac{\partial X_{i}}{\partial t} \\
&=\frac{\partial \phi}{\partial t} + \left(\frac{\partial \phi}{\partial x_{j}}\frac{\partial x_{j}}{\partial X_{i}}\right)\frac{\partial X_{i}}{\partial t}\\
&=\frac{\partial \phi}{\partial t} + \frac{\partial \phi}{\partial x_{j}}\left(\frac{\partial x_{j}}{\partial X_{i}}\frac{\partial X_{i}}{\partial t}\right)\\
&=\frac{\partial \phi}{\partial t} + \frac{\partial \phi}{\partial x_{j}}\frac{\partial x_{j}}{\partial t}\\
&=\frac{\partial \phi}{\partial t} + \mathbf{v}\cdot\nabla\phi
\end{aligned}
$$

其中，$\mathbf{v}=\dot{\mathbf{x}}$ 是速度场

于是得到空间场的物质导数算子

$$
\frac{\mathrm{d}}{\mathrm{d}t}=\frac{\partial}{\partial t} + \mathbf{v}\cdot\nabla
$$

```{admonition} 示例
:class: tip, dropdown

例如，对于 $t$ 时刻占据位置 $\mathbf{x}$ 的物质点 $\mathbf{X}$ 的加速度为

$$
\mathbf{a}(\mathbf{x},t)=\frac{\mathrm{d} \mathbf{v}(\mathbf{x},t)}{\mathrm{d}t}=\frac{\partial \mathbf{v}}{\partial t}+\mathbf{v}\cdot\nabla\mathbf{v},
$$

即

$$
a_{i} = \frac{\partial v_{i}}{\partial t}+v_{j}\frac{\partial v_{i}}{\partial x_{j}}.
$$

```

### 位移场

```{figure} ../../../images/Continuum/chap1/displacement.png
---
width: 400px
name: sec1-fig:displacement
---
位移场
```

变形通常可以通过物质体内各物质点的相对位移来刻画，对于物质点 $\mathbf{X}$，其位移为

$$
\mathbf{u} = \mathbf{x} - \mathbf{X},
$$

在物质描述中，上式可以写为

$$
\mathbf{u}({\color{red}\mathbf{X}},t) = \mathbf{x}({\color{red}\mathbf{X}},t) - {\color{red}\mathbf{X}},
$$

而在空间描述中，写为

$$
\mathbf{u}({\color{red}\mathbf{x}},t) = {\color{red}\mathbf{x}} - \mathbf{X}({\color{red}\mathbf{x}},t),
$$

