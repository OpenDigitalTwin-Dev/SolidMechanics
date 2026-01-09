# 连续介质力学方程

## 质量守恒方程

也被成为连续方程，其可以表述为

*在一个封闭系统内，质量在化学反应或物理变化过程中保持不变，不会凭空产生，也不会凭空消失*

假设物质体中的质量点以速度 $\mathbf{v}(\mathbf{x},t)$ 运动，考虑一个空间区域 $\Omega$，其边界表面 $\Gamma$ 始终跟随一组特定的物质元素移动。因此，$\Omega$ 是一个**随体区域**，其包含的质量始终保持不变——即，满足质量守恒

### 空间描述

对于分布函数（或物理场） $\phi(\mathbf{x},t)$，其变化满足

$$
\frac{\mathrm{d} }{\mathrm{d}t}\int_{\Omega}\phi(\mathbf{x},t)\mathrm{d}v=\int_{\Omega}\frac{\partial \phi}{\partial t}\mathrm{d}v+\oint_{\Gamma}\phi\mathbf{v}\cdot\mathbf{n}\mathrm{d}s
$$ (sec6-eq:contiuum-spacial)

即区域 $\Omega$ 中 $\phi$ 的总变化率，等于 $\phi$ 在区域内的瞬时变化率加上通过通过边界 $\Gamma$ 的流出（或流入）速率

将密度场函数 $\rho(\mathbf{x},t)$ 代入，质量守恒要求

$$
0=\frac{\mathrm{d} }{\mathrm{d}t}\int_{\Omega}\rho\mathrm{d}v=\int_{\Omega}\frac{\partial \rho}{\partial t}\mathrm{d}v+\oint_{\Gamma}\rho\mathbf{v}\cdot\mathbf{n}\mathrm{d}s
$$

将面积分转换为体积分

$$
\oint_{\Gamma}\rho\mathbf{v}\cdot\mathbf{n}\mathrm{d}s = \int_{\Omega}\nabla\cdot(\rho\mathbf{v})\mathrm{d}v
$$

于是得到

$$
\int_{\Omega}\left[\frac{\partial \rho}{\partial t} + \nabla\cdot(\rho\mathbf{v})\right]\mathrm{d}v = 0
$$

由区域 $\Omega$ 的任意性，得到其局部形式

$$
\frac{\partial \rho}{\partial t} + \nabla\cdot(\rho\mathbf{v}) = 0
$$ (sec6-eq:contiuum-local)

### 物质描述

设物质体 $\mathcal{B}$ 在初始时刻的构型为 $\Omega_{0}$，密度分布为 $\rho_{0}(\mathbf{X}, 0)$；在时刻 $t$，其当前构型为 $\Omega$，密度分布为 $\rho(\mathbf{X}, t)$，于是，根据质量守恒原理，有

$$
\int_{\Omega_{0}}\rho_{0}\mathrm{d}V=\int_{\Omega}\rho\mathrm{d}v
$$

根据体积变换公式，得到

$$
\int_{{\color{red}\Omega_{0}}}(\rho_{0}-J\rho)\mathrm{d}V = 0
$$

由于 $\Omega_{0}$ 的任意性，得到其局部形式

$$
\rho_{0}=J\rho
$$

### Reynolds 输运定理

代入 $\phi = \rho Q$ 到方程 {eq}`sec6-eq:contiuum-spacial`，并将面积分转换为体积分得到

$$
\begin{aligned}
\frac{\mathrm{d} }{\mathrm{d}t}\int_{\Omega}\rho Q\mathrm{d}v&=\int_{\Omega}\left(\frac{\partial (\rho Q)}{\partial t}+\nabla \cdot(\rho Q\mathbf{v})\right)\mathrm{d}v\\
&=\int_{\Omega}\left(\frac{\partial \rho}{\partial t} Q+\frac{\partial Q}{\partial t} \rho+\nabla Q\cdot(\rho\mathbf{v})+Q\nabla\cdot(\rho\mathbf{v})\right)\mathrm{d}v
\end{aligned}
$$

根据连续性方程 {eq}`sec6-eq:contiuum-local`，有

$$
\frac{\partial \rho}{\partial t} Q+Q\nabla\cdot(\rho\mathbf{v}) = Q(\frac{\partial \rho}{\partial t}+\nabla\cdot(\rho\mathbf{v}))=0
$$

另一方面，根据物质导数算子 {eq}`sec1-eq:material-derivative`

