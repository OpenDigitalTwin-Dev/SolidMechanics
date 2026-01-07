# 应力度量

真实应力，是指在变形后构形 $\Omega$ 中的应力，其度量基于变形后构形 $\Omega$ 的单位面积，单位面积的方向由所选截面的位置和取向决定

$$
\mathbf{t}(\mathbf{n})=\lim_{\Delta a\rightarrow0}\frac{\Delta \mathbf{f}(\mathbf{n})}{\Delta a}
$$

## Cauchy 公式与应力张量

取一体积为 $\Delta v$ 的微元四面体，其各个截面上获得的应力（朝侧外正）和面积分别为 $-\mathbf{t}_{1},-\mathbf{t}_{2},-\mathbf{t}_{3},\mathbf{t}$ 和 $\Delta a_{1},\Delta a_{2},\Delta a_{3},\Delta a$，根据牛顿第二定律，有

$$
\mathbf{t}\Delta a-\mathbf{t}_{1}\Delta a_{1}-\mathbf{t}_{2}\Delta a_{2}-\mathbf{t}_{3}\Delta a_{3}+\rho\Delta v\mathbf{f}=\rho\Delta v \mathbf{a}
$$

其中，$\rho$ 是密度，$\mathbf{f}$ 是体积力，$\mathbf{a}$ 是加速度。由于

$$
\Delta a\mathbf{n}-\Delta a_{1}\mathbf{e}_{1}-\Delta a_{1}\mathbf{e}_{2}-\Delta a_{1}\mathbf{e}_{3}=\mathbf{0}
$$

其中，$\mathbf{n},\mathbf{e}_{i}$ 分别是四个面对应的单位外法向，于是有

$$
\Delta a_{i}=(\mathbf{n}\cdot\mathbf{e}_{i})\Delta a,\quad i=1,2,3
$$

由于 $\Delta v$ 是 $\Delta a$ 的高阶无穷小项，因此

$$
\mathbf{t} = (\mathbf{n}\cdot\mathbf{e}_{i})\mathbf{t}_{i}=\mathbf{t}_{i}(\mathbf{n}\cdot\mathbf{e}_{i})=\mathbf{t}_{i}\mathbf{e}_{i}^{T}\mathbf{n} = (\mathbf{t}_{i}\mathbf{e}_{i}^{T})\mathbf{n},
$$

至此，定义应力张量（Cauchy 应力张量）

$$
\boldsymbol{\sigma}=\mathbf{t}_{i}\mathbf{e}_{i}^{T}=\mathbf{t}_{1}\mathbf{e}_{1}^{T}+\mathbf{t}_{2}\mathbf{e}_{2}^{T}+\mathbf{t}_{3}\mathbf{e}_{3}^{T}
$$

此时

$$
\mathbf{t}(\mathbf{n})=\boldsymbol{\sigma}\mathbf{n}
$$

若 $\mathbf{e}_{i}$ 取为标准正交基，则 $\boldsymbol{\sigma}$ 的形式与[线弹性力学部分](../../Elasticity/sec3-balance-equa.md)推导一致

## Piola-Kirchhoff 应力张量

Cauchy 应力张量是单点应力状态最自然，最符合物理的度量方式

在物质（Lagrange）描述中，材料体的运动方程或平衡方程必须针对时刻 $t$ 的变形后的当前构型 $\Omega$ 进行推导。然而，由于变形后构型的几何形状通常未知，相关方程只能以已知的参考构型 $\Omega_{r}$ 为基础进行表述。为此，需要引入不同类型的应力度量。当体积和面积从变形后构型变换到参考构型时，这些应力度量会以一种自然的方式出现。需要注意的是，这些应力度量本质上属于纯数学范畴

### 第一 Piola-Kirchhoff 应力张量

考虑当前构型上的区域 $\mathrm{d}\mathbf{a}$ 上的力 $\mathrm{d}\mathbf{f}$，于是，根据 Nanson 公式，有

$$
\mathrm{d}\mathbf{f}=\boldsymbol{\sigma}\mathbf{n}\mathrm{d}a=\boldsymbol{\sigma}J\mathbf{F}^{-T}\mathbf{N}\mathrm{d}A = \mathbf{P}\mathbf{N}\mathrm{d}A,
$$

其中

$$
\mathbf{P} = J\boldsymbol{\sigma}\mathbf{F}^{-T}
$$

是第一 Piola-Kirchhoff 应力张量（简称为 PK1 应力张量），通常，PK1 应力张量不是对称的

### 第二 Piola-Kirchhoff 应力张量

第一 Piola-Kirchhoff 应力张量定义为

$$
\mathbf{S}=\mathbf{F}^{-1}\mathbf{P} = J\mathbf{F}^{-1}\boldsymbol{\sigma}\mathbf{F}^{-T}
$$

简称为 PK2 应力张量，常用于大变形分析