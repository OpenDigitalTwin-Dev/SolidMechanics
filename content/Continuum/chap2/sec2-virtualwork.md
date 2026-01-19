# 虚功原理

当一个力 $\mathbf{F}$ 作用于材料点并使其发生位移 $\mathbf{u}$ 时，力所做的功定义为力在位移方向上的分量与位移大小的乘积，即

$$
\mathbf{F}\cdot\mathbf{u}
$$

对于一个物质体 $\Omega$，力 $\mathbf{F}$ 在其上所做的总功为

$$
W = \int_{\Omega}\mathbf{F}\cdot\mathbf{u}\ \mathrm{d}v
$$

如果物质体在力 $\mathbf{F}$ 的作用下发生了一段无穷小的位移 $\delta \mathbf{u}$（称为虚位移），则此时力 $\mathbf{F}$ 所做的功为

$$
\delta {W} = \int_{\Omega}\mathbf{F}\cdot\delta \mathbf{u}\ \mathrm{d}v
$$

称为**虚功**。系统处于平衡时，对任意满足约束的虚位移，所有外力（或主动力）的合虚功为零



### 虚位移（速度）原理

设在体积力 $\mathbf{f}$ 与表面力 $\mathbf{t}$ 作用下虚功率为

$$
\delta W_{E}\equiv-\left(\int_{\Omega}\mathbf{f}\cdot\delta\mathbf{v}\ \mathrm{d}v+\int_{\Gamma_{\sigma}}\mathbf{t}\cdot\delta\mathbf{v}\ \mathrm{d}s\right),
$$

其中，$\mathbf{v}$ 是速度，$\Gamma_{\sigma}$ 是力边界，在剩余边界 $\Gamma_{u} = \Gamma-\Gamma_{\sigma}$ 上，位移是被指定的，因此虚位移（虚速度）在这些边界上满足齐次性条件，即 $\delta\mathbf{u} = \delta\mathbf{v} = \mathbf{0}$，故上述方程可以写为

$$
\delta W_{E}\equiv-\left(\int_{\Omega}\mathbf{f}\cdot\delta\mathbf{v}\ \mathrm{d}v+\oint_{\Gamma}\mathbf{t}\cdot\delta\mathbf{v}\ \mathrm{d}s\right),
$$

由于 

$$
\mathbf{t}\cdot\delta\mathbf{v} = (\boldsymbol{\sigma}\mathbf{n})\cdot\delta\mathbf{v} = \delta\mathbf{v}^{T}\boldsymbol{\sigma}\mathbf{n} = \mathbf{n}^{T}\boldsymbol{\sigma}\delta\mathbf{v} = (\boldsymbol{\sigma}\delta\mathbf{v})\cdot\mathbf{n}
$$

和

$$
\nabla\cdot(\boldsymbol{\sigma}\mathbf{v})=\left(\nabla \cdot \boldsymbol{\sigma}\right) \cdot \mathbf{v}+\boldsymbol{\sigma}:\nabla\mathbf{v},
$$

故，使用散度定理

$$
\begin{aligned}
\int_{\Omega}\mathbf{f}\cdot\delta\mathbf{v}\ \mathrm{d}v+\oint_{\Gamma}\mathbf{t}\cdot\delta\mathbf{v}\ \mathrm{d}s&=\int_{\Omega}\mathbf{f}\cdot\delta\mathbf{v}\ \mathrm{d}v+\int_{\Omega}\nabla\cdot(\boldsymbol{\sigma}\mathbf{n})\ \mathrm{d}v\\
&=\int_{\Omega}\left((\mathbf{f}+\nabla\cdot\boldsymbol{\sigma})\cdot\delta\mathbf{v}+\boldsymbol{\sigma}:\nabla\delta\mathbf{v}\right)\ \mathrm{d}v
\end{aligned}
$$

对于平衡状态，满足

$$
\mathbf{f}+\nabla\cdot\boldsymbol{\sigma} = \mathbf{0},
$$

因此

