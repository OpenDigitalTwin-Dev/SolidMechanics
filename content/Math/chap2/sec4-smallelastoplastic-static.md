# 小变形弹塑性问题（静力学）

在涉及塑性变形的问题中，除了需要考虑基本的力学方程外，还需引入屈服准则、流动法则和硬化法则，因此其数学模型更加复杂。此处考虑**小变形、小旋转**的弹塑性问题，并使用**静力学**求解

## 求解方程

**平衡方程（动量守恒方程）：**

$$
\begin{equation}
\nabla\cdot \boldsymbol{\sigma} + \mathbf{f} = \rho\ddot{\mathbf{u}},
\end{equation}
$$

在静力学求解中，假定加速度 $\mathbf{a}=\ddot{\mathbf{u}} = \mathbf{0}$

**几何方程**

$$
\begin{equation}
\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla \mathbf{u} + \nabla\mathbf{u}^{T}),
\end{equation}
$$

**应变分解**

$$
\begin{equation}
\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^e + \boldsymbol{\varepsilon}^p,
\end{equation}
$$

**弹塑性本构关系**

$$
\begin{equation}
\boldsymbol{\sigma} = \mathbf{D} : \boldsymbol{\varepsilon}^e = \mathbf{D} : (\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^p)，
\end{equation}
$$

**屈服函数**

例如，对于经典的 [Mises 准则](../../Plasticity/chap2/sec2-mises.md)

$$
\begin{equation}
f(\boldsymbol{\sigma}, \bar{\varepsilon}^p) = \sqrt{\frac{3}{2} \mathbf{s} : \mathbf{s}} - \sigma_y(\bar{\varepsilon}^p)，
\end{equation}
$$

其中，$\sigma_y(\bar{\varepsilon}^p)$ 是屈服应力，$\bar{\varepsilon}^p$ 是[等效塑性应变](../../Plasticity/chap1/sec2-uniaxial.md)，基于各向同性的 Mises 准则，其通常定义为

$$
\begin{equation}
\dot{\bar{\varepsilon}}^{p} = \sqrt{\frac{2}{3} \dot{\boldsymbol{\varepsilon}}^p : \dot{\boldsymbol{\varepsilon}}^p}=\sqrt{\frac{2}{3}}\|\dot{\boldsymbol{\varepsilon}}^p\|.
\end{equation}
$$


**流动法则**

例如，考虑关联性流动法则

$$
\begin{equation}
\dot{\boldsymbol{\varepsilon}}^p = \dot{\gamma} \frac{\partial f}{\partial \boldsymbol{\sigma}}，
\end{equation}
$$

其中，$\dot{\gamma}$ 是[塑性乘子](../../Plasticity/chap3/intro.md)

**硬化法则**

例如，对于线性硬化

$$
\begin{equation}
\sigma_y(\bar{\varepsilon}^p) = \sigma_{y0} + H\bar{\varepsilon}^{p},
\end{equation}
$$

其中，$\sigma_{y0}$ 是初始屈服强度，$H$ 是硬化模量

**塑性加载/卸载条件**

也称 Kuhn-Tucker 条件

$$
\begin{equation}
f \leq 0, \quad \dot{\gamma} \geq 0, \quad \dot{\gamma} f = 0,
\end{equation}
$$

当

- $f<0$，则处于弹性状态，此时 $\dot{\gamma} = 0$
- $f=0$，则材料可能屈服，此时 $\dot{\gamma} \geq 0$

当 $\dot{\gamma} > 0$ 时，有 $f\equiv0$，因此

$$
\begin{equation}
  \dot{f} = \frac{\partial f}{\partial \boldsymbol{\sigma}} : \dot{\boldsymbol{\sigma}} + \frac{\partial f}{\partial \bar{\varepsilon}^p} \dot{\bar{\varepsilon}}^p = 0,
\end{equation}
$$

即塑性流动始终发生在屈服面上，这也是塑性流动的**一致性条件**

**边界条件**

以及用来描述边界载荷的三类边界条件

$$
\begin{equation}
\begin{aligned}
\mathbf{u} &= \tilde{\mathbf{u}},\quad &\text{on}\,\, \Gamma_{D},\\
\boldsymbol{\sigma}\mathbf{n} &= \tilde{\mathbf{p}},\quad &\text{on}\,\, \Gamma_{N},\\
\boldsymbol{\sigma}\mathbf{n} + \alpha\mathbf{u} &= \mathbf{f}_{R},\quad &\text{on}\,\, \Gamma_{R}.
\end{aligned}
\end{equation}
$$

## 有限元求解

### 静力学分析

