# 小变形弹塑性问题（静力学）

在涉及塑性变形的问题中，除了需要考虑基本的力学方程外，还需引入屈服准则、流动法则和硬化法则，因此其数学模型更加复杂。此处考虑**小变形、小旋转**的弹塑性问题，并使用**静力学**求解

## 静力学分析

弹塑性材料的响应具有明显的**路径依赖性**（历史相关性），即材料的本构状态会随着加载过程不断变化。因此，准确反映材料的历史演化过程，是实现高精度数值仿真的关键。尽管静力学分析侧重于最终的平衡状态，忽略了加载过程中的速率和惯性效应，但通过**将总载荷或总位移分解为多个加载步，逐步施加，并在每一步进行平衡迭代和状态变量更新**，可以更真实地反映材料在整个加载过程中的变化轨迹，从而提高仿真的准确性

静力学分析主要适用于结构或材料在静止或准静止状态下的受力响应研究，适合处理**惯性和速率效应可以忽略的情形**，如常温下的缓慢加载、结构稳定性分析等。在此范围内，分步加载方法能够有效捕捉弹塑性材料的路径依赖性，是静力学弹塑性分析的重要手段

### 时间离散（增量）

将总时间划分为 $N$ 个离散时刻，记为 $\{t_{i}\}_{i=1}^{N}$。在数值仿真中，通常根据第 $n$ 个时间点的状态递推求解第 $n+1$ 个时间点的状态，其中最关键的环节包括两个**非线性**问题的求解：

1. [在积分点处通过本构积分处理材料的弹塑性变形](../../Plasticity/chap5/intro.md)
2. 通过有限元方法求解结构的位移响应

两者协同作用，确保材料和结构在每个新时间步上的状态能够合理更新


## 求解方程

**平衡方程（动量守恒方程）：**

$$
\begin{equation}
\nabla\cdot \boldsymbol{\sigma} + \mathbf{f} = \mathbf{0},
\end{equation}
$$

在静力学求解中，$\dot{\mathbf{u}} = \mathbf{0},\ddot{\mathbf{u}} = \mathbf{0}$

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

**弹性本构关系**

$$
\begin{equation}
\boldsymbol{\sigma} = \mathbb{C} : \boldsymbol{\varepsilon}^e = \mathbb{C} : (\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^p)，
\end{equation}
$$

**屈服准则**

例如，对于经典的 [Mises 准则](../../Plasticity/chap2/sec2-mises.md)

$$
\begin{equation}
f(\boldsymbol{\sigma}, \bar{\varepsilon}^p) = \sqrt{\frac{3}{2} \mathbf{s} : \mathbf{s}} - \sigma_y(\bar{\varepsilon}^p)\leq0，
\end{equation}
$$

其中，$\sigma_y(\bar{\varepsilon}^p)$ 是屈服应力，$\bar{\varepsilon}^p$ 是[等效塑性应变](../../Plasticity/chap1/sec2-uniaxial.md)，基于各向同性的 Mises 准则，其通常定义为

$$
\begin{equation}
\dot{\bar{\varepsilon}}^{p} = \sqrt{\frac{2}{3} \dot{\boldsymbol{\varepsilon}}^p : \dot{\boldsymbol{\varepsilon}}^p}=\sqrt{\frac{2}{3}}\|\dot{\boldsymbol{\varepsilon}}^p\|.
\end{equation}
$$

**塑性流动法则**

例如，考虑关联性流动法则

$$
\begin{equation}
\dot{\boldsymbol{\varepsilon}}^p = \dot{\gamma} \frac{\partial f}{\partial \boldsymbol{\sigma}}，
\end{equation}
$$

其中，$\dot{\gamma}$ 是[塑性乘子](../../Plasticity/chap3/intro.md)

**硬化规律**

例如，对于线性硬化

$$
\begin{equation}
\sigma_y(\bar{\varepsilon}^p) = \sigma_{y0} + H\bar{\varepsilon}^{p},
\end{equation}
$$

其中，$\sigma_{y0}$ 是初始屈服强度，$H$ 是硬化模量

**Kuhn-Tucker 条件**

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

描述边界载荷的三类边界条件

