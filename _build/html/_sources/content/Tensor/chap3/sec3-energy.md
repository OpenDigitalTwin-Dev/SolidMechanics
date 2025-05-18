# 内功和应变能

## 内功

表面力对材料做功的总功率为

```{margin}
$\boldsymbol{\sigma}$ 对称
```

$$
\begin{equation}
\begin{aligned}
P &= \int_{\partial V}\mathbf{v}\cdot(\boldsymbol{\sigma}\ \mathrm{d}\mathbf{S}) 
= \int_{\partial V}\mathbf{v}\cdot\boldsymbol{\sigma}\mathbf{n}\ \mathrm{d}S\\
&= \int_{\partial V}\boldsymbol{\sigma}\mathbf{v}\cdot\mathbf{n}\ \mathrm{d}S 
= \int_{V}\nabla\cdot(\boldsymbol{\sigma}\mathbf{v})\ \mathrm{d}V\\
&=\int_{V}\boldsymbol{\sigma}:\nabla\mathbf{v}\ \mathrm{d}V + \int_{V}(\nabla\cdot\boldsymbol{\sigma})\cdot\mathbf{v}\ \mathrm{d}V,
\end{aligned}
\end{equation}
$$

第一项称为**内功率**（或应力功率密度）$P_{\text{int}}$，表示单位时间内，材料内部应力对变形所做的功，反映了**由于变形引起的能量变化速率**

第二项则表达了惯性效应和体积力对整体运动的功率贡献（结合动量守恒方程）

由于

$$
\nabla\mathbf{v} = \mathbf{D} + \mathbf{W},
$$

于是

$$
\int_{V}\boldsymbol{\sigma}:\nabla\mathbf{v}\ \mathrm{d}V = \int_{V}\boldsymbol{\sigma}:\mathbf{D} + \boldsymbol{\sigma}:\mathbf{W}\ \mathrm{d}V = \int_{V}\boldsymbol{\sigma}:\mathbf{D}\ \mathrm{d}V,
$$

由于 $\boldsymbol{\sigma}$ 对称，$\mathbf{W}$ 反对称，故

$$
P_{\text{int}} = \int_{V}\boldsymbol{\sigma}:\mathbf{D}\ \mathrm{d}V,
$$

内力对材料内部变形所做的总功为**内功**

$$
W_{\text{int}} = \int_{0}^{t}P_{\text{int}}\ \mathrm{d}t.
$$


## 应变能

```{margin}
超弹性材料：又称伪弹性材料，是一类在较大应变范围（5%~10%）内能够完全恢复原始形状的材料
```

**应变能** $U$ 是材料在**弹性变形**过程中，由于抵抗外力做功而储存在其内部的能量。当外力卸载时，这部分能量能够完全释放，使材料恢复到原始形状

**应变能仅指材料在弹性变形过程中储存的能量，在非弹性变形（如塑性变形）过程中，外部做功不再全部以应变能形式储存**

因此，应变能是依赖于变形状态的一种势能

$$
U(\boldsymbol{\varepsilon}) = \int_{V}\Psi(\boldsymbol{\varepsilon})\ \mathrm{d}V,
$$


$\Psi$ 是**应变能密度**函数，表示材料在弹性变形过程中单位参考体积储存的能量，仅依赖于变形状态。应变能密度是在变形过程中逐步累积的，故

$$
\Psi(\boldsymbol{\varepsilon}) = \int_{0}^{\varepsilon_{ij}}\sigma_{ij}\ \mathrm{d}\varepsilon_{ij},
$$

有

$$
\frac{\partial \Psi}{\partial \boldsymbol{\varepsilon}} = \boldsymbol{\sigma}\quad\Longrightarrow\quad \frac{\partial \Psi}{\partial t} = \frac{\partial \Psi}{\partial \boldsymbol{\varepsilon}}:\frac{\partial \boldsymbol{\varepsilon}}{\partial t} = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}},
$$

```{note}

对于线弹性材料，代入 $\sigma_{ij}=C_{ijkl}\varepsilon_{kl}$，得到

$$
\Psi(\boldsymbol{\varepsilon}) = \frac{1}{2}\sigma_{ij}\varepsilon_{ij} = \frac{1}{2}\boldsymbol{\sigma}:\boldsymbol{\varepsilon}.
$$

```

应变能可以写为

$$
U(\boldsymbol{\varepsilon}) = \int_{V}\int_{0}^{\varepsilon_{ij}}\sigma_{ij}\ \mathrm{d}\varepsilon_{ij}\ \mathrm{d}V,
$$


应变能率为

$$
\begin{equation}
\begin{aligned}
\dot{U}(\boldsymbol{\varepsilon}) = \frac{\mathrm{d}}{\mathrm{d}t}\int_{V}\Psi\ \mathrm{d}V.
\end{aligned}
\end{equation}
$$

若积分体区域 $V$ 不随时间变化，则

$$
\dot{U}(\boldsymbol{\varepsilon}) = \int_{V}\frac{\mathrm{d}\Psi}{\mathrm{d}t}\ \mathrm{d}V= \int_{V}\frac{\partial \Psi}{\partial \boldsymbol{\varepsilon}}:\frac{\partial \boldsymbol{\varepsilon}}{\partial t}\ \mathrm{d}V = \int_{V}\boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}\ \mathrm{d}V.
$$