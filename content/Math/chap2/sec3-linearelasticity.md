# 线弹性问题

线弹性问题的控制方程为

$$
\begin{equation}
\begin{aligned}
&\nabla\cdot \boldsymbol{\sigma} + \mathbf{f} = \mathbf{0},\\
&\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla \mathbf{u} + \nabla\mathbf{u}^{T}),\\
&\boldsymbol{\sigma}=\mathbb{C}:\boldsymbol{\varepsilon},
\end{aligned}
\end{equation}
$$

其中，$\boldsymbol{\sigma}$ 是应力张量，$\mathbf{f}$ 是体积力向量，$\boldsymbol{\varepsilon}$ 是应变张量，$\mathbf{u}$ 是位移向量，$\mathbb{C}$ 是四阶本构张量

计算区域为 $\Omega$，边界 $\partial\Omega=\Gamma_{D}\cup\Gamma_{N}\cup\Gamma_{R}$，边界条件为

```{margin}
$\mathbf{n}$ 是边界外法向量，$\alpha$ 是系数，$\mathbf{f}_{R}$ 是边界上的外部载荷
```

$$
\begin{equation}
\begin{aligned}
\mathbf{u} &= \tilde{\mathbf{u}},\quad &\text{on}\,\, \Gamma_{D},\\
\boldsymbol{\sigma}\mathbf{n} &= \tilde{\mathbf{p}},\quad &\text{on}\,\, \Gamma_{N},\\
\boldsymbol{\sigma}\mathbf{n} + \alpha\mathbf{u} &= \mathbf{f}_{R},\quad &\text{on}\,\, \Gamma_{R}.
\end{aligned}
\end{equation}
$$

边界条件通常分为三种：

- **Dirichlet** 边界条件（本质边界条件）：强制规定规定边界上的位移 $\tilde{u}$
- **Neumann** 边界条件（自然边界条件）：规定边界上的力或应力分布 $\tilde{p}$；当 $\tilde{p} = 0$ 时，称为自由边界条件，此时对应的边界上无牵引力作用
- **Robin** 边界条件（混合边界条件）：描述位移与力的线性组合关系，常用于弹性支撑等场景

在有限元方法中，Dirichlet 边界条件通过选取齐次的测试函数空间，并直接强加边界节点值来处理；而 Neumann 边界条件和 Robin 边界条件则通过分部积分自然引入到弱形式中，从而在求解过程中自动满足

## 变分

使用位移法求解，选择测试函数 $\mathbf{v}\in\mathcal{V}$，其中

$$
\mathcal{V}=\left\{\left.\mathbf{v}\in \left[H^{k}(\Omega)\right]^d \,\,\right|\,\, \mathbf{v}=\mathbf{0} \,\, \text{on}\,\, \Gamma_{D} \right\},
$$

$H^{k}(\Omega)$ 是 $k$ 阶 Sobolev 空间，$d$ 是空间维数。将方程转为积分形式

$$
\int_{\Omega}\left(\nabla\cdot\boldsymbol{\sigma}+\mathbf{f}\right)\cdot \mathbf{v}\,\mathrm{d}V = 0,\quad \forall \, \mathbf{v} \in \, \mathcal{V},
$$

由于

$$
\left(\nabla \cdot \boldsymbol{\sigma}\right) \cdot \mathbf{v} = \nabla\cdot(\boldsymbol{\sigma}\mathbf{v})-\boldsymbol{\sigma}:\nabla\mathbf{v},
$$

因此，对第一项应用散度定理得到

```{margin}
$\boldsymbol{\sigma}$ 是对称的，因此 $(\boldsymbol{\sigma}\mathbf{v})\cdot \mathbf{n} = (\boldsymbol{\sigma}\mathbf{n})\cdot \mathbf{v}$
```