$$
\begin{equation}
\begin{aligned}
\mathbf{u} &= \tilde{\mathbf{u}},\quad &\text{on}\,\, \Gamma_{D},\\
\boldsymbol{\sigma}\mathbf{n} &= \tilde{\mathbf{p}},\quad &\text{on}\,\, \Gamma_{N},\\
\boldsymbol{\sigma}\mathbf{n} + \alpha\mathbf{u} &= \mathbf{f}_{R},\quad &\text{on}\,\, \Gamma_{R}.
\end{aligned}
\end{equation}
$$

## 弱形式

与 [线弹性方程](../chap2/sec3-linearelasticity.md) 类似，弱形式为

$$
\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}) : \boldsymbol{\sigma} \, \mathrm{d}V + \int_{\Gamma_{R}} \alpha\mathbf{u} \cdot \mathbf{v} \, \mathrm{d}S
= \int_{\Omega}\mathbf{f}\cdot \mathbf{v}\,\mathrm{d}V + \int_{\Gamma_{N}} \tilde{\mathbf{p}} \cdot \mathbf{v} \, \mathrm{d}S + \int_{\Gamma_{R}} \mathbf{f}_{R} \cdot \mathbf{v} \, \mathrm{d}S,\quad \forall \, \mathbf{v} \in \, \mathcal{V},
$$

其中，$\mathbf{v}\in\mathcal{V}$ 是试验函数，$\mathbf{u} = \mathbf{\tilde{u}},\, \text{on}\, \Gamma_{D}$

## 离散形式

类似地，我们得到 $3N$ 个求解方程

$$
\begin{equation}
\begin{aligned}
&\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \boldsymbol{\sigma} \, \mathrm{d}V + \int_{\Gamma_{R}} \alpha\mathbf{u} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S \\
=& \int_{\Omega}\mathbf{f}\cdot \mathbf{v}_{*,i}\,\mathrm{d}V + \int_{\Gamma_{N}} \tilde{\mathbf{p}} \cdot \mathbf{v}_{*,i}\ \mathrm{d}S + \int_{\Gamma_{R}} \mathbf{f}_{R} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S,\quad \forall \, \mathbf{v}_{*,i} \in \, \mathcal{V},\quad *=x,y,z;\ i=1:N.
\end{aligned}
\end{equation}
$$

$3N$ 个位移自由度 

$$
u_{x,1},u_{y,1},u_{z,1},u_{x,2},u_{y,2},u_{z,2},\cdots,u_{x,N},u_{y,N},u_{z,N},
$$


不同于线弹性问题，由于 $\boldsymbol{\sigma}$ 是关于历史应变的非线性函数，因此上述方程是一个非线性方程组，通常采用 Newton-Rapshon 方法求解

将求解方程组记为

$$
\mathbf{R}(\mathbf{u}) = \mathbf{F}^{\text{int}} + \mathbf{F}^{r}-\mathbf{F}^{\text{ext}} = \mathbf{0},
$$

其中

- 内力项向量：$\mathbf{F}^{\text{int}}:=\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \boldsymbol{\sigma} \, \mathrm{d}V,\,\forall \, \mathbf{v}_{*,i}$
- Robin 边界条件贡献向量：$\mathbf{F}^{\text{r}}:=\int_{\Gamma_{R}} \alpha\mathbf{u} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S,\,\forall \, \mathbf{v}_{*,i}$
- 外力向量：$\mathbf{F}^{\text{ext}}:=\int_{\Omega}\mathbf{f}\cdot \mathbf{v}_{*,i}\,\mathrm{d}V + \int_{\Gamma_{N}} \tilde{\mathbf{p}} \cdot \mathbf{v}_{*,i}\ \mathrm{d}S + \int_{\Gamma_{R}} \mathbf{f}_{R} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S,\,\forall \, \mathbf{v}_{*,i}$

此时，需要计算 $\mathbf{F}^{\text{int}}$ 和 $\mathbf{F}^{\text{r}}$ 对 $u_{*,i}$ 的导数


### 张量分量形式

#### $\mathbf{F}^{\text{int}}$ 对刚度矩阵的贡献

