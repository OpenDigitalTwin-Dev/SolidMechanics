# 离散 

## 基函数

设有限元解空间 $\mathcal{U}_{h}$ 的基函数为

$$
\mathbf{v}_{1},\mathbf{v}_{2},\cdots,\mathbf{v}_{N},
$$

$\mathbf{v}_{i} = \left[v_{x,i},v_{y,i},v_{z,i}\right]$，其中，$v_{x,i},v_{y,i},v_{z,i}$ 表示位移在 $x,y,z$ 方向的插值基函数，通常 $v_{x,i}=v_{y,i}=v_{z,i}=:v_{i}$，于是位移分布函数为

$$
\mathbf{u} = \sum_{i=1}^{N}\mathbf{u}_{i}v_{i}=\sum_{i=1}^{N}\left(u_{x,i}\mathbf{v}_{x,i}+u_{y,i}\mathbf{v}_{y,i}+u_{z,i}\mathbf{v}_{z,i}\right),
$$ (sec2-eq:u-exp)

其中，$\mathbf{u}_{i} = \left[u_{x,i},u_{y,i},u_{z,i}\right]^{T}$，且

$$
\mathbf{v}_{x,i}=\begin{bmatrix}
v_{i} \\ 0 \\ 0
\end{bmatrix},\quad 
\mathbf{v}_{y,i}=\begin{bmatrix}
 0  \\ v_{i} \\ 0
\end{bmatrix},\quad
\mathbf{v}_{z,i}=\begin{bmatrix}
 0 \\ 0 \\ v_{i} 
\end{bmatrix},
$$

此处，测试函数空间 $\mathcal{V}_{h} = \mathcal{U}_{h}$

于是，共计 $3N$ 个位移自由度 

$$
u_{x,1},u_{y,1},u_{z,1},u_{x,2},u_{y,2},u_{z,2},\cdots,u_{x,N},u_{y,N},u_{z,N},
$$

和 $3N$ 个求解方程

$$
\begin{equation}
\begin{aligned}
&\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \mathbb{C} : \boldsymbol{\varepsilon}(\mathbf{u}) \, \mathrm{d}V + \int_{\Gamma_{R}} \alpha\mathbf{u} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S \\
=& \int_{\Omega}\mathbf{f}\cdot \mathbf{v}_{*,i}\,\mathrm{d}V + \int_{\Gamma_{N}} \tilde{\mathbf{p}} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S + \int_{\Gamma_{R}} \mathbf{f}_{R} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S,\quad \forall \, \mathbf{v}_{*,i} \in \, \mathcal{V},\quad *=x,y,z;\ i=1:N.
\end{aligned}
\end{equation}
$$  (chap2-sec3-eq:discrete-eqs-tensor)

或 Voigt 形式

$$
\begin{equation}
\begin{aligned}
&\int_{\Omega} (\mathcal{B}\mathbf{v}_{*,i})^{T}\mathbb{C}(\mathcal{B}\mathbf{u}) \, \mathrm{d}V + \int_{\Gamma_{R}} \alpha\mathbf{u} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S \\
=& \int_{\Omega}\mathbf{f}\cdot \mathbf{v}_{*,i}\,\mathrm{d}V + \int_{\Gamma_{N}} \tilde{\mathbf{p}} \cdot \mathbf{v}_{*,i}\ \mathrm{d}S + \int_{\Gamma_{R}} \mathbf{f}_{R} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S,\quad \forall \, \mathbf{v}_{*,i} \in \, \mathcal{V},\quad *=x,y,z;\ i=1:N.
\end{aligned}
\end{equation}
$$ (chap2-sec3-eq:discrete-eqs-vogit)

式 {eq}`chap2-sec3-eq:discrete-eqs-tensor` 和 {eq}`chap2-sec3-eq:discrete-eqs-vogit` 是关于 $u_{*,i}$ 的线性方程组，关键在于计算出求解矩阵，即 **刚度矩阵**，其主要贡献项是

$$
\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \mathbb{C} : \boldsymbol{\varepsilon}(\mathbf{u}) \, \mathrm{d}V\quad \text{或} \quad \int_{\Omega} (\mathcal{B}\mathbf{v}_{*,i})^{T}\mathbb{C}(\mathcal{B}\mathbf{u}) \, \mathrm{d}V,
$$

这些积分项在整个计算区域上进行的，将其转换为各个单元上的积分之和