$$
\int_{\Omega} \left(\nabla \cdot \boldsymbol{\sigma}\right) \cdot \mathbf{v} \, \mathrm{d}V =
\int_{\partial \Omega} \left(\boldsymbol{\sigma} \mathbf{n}\right) \cdot \mathbf{v} \, \mathrm{d}S -
\int_{\Omega} \boldsymbol{\sigma} : \nabla \mathbf{v} \, \mathrm{d}V,
$$

其中，$\mathbf{n}$ 是 $\partial \Omega$ 的外法向量。于是

$$
-
\int_{\Omega} \boldsymbol{\sigma} : \nabla \mathbf{v} \, \mathrm{d}V + \int_{\Omega}\mathbf{f}\cdot \mathbf{v}\,\mathrm{d}V + \int_{\partial \Omega} \left(\boldsymbol{\sigma} \mathbf{n}\right) \cdot \mathbf{v} \, \mathrm{d}S = 0,\quad \forall \, \mathbf{v} \in \, \mathcal{V},
$$

代入边界条件

$$
\int_{\partial \Omega} \left(\boldsymbol{\sigma} \mathbf{n}\right) \cdot \mathbf{v} \, \mathrm{d}S = \int_{\Gamma_{N}} \tilde{\mathbf{p}} \cdot \mathbf{v} \, \mathrm{d}S + \int_{\Gamma_{R}} (\mathbf{f}_{R}- \alpha\mathbf{u}) \cdot \mathbf{v} \, \mathrm{d}S
$$

于是

$$
-
\int_{\Omega} \boldsymbol{\sigma} : \nabla \mathbf{v} \, \mathrm{d}V + \int_{\Omega}\mathbf{f}\cdot \mathbf{v}\,\mathrm{d}V + \int_{\Gamma_{N}} \tilde{\mathbf{p}} \cdot \mathbf{v} \, \mathrm{d}S + \int_{\Gamma_{R}} (\mathbf{f}_{R}- \alpha\mathbf{u}) \cdot \mathbf{v} \, \mathrm{d}S = 0,\quad \forall \, \mathbf{v} \in \, \mathcal{V}.
$$

定义对称算子

$$
\boldsymbol{\varepsilon}(\mathbf{u})=\frac{1}{2}\left(\nabla\mathbf{u} + \nabla\mathbf{u}^{T}\right),
$$

类似地

$$
\boldsymbol{\varepsilon}(\mathbf{v})=\frac{1}{2}\left(\nabla\mathbf{v} + \nabla\mathbf{v}^{T}\right),
$$

由于 $\boldsymbol{\sigma}$ 是对称张量，因此 $\boldsymbol{\sigma} : \nabla \mathbf{v} = \boldsymbol{\sigma} : (\nabla \mathbf{v})^T$，故 

$$
\boldsymbol{\sigma} : \nabla \mathbf{v} = \boldsymbol{\sigma} : \boldsymbol{\varepsilon}(\mathbf{v}),
$$

代入到方程中，得到

$$
-
\int_{\Omega} \boldsymbol{\sigma} : \boldsymbol{\varepsilon}(\mathbf{v}) \, \mathrm{d}V + \int_{\Omega}\mathbf{f}\cdot \mathbf{v}\,\mathrm{d}V + \int_{\Gamma_{N}} \tilde{\mathbf{p}} \cdot \mathbf{v} \, \mathrm{d}S + \int_{\Gamma_{R}} (\mathbf{f}_{R}- \alpha\mathbf{u}) \cdot \mathbf{v} \, \mathrm{d}S = 0,\quad \forall \, \mathbf{v} \in \, \mathcal{V},
$$

再将本构方程 $\boldsymbol{\sigma}=\mathbb{C}:\boldsymbol{\varepsilon}(\mathbf{u})$ 代入上述方程，最终得到弱形式