弹塑性材料的响应具有明显的**路径依赖性**（历史相关性），即材料的本构状态会随着加载过程不断变化。因此，准确反映材料的历史演化过程，是实现高精度数值仿真的关键。尽管静力学分析侧重于最终的平衡状态，忽略了加载过程中的速率和惯性效应，但通过**将总载荷或总位移分解为多个加载步，逐步施加，并在每一步进行平衡迭代和状态变量更新**，可以更真实地反映材料在整个加载过程中的变化轨迹，从而提高仿真的准确性

静力学分析主要适用于结构或材料在静止或准静止状态下的受力响应研究，适合处理**惯性和速率效应可以忽略的情形**，如常温下的缓慢加载、结构稳定性分析等。在此范围内，分步加载方法能够有效捕捉弹塑性材料的路径依赖性，是静力学弹塑性分析的重要手段

### 时间离散（增量）

将总时间划分为 $N$ 个离散时刻，记为 $\{t_{i}\}_{i=1}^{N}$。在数值仿真中，通常根据第 $n$ 个时间点的状态递推求解第 $n+1$ 个时间点的状态，其中最关键的环节包括两个**非线性**问题的求解：

1. [在积分点处通过本构积分处理材料的弹塑性变形](../../Plasticity/chap5/intro.md)
2. 通过有限元方法求解结构的位移响应

两者协同作用，确保材料和结构在每个新时间步上的状态能够合理更新

### 有限元弱形式

与 [线弹性方程](../chap2/sec3-linearelasticity.md) 类似，弱形式为

$$
\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}) : \boldsymbol{\sigma} \, \mathrm{d}\Omega + \int_{\Gamma_{R}} \alpha\mathbf{u} \cdot \mathbf{v} \, \mathrm{d}S
= \int_{\Omega}\mathbf{f}\cdot \mathbf{v}\,\mathrm{d}\Omega + \int_{\Gamma_{N}} \tilde{\mathbf{p}} \cdot \mathbf{v} \, \mathrm{d}S + \int_{\Gamma_{R}} \mathbf{f}_{R} \cdot \mathbf{v} \, \mathrm{d}S,\quad \forall \, \mathbf{v} \in \, \mathcal{V},
$$

其中，$\mathbf{v}\in\mathcal{V}$ 是试验函数，$\mathbf{u} = \mathbf{\tilde{u}},\, \text{on}\, \Gamma_{D}$

### 有限元离散形式

设有限元解空间 $\mathcal{U}_{h}$ 的基函数为

$$
\boldsymbol{\phi}_{1},\boldsymbol{\phi}_{2},\cdots,\boldsymbol{\phi}_{N},
$$

$\boldsymbol{\phi}_{i} = \left[\phi_{x,i},\phi_{y,i},\phi_{z,i}\right]$，其中，$\phi_{x,i},\phi_{y,i},\phi_{z,i}$ 表示位移在 $x,y,z$ 方向的插值基函数，通常 $\phi_{x,i}=\phi_{y,i}=\phi_{z,i}=:\phi_{i}$，于是位移分布函数为

$$
\mathbf{u} = \sum_{i=1}^{N}\mathbf{u}_{i}\phi_{i},
$$

其中，$\mathbf{u}_{i} = \left[u_{x,i},u_{y,i},u_{z,i}\right]^{T}$. 测试函数空间 $\mathcal{V}_{h} = \mathcal{U}_{h}$，在节点 $i$ 上，测试函数选为

$$
\begin{bmatrix}
\phi_{i} \\ 0 \\ 0
\end{bmatrix},\quad 
\begin{bmatrix}
 0  \\ \phi_{i} \\ 0
\end{bmatrix},\quad
\begin{bmatrix}
 0 \\ 0 \\ \phi_{i} 
\end{bmatrix}，
$$

分别记为 $\mathbf{v}_{x,i},\mathbf{v}_{y,i},\mathbf{v}_{z,i}$

共计 $3N$ 个位移自由度 

$$
u_{x,1},u_{y,1},u_{z,1},u_{x,2},u_{y,2},u_{z,2},\cdots,u_{x,N},u_{y,N},u_{z,N},
$$

和 $3N$ 个求解方程

$$
\begin{equation}
\begin{aligned}
&\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \boldsymbol{\sigma} \, \mathrm{d}\Omega + \int_{\Gamma_{R}} \alpha\mathbf{u} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S \\
=& \int_{\Omega}\mathbf{f}\cdot \mathbf{v}_{*,i}\,\mathrm{d}\Omega + \int_{\Gamma_{N}} \tilde{\mathbf{p}} \cdot \mathbf{v}_{*,i}\ \mathrm{d}S + \int_{\Gamma_{R}} \mathbf{f}_{R} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S,\quad \forall \, \mathbf{v}_{*,i} \in \, \mathcal{V},\quad *=x,y,z;\ i=1:N.
\end{aligned}
\end{equation}
$$