$$
\sum_{E}\int_{E} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \mathbb{C} : \boldsymbol{\varepsilon}(\mathbf{u}) \, \mathrm{d}V\quad \text{或} \quad \sum_{E}\int_{E} (\mathcal{B}\mathbf{v}_{*,i})^{T}\mathbb{C}(\mathcal{B}\mathbf{u}) \, \mathrm{d}V,
$$

根据 {eq}`sec2-eq:u-exp`，$\mathbf{u}$ 可以表示为 $\mathbf{v}_{*,i}$ 的线性组合，且由于 $a(\mathbf{u},\mathbf{v})$ 的双线性形式，故只需考虑

$$
\int_{E} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \mathbb{C} : \boldsymbol{\varepsilon}(\mathbf{v}_{+,j}) \, \mathrm{d}V\quad \text{或} \quad \int_{E} (\mathcal{B}\mathbf{v}_{*,i})^{T}\mathbb{C}(\mathcal{B}\mathbf{v}_{+,j}) \, \mathrm{d}V,
$$

由于基函数具有局部支撑性，因此在单元上的积分仅与该单元有限元节点上的基函数有关，故在计算单元积分时，只需考虑在该单元上取值不为零的基函数，且在单元积分运算时，只需考虑其在单元上的限制 $\mathbf{v}_{*,i} = \mathbf{v}_{*,i}|_{E}$，以下在单元积分时，$\mathbf{v}_{*,i}$ 默认为 $\mathbf{v}_{*,i}|_{E}$

通过选取与单元相关的 $\mathbf{v}_{*,i}$ 和 $\mathbf{v}_{*,j}$ 进行计算，得到**单元刚度矩阵**。由于物理单元的复杂性和多样性，物理单元上的积分通常会转换到参考单元上进行，此时需要利用形函数进行坐标变换和积分计算


## 形函数

记参考单元上的形函数为

$$
N_{1},N_{2},\cdots,N_{n}.
$$

### 几何映射

在物理单元 $E_{\text{}}$ 上（以下为局部编号）

$$
\begin{equation}
x = \sum_{i=1}^{n} N_{i}(\xi,\eta,\zeta)x_{i},\quad y = \sum_{i=1}^{n} N_{i}(\xi,\eta,\zeta)y_{i},\quad z = \sum_{i=1}^{n} N_{i}(\xi,\eta,\zeta)z_{i}.
\end{equation}
$$

### 等参变换

根据等参变换，基函数

$$
v_{i}(x,y,z) =  N_{i}(x(\xi,\eta,\zeta),y(\xi,\eta,\zeta),z(\xi,\eta,\zeta)),
$$ (sec2-eq:shape-value)

有

$$
\nabla_{\mathbf{x}}v_{i} = \nabla_{\mathbf{x}}N_{i} = \mathbf{J}^{-1}\nabla_{\boldsymbol{\xi}}N_{i}.
$$ (sec2-eq:shape-gradient)

### Jacobian 矩阵

在物理单元 $E$ 上（以下为局部编号）

$$
\begin{equation}
\begin{aligned}
\mathbf{J} =
\begin{bmatrix}
\frac{\partial x}{\partial \xi} & \frac{\partial y}{\partial \xi} & \frac{\partial z}{\partial \xi} \\
\frac{\partial x}{\partial \eta} & \frac{\partial y}{\partial \eta} & \frac{\partial z}{\partial \eta} \\
\frac{\partial x}{\partial \zeta} & \frac{\partial y}{\partial \zeta} & \frac{\partial z}{\partial \zeta}
\end{bmatrix}
&=
\sum_{i=1}^{n}
\begin{bmatrix}
\frac{\partial N_i}{\partial \xi} x_i & \frac{\partial N_i}{\partial \xi} y_i & \frac{\partial N_i}{\partial \xi} z_i \\
\frac{\partial N_i}{\partial \eta} x_i & \frac{\partial N_i}{\partial \eta} y_i & \frac{\partial N_i}{\partial \eta} z_i \\
\frac{\partial N_i}{\partial \zeta} x_i & \frac{\partial N_i}{\partial \zeta} y_i & \frac{\partial N_i}{\partial \zeta} z_i
\end{bmatrix}\\
&=\begin{bmatrix}
\frac{\partial N_{1}}{\partial \xi} & \frac{\partial N_{2}}{\partial \xi} & \cdots & \frac{\partial {N_n}}{\partial \xi} \\
 \frac{\partial N_{1}}{\partial \eta} & \frac{\partial N_{2}}{\partial \eta} & \cdots & \frac{\partial N_{n}}{\partial \eta} \\ 
 \frac{\partial N_{1}}{\partial \zeta} &  \frac{\partial N_{2}}{\partial \zeta} & \cdots & \frac{\partial N_{n}}{\partial \zeta}