$$
\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}) : \mathbb{C} : \boldsymbol{\varepsilon}(\mathbf{u}) \, \mathrm{d}V + \int_{\Gamma_{R}} \alpha\mathbf{u} \cdot \mathbf{v} \, \mathrm{d}S
= \int_{\Omega}\mathbf{f}\cdot \mathbf{v}\,\mathrm{d}V + \int_{\Gamma_{N}} \tilde{\mathbf{p}} \cdot \mathbf{v} \, \mathrm{d}S + \int_{\Gamma_{R}} \mathbf{f}_{R} \cdot \mathbf{v} \, \mathrm{d}S,\quad \forall \, \mathbf{v} \in \, \mathcal{V},
$$

且 $\mathbf{u} = \mathbf{\tilde{u}},\, \text{on}\, \Gamma_{D}$

### Voigt 形式

```{margin}
注意，为了方便，这里记号混用
```

为了便于有限元计算，通常将第一项写为 Voigt 形式

$$
\mathbb{C} : \boldsymbol{\varepsilon}(\mathbf{u}) 
\Rightarrow\mathbb{C}\boldsymbol{\varepsilon}(\mathbf{u})= \begin{bmatrix}
\lambda + 2\mu & \lambda & \lambda & 0 & 0 & 0 \\
\lambda & \lambda + 2\mu & \lambda & 0 & 0 & 0 \\
\lambda & \lambda & \lambda + 2\mu & 0 & 0 & 0 \\
0 & 0 & 0 & \mu & 0 & 0 \\
0 & 0 & 0 & 0 & \mu & 0 \\
0 & 0 & 0 & 0 & 0 & \mu
\end{bmatrix}\begin{bmatrix}
\varepsilon_{xx}\\\varepsilon_{yy}\\\varepsilon_{zz}\\2\varepsilon_{xy}\\2\varepsilon_{xz}\\2\varepsilon_{yz}
\end{bmatrix},
$$

以及

```{margin}
$\mathcal{B}$ 是应变-位移算子矩阵
```

$$
\begin{equation}
\boldsymbol{\varepsilon}({\mathbf{u}}) = \mathcal{B}\mathbf{u}\quad \Rightarrow\quad
\begin{bmatrix}
\varepsilon_{xx}\\\varepsilon_{yy}\\\varepsilon_{zz}\\2\varepsilon_{xy}\\2\varepsilon_{yz}\\2\varepsilon_{zx}
\end{bmatrix}
=\begin{bmatrix}
\frac{\partial}{\partial x} & 0 & 0 \\
0 & \frac{\partial}{\partial y} & 0 \\
0 & 0 & \frac{\partial}{\partial z} \\
\frac{\partial}{\partial y} & \frac{\partial}{\partial x} & 0 \\
0 & \frac{\partial}{\partial z} & \frac{\partial}{\partial y} \\
\frac{\partial}{\partial z} & 0 & \frac{\partial}{\partial x}
\end{bmatrix}
\begin{bmatrix}
u_{x}\\u_{y}\\u_{z}
\end{bmatrix}.
\end{equation}
$$

于是 

$$
\boldsymbol{\varepsilon}(\mathbf{v}) : \mathbb{C} : \boldsymbol{\varepsilon}(\mathbf{u}) = \boldsymbol{\varepsilon}(\mathbf{v})^{T} \mathbb{C} \boldsymbol{\varepsilon}(\mathbf{u})=(\mathcal{B}\mathbf{v})^{T}\mathbb{C}(\mathcal{B}\mathbf{u}),
$$


于是积分运算可以写为

$$
\begin{align}
\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}) : \mathbb{C} : \boldsymbol{\varepsilon}(\mathbf{u}) \, \mathrm{d}V 
&= \int_{\Omega} (\mathcal{B}\mathbf{v})^{T}\mathbb{C}(\mathcal{B}\mathbf{u}) \, \mathrm{d}V.
\end{align}
$$

## 离散 

