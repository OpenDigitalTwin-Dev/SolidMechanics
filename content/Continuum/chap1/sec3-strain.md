# 应变度量

连续介质的几何变化可以通过多种方式进行度量，这里讨论一种通用的度量方法，该方法能够有效排除平移和旋转的影响，从而独立地反映介质的本质变形

考虑初始构型 $\Omega_{0}$ 上的微元段 $\mathrm{d}\mathbf{X}$，在当前构型 $\Omega$ 上为 $\mathrm{d}\mathbf{x} = \mathbf{F}\mathrm{d}\mathbf{X}$，于是


$$
\begin{aligned}
(\mathrm{d}S)^{2}&=\mathrm{d}\mathbf{X}\cdot\mathrm{d}\mathbf{X} = (\mathrm{d}\mathbf{x})^{T}(\mathbf{F}^{-T}\mathbf{F}^{-1})\mathrm{d}\mathbf{x}\\
(\mathrm{d}s)^{2}&=\mathrm{d}\mathbf{x}\cdot\mathrm{d}\mathbf{x}=（\mathrm{d}\mathbf{X})^{T}(\mathbf{F}^{T}\mathbf{F})\mathrm{d}\mathbf{X}
\end{aligned}
$$

上式中

$$
\begin{aligned}
\mathbf{C}&=\mathbf{F}^{T}\mathbf{F}\\
\mathbf{B}&=\mathbf{C}^{-1}=\mathbf{F}^{-1}\mathbf{F}^{-T}
\end{aligned}
$$

$\mathbf{C}$ 被称为 右 Cauchy-Green 变形张量，是基于物质描述，$\mathbf{B}$ 被称为 Piola 变形张量

$$
\begin{aligned}
\mathbf{c}&=\mathbf{F}^{-T}\mathbf{F}^{-1}\\
\mathbf{b}&=\mathbf{c}^{-1}=\mathbf{F}\mathbf{F}^{T}
\end{aligned}
$$

$\mathbf{b}$ 被称为 左 Cauchy-Green 应变张量，也称为 Finger 变形张量，是基于空间描述

## Green-Lagrange 应变张量

任意微元段的长度变化能够真实地反映出物质体的形变特征

$$
(\mathrm{d}s)^{2} - (\mathrm{d}S)^{2} = ({\color{red}\mathrm{d}\mathbf{X}})^{T}(\mathbf{F}^{T}\mathbf{F} - \mathbf{I}){\color{red}\mathrm{d}\mathbf{X}}=2({\color{red}\mathrm{d}\mathbf{X}})^{T}\mathbf{E}{\color{red}\mathrm{d}\mathbf{X}}
$$

其中

$$
\begin{aligned}
\mathbf{E}&=\frac{1}{2}(\mathbf{F}^{T}\mathbf{F} - \mathbf{I}) = \frac{1}{2}(\mathbf{C} - \mathbf{I})\\
&=\frac{1}{2}[\nabla_{0}\mathbf{u}+(\nabla_{0}\mathbf{u})^{T}+(\nabla_{0}\mathbf{u})^{T}\cdot(\nabla_{0}\mathbf{u})]
\end{aligned}
$$

被称为 Green-Lagrange 应变张量（或简称为 Green 张量）；Green 张量是对称张量，当且仅当长度变化为 0 时，$\mathbf{E}=\mathbf{0}$

写为分量形式，有

$$
\begin{aligned}
C_{IJ} &= \frac{x_{k}}{X_{I}}\frac{x_{k}}{X_{J}}\\
E_{IJ} &= \frac{1}{2}\left(\frac{\partial u_{I}}{X_{J}} + \frac{\partial u_{J}}{X_{I}} + \frac{\partial u_{k}}{X_{I}}\frac{\partial u_{k}}{X_{J}}\right)
\end{aligned}
$$

注意到，$\mathbf{C}$ 和 $\mathbf{E}$ 都是物质描述下的应变张量

## Cauchy 和 Euler 应变张量

使用空间描述表征微元长度变化

$$
(\mathrm{d}s)^{2} - (\mathrm{d}S)^{2} = ({\color{red}\mathrm{d}\mathbf{x}})^{T}(\mathbf{I} - \mathbf{F}^{-T}\mathbf{F}^{-1}){\color{red}\mathrm{d}\mathbf{x}}=2({\color{red}\mathrm{d}\mathbf{x}})^{T}\mathbf{e}{\color{red}\mathrm{d}\mathbf{x}},
$$

其中