\end{bmatrix}
\begin{bmatrix}
x_{1} & y_{1} & z_{1}     \\
x_{2} & y_{2} & z_{2}     \\
\vdots & \vdots & \vdots  \\
x_{n} & y_{n} & z_{n}
\end{bmatrix}.
\end{aligned}
\end{equation}
$$

### 场变量插值

在物理单元 $E$ 上（以下为局部编号）

$$
\begin{equation}
\mathbf{u} 
= 
\begin{bmatrix}
u_{x} \\ u_{y} \\ u_{z}
\end{bmatrix}
=
\begin{bmatrix}
\sum_{i=1}^{n}N_{i}(\xi,\eta,\zeta)u_{x,i} \\
\sum_{i=1}^{n}N_{i}(\xi,\eta,\zeta)u_{y,i} \\
\sum_{i=1}^{n}N_{i}(\xi,\eta,\zeta)u_{z,i}
\end{bmatrix}
=
\sum_{i=1}^{n}N_{i}\mathbf{u}_{i}.
\end{equation}
$$

### 梯度计算
在物理单元 $E$ 上（以下为局部编号），对于场分布函数

$$
\begin{equation}
\begin{aligned}
\begin{bmatrix}
\frac{\partial u_{x}}{\partial x} & \frac{\partial u_{y}}{\partial x} & \frac{\partial u_{z}}{\partial x} \\ 
\frac{\partial u_{x}}{\partial y} & \frac{\partial u_{y}}{\partial y} & \frac{\partial u_{z}}{\partial y} \\ 
\frac{\partial u_{x}}{\partial z} & \frac{\partial u_{y}}{\partial z} & \frac{\partial u_{z}}{\partial z}
\end{bmatrix} &= \begin{bmatrix}
\frac{\partial x}{\partial \xi} & \frac{\partial y}{\partial \xi} & \frac{\partial z}{\partial \xi} \\
\frac{\partial x}{\partial \eta} & \frac{\partial y}{\partial \eta} & \frac{\partial z}{\partial \eta} \\
\frac{\partial x}{\partial \zeta} & \frac{\partial y}{\partial \zeta} & \frac{\partial z}{\partial \zeta}
\end{bmatrix}^{-1}
\begin{bmatrix}
\frac{\partial u_{x}}{\partial \xi} & \frac{\partial u_{y}}{\partial \xi} & \frac{\partial u_{z}}{\partial \xi} \\ 
\frac{\partial u_{x}}{\partial \eta} & \frac{\partial u_{y}}{\partial \eta} & \frac{\partial u_{z}}{\partial \eta} \\ 
\frac{\partial u_{x}}{\partial \zeta} & \frac{\partial u_{y}}{\partial \zeta} & \frac{\partial u_{z}}{\partial \zeta}
\end{bmatrix}\\
&=\mathbf{J}^{-1}
\begin{bmatrix}
\frac{\partial N_{1}}{\partial \xi} & \frac{\partial {N_2}}{\partial \xi} & \cdots & \frac{\partial {N_n}}{\partial \xi} \\ 
\frac{\partial N_{1}}{\partial \eta} & \frac{\partial N_{2}}{\partial \eta} & \cdots & \frac{\partial N_{n}}{\partial \eta} \\ 
\frac{\partial N_{1}}{\partial \zeta} & \frac{\partial N_{2}}{\partial \zeta} & \cdots & \frac{\partial N_{n}}{\partial \zeta}
\end{bmatrix}
\begin{bmatrix}
u_{x,1} & u_{y,1} & u_{z,1} \\
u_{x,2} & u_{y,2} & u_{z,2} \\
\vdots & \vdots & \vdots    \\
u_{x,n} & u_{y,n} & u_{z,n}
\end{bmatrix}.
\end{aligned}
\end{equation}
$$

对于形函数，例如

$$
\begin{equation}
\begin{bmatrix}
\frac{\partial N_{1}(x,y,z)}{\partial x} \\ 
\frac{\partial N_{1}(x,y,z)}{\partial y} \\ 
\frac{\partial N_{1}(x,y,z)}{\partial z}
\end{bmatrix} 
= 
\mathbf{J}^{-1}
\begin{bmatrix}
\frac{\partial N_{1}(\xi,\eta,\zeta)}{\partial \xi}  \\
\frac{\partial N_{1}(\xi,\eta,\zeta)}{\partial \eta} \\ 
\frac{\partial N_{1}(\xi,\eta,\zeta)}{\partial \zeta}
\end{bmatrix}.
\end{equation}
$$ (chap2-sec3:shape-der)