### 基函数

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
&\int_{\Omega} (\mathcal{B}\mathbf{v}_{*,i})^{T}\mathbb{C}(\mathcal{B}\mathbf{u}) \, \mathrm{d}V + \int_{\Gamma_{R}} \alpha\mathbf{u} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S \\
=& \int_{\Omega}\mathbf{f}\cdot \mathbf{v}_{*,i}\,\mathrm{d}V + \int_{\Gamma_{N}} \tilde{\mathbf{p}} \cdot \mathbf{v}_{*,i}\ \mathrm{d}S + \int_{\Gamma_{R}} \mathbf{f}_{R} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S,\quad \forall \, \mathbf{v}_{*,i} \in \, \mathcal{V},\quad *=x,y,z;\ i=1:N.
\end{aligned}
\end{equation}
$$ (chap2-sec3-eq:discrete-eqs)

### 形函数

设参考单元上的形函数为

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

### 导数计算
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

对于形函数

$$
\begin{equation}
\begin{bmatrix}
\frac{\partial N_{1}}{\partial x} & \frac{\partial {N_2}}{\partial x} & \cdots & \frac{\partial {N_n}}{\partial x} \\ 
\frac{\partial N_{1}}{\partial y} & \frac{\partial N_{2}}{\partial y} & \cdots & \frac{\partial N_{n}}{\partial y}\\ 
\frac{\partial N_{1}}{\partial z} & \frac{\partial N_{2}}{\partial z} & \cdots & \frac{\partial N_{n}}{\partial z}
\end{bmatrix} 
= 
\mathbf{J}^{-1}
\begin{bmatrix}
\frac{\partial N_{1}}{\partial \xi} & \frac{\partial {N_2}}{\partial \xi} & \cdots & \frac{\partial {N_n}}{\partial \xi} \\
 \frac{\partial N_{1}}{\partial \eta} & \frac{\partial N_{2}}{\partial \eta} & \cdots & \frac{\partial N_{n}}{\partial \eta} \\ 
 \frac{\partial N_{1}}{\partial \zeta} & \frac{\partial N_{2}}{\partial \zeta} & \cdots & \frac{\partial N_{n}}{\partial \zeta}
\end{bmatrix}.
\end{equation}
$$ (chap2-sec3:shape-der)

### 单元刚度矩阵

在有限元方法中，积分运算被划分至每个物理单元

$$ \sum_{E}\int_{E} (\mathcal{B}\mathbf{v})^{T}\mathbb{C}(\mathcal{B}\mathbf{u})\, \mathrm{d}E,
$$

在物理单元 $E$ 上（以下为局部编号），测试函数 $\mathbf{v}$ 为

```{margin}
坐标为 $x,y,z$
```

$$
\begin{bmatrix}
\phi_{1}|_E \\ 0 \\ 0
\end{bmatrix},\,
\begin{bmatrix}
0 \\ \phi_{1}|_E \\  0
\end{bmatrix},\,
\begin{bmatrix}
0 \\ 0 \\ \phi_{1}|_E 
\end{bmatrix},\,
\begin{bmatrix}
\phi_{2}|_E \\ 0 \\ 0
\end{bmatrix},\,
\begin{bmatrix}
0 \\ \phi_{2}|_E \\  0
\end{bmatrix},\,
\begin{bmatrix}
0 \\ 0 \\ \phi_{2}|_E 
\end{bmatrix},\,\cdots
$$

使用参考单元上的形函数插值

```{margin}
坐标为 $\xi,\eta,\zeta$，通过插值映射到物理单元
```

$$
\begin{bmatrix}
N_{1} \\ 0 \\ 0
\end{bmatrix},\,
\begin{bmatrix}
0 \\ N_{1} \\  0
\end{bmatrix},\,
\begin{bmatrix}
0 \\ 0 \\ N_{1} 
\end{bmatrix},\,
\begin{bmatrix}
N_{2} \\ 0 \\ 0
\end{bmatrix},\,
\begin{bmatrix}
0 \\ N_{2} \\  0
\end{bmatrix},\,
\begin{bmatrix}
0 \\ 0 \\ N_{2} 
\end{bmatrix},\,\cdots
$$