$$
\frac{\partial Q}{\partial t} \rho+\nabla Q\cdot(\rho\mathbf{v}) = \rho(\frac{\partial Q}{\partial t}+\nabla Q\cdot\mathbf{v})=\rho\frac{\mathrm{d}Q}{\mathrm{d}t}
$$

因此，上式可以写为

$$
\frac{\mathrm{d} }{\mathrm{d}t}\int_{\Omega}\rho Q\mathrm{d}v=\int_{\Omega}\rho\frac{\mathrm{d}Q}{\mathrm{d}t}\mathrm{d}v
$$ (sec6-eq:reynolds)

这被称为 Reynolds 输运定理

## 动量平衡方程

### 线动量平衡方程

*线动量的变化率等于作用在连续体上的所有力之和*

#### 空间形式

设 $\mathbf{f}$ 是体积力，$\mathbf{t}$ 是单位面积的表面力，线动量守恒要求

$$
\frac{\mathrm{d}}{\mathrm{d}\mathrm{t}}\int_{\Omega}\rho\mathbf{v}\mathrm{d}v=\oint_{\Gamma}\mathbf{t}\mathrm{d}s+\int_{\Omega}\mathbf{f}\mathrm{d}v=\int_{\Omega}\left(\nabla\cdot\boldsymbol{\sigma}+\mathbf{f}\right)\mathrm{d}v
$$

```{admonition} $\nabla\cdot\boldsymbol{\sigma}$
:class: tip, dropdown

记 $\boldsymbol{\sigma}_{i}$ 为 $\boldsymbol{\sigma}$ 的行向量

$$
\begin{aligned}
\oint_{\Gamma}\mathbf{t}\mathrm{d}s &= \oint_{\Gamma}\boldsymbol{\sigma}\mathbf{n}\mathrm{d}s=\oint_{\Gamma}\begin{bmatrix}\boldsymbol{\sigma}_{1}\cdot\mathbf{n}\\\boldsymbol{\sigma}_{2}\cdot\mathbf{n}\\\boldsymbol{\sigma}_{3}\cdot\mathbf{n}\end{bmatrix}\mathrm{d}s=\int_{\Omega}\begin{bmatrix}\nabla\cdot\boldsymbol{\sigma}_{1}\\\nabla\cdot\boldsymbol{\sigma}_{2}\\\nabla\cdot\boldsymbol{\sigma}_{3}\end{bmatrix}\mathrm{d}v
\end{aligned}=\int_{\Omega}\nabla\cdot\boldsymbol{\sigma}\mathrm{d}v
$$

```

根据 Reynolds 输运定理，得到

$$
0=\int_{\Omega}\left(\nabla\cdot\boldsymbol{\sigma}+\mathbf{f} -\rho\frac{\mathrm{d}\mathbf{v}}{\mathrm{d}\mathrm{t}}\right)\mathrm{d}v
$$ (sec6-eq:linear-momentum)

由 $\Omega$ 的任意性，得到其微分形式

$$
\nabla\cdot\boldsymbol{\sigma}+\mathbf{f} =\rho\frac{\mathrm{d}\mathbf{v}}{\mathrm{d}\mathrm{t}}
$$ (sec6-eq:linear-momentum-local)

代入物质导数算子 {eq}`sec1-eq:material-derivative`，得到

$$
\nabla\cdot\boldsymbol{\sigma}+\mathbf{f} =\rho\left(\frac{\partial \mathbf{v}}{\partial t}+\mathbf{v}\cdot\nabla\mathbf{v}\right)
$$

写为分量形式

```{margin}
$[\nabla\mathbf{v}]_{ij} = \frac{\partial v_{i}}{\partial x_{j}}$
```

$$
\frac{\sigma_{ij}}{\partial x_{j}} + f_{i} = \rho\left(\frac{\partial v_{i}}{\partial t} + v_{j}\frac{\partial v_{i}}{\partial x_{j}}\right)
$$


#### 物质形式

将积分变换到初始构型

$$
\begin{aligned}
\int_{\Omega}\nabla\cdot\boldsymbol{\sigma}\mathrm{d}v
&=\int_{\Omega_{0}}\nabla_{0}\cdot(\boldsymbol{\sigma}\mathbf{F}^{-T}J)\mathrm{d}V=\int_{\Omega_{0}}\nabla_{0}\cdot\mathbf{P}\mathrm{d}V
\end{aligned}
$$