## 单元刚度矩阵

### 张量形式

将物理单元上的积分运算映射回参考单元

$$
\int_{E} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \mathbb{C} : \boldsymbol{\varepsilon}(\mathbf{v}_{+,j}) \, \mathrm{d}V = \int_{E_{\text{参考}}} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \mathbb{C} : \boldsymbol{\varepsilon}(\mathbf{v}_{+,j})\left|\det(\mathbf{J})\right| \, \mathrm{d}V_{\text{参考}}
$$

需要注意的是，左端式子的坐标是 $(x,y,z)$，而右端式子的坐标是 $(\xi,\eta,\zeta)$，转换到参考单元上的计算见 {eq}`sec2-eq:shape-value` 和 {eq}`sec2-eq:shape-gradient`

考虑

$$
\boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \mathbb{C} : \boldsymbol{\varepsilon}(\mathbf{v}_{+,j}),
$$

由于

$$
\mathbb{C} : \boldsymbol{\varepsilon} = \mathbb{C}:\boldsymbol{\varepsilon} = \lambda\text{tr}(\boldsymbol{\varepsilon})\mathbf{I} + 2\mu\boldsymbol{\varepsilon},
$$

故

$$
\boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \mathbb{C} : \boldsymbol{\varepsilon}(\mathbf{v}_{+,j}) = \lambda\text{tr}(\boldsymbol{\varepsilon}(\mathbf{v}_{*,i}))\text{tr}(\boldsymbol{\varepsilon}(\mathbf{v}_{+,j})) + 2\mu\boldsymbol{\varepsilon}(\mathbf{v}_{*,i}):\boldsymbol{\varepsilon}(\mathbf{v}_{+,j}),
$$

其中

$$
\boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) = \frac{1}{2}\left(\nabla\mathbf{v}_{*,i} + \nabla\mathbf{v}_{*,i}^{T}\right).
$$

使用数值积分，得到

$$
\mathbf{K}^{e}_{(*,i),(+,j)} \approx \left(\sum_{q}\lambda\text{tr}(\boldsymbol{\varepsilon}(\mathbf{v}_{*,i}))\text{tr}(\boldsymbol{\varepsilon}(\mathbf{v}_{+,j})) + 2\mu\boldsymbol{\varepsilon}(\mathbf{v}_{*,i}):\boldsymbol{\varepsilon}(\mathbf{v}_{+,j})\right)\cdot w_{q} \left|\det(\mathbf{J}_{q})\right|.
$$

通常 $\mathbf{v}_{*,i}$ 的排序为

$$
\mathbf{v}_{x,1},\mathbf{v}_{y,1},\mathbf{v}_{z,1},\mathbf{v}_{x,2},\mathbf{v}_{y,2},\mathbf{v}_{z,2},\cdots
$$

### Vogit 形式

将物理单元上的积分运算映射回参考单元

$$
\int_{E} (\mathcal{B}\mathbf{v}_{*,i})^{T}\mathbb{C}(\mathcal{B}\mathbf{v}_{+,j})\, \mathrm{d}V = \int_{E_{\text{参考}}} (\mathcal{B}\mathbf{v}_{*,i})^{T}\mathbb{C}(\mathcal{B}\mathbf{v}_{+,j})\left|\det(\mathbf{J})\right|\, \mathrm{d}V_{\text{参考}},
$$ (sec2-eq:vogit-1)

需要注意的是，左端式子的坐标是 $(x,y,z)$，而右端式子的坐标是 $(\xi,\eta,\zeta)$

$\mathcal{B}\mathbf{v}_{*,i}$ 转换到参考单元后的梯度计算公式见 {eq}`sec2-eq:shape-gradient`

接下来，我们将 {eq}`sec2-eq:vogit-1` 转换为矩阵形式，即计算 $(\mathbf{v}_{*,i},\mathbf{v}_{+,j})$ 的所有组合，将它们依次选取为

$$
\mathbf{v}_{x,1},\mathbf{v}_{y,1},\mathbf{v}_{z,1},\mathbf{v}_{x,2},\mathbf{v}_{y,2},\mathbf{v}_{z,2},\cdots
$$

于是，式 {eq}`sec2-eq:vogit-1` 写为