依次记为 $\mathbf{v}_{x,1},\mathbf{v}_{y,1},\mathbf{v}_{z,1},\mathbf{v}_{x,2},\mathbf{v}_{y,2},\mathbf{v}_{z,2},\cdots$，于是在物理单元 $E$ 上，得到如下关系式

$$
\begin{equation}
\int_{E} (\mathcal{B}\mathbf{v}_{*,i})^{T}\mathbb{C}(\mathcal{B}\mathbf{u}) \, \mathrm{d}E,\quad *=x,y,z;\ i=1:n.
\end{equation}
$$ (chap2-sec3-eq:element-stiffness)

上述关系式给出了单元内自由度 $\mathbf{u}_{i}$ 之间的关系，其可以表示为矩阵形式，该矩阵称为**单元刚度矩阵**

由于

$$
\mathcal{B}\mathbf{u}
=\sum_{i=1}^{n}\mathcal{B}N_{i}\mathbf{u}_{i}
=\sum_{i=1}^{n}\mathbf{B}_{i}\mathbf{u}_{i},
$$

其中

$$
\mathbf{B}_{i} := \mathcal{B}N_{i} = \begin{bmatrix}
\frac{\partial N_{i}}{\partial x} & 0 & 0 \\
0 & \frac{\partial N_{i}}{\partial y} & 0 \\
0 & 0 & \frac{\partial N_{i}}{\partial z} \\
\frac{\partial N_{i}}{\partial y} & \frac{\partial N_{i}}{\partial x} & 0 \\
0 & \frac{\partial N_{i}}{\partial z} & \frac{\partial N_{i}}{\partial y} \\
\frac{\partial N_{i}}{\partial z} & 0 & \frac{\partial N_{i}}{\partial x}
\end{bmatrix},
$$

于是

$$
\mathcal{B}\mathbf{u} = 
\begin{bmatrix}
\mathbf{B}_{1} & \mathbf{B}_{2} & \cdots & \mathbf{B}_{n}
\end{bmatrix}
\begin{bmatrix}
\mathbf{u}_{1} \\ \mathbf{u}_{2} \\ \vdots \\ \mathbf{u}_{n}
\end{bmatrix}=\begin{bmatrix}
\mathbf{B}_{1} & \mathbf{B}_{2} & \cdots & \mathbf{B}_{n}
\end{bmatrix}
\begin{bmatrix}
u_{x,1} \\ u_{y,1} \\ u_{z,1} \\ u_{x,2} \\ u_{y,2} \\ u_{z,2} \\ \vdots \\ u_{x,n} \\ u_{y,n} \\ u_{z,n}
\end{bmatrix} = \mathbf{B}\mathbf{u}_{E},
$$

代入 $v_{*,i}$，将积分式 {eq}`chap2-sec3-eq:element-stiffness` 写为矩阵形式

$$
\begin{align*}
&\int_{E}
\begin{bmatrix}
(\mathcal{B}\mathbf{v}_{x,1})^{T}\mathbb{C}\mathbf{B}\mathbf{u}_{E} \\
(\mathcal{B}\mathbf{v}_{y,1})^{T}\mathbb{C}\mathbf{B}\mathbf{u}_{E} \\
(\mathcal{B}\mathbf{v}_{z,1})^{T}\mathbb{C}\mathbf{B}\mathbf{u}_{E} \\
\vdots \\
(\mathcal{B}\mathbf{v}_{x,n})^{T}\mathbb{C}\mathbf{B}\mathbf{u}_{E} \\
(\mathcal{B}\mathbf{v}_{y,n})^{T}\mathbb{C}\mathbf{B}\mathbf{u}_{E} \\
(\mathcal{B}\mathbf{v}_{z,n})^{T}\mathbb{C}\mathbf{B}\mathbf{u}_{E}
\end{bmatrix}\ 
\mathrm{d}E
= \int_{E}
\begin{bmatrix}
(\mathcal{B}\mathbf{v}_{x,1})^{T} \\
(\mathcal{B}\mathbf{v}_{y,1})^{T} \\
(\mathcal{B}\mathbf{v}_{z,1})^{T} \\
\vdots \\
(\mathcal{B}\mathbf{v}_{x,n})^{T} \\
(\mathcal{B}\mathbf{v}_{y,n})^{T} \\
(\mathcal{B}\mathbf{v}_{z,n})^{T} \\
\end{bmatrix}\mathbb{C}\mathbf{B}\mathbf{u}_{E}\ 
\mathrm{d}E,
\end{align*}
$$