```{admonition} 证明
:class: tip, dropdown

记

$$
\nabla\cdot\boldsymbol{\sigma} = 
\begin{bmatrix}
\frac{\partial \sigma_{xx}}{\partial x} + \frac{\partial \sigma_{xy}}{\partial y} + \frac{\partial \sigma_{xz}}{\partial z} \\
\frac{\partial \sigma_{yx}}{\partial x} + \frac{\partial \sigma_{yy}}{\partial y} + \frac{\partial \sigma_{yz}}{\partial z} \\
\frac{\partial \sigma_{zx}}{\partial x} + \frac{\partial \sigma_{zy}}{\partial y} + \frac{\partial \sigma_{zz}}{\partial z} \\
\end{bmatrix}=\begin{bmatrix}
\nabla\cdot\boldsymbol{\sigma}_{1}\\
\nabla\cdot\boldsymbol{\sigma}_{2}\\
\nabla\cdot\boldsymbol{\sigma}_{3}
\end{bmatrix}
$$

根据 Piola 恒等式 {eq}`sec2-eq:piola-eqs`，有

$$
\nabla\cdot\boldsymbol{\sigma}_{i}=\frac{1}{J}\nabla_{0}\cdot(J\mathbf{F}^{-1}\boldsymbol{\sigma}_{i})
$$

于是

$$
\begin{aligned}
\nabla\cdot\boldsymbol{\sigma}&=\frac{1}{J}\begin{bmatrix}
\nabla_{0}\cdot(J\mathbf{F}^{-1}\boldsymbol{\sigma}_{1})\\
\nabla_{0}\cdot(J\mathbf{F}^{-1}\boldsymbol{\sigma}_{2})\\
\nabla_{0}\cdot(J\mathbf{F}^{-1}\boldsymbol{\sigma}_{3})
\end{bmatrix}=\frac{1}{J}\nabla_{0}\cdot\begin{bmatrix}
(J\mathbf{F}^{-1}\boldsymbol{\sigma}_{1})^{T}\\
(J\mathbf{F}^{-1}\boldsymbol{\sigma}_{2})^{T}\\
(J\mathbf{F}^{-1}\boldsymbol{\sigma}_{3})^{T}
\end{bmatrix}\\
&= \frac{1}{J}\nabla_{0}\cdot(J\boldsymbol{\sigma}\mathbf{F}^{-T})=\frac{1}{J}\nabla_{0}\cdot\mathbf{P}
\end{aligned}
$$

故

$$
\int_{\Omega}\nabla\cdot\boldsymbol{\sigma}\mathrm{d}v = \int_{\Omega_{0}}J\nabla\cdot\boldsymbol{\sigma}\mathrm{d}V = \int_{\Omega_{0}}\nabla_{0}\cdot\mathbf{P}\mathrm{d}V 
$$

```

且

$$
\int_{\Omega}\rho\frac{\mathrm{d}\mathbf{v}}{\mathrm{d}\mathrm{t}}\mathrm{d}v = \int_{\Omega_{0}}\rho_{0}\frac{\mathrm{d}\mathbf{v}(\mathbf{X},t)}{\mathrm{d}\mathrm{t}}\mathrm{d}v
=\int_{\Omega_{0}}\rho_{0}\frac{\partial\mathbf{V}}{\partial\mathrm{t}}\mathrm{d}v$$

于是，方程 {eq}`sec6-eq:linear-momentum` 在初始构型上写为

$$
\begin{aligned}
0&=\int_{\Omega_{0}}\left(\nabla_{0}\cdot\mathbf{P}+\mathbf{f}_{0}-\rho_{0}\frac{\partial \mathbf{V}}{\partial t}\right)\mathrm{d}V\\
&=\int_{\Omega_{0}}\left(\nabla_{0}\cdot(\mathbf{F}\mathbf{S})+\mathbf{f}_{0}-\rho_{0}\frac{\partial \mathbf{V}}{\partial t}\right)\mathrm{d}V
\end{aligned}
$$

其中

$$
\mathbf{f}_{0} = J\mathbf{f},\quad 
$$

### 角动量平衡方程

*动量矩的变化率等于作用在连续体上的外力矩的矢量和*

若连续体没有体偶（即没有体积相关的力偶），即 $\lim_{\Delta V\rightarrow0}\Delta M/\Delta V=\mathbf{0}$，此时 Cauchy 应力张量 $\boldsymbol{\sigma}$ 对称，且角动量守恒要求满足

$$
\oint_{\Gamma}\mathbf{x}\times\mathbf{t}\mathrm{d}s+\int_{\Omega}\mathbf{x}\times\mathbf{f}\mathrm{d}v=\frac{\mathrm{d}}{\mathrm{d}t}\int_{\Omega}\mathbf{x}\times\rho\mathbf{v}\mathrm{d}v
$$