$$
\begin{equation}
\begin{bmatrix}
(\mathcal{B}\mathbf{v}_{x,1})^{T}\mathbb{C}(\mathcal{B}\mathbf{v}_{x,1}) & (\mathcal{B}\mathbf{v}_{x,1})^{T}\mathbb{C}(\mathcal{B}\mathbf{v}_{y,1}) & (\mathcal{B}\mathbf{v}_{x,1})^{T}\mathbb{C}(\mathcal{B}\mathbf{v}_{z,1}) &  \cdots \\
(\mathcal{B}\mathbf{v}_{y,1})^{T}\mathbb{C}(\mathcal{B}\mathbf{v}_{x,1}) & (\mathcal{B}\mathbf{v}_{y,1})^{T}\mathbb{C}(\mathcal{B}\mathbf{v}_{y,1}) & (\mathcal{B}\mathbf{v}_{y,1})^{T}\mathbb{C}(\mathcal{B}\mathbf{v}_{z,1}) &  \cdots \\
(\mathcal{B}\mathbf{v}_{z,1})^{T}\mathbb{C}(\mathcal{B}\mathbf{v}_{x,1}) & (\mathcal{B}\mathbf{v}_{z,1})^{T}\mathbb{C}(\mathcal{B}\mathbf{v}_{y,1}) & (\mathcal{B}\mathbf{v}_{z,1})^{T}\mathbb{C}(\mathcal{B}\mathbf{v}_{z,1}) &  \cdots \\
\vdots & \vdots & \vdots & \ddots
\end{bmatrix},
\end{equation}
$$

进一步写为

$$
\begin{equation}
\begin{bmatrix}
(\mathcal{B}\mathbf{v}_{x,1})^{T}\mathbb{C}(\mathcal{B}\left[\mathbf{v}_{x,1}\ \mathbf{v}_{y,1}\ \mathbf{v}_{y,1}\right]) & (\mathcal{B}\mathbf{v}_{x,1})^{T}\mathbb{C}(\mathcal{B}\left[\mathbf{v}_{x,2}\ \mathbf{v}_{y,2}\ \mathbf{v}_{y,2}\right]) &  \cdots \\
(\mathcal{B}\mathbf{v}_{y,1})^{T}\mathbb{C}(\mathcal{B}\left[\mathbf{v}_{x,1}\ \mathbf{v}_{y,1}\ \mathbf{v}_{y,1}\right]) & (\mathcal{B}\mathbf{v}_{y,1})^{T}\mathbb{C}(\mathcal{B}\left[\mathbf{v}_{x,2}\ \mathbf{v}_{y,2}\ \mathbf{v}_{y,2}\right]) &  \cdots \\
(\mathcal{B}\mathbf{v}_{z,1})^{T}\mathbb{C}(\mathcal{B}\left[\mathbf{v}_{x,1}\ \mathbf{v}_{y,1}\ \mathbf{v}_{y,1}\right]) & (\mathcal{B}\mathbf{v}_{z,1})^{T}\mathbb{C}(\mathcal{B}\left[\mathbf{v}_{x,2}\ \mathbf{v}_{y,2}\ \mathbf{v}_{y,2}\right]) &  \cdots \\
\vdots & \vdots  & \ddots
\end{bmatrix},
\end{equation}
$$

记

$$
\mathbf{B}_{i} = \mathcal{B}\left[\mathbf{v}_{x,i}\ \mathbf{v}_{y,i}\ \mathbf{v}_{y,i}\right] = \begin{bmatrix}
\frac{\partial N_{i}}{\partial x} & 0 & 0 \\
0 & \frac{\partial N_{i}}{\partial y} & 0 \\
0 & 0 & \frac{\partial N_{i}}{\partial z} \\
\frac{\partial N_{i}}{\partial y} & \frac{\partial N_{i}}{\partial x} & 0 \\
0 & \frac{\partial N_{i}}{\partial z} & \frac{\partial N_{i}}{\partial y} \\
\frac{\partial N_{i}}{\partial z} & 0 & \frac{\partial N_{i}}{\partial x}
\end{bmatrix},
$$

且

$$
\mathbf{B}=
\begin{bmatrix}
\mathbf{B}_{1} & \mathbf{B}_{2} & \cdots & \mathbf{B}_{n}
\end{bmatrix},
$$

:::{note}
:class: tip, dropdown

记

$$
\mathbf{N} = \begin{bmatrix}
N_{1} & & &  & N_{n} \\
& N_{1} & & \cdots & & N_{n} \\
& & N_{1} & & & & N_{n}
\end{bmatrix},
$$

于是

$$
\mathbf{B} = \mathcal{B}\mathbf{N}.
$$

:::

于是，上述矩阵进一步写为

