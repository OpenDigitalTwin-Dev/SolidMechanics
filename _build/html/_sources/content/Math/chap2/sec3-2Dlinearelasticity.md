# 线弹性问题

线弹性问题的控制方程为

$$
\begin{equation}
\begin{aligned}
&\nabla\cdot \boldsymbol{\sigma} + \mathbf{f} = \mathbf{0},\\
&\boldsymbol{\varepsilon} = (\nabla \mathbf{u} + (\nabla\mathbf{u})^{T})/2,\\
&\boldsymbol{\sigma}=\mathbf{D}:\boldsymbol{\varepsilon},
\end{aligned}
\end{equation}
$$

其中，$\boldsymbol{\sigma}$ 是应力张量，$\mathbf{f}$ 是体积力向量，$\boldsymbol{\varepsilon}$ 是应变张量，$\mathbf{u}$ 是位移向量，$\mathbf{D}$ 是四阶本构张量

计算区域为 $\Omega$，边界 $\partial\Omega=\Gamma_{u}\cup\Gamma_{p}$，边界条件为

$$
\begin{equation}
\begin{aligned}
\mathbf{u} = \tilde{\mathbf{u}},\quad \text{on}\,\, \Gamma_{u},\\
\boldsymbol{\sigma}\mathbf{n} = \tilde{\mathbf{p}},\quad \text{on}\,\, \Gamma_{p}.
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
\mathcal{V}=\left\{\left.\mathbf{v}\in \left[H^{1}(\Omega)\right]^d \,\,\right|\,\, \mathbf{v}=\mathbf{0} \,\, \text{on}\,\, \Gamma_{u} \right\},
$$

$H^{1}(\Omega)$ 是一阶 Sobolev 空间，$d$ 是空间维数。将方程转为积分形式

$$
\int_{\Omega}\left(\nabla\cdot\boldsymbol{\sigma}\right)\cdot \mathbf{v}\,\mathrm{d}\Omega  + \int_{\Omega}\mathbf{f}\cdot \mathbf{v}\,\mathrm{d}\Omega = 0,\quad \forall \, \mathbf{v} \in \, \mathcal{V},
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
\int_{\Omega} \left(\nabla \cdot \boldsymbol{\sigma}\right) \cdot \mathbf{v} \, \mathrm{d}\Omega =
\int_{\partial \Omega} \left(\boldsymbol{\sigma} \mathbf{n}\right) \cdot \mathbf{v} \, \mathrm{d}S -
\int_{\Omega} \boldsymbol{\sigma} : \nabla \mathbf{v} \, \mathrm{d}\Omega,
$$

其中，$\mathbf{n}$ 是 $\partial \Omega$ 的外法向量。于是

$$
-
\int_{\Omega} \boldsymbol{\sigma} : \nabla \mathbf{v} \, \mathrm{d}\Omega + \int_{\Omega}\mathbf{f}\cdot \mathbf{v}\,\mathrm{d}\Omega + \int_{\partial \Omega} \left(\boldsymbol{\sigma} \mathbf{n}\right) \cdot \mathbf{v} \, \mathrm{d}S = 0,\quad \forall \, \mathbf{v} \in \, \mathcal{V},
$$

代入边界条件

$$
\int_{\partial \Omega} \left(\boldsymbol{\sigma} \mathbf{n}\right) \cdot \mathbf{v} \, \mathrm{d}S = \int_{\Gamma_{p}} \tilde{\mathbf{p}} \cdot \mathbf{v} \, \mathrm{d}S，
$$

于是

$$
-
\int_{\Omega} \boldsymbol{\sigma} : \nabla \mathbf{v} \, \mathrm{d}\Omega + \int_{\Omega}\mathbf{f}\cdot \mathbf{v}\,\mathrm{d}\Omega + \int_{\Gamma_{p}} \tilde{\mathbf{p}} \cdot \mathbf{v} \, \mathrm{d}S = 0,\quad \forall \, \mathbf{v} \in \, \mathcal{V}.
$$