$$
\int_{\Omega}\boldsymbol{\sigma}:\nabla\delta\mathbf{v}\ \mathrm{d}v-\left(\int_{\Omega}\mathbf{f}\cdot\delta\mathbf{v}\ \mathrm{d}v+\oint_{\Gamma}\mathbf{t}\cdot\delta\mathbf{v}\ \mathrm{d}s\right) = 0
$$ (sec8-eq:virtualworkpower)

第一项被成为内虚功率，记为

```{margin}
由于 $\boldsymbol{\sigma}$ 的对称性和 $\delta\mathbf{w}$ 的反对称性
```

$$
\delta W_{I}\equiv\int_{\Omega}\boldsymbol{\sigma}:\nabla\delta\mathbf{v}\ \mathrm{d}v = \int_{\Omega}\boldsymbol{\sigma}:\delta\mathbf{d}\ \mathrm{d}v = \int_{\Omega}\boldsymbol{\sigma}:\delta\mathbf{l}\ \mathrm{d}v
$$

因此，对于处于**平衡状态**的连续体，所有实际力在通过虚位移时的虚功均为零，即

$$
\delta W \equiv \delta W_{E} + \delta W_{I} = 0
$$

对于线弹性问题，使用虚位移 $\delta\mathbf{u}$ 推导，则得到

$$
\int_{\Omega}\boldsymbol{\sigma}:\delta\boldsymbol{\varepsilon}\ \mathrm{d}v-\left(\int_{\Omega}\mathbf{f}\cdot\delta\mathbf{u}\ \mathrm{d}v+\oint_{\Gamma}\mathbf{t}\cdot\delta\mathbf{u}\ \mathrm{d}s\right) = 0
$$

将 {eq}`sec8-eq:virtualworkpower` 转换到初始构型上，得到

$$
\int_{\Omega_{0}}J\boldsymbol{\sigma}:\nabla\delta V\ \mathrm{d}V - \left(\int_{\Omega_{0}}\mathbf{f}_{0}\cdot\delta\mathbf{V}\ \mathrm{d}V+\oint_{\Gamma_{0}}\mathbf{t}_{0}\cdot\delta\mathbf{V}\ \mathrm{d}S\right) = 0
$$

其中，$\mathbf{f}_{0} = J\mathbf{f},\mathbf{t}_{0}=\mathbf{t}(\mathrm{d}s/\mathrm{d}S)$，$J\boldsymbol{\sigma}$ 被称为 Kirchhoff 应力张量，故

$$
\begin{aligned}
\delta W_{I} &= \int_{\Omega_{0}}J\boldsymbol{\sigma}:\nabla\delta V\ \mathrm{d}V = \int_{\Omega_{0}}J\boldsymbol{\sigma}:\delta \mathbf{d}\ \mathrm{d}V\\
&=\int_{\Omega_{0}}J\boldsymbol{\sigma}:\text{sym}(\delta\dot{\mathbf{F}}\mathbf{F}^{-1})\ \mathrm{d}V = \int_{\Omega_{0}}J\boldsymbol{\sigma}:\delta\dot{\mathbf{F}}\mathbf{F}^{-1}\ \mathrm{d}V\\
&=\int_{\Omega_{0}}J\boldsymbol{\sigma}\mathbf{F}^{-T}:\delta\dot{\mathbf{F}}\ \mathrm{d}V=\int_{\Omega_{0}}\mathbf{P}:\delta\dot{\mathbf{F}}\ \mathrm{d}V
\end{aligned}
$$

得到其 PK1 应力张量的表达形式；另一方面

$$
\delta W_{I} = \int_{\Omega}\boldsymbol{\sigma}:\delta\mathbf{d}\ \mathrm{d}v=\int_{V_0} \mathbf{S} : \delta \dot{\mathbf{E}} \, dV_0
$$

得到其 PK2 应力张量的表达形式