$$
\begin{equation}
\begin{bmatrix}
(\mathcal{B}\mathbf{v}_{x,1})^{T}\mathbb{C}\mathbf{B}\\
(\mathcal{B}\mathbf{v}_{y,1})^{T}\mathbb{C}\mathbf{B}\\
(\mathcal{B}\mathbf{v}_{z,1})^{T}\mathbb{C}\mathbf{B}\\
\vdots
\end{bmatrix} = \begin{bmatrix}
(\mathcal{B}\mathbf{v}_{x,1})^{T}\\
(\mathcal{B}\mathbf{v}_{y,1})^{T}\\
(\mathcal{B}\mathbf{v}_{z,1})^{T}\\
\vdots
\end{bmatrix}\mathbb{C}\mathbf{B} = \mathbf{B}^{T}\mathbb{C}\mathbf{B}
\end{equation}
$$

带入积分，得到单元刚度矩阵，记为 

$$
\mathbf{K}^{e} = \int_{E_{\text{参考}}} \mathbf{B}^{T}\mathbb{C}\mathbf{B}\left|\det(\mathbf{J})\right|\, \mathrm{d}V_{\text{参考}}
$$


### 数值积分

单元刚度矩阵 $\mathbf{K}^{e}$ 通常采用数值积分方法计算

$$
\mathbf{K}^{e}\approx\sum_{q}\mathbf{B}_{q}^{T}\mathbb{C}\mathbf{B}_{q}\cdot w_{q}\cdot\left|\det(\mathbf{J}_{q})\right|,
$$

其中，积分点是 $\left\{(\xi_{q},\eta_{q},\zeta_{q})\right\}$，积分权重是 $w_{q}$

## 全局矩阵

单元刚度矩阵描述了单元内自由度之间的关系，这些自由度按照特定顺序进行局部编号

$$
\begin{array}{c|ccc}
& u_{x,1}^{e} & u_{y,2}^{e} & u_{z,3}^{e} & u_{x,2}^{e} & u_{y,2}^{e} & u_{z,2}^{e} & \cdots \\ 
\hline
u_{x,1}^{e} & K_{11}^{e} & K_{12}^{e} & K_{13}^{e} & K_{14}^{e} & K_{15}^{e} & K_{16}^{e} & \cdots \\
u_{y,1}^{e} & K_{21}^{e} & K_{22}^{e} & K_{23}^{e} & K_{24}^{e} & K_{25}^{e} & K_{26}^{e} & \cdots \\
u_{z,1}^{e} & K_{31}^{e} & K_{32}^{e} & K_{33}^{e} & K_{34}^{e} & K_{35}^{e} & K_{16}^{e} & \cdots \\
u_{x,2}^{e} & K_{41}^{e} & K_{42}^{e} & K_{43}^{e} & K_{44}^{e} & K_{45}^{e} & K_{46}^{e} & \cdots \\
u_{y,2}^{e} & K_{51}^{e} & K_{52}^{e} & K_{53}^{e} & K_{54}^{e} & K_{55}^{e} & K_{56}^{e} & \cdots \\
u_{z,2}^{e} & K_{61}^{e} & K_{62}^{e} & K_{63}^{e} & K_{64}^{e} & K_{65}^{e} & K_{66}^{e} & \cdots \\
\vdots & \vdots & \vdots & \vdots & \vdots & \vdots & \vdots & \ddots
\end{array}
$$

通过单元刚度矩阵可以建立起所有自由度之间的关系。设全局刚度矩阵为 $\mathbf{K}$，单元 $E$ 内编号为 $i$ 的自由度对应的全局编号为 $g(E,i)$，则

$$
\mathbf{K}(g(E,i),g(E,j)) \ +\!\!= \ \mathbf{K}^{e}(i,j).
$$

## 右端项

右端项的计算方式与刚度矩阵类似，首先将积分划分到各个物理单元内，然后通过坐标映射将物理单元上的积分转化为参考单元上的积分运算

$$
\int_{\Omega}\mathbf{f}\cdot \mathbf{v}_{*,i}\,\mathrm{d}V = \sum_{E}\int_{E}\mathbf{f}\cdot \mathbf{v}_{*,i}\,\mathrm{d}V = \sum_{E}\int_{E_{\text{参考}}}\mathbf{f}\cdot \mathbf{v}_{*,i}\left|\det(\mathbf{J}_{q})\right|\,\mathrm{d}V_{\text{参考}},\quad *=x,y,z;\ i=1:N.
$$

写为矩阵形式