定义对称算子

$$
\boldsymbol{\varepsilon}(\mathbf{u})=\frac{1}{2}\left(\nabla\mathbf{u} + (\nabla\mathbf{u})^{T}\right),
$$

类似地

$$
\boldsymbol{\varepsilon}(\mathbf{v})=\frac{1}{2}\left(\nabla\mathbf{v} + (\nabla\mathbf{v})^{T}\right),
$$

由于 $\boldsymbol{\sigma}$ 是对称张量，因此 $\boldsymbol{\sigma} : \nabla \mathbf{v} = \boldsymbol{\sigma} : (\nabla \mathbf{v})^T$，故 

$$
\boldsymbol{\sigma} : \nabla \mathbf{v} = \boldsymbol{\sigma} : \boldsymbol{\varepsilon}(\mathbf{v}),
$$

代入到方程中，得到

$$
-
\int_{\Omega} \boldsymbol{\sigma} : \boldsymbol{\varepsilon}(\mathbf{v}) \, \mathrm{d}\Omega + \int_{\Omega}\mathbf{f}\cdot \mathbf{v}\,\mathrm{d}\Omega + \int_{\Gamma_{p}} \tilde{\mathbf{p}} \cdot \mathbf{v} \, \mathrm{d}S = 0,\quad \forall \, \mathbf{v} \in \, \mathcal{V},
$$

再将本构方程 $\boldsymbol{\sigma}=\mathbf{D}:\boldsymbol{\varepsilon}(\mathbf{u})$ 代入上述方程，最终得到弱形式

$$
\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}) : \mathbf{D} : \boldsymbol{\varepsilon}(\mathbf{u}) \, \mathrm{d}\Omega = \int_{\Omega}\mathbf{f}\cdot \mathbf{v}\,\mathrm{d}\Omega + \int_{\Gamma_{p}} \tilde{\mathbf{p}} \cdot \mathbf{v} \, \mathrm{d}S,\quad \forall \, \mathbf{v} \in \, \mathcal{V},
$$

且 $\mathbf{u} = \mathbf{\tilde{u}},\, \text{on}\, \Gamma_{u}$

### Voigt 形式

```{margin}
注意，这里记号混用
```

为了便于有限元计算，通常将第一项写为 Voigt 形式

$$
\mathbf{D} : \boldsymbol{\varepsilon}(\mathbf{u}) 
\rightarrow\mathbf{D}\boldsymbol{\varepsilon}(\mathbf{u})= \begin{bmatrix}
\lambda + 2\mu & \lambda & \lambda & 0 & 0 & 0 \\
\lambda & \lambda + 2\mu & \lambda & 0 & 0 & 0 \\
\lambda & \lambda & \lambda + 2\mu & 0 & 0 & 0 \\
0 & 0 & 0 & \mu & 0 & 0 \\
0 & 0 & 0 & 0 & \mu & 0 \\
0 & 0 & 0 & 0 & 0 & \mu
\end{bmatrix}\begin{bmatrix}
\varepsilon_{xx}\\\varepsilon_{yy}\\\varepsilon_{zz}\\2\varepsilon_{xy}\\2\varepsilon_{xz}\\2\varepsilon_{yz}
\end{bmatrix}
$$

以及

```{margin}
$\mathbf{B}$ 是应变-位移矩阵
```

$$
\begin{equation}
\boldsymbol{\varepsilon}({\mathbf{u}}) = \mathbf{B}\mathbf{u}\quad \rightarrow\quad
\begin{bmatrix}
\varepsilon_{xx}\\\varepsilon_{yy}\\\varepsilon_{zz}\\2\varepsilon_{xy}\\2\varepsilon_{xz}\\2\varepsilon_{yz}
\end{bmatrix}
=\begin{bmatrix}
\frac{\partial}{\partial x} & 0 & 0 \\
0 & \frac{\partial}{\partial y} & 0 \\
0 & 0 & \frac{\partial}{\partial z} \\
0 & \frac{\partial}{\partial z} & \frac{\partial}{\partial y} \\
\frac{\partial}{\partial z} & 0 & \frac{\partial}{\partial x} \\
\frac{\partial}{\partial y} & \frac{\partial}{\partial x} & 0
\end{bmatrix}
\begin{bmatrix}
u_{x}\\u_{y}\\u_{z}
\end{bmatrix}
\end{equation}
$$