分别考虑每个物理单元上的计算

$$
\begin{equation}
\begin{aligned}
\int_{E_{\text{物理}}} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \boldsymbol{\sigma}(\boldsymbol{\varepsilon}(\mathbf{u})) \, \mathrm{d}V 
&=
\int_{E_{\text{物理}}} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \boldsymbol{\sigma}(\boldsymbol{\varepsilon}(\sum_{+,j}u_{+,j}\mathbf{v}_{+,j})) \, \mathrm{d}V,
\end{aligned}
\end{equation}
$$

由于基函数具有局部支撑性，因此只需考虑 $E_{\text{物理}}$ 上的基函数，将积分运算映射回参考单元，记为

$$
F_{*,i}^{\text{int}} = \int_{E_{\text{参考}}} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \boldsymbol{\sigma}(\boldsymbol{\varepsilon}(\sum_{+,j}u_{+,j}\mathbf{v}_{+,j}))\left|\det(\mathbf{J})\right| \, \mathrm{d}V,
$$

此时，$\mathbf{v}_{*,i},\mathbf{v}_{+,j}$ 为参考单元上所有形函数的组合，于是

$$
\begin{equation}
\begin{aligned}
\frac{\partial F_{*,i}^{\text{int}}}{\partial u_{+,j}} &= \int_{E_{\text{参考}}} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \frac{\partial \boldsymbol{\sigma}(\boldsymbol{\varepsilon}(\sum_{+,j}u_{+,j}\mathbf{v}_{+,j}))}{\partial u_{+,j}}\left|\det(\mathbf{J})\right| \, \mathrm{d}V\\
&= \int_{E_{\text{参考}}} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \left(\frac{\partial \boldsymbol{\sigma}(\boldsymbol{\varepsilon}(\sum_{+,j}u_{+,j}\mathbf{v}_{+,j}))}{\partial \boldsymbol{\varepsilon}}:\frac{\partial \boldsymbol{\varepsilon}}{\partial u_{+,j}}\right)\left|\det(\mathbf{J})\right| \, \mathrm{d}V\\
&=\int_{E_{\text{参考}}} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \left(\mathbb{C}_{ep}^{\text{alg}}:\frac{\partial \boldsymbol{\varepsilon}}{\partial u_{+,j}}\right)\left|\det(\mathbf{J})\right| \, \mathrm{d}V,
\end{aligned}
\end{equation}
$$

由于

$$
\boldsymbol{\varepsilon}(\sum_{+,j}u_{+,j}\mathbf{v}_{+,j}) = \sum_{+,j}\boldsymbol{\varepsilon}\left(u_{+,j}\mathbf{v}_{+,j}\right) =\sum_{+,j}\frac{u_{+,j}}{2}\left(\nabla\mathbf{v}_{+,j} + \nabla\mathbf{v}_{+,j}^{T}\right),
$$

因此

$$
\frac{\partial \boldsymbol{\varepsilon}}{\partial u_{+,j}} = \boldsymbol{\varepsilon}\left(\mathbf{v}_{+,j}\right),
$$

故

$$
\begin{equation}
\begin{aligned}
\frac{\partial F_{*,i}^{\text{int}}}{\partial u_{+,j}} &= \int_{E_{\text{参考}}} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \mathbb{C}_{ep}^{\text{alg}}:\boldsymbol{\varepsilon}\left(\mathbf{v}_{+,j}\right)\left|\det(\mathbf{J})\right| \, \mathrm{d}V\\
&= \sum_{q} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \mathbb{C}_{ep}^{\text{alg}}:\boldsymbol{\varepsilon}\left(\mathbf{v}_{+,j}\right)\cdot w_{q}\left|\det(\mathbf{J})\right|
\end{aligned}
\end{equation}
$$


#### $\mathbf{F}^{\text{r}}$ 对刚度矩阵的贡献

分别考虑每个物理单元上的计算

$$
\begin{equation}
\begin{aligned}
\int_{\Gamma_{R}^{E_{\text{物理}}}} \alpha\mathbf{u} \cdot \mathbf{v}_{*,i} = \int_{\Gamma_{R}^{E}} \alpha \mathbf{v}_{*,i} \cdot\sum_{+,j}u_{+,j}\mathbf{v}_{+,j},
\end{aligned}
\end{equation}
$$