$$
\begin{align*}
&
\begin{bmatrix}
(\mathbf{v}_{x,1})^{T}\mathbf{f} \\
(\mathbf{v}_{y,1})^{T}\mathbf{f} \\
(\mathbf{v}_{z,1})^{T}\mathbf{f} \\
\vdots \\
(\mathbf{v}_{x,n})^{T}\mathbf{f} \\
(\mathbf{v}_{y,n})^{T}\mathbf{f} \\
(\mathbf{v}_{z,n})^{T}\mathbf{f}
\end{bmatrix}\ 
= 
\begin{bmatrix}
(\mathbf{v}_{x,1})^{T} \\
(\mathbf{v}_{y,1})^{T} \\
(\mathbf{v}_{z,1})^{T} \\
\vdots \\
(\mathbf{v}_{x,n})^{T} \\
(\mathbf{v}_{y,n})^{T} \\
(\mathbf{v}_{z,n})^{T}
\end{bmatrix}
\mathbf{f} = \mathbf{N}^{T}\mathbf{f},
\end{align*}
$$

数值积分技术计算得到

$$
\mathbf{F}^{e}
\approx \sum_{q}\mathbf{N}^{T}_{q}\mathbf{f}_{q}\cdot w_{q} \cdot \left|\det(\mathbf{J}_{q})\right|,
$$

其中，积分点是 $\left\{(\xi_{q},\eta_{q},\zeta_{q})\right\}$，积分权重是 $w_{q}$，$\mathbf{f}$ 需使用 $\xi,\eta,\zeta$ 坐标表示

类似地，单元右端项到全局右端项的映射关系如下

$$
\mathbf{F}(g(E,i))\ +\!\!= \ \mathbf{F}^{e}(i).
$$

## 边界条件

在有限元计算中，边界条件通常在组装完成全局刚度矩阵和右端项后进行附加处理

### Dirichlet 边界条件

Dirichlet 边界条件直接指定了边界节点的自由度值，因此只需对全局刚度矩阵和右端项进行相应的修正

$$
\begin{array}{c|ccc}
& \cdots & \cdots & u_{x,k} & \cdots & \cdots\\ 
\hline
\vdots &  &  & 0 &  &  &  \\
\vdots &  &  & 0 &  &  &  \\
u_{x,k} & 0 & 0 & 1 & 0 & 0 &  \\
\vdots &  &  & 0 &  &  &  \\
\vdots  &  &  & 0 &  &  &  \\
\end{array},\quad\quad\quad\quad
\begin{bmatrix}
\\
\vdots\\
\vdots\\
u_{D}\\
\vdots\\
\vdots\\
\end{bmatrix},
$$

其中 $u_{D}$ 是边界节点自由度 $u_{x,k}$ 的值

### Neumann 边界条件

边界积分通常通过划分至对应的边界单元表面进行计算

$$
\int_{\Gamma_{N}} \tilde{\mathbf{p}} \cdot \mathbf{v}_{*,i} \ \mathrm{d}S = \sum_{\Gamma_{N}^{E}}\int_{\Gamma_{N}^{E}} \tilde{\mathbf{p}} \cdot \mathbf{v}_{*,i} \ \mathrm{d}\Gamma_{N}^{E},\quad *=x,y,z;\ i=1:N.
$$

其中，$\Gamma_{N}^{E}$ 表示单元 $E$ 与边界 $\Gamma_{N}$ 的交集面。类似地，可以将物理单元上的面积分转换为参考单元上的面积分，但需要事先确定物理单元上的边界面与参考单元上哪个面相对应（例如六面体单元的 $\xi=1$ 面或 $\eta=-1$ 面），此时，积分通过坐标变换转换到参考面上计算

```{margin}
$\partial E_{\text{参考}}$ 表示 $\Gamma_{N}^{E}$ 对应的参考单元的某一面
```

$$
\begin{equation}
\begin{aligned}
\mathbf{F}_{\Gamma_{N}^{E}} &= \int_{\Gamma_{N}^{E}} \mathbf{N}^{T}\tilde{\mathbf{p}}\ \mathrm{d}\Gamma_{N}^{E}
=\int_{\partial E_{\text{参考}}} \mathbf{N}^{T}\tilde{\mathbf{p}}\ \left|\det(\mathbf{J}^{(\xi,\eta)})\right| \mathrm{d} S \\
&= \sum_{q}\mathbf{N}^{T}_{q}\tilde{\mathbf{p}}_{q}\cdot w_{q}\cdot\left|\det(\mathbf{J}^{(\xi,\eta)}_{q})\right|,
\end{aligned}
\end{equation}
$$

