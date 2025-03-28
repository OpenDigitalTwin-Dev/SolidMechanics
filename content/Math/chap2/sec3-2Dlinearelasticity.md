# 线弹性问题

线弹性问题的控制方程为

$$
\begin{equation}
\begin{aligned}
&\nabla\cdot \boldsymbol{\sigma} + \mathbf{f} = \mathbf{0},\\
&\boldsymbol{\epsilon} = (\nabla \mathbf{u} + (\nabla\mathbf{u})^{T})/2,\\
&\boldsymbol{\sigma}=\mathbf{D}:\boldsymbol{\epsilon},
\end{aligned}
\end{equation}
$$

其中，$\boldsymbol{\sigma}$ 是应力张量，$\mathbf{f}$ 是体积力向量，$\boldsymbol{\epsilon}$ 是应变张量，$\mathbf{u}$ 是位移向量，$\mathbf{D}$ 是四阶本构张量

计算区域为 $\Omega$，边界 $\partial\Omega=\Gamma_{u}\cup\Gamma_{p}$，边界条件为

$$
\begin{equation}
\begin{aligned}
\mathbf{u} = \tilde{\mathbf{u}},\quad \text{on}\,\, \Gamma_{u},\\
\boldsymbol{\sigma}\mathbf{n} = \tilde{\mathbf{p}},\quad \text{on}\,\, \Gamma_{p}.
\end{aligned}
\end{equation}
$$

## 变分

选择测试函数 $\mathbf{v}\in\mathcal{V}$，其中

$$
\mathcal{V}=\left\{\left.\mathbf{v}\in \left[H^{1}(\Omega)\right]^d \,\,\right|\,\, \mathbf{v}=\mathbf{0} \,\, \text{on}\,\, \Gamma_{u} \right\}.
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
\int_{\Omega} \boldsymbol{\sigma} : \nabla \mathbf{v} \, \mathrm{d}\Omega + \int_{\Omega}\mathbf{f}\cdot \mathbf{v}\,\mathrm{d}\Omega + \int_{\partial \Omega} \left(\boldsymbol{\sigma} \mathbf{n}\right) \cdot \mathbf{v} \, \mathrm{d}S = 0.
$$

代入边界条件

$$
\int_{\partial \Omega} \left(\boldsymbol{\sigma} \mathbf{n}\right) \cdot \mathbf{v} \, \mathrm{d}S = \int_{\Gamma_{p}} \tilde{\mathbf{p}} \cdot \mathbf{v} \, \mathrm{d}S，
$$

于是

$$
-
\int_{\Omega} \boldsymbol{\sigma} : \nabla \mathbf{v} \, \mathrm{d}\Omega + \int_{\Omega}\mathbf{f}\cdot \mathbf{v}\,\mathrm{d}\Omega + \int_{\Gamma_{p}} \tilde{\mathbf{p}} \cdot \mathbf{v} \, \mathrm{d}S = 0.
$$

定义对称算子

$$
\boldsymbol{\epsilon}(\mathbf{u})=\frac{1}{2}\left(\nabla\mathbf{u} + (\nabla\mathbf{u})^{T}\right)
$$

类似地

$$
\boldsymbol{\epsilon}(\mathbf{v})=\frac{1}{2}\left(\nabla\mathbf{v} + (\nabla\mathbf{v})^{T}\right)
$$

由于 $\boldsymbol{\sigma}$ 是对称张量，因此 $\boldsymbol{\sigma} : \nabla \mathbf{v} = \boldsymbol{\sigma} : (\nabla \mathbf{v})^T$，故 

$$
\boldsymbol{\sigma} : \nabla \mathbf{v} = \boldsymbol{\sigma} : \boldsymbol{\epsilon}(\mathbf{v})
$$

代入到方程中，得到

$$
-
\int_{\Omega} \boldsymbol{\sigma} : \boldsymbol{\epsilon}(\mathbf{v}) \, \mathrm{d}\Omega + \int_{\Omega}\mathbf{f}\cdot \mathbf{v}\,\mathrm{d}\Omega + \int_{\Gamma_{p}} \tilde{\mathbf{p}} \cdot \mathbf{v} \, \mathrm{d}S = 0.
$$

再将本构方程 $\boldsymbol{\sigma}=\mathbf{D}:\boldsymbol{\epsilon}(\mathbf{u})$ 代入上述方程，最终得到弱形式


$$
\int_{\Omega} \boldsymbol{\epsilon}(\mathbf{v}) : \mathbf{D} : \boldsymbol{\epsilon}(\mathbf{u}) \, \mathrm{d}\Omega = \int_{\Omega}\mathbf{f}\cdot \mathbf{v}\,\mathrm{d}\Omega + \int_{\Gamma_{p}} \tilde{\mathbf{p}} \cdot \mathbf{v} \, \mathrm{d}S = 0.
$$

## 离散

### 积分计算