```{admonition} 证明
:class: tip, dropdown

应力功率是标量，在任何描述下都相等，故

$$
P = \int_{V_0} \mathbf{S} : \dot{\mathbf{E}} \, dV_0 = \int_{V} \boldsymbol{\sigma} : \mathbf{d} \, dV
$$

这是因为

$$
\begin{aligned}
\dot{\mathbf{E}} = \frac{1}{2} (\dot{\mathbf{F}}^T \mathbf{F} + \mathbf{F}^T \dot{\mathbf{F}}) &= \frac{1}{2}\mathbf{F}^{T}(\mathbf{F}^{-T}\dot{\mathbf{F}}+\dot{\mathbf{F}}\mathbf{F}^{-1})\mathbf{F}=\mathbf{F}^{T}\mathbf{d}\mathbf{F}
\end{aligned}
$$

由于（迹运算交换）

$$
\mathbf{S} : (\mathbf{F}^T \mathbf{X} \mathbf{F}) = (\mathbf{F} \mathbf{S} \mathbf{F}^T) : \mathbf{X}
$$

故

$$
\mathbf{S} : \dot{\mathbf{E}} = \mathbf{S} : \mathbf{F}^{T}\mathbf{d}\ \mathbf{F} = \mathbf{F}\mathbf{S}\mathbf{F}^{T}:\mathbf{d}
$$

得到

$$
\int_{V_0} \mathbf{S} : \dot{\mathbf{E}} \, dV_0 = \int_{V} J^{-1}\mathbf{F}\mathbf{S}\mathbf{F}^{T}:\mathbf{d} \, dV=\int_{V} \boldsymbol{\sigma} : \mathbf{d} \, dV
$$

由于

$$
\begin{aligned}
\delta \dot{\mathbf{E}} &= \delta \left(\frac{1}{2} (\dot{\mathbf{F}}^T \mathbf{F} + \mathbf{F}^T \dot{\mathbf{F}})\right)\\
&= \frac{1}{2} \delta\left( (\nabla_0 \mathbf{v})^T \mathbf{F} + \mathbf{F}^T (\nabla_0 \mathbf{v}) \right)\\
&=\frac{1}{2} \left( (\nabla_0 \delta\mathbf{v})^T \mathbf{F} + \mathbf{F}^T (\nabla_0 \delta\mathbf{v}) \right)\\
&=\mathbf{F}^T [\operatorname{sym}(\nabla \delta \mathbf{v})] \mathbf{F}\\
&=\mathbf{F}^T \delta\mathbf{d}\ \mathbf{F}
\end{aligned}
$$

于是虚功率

$$
\delta P = \int_{V_0} \mathbf{S} : \delta \dot{\mathbf{E}} \, dV_0=
\int_{V_0} \mathbf{S} : (\mathbf{F}^T \delta\mathbf{d}\  \mathbf{F}) \, dV_0
$$

故

$$
\begin{aligned}
\delta P &= \int_{V_0} (\mathbf{F}\mathbf{S}\mathbf{F}^{T}) : \delta\mathbf{d}\  \mathrm{d}V_0\\
&=\int_{V} \frac{1}{J}(\mathbf{F}\mathbf{S}\mathbf{F}^{T}) : \delta\mathbf{d}\  \mathrm{d}V\\
&=\int_{V} \boldsymbol{\sigma} : \delta\mathbf{d}\  \mathrm{d}V
\end{aligned}
$$

因此

$$
\int_{V_0} \mathbf{S} : \delta \dot{\mathbf{E}} \, dV_0=\int_{V} \boldsymbol{\sigma} : \delta\mathbf{d}  \, dV
$$

```

类似地，对于平衡问题，使用虚位移 $\delta\mathbf{u}$ 推导，得到

```{margin}
此处不区分：$\delta\mathbf{U} = \delta\mathbf{u}$
```

$$
\int_{\Omega_{0}} \mathbf{S}:\delta\mathbf{E}\ \mathrm{d}V - \left(\int_{\Omega_{0}}\mathbf{f}_{0}\cdot\delta\mathbf{u}\ \mathrm{d}V+\oint_{\Gamma_{0}}\mathbf{t}_{0}\cdot\delta\mathbf{u}\ \mathrm{d}S\right) = 0
$$