因为

$$
\begin{align*}
\begin{bmatrix}
(\mathcal{B}\mathbf{v}_{x,1})^{T} \\
(\mathcal{B}\mathbf{v}_{y,1})^{T} \\
(\mathcal{B}\mathbf{v}_{z,1})^{T} \\
\vdots \\
(\mathcal{B}\mathbf{v}_{x,n})^{T} \\
(\mathcal{B}\mathbf{v}_{y,n})^{T} \\
(\mathcal{B}\mathbf{v}_{z,n})^{T}
\end{bmatrix} 
&= 
\begin{bmatrix}
\mathcal{B}\mathbf{v}_{x,1} & \mathcal{B}\mathbf{v}_{y,1} & \mathcal{B}\mathbf{v}_{z,1} & \cdots & \mathcal{B}\mathbf{v}_{x,n} & \mathcal{B}\mathbf{v}_{y,n} & \mathcal{B}\mathbf{v}_{z,n}
\end{bmatrix}^{T}\\
&=
\begin{bmatrix}
\mathbf{B}_{1} & \cdots & \mathbf{B}_{n}
\end{bmatrix}^{T}
= \mathbf{B}^{T},
\end{align*}
$$

于是积分式变为

$$
\int_{E}
\mathbf{B}^{T}\mathbb{C}\mathbf{B}\mathbf{u}_{E}\ \mathrm{d}E
=\int_{E}
\mathbf{B}^{T}\mathbb{C}\mathbf{B}\ \mathrm{d}E\cdot\mathbf{u}_{E}=\mathbf{K}^{e}\cdot\mathbf{u}_{E}.
$$

其中 $\mathbf{K}^{e}$ 是单元刚度矩阵

通过坐标映射，将 $\mathbf{K}^{e}$ 转换到参考单元计算

$$
\mathbf{K}^{e} 
=\int_{E}\mathbf{B}^{T}\mathbb{C}\mathbf{B}\ \mathrm{d}E
=\int_{E_{\text{参考}}}\mathbf{B}^{T}\mathbb{C}\mathbf{B}\left|\det(\mathbf{J})\right|\ \mathrm{d}E_{\text{参考}},
$$

其中 $\mathbf{B}$ 中的导数应依据公式 {eq}`chap2-sec3:shape-der` 转换为自然坐标下的导数进行计算

#### 数值积分

单元刚度矩阵 $\mathbf{K}^{e}$ 通常采用数值积分方法计算

$$
\mathbf{K}^{e}\approx\sum_{q}B_{q}^{T}DB_{q}\cdot w_{q}\cdot\left|\det(\mathbf{J}_{q})\right|,
$$

其中，积分点是 $\left\{(\xi_{q},\eta_{q},\zeta_{q})\right\}$，积分权重是 $w_{q}$

### 全局矩阵

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

### 右端项

右端项的计算方式与刚度矩阵类似，首先将积分划分到各个物理单元内，然后通过坐标映射将物理单元上的积分转化为参考单元上的积分运算

$$
\int_{\Omega}\mathbf{f}\cdot \mathbf{v}_{*,i}\,\mathrm{d}V = \sum_{E}\int_{E}\mathbf{f}\cdot \mathbf{v}_{*,i}\,\mathrm{d}E,\quad *=x,y,z;\ i=1:N.
$$

在物理单元 $E$ 上（以下为局部编号），得到的关系式如下