不同于线弹性问题，由于 $\boldsymbol{\sigma}$ 是关于历史应变的非线性函数，因此上述方程是一个非线性方程组，通常采用 Newton-Rapshon 方法求解

将上述方程记为

$$
\mathbf{R}(\mathbf{u}) = \mathbf{F}^{\text{int}} + \mathbf{F}^{r}-\mathbf{F}^{\text{ext}} = \mathbf{0},
$$

其中

- 内力项向量：$\mathbf{F}^{\text{int}}:=\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \boldsymbol{\sigma} \, \mathrm{d}\Omega$
- Robin 边界条件贡献向量：$\mathbf{F}^{\text{r}}:=\int_{\Gamma_{R}} \alpha\mathbf{u} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S$
- 外力向量：$\mathbf{F}^{\text{ext}}:=\int_{\Omega}\mathbf{f}\cdot \mathbf{v}_{*,i}\,\mathrm{d}\Omega + \int_{\Gamma_{N}} \tilde{\mathbf{p}} \cdot \mathbf{v}_{*,i}\ \mathrm{d}S + \int_{\Gamma_{R}} \mathbf{f}_{R} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S$

#### $\mathbf{F}^{\text{int}}$ 对刚度矩阵的贡献

使用 Vogit 形式，对于每个单元，由于 $\mathbf{v}$ 选为单元上所有基函数，于是单元的内力项

$$
\mathbf{F}^{\text{int}} := \int_{E} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \boldsymbol{\sigma} \, \mathrm{d}E = \int_{E}\mathbf{B}^{T}\boldsymbol{\sigma}\ \mathbf{d}E,
$$

由于 

$$
\boldsymbol{\varepsilon}=\mathcal{B}\mathbf{u} = \mathbf{B}\mathbf{u}^{e},
$$

故 Jacobian 矩阵为

$$
\begin{equation}
\begin{aligned}
\mathbf{K}_{\text{int}}=\frac{\partial \mathbf{F}^{\text{int}}}{\partial \mathbf{u}^{e}} &= \int_{E}\mathbf{B}^{T}\frac{\partial \boldsymbol{\sigma}}{\partial \mathbf{u}^{e}}\ \mathbf{d}E\\
&=\int_{E}\mathbf{B}^{T}\frac{\partial \boldsymbol{\sigma}}{\partial \boldsymbol{\varepsilon}}\frac{\partial \boldsymbol{\varepsilon}}{\partial \mathbf{u}^{e}} \mathbf{d}E\\
&=\int_{E}\mathbf{B}^{T}\mathbf{D}_{ep}^{\text{alg}}\ \mathbf{B} \mathbf{d}E,
\end{aligned}
\end{equation}
$$

其中，$\mathbf{D}_{ep}^{\text{alg}}$ 是[一致性切线模量](../../Plasticity/chap5/returnmapping.md)

#### $\mathbf{F}^{\text{r}}$ 对刚度矩阵的贡献

$$
\begin{equation}
\begin{aligned}
\mathbf{F}^{r}&=\int_{\Gamma_{R,E}} \alpha\mathbf{u} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S=\int_{\Gamma_{R,E}} \alpha\mathbf{N}^{T}\mathbf{u}\, \mathrm{d}S.
\end{aligned}
\end{equation}
$$

由于

$$
\mathbf{u} = \mathbf{N}\mathbf{u}^{e},
$$

故

$$
\begin{equation}
\begin{aligned}
\mathbf{K}_{r} = \frac{\partial \mathbf{F}^{r}}{\partial \mathbf{u}^{e}}&=\int_{\Gamma_{R}} \alpha\frac{\partial \mathbf{u}}{\partial \mathbf{u}^{e}} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S\\
&=\int_{\Gamma_{R}} \alpha\left(\frac{\partial \mathbf{u}}{\partial \mathbf{u}^{e}}\right)^{T} \mathbf{v}_{*,i} \, \mathrm{d}S\\
&=\int_{\Gamma_{R}} \alpha\mathbf{N}^{T}\mathbf{N} \, \mathrm{d}S.
\end{aligned}
\end{equation}
$$

#### $\mathbf{F}^{\text{ext}}$ 对右端项的贡献

$$
\begin{equation}
\begin{aligned}
\mathbf{F}^{\text{ext}}=\int_{E}\mathbf{N}^{T}\mathbf{f}\,\mathrm{d}E + \int_{\Gamma_{N,E}} \mathbf{N}^{T}\tilde{\mathbf{p}}\ \mathrm{d}S + \int_{\Gamma_{R,E}} \mathbf{N}^{T}\mathbf{f}_{R}\, \mathrm{d}S.
\end{aligned}
\end{equation}
$$