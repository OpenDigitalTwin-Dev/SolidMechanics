# 变分

## 控制方程

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

且 $\mathbf{u} = \mathbf{\tilde{u}},\, \text{on}\, \Gamma_{D}$，通常记

$$
a(\mathbf{u},\mathbf{v})=\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}) : \mathbb{C} : \boldsymbol{\varepsilon}(\mathbf{u}) \, \mathrm{d}V,
$$

这是关于 $\mathbf{u}$ 和 $\mathbf{v}$ 的双线性形式

### Voigt 形式

```{margin}
注意，为了方便，这里记号混用
```

通过使用 Voigt 形式，可将张量形式变为矩阵形式

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
\end{bmatrix}=\begin{bmatrix}
\sigma_{xx}\\\sigma_{yy}\\\sigma_{zz}\\\sigma_{xy}\\\sigma_{xz}\\\sigma_{yz}
\end{bmatrix},
$$

其中，$\lambda=\frac{E \nu}{(1+\nu)(1-2\nu)}$，$\mu=G=\frac{E}{2(1+\nu)}$.

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