$$
\begin{aligned}
\mathbf{e}&= \frac{1}{2}(\mathbf{I} - \mathbf{F}^{-T}\mathbf{F}^{-1})=\frac{1}{2}(\mathbf{I}-\mathbf{b}^{-1})\\
&=\frac{1}{2}[\mathbf{I} - (\mathbf{I} - \nabla\mathbf{u})^{T}(\mathbf{I} - \nabla\mathbf{u})]\\
&=\frac{1}{2}[\nabla\mathbf{u} + (\nabla\mathbf{u})^{T} - (\nabla\mathbf{u})^{T}\nabla\mathbf{u}]
\end{aligned}
$$

被称为 Euler-Almansi 应变张量 或 Euler 应变张量，其分量形式为

$$
e_{ij}=\frac{1}{2}\left(\delta_{ij}-\frac{\partial X_{K}}{\partial x_{i}}\frac{\partial X_{K}}{\partial x_{j}}\right)=\frac{1}{2}\left(\frac{\partial u_{i}}{\partial x_{j}}+\frac{\partial u_{j}}{\partial x_{i}}-\frac{\partial u_{k}}{\partial x_{i}}\frac{\partial u_{k}}{\partial x_{j}}\right)
$$

注意到，$\mathbf{b}$ 和 $\mathbf{e}$ 都是空间描述下的应变张量

## 度量构型变换

在空间描述和物质描述下的变换通常称为 push-forward 算子和 pull-back 算子，前者将参考构型 $\Omega_{0}$ 下的描述转换到当前构型 $\Omega$ 下，后者则反之。对于 $\mathbf{E}$ 和 $\mathbf{e}$，有

$$
\begin{aligned}
\mathbf{e}&= \frac{1}{2}(\mathbf{I} - \mathbf{F}^{-T}\mathbf{F}^{-1})=\frac{1}{2}\mathbf{F}^{-T}(\mathbf{F}^{T}\mathbf{F}-\mathbf{I})\mathbf{F}^{-1}\\
&=\mathbf{F}^{-T}\mathbf{E}\mathbf{F}^{-1}
\end{aligned}
$$

反之

$$
\mathbf{E} = \mathbf{F}^{T}\mathbf{e}\mathbf{F}
$$

## 无穷小应变张量与旋转

### 无穷小应变张量

当

$$
\frac{\partial u_{I}}{\partial X_{J}} = O(\epsilon)
$$

时，有

$$
\mathbf{E}_{IJ}\approx\frac{1}{2}\left(\frac{\partial u_{I}}{X_{J}} + \frac{\partial u_{J}}{X_{I}}\right) = O(\epsilon)
$$

并且有

$$
|\nabla \mathbf{u}| \approx |\nabla_{0} \mathbf{u}| = O(\epsilon)
$$

此时，无需再区分构型，可以忽略 $\mathbf{E}$ 和 $\mathbf{e}$ 的差异，统一使用无穷小应变张量 $\boldsymbol{\varepsilon}$ 表示

$$
\mathbf{E}\approx\mathbf{e}\approx\boldsymbol{\varepsilon}=\frac{1}{2}[\nabla_{0}\mathbf{u}+(\nabla_{0}\mathbf{u})^{T}],
$$

其分量形式为

$$
\varepsilon_{ij}=\frac{1}{2}\left(\frac{\partial u_{i}}{\partial X_{j}}+\frac{\partial u_{j}}{\partial X_{i}}\right).
$$

其中，$\gamma_{ij}=2\varepsilon_{ij},i\neq j$ 称为工程剪切应变

### 旋转

将 $\nabla_{0}\mathbf{u}$ 分解为对称和反对称的部分

$$
\nabla_{0}\mathbf{u} = \frac{1}{2}[\nabla_{0}\mathbf{u} + (\nabla_{0}\mathbf{u})^{T}] + \frac{1}{2}[\nabla_{0}\mathbf{u} - (\nabla_{0}\mathbf{u})^{T}] = \boldsymbol{\varepsilon} + \boldsymbol{\Omega}
$$

其中，对称的部分是无穷小应变张量，而反对称的部分是无穷小旋转张量；上述分解将应变分解为了对称剪切部分和旋转部分

$$
\Omega_{ij} = \frac{1}{2}\left(\frac{\partial u_{i}}{\partial X_{j}} - \frac{\partial u_{j}}{\partial X_{i}}\right),\quad \Omega_{ij} = -\Omega_{ji}
$$

三阶反对称矩阵只有三个独立元分量

$$
\boldsymbol{\Omega}=\begin{bmatrix}
0&\Omega_{12}&\Omega_{13}\\
-\Omega_{12}&0&\Omega_{23}\\
-\Omega_{13}&-\Omega_{23}&0
\end{bmatrix}
$$

$\boldsymbol{\Omega}$ 可以写为

$$
\begin{aligned}
\boldsymbol{\Omega} &= -\mathcal{E}\boldsymbol{\omega}\quad &\text{or} \quad \boldsymbol{\omega} &= -\frac{1}{2}\mathcal{E}:\boldsymbol{\Omega}\\
\Omega_{ij}&=-e_{ijk}\omega_{k} &\text{or} \quad \omega_{i}&=-\frac{1}{2}e_{ijk}\Omega_{jk}
\end{aligned}
$$