于是 

$$
\boldsymbol{\varepsilon}(\mathbf{v}) : \mathbf{D} : \boldsymbol{\varepsilon}(\mathbf{u}) = \boldsymbol{\varepsilon}(\mathbf{v})^{T} \mathbf{D} \boldsymbol{\varepsilon}(\mathbf{u})=(\mathbf{B}\mathbf{v})^{T}\mathbf{D}(\mathbf{B}\mathbf{u}),
$$


于是积分运算可以写为

$$
\begin{align}
\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}) : \mathbf{D} : \boldsymbol{\varepsilon}(\mathbf{u}) \, \mathrm{d}\Omega &= \sum_{E_{\text{物理}}}\int_{E_{\text{物理}}} \boldsymbol{\varepsilon}(\mathbf{v}) : \mathbf{D} : \boldsymbol{\varepsilon}(\mathbf{u}) \, \mathrm{d}E_{\text{物理}} \\
&= \sum_{E_{\text{物理}}}\int_{E_{\text{物理}}} (\mathbf{B}\mathbf{v})^{T}\mathbf{D}(\mathbf{B}\mathbf{u})\, \mathrm{d}E_{\text{物理}} \\
&= \sum_{E_{\text{参考}}}\int_{E_{\text{参考}}} (\mathbf{B}\mathbf{v})^{T}\mathbf{D}(\mathbf{B}\mathbf{u})\cdot\left|\det(\mathbf{J})\right| \, \mathrm{d}E_{\text{参考}}.
\end{align}
$$

## 离散

### 基本定义

设形函数为 $N_{i}$

#### 几何映射

$$
\begin{equation}
x = \sum_{i} N_{i}x_{i},\quad y = \sum_{i} N_{i}y_{i},\quad z = \sum_{i} N_{i}z_{i}.
\end{equation}
$$

#### 场变量插值

$$
\begin{equation}
\mathbf{u} 
= 
\begin{bmatrix}
u_{x} \\ u_{y} \\ u_{z}
\end{bmatrix}
=
\begin{bmatrix}
\sum_{i}N_{i}(\xi,\eta)u_{x,i} \\
\sum_{i}N_{i}(\xi,\eta)u_{y,i} \\
\sum_{i}N_{i}(\xi,\eta)u_{z,i}
\end{bmatrix}.
\end{equation}
$$

#### Jacobian 矩阵

$$
\begin{equation}
\mathbf{J} =
\begin{bmatrix}
\frac{\partial x}{\partial \xi} & \frac{\partial y}{\partial \xi} & \frac{\partial z}{\partial \xi} \\
\frac{\partial x}{\partial \eta} & \frac{\partial y}{\partial \eta} & \frac{\partial z}{\partial \eta} \\
\frac{\partial x}{\partial \zeta} & \frac{\partial y}{\partial \zeta} & \frac{\partial z}{\partial \zeta}
\end{bmatrix}
=
\sum_{i}
\begin{bmatrix}
\frac{\partial N_i}{\partial \xi} x_i & \frac{\partial N_i}{\partial \xi} y_i & \frac{\partial N_i}{\partial \xi} z_i \\
\frac{\partial N_i}{\partial \eta} x_i & \frac{\partial N_i}{\partial \eta} y_i & \frac{\partial N_i}{\partial \eta} z_i \\
\frac{\partial N_i}{\partial \zeta} x_i & \frac{\partial N_i}{\partial \zeta} y_i & \frac{\partial N_i}{\partial \zeta} z_i
\end{bmatrix}.
\end{equation}
$$

#### 积分运算

于是