由于基函数具有局部支撑性，因此只需考虑 $E_{\text{物理}}$ 上的基函数，将积分运算映射回参考单元，记为

$$
F_{*,i}^{\text{r}} = \int_{\partial E_{\text{参考}}} \alpha \mathbf{v}_{*,i} \cdot\sum_{+,j}u_{+,j}\mathbf{v}_{+,j}\left|\det(\mathbf{J})\right| \, \mathrm{d}S,
$$

于是

$$
\begin{equation}
\begin{aligned}
\frac{\partial F_{*,i}^{\text{r}}}{\partial u_{+,j}} &= \int_{\partial E_{\text{参考}}} \alpha \mathbf{v}_{*,i} \cdot\mathbf{v}_{+,j}\left|\det(\mathbf{J})\right| \, \mathrm{d}S\\
&\approx \sum_{q} \alpha \mathbf{v}_{*,i} \cdot\mathbf{v}_{+,j}\cdot w_{q}\left|\det(\mathbf{J})\right|.
\end{aligned}
\end{equation}
$$

**在推导过程中需要特别注意：对自由度求导时若忽略了 $\left|\det(\mathbf{J})\right|$，实际上等同于忽略了几何变形对积分体积的影响。这种处理在小变形假设下是合理的，因为此时雅可比行列式近似为常数，不随位移变化。但如果进行大变形分析，则必须将几何作用纳入考虑，即在求导过程中保留 $\left|\det(\mathbf{J})\right|$ 对自由度的影响，以准确反映变形对体积和刚度的修正**

### Vogit 形式

#### $\mathbf{F}^{\text{int}}$ 对刚度矩阵的贡献

考虑每个物理单元上的积分，映射回参考单元计算

$$
\mathbf{F}^{\text{int}} := \int_{E} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \boldsymbol{\sigma} \, \mathrm{d}V = \int_{E}\mathbf{B}^{T}\boldsymbol{\sigma}\ \mathbf{d}V = \int_{E_{\text{物理}}}\mathbf{B}^{T}\boldsymbol{\sigma}\ \mathbf{d}V,
$$



由于 

$$
\boldsymbol{\varepsilon}=\mathcal{B}\mathbf{u} = \mathbf{B}\mathbf{u}_{E},
$$

故 Jacobian 矩阵为

$$
\begin{equation}
\begin{aligned}
\mathbf{K}_{\text{int}}=\frac{\partial \mathbf{F}^{\text{int}}}{\partial \mathbf{u}_{E}} &= \int_{E}\mathbf{B}^{T}\frac{\partial \boldsymbol{\sigma}}{\partial \mathbf{u}_{E}}\ \mathbf{d}E\\
&=\int_{E}\mathbf{B}^{T}\frac{\partial \boldsymbol{\sigma}}{\partial \boldsymbol{\varepsilon}}\frac{\partial \boldsymbol{\varepsilon}}{\partial \mathbf{u}_{E}} \mathbf{d}E\\
&=\int_{E}\mathbf{B}^{T}\mathbb{C}_{ep}^{\text{alg}}\ \mathbf{B} \mathbf{d}E,
\end{aligned}
\end{equation}
$$

其中，$\mathbb{C}_{ep}^{\text{alg}}$ 是[一致性切线模量](../../Plasticity/chap5/returnmapping.md)

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
\mathbf{u} = \mathbf{N}\mathbf{u}_{E},
$$

故

$$
\begin{equation}
\begin{aligned}
\mathbf{K}_{r} = \frac{\partial \mathbf{F}^{r}}{\partial \mathbf{u}_{E}}&=\int_{\Gamma_{R}} \alpha\frac{\partial \mathbf{u}}{\partial \mathbf{u}_{E}} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S\\
&=\int_{\Gamma_{R}} \alpha\left(\frac{\partial \mathbf{u}}{\partial \mathbf{u}_{E}}\right)^{T} \mathbf{v}_{*,i} \, \mathrm{d}S\\
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