其中，$\mathcal{E}=e_{ijk}\mathbf{e}_{i}\mathbf{e}_{j}\mathbf{e}_{k}=e_{ijk}\mathbf{e}_{i}\otimes\mathbf{e}_{j}\otimes\mathbf{e}_{k}$ 是排序张量

$$
\omega_{i}=\frac{1}{2}e_{ijk}\frac{\partial u_{k}}{\partial X_{j}}\quad \text{or} \quad \boldsymbol{\omega}=\frac{1}{2}\nabla_{0}\times\mathbf{u}
$$

## 速度梯度场

速度梯度场的空间描述为

$$
\mathbf{l}=\nabla \mathbf{v}(\mathbf{x},t)\quad \text{or} \quad l_{ij}=\frac{\partial v_{i}}{\partial x_{j}}
$$

对速度梯度张量 $\mathbf{l}$ 进行分解，可得

$$
\mathbf{l}=\frac{1}{2}[\nabla \mathbf{v} + (\nabla \mathbf{v})^{T}] + \frac{1}{2}[\nabla \mathbf{v} - (\nabla \mathbf{v})^{T}]\equiv \mathbf{d} + \mathbf{w}，
$$

其中，对称部分 

$$
\mathbf{d}=\frac{1}{2}(\mathbf{l}+\mathbf{l}^{T})
$$ 

被称为变形率张量，用于刻画局部变形速率；反对称部分 

$$
\mathbf{w}=\frac{1}{2}(\mathbf{l}-\mathbf{l}^{T})
$$

被称为旋转率张量，用于描述局部旋转速率

使用物质描述表示速度梯度场

$$
\mathbf{l}=\nabla\mathbf{v}=\frac{\partial \dot{\mathbf{x}}}{\partial \mathbf{x}}=\frac{\partial \dot{\mathbf{x}}}{\partial \mathbf{X}}\frac{\partial \mathbf{X}}{\partial \mathbf{x}}=\dot{\mathbf{F}}\mathbf{F}^{-1}
$$

或

$$
\dot{\mathbf{F}}=\mathbf{l}\mathbf{F}
$$

由此，Green 应变张量 $\mathbf{E}$ 的物质时间导数为

$$
\begin{aligned}
\dot{\mathbf{E}}&=\frac{1}{2}\left(\dot{\mathbf{F}}^{T}\mathbf{F}+\mathbf{F}^{T}\dot{\mathbf{F}}\right)\\
&=\frac{1}{2}\left(\mathbf{F}^{T}\mathbf{l}^{T}\mathbf{F}+\mathbf{F}^{T}\mathbf{l}\mathbf{F}\right)\\
&=\mathbf{F}^{T}[\frac{1}{2}\left(\mathbf{l}^{T}+\mathbf{l}\right)]\mathbf{F}\\
&=\mathbf{F}^{T}\mathbf{d}\mathbf{F},
\end{aligned}
$$

类似地，Euler-Almansi 应变张量的时间导数为

$$
\begin{aligned}
\dot{\mathbf{e}}&=\frac{\mathrm{d}}{\mathrm{d}t}(\mathbf{F}^{-T})\mathbf{E}\mathbf{F}^{-1}+\mathbf{F}^{-T}\dot{\mathbf{E}}\mathbf{F}^{-1}+\mathbf{F}^{-T}\mathbf{E}\frac{\mathrm{d}}{\mathrm{d}t}(\mathbf{F}^{-1})\\
&=-\mathbf{F}^{-T}\dot{\mathbf{F}}^{T}\mathbf{F}^{-T}\mathbf{E}\mathbf{F}^{-1}+\mathbf{d}-\mathbf{F}^{-T}\mathbf{E}\mathbf{F}^{-1}\dot{\mathbf{F}}\mathbf{F}^{-1}\\
&=\mathbf{d}-\mathbf{l}^{T}\mathbf{e}-\mathbf{e}\mathbf{l}
\end{aligned}
$$

```{admonition} 矩阵逆的导数
:class: tip, dropdown

由于

$$
\mathbf{A}\mathbf{A}^{-1} = \mathbf{I},
$$

故

$$
\dot{\mathbf{A}}\mathbf{A}^{-1}+\mathbf{A}\frac{\mathrm{d}}{\mathrm{d}t}(\mathbf{A}^{-1})=\mathbf{0},
$$

于是

$$
\frac{\mathrm{d}}{\mathrm{d}t}(\mathbf{A}^{-1}) = -\mathbf{A}^{-1}\dot{\mathbf{A}}\mathbf{A}^{-1}
$$

```