$$
\int_{E}\mathbf{f}\cdot \mathbf{v}_{*,i}\,\mathrm{d}E,\quad *=x,y,z;\ i=1:n.
$$
写为矩阵形式

$$
\begin{align*}
&\int_{E}
\begin{bmatrix}
(\mathbf{v}_{x,1})^{T}\mathbf{f} \\
(\mathbf{v}_{y,1})^{T}\mathbf{f} \\
(\mathbf{v}_{z,1})^{T}\mathbf{f} \\
\vdots \\
(\mathbf{v}_{x,n})^{T}\mathbf{f} \\
(\mathbf{v}_{y,n})^{T}\mathbf{f} \\
(\mathbf{v}_{z,n})^{T}\mathbf{f}
\end{bmatrix}\ 
\mathrm{d}E
= \int_{E}
\begin{bmatrix}
(\mathbf{v}_{x,1})^{T} \\
(\mathbf{v}_{y,1})^{T} \\
(\mathbf{v}_{z,1})^{T} \\
\vdots \\
(\mathbf{v}_{x,n})^{T} \\
(\mathbf{v}_{y,n})^{T} \\
(\mathbf{v}_{z,n})^{T}
\end{bmatrix}
\mathbf{f}\ 
\mathrm{d}E,
\end{align*}
$$

代入 $\mathbf{v}_{*,i}$ 对应的形函数插值得到

$$
\int_{E}
\begin{bmatrix}
N_{1} & &  \\
& N_{1} &  \\
& & N_{1}   \\
& \vdots & \\
N_{n} & &  \\
& N_{n} &  \\
& & N_{n}   \\
\end{bmatrix}
\mathbf{f}\ 
\mathrm{d}E 
= \int_{E}
\mathbf{N}^{T}
\mathbf{f}\ 
\mathrm{d}E,
$$

将积分变换到参考单元上进行，并采用数值积分技术，于是

$$
\mathbf{F}^{e}=
\int_{E}
\mathbf{N}^{T}
\mathbf{f}\ 
\mathrm{d}E = \int_{E_{\text{参考}}}
\mathbf{N}^{T}
\mathbf{f}\left|\det(\mathbf{J})\right|\ 
\mathrm{d}E_{\text{参考}} 
\approx \sum_{q}\mathbf{N}^{T}_{q}\mathbf{f}_{q}\cdot w_{q} \cdot \left|\det(\mathbf{J}_{q})\right|,
$$

其中，积分点是 $\left\{(\xi_{q},\eta_{q},\zeta_{q})\right\}$，积分权重是 $w_{q}$，$\mathbf{f}$ 需使用 $\xi,\eta,\zeta$ 坐标表示

类似地，单元右端项到全局右端项的映射关系如下

$$
\mathbf{F}(g(E,i))\ +\!\!= \ \mathbf{F}^{e}(i).
$$

### 边界条件

在有限元计算中，边界条件通常在组装完成全局刚度矩阵和右端项后进行附加处理

#### Dirichlet 边界条件

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

#### Neumann 边界条件

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

#### Robin 边界条件

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

## 求解

### 位移求解

通常，[选择位移作为求解变量](../../Elasticity/chap1/sec8-two-2D-solution.md)。经过离散化后，可以得到有限元节点上以位移自由度为未知量的线性方程组：

```{margin}
这里对 $\mathbf{u}$ 记号混用
```

$$
\mathbf{K}\mathbf{u} = \mathbf{F}.
$$

通过求解线性方程组（直接法或迭代法），可以得到有限元节点上的位移解

**接着，通过场变量插值，可以得到任意单元内任意点的位移值，特别是积分点上的位移值，进而通过几何方程和本构方程求得积分点上的应变和应力（对于非线性问题，这些结果还可以用于更新刚度矩阵；对于线性问题，刚度矩阵只需组装一次，因此没有必要）。而有限元节点上的应力应变值则通常通过积分点上的应力应变进行插值得到，以满足可视化的需求**