其中，积分点是 $\left\{(\xi_{q},\eta_{q})\right\}$，积分权重是 $w_{q}$，$\tilde{\mathbf{p}}$ 需使用 $\xi,\eta$ 坐标表示

单元右端项到全局右端项的映射关系如下

$$
\mathbf{F}(g(E,i)) \ +\!\!= \ \mathbf{F}_{\Gamma_{N}^{E}}(i).
$$

### Robin 边界条件

Robin 边界条件通常有两项需要处理

$$
\int_{\Gamma_{R}} \alpha\mathbf{u} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S
\quad \text{和} \quad
\int_{\Gamma_{R}} \mathbf{f}_{R} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S,\quad \forall \, \mathbf{v}_{*,i} \in \, \mathcal{V},\quad *=x,y,z;\ i=1:N.
$$

第二项的处理与 Neumann 边界条件类似。对于第一项

$$
\int_{\Gamma_{R}} \alpha\mathbf{u} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S = \sum_{\Gamma_{R}^{E}}\int_{\Gamma_{R}^{E}} \alpha \mathbf{u} \cdot \mathbf{v}_{*,i} \ \mathrm{d}\Gamma_{R}^{E},\quad *=x,y,z;\ i=1:N.
$$

因为

$$
\mathbf{u} = \sum_{i=1}^{n}N_{i}\mathbf{u}_{i} = 
\begin{bmatrix}
N_{1} & & &  & N_{n} \\
& N_{1} & & \cdots & & N_{n} \\
& & N_{1} & & & & N_{n}
\end{bmatrix}\begin{bmatrix}
u_{x,1} \\ u_{y,1} \\ u_{z,1} \\ u_{x,2} \\ u_{y,2} \\ u_{z,2} \\ \vdots \\ u_{x,n} \\ u_{y,n} \\ u_{z,n}
\end{bmatrix}=\mathbf{N}\mathbf{u}_{E},
$$

对于单元 $E$ ，积分写为矩阵形式

```{margin}
$\partial E_{\text{参考}}$ 表示 $\Gamma_{R}^{E}$ 对应的参考单元的某一面
```

$$
\begin{equation}
\begin{aligned}
\mathbf{F}_{\Gamma_{R}^{E}} 
&= 
\int_{\Gamma_{R}^{E}} \alpha\mathbf{N}^{T}\mathbf{N}\mathbf{u}_{E} \ \mathrm{d}\Gamma_{R}^{E}\\
&= 
\int_{\Gamma_{R}^{E}} \alpha\mathbf{N}^{T}\mathbf{N} \ \mathrm{d}\Gamma_{R}^{E} \cdot \mathbf{u}_{E}\\
&=\int_{\partial E_{\text{参考}}} \alpha\mathbf{N}^{T}\mathbf{N}\ \left|\det(\mathbf{J}^{(\xi,\eta)})\right| \mathrm{d} S \ \mathbf{u}_{E} \\
&= \sum_{q}\alpha\mathbf{N}^{T}_{q}\mathbf{N}_{q}\cdot w_{q}\cdot\left|\det(\mathbf{J}^{(\xi,\eta)}_{q})\right|\mathbf{u}_{E}\\
&=\mathbf{K}_{r}^{e}\cdot \mathbf{u}_{E},
\end{aligned}
\end{equation}
$$

其中，积分点是 $\left\{(\xi_{q},\eta_{q})\right\}$，积分权重是 $w_{q}$

单元右端项到全局右端项的映射关系如下

$$
\mathbf{F}(g(E,i)) \ +\!\!= \ \mathbf{F}_{\Gamma_{R}^{E}}(i).
$$

# 求解

## 位移求解

通常，[选择位移作为求解变量](../../Elasticity/chap1/sec8-two-2D-solution.md)。经过离散化后，可以得到有限元节点上以位移自由度为未知量的线性方程组：

```{margin}
这里对 $\mathbf{u}$ 记号混用
```

$$
\mathbf{K}\mathbf{u} = \mathbf{F}.
$$

通过求解线性方程组（直接法或迭代法），可以得到有限元节点上的位移解

**接着，通过场变量插值，可以得到任意单元内任意点的位移值，特别是积分点上的位移值，进而通过几何方程和本构方程求得积分点上的应变和应力（对于非线性问题，这些结果还可以用于更新刚度矩阵；对于线性问题，刚度矩阵只需组装一次，因此没有必要）。而有限元节点上的应力应变值则通常通过积分点上的应力应变进行插值得到，以满足可视化的需求**