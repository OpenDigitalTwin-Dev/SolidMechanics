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

称为**虚功**

## 一阶变分

设 $\varphi = \varphi(\mathbf{u})$ 是 $\mathbf{u}$ 的可微函数，则 $\varphi(\mathbf{u})$ 在 $\mathbf{u}$ 处的方向为 $\delta\mathbf{u}$ 的一阶变分定义为

$$
\delta\varphi(\mathbf{u},{\color{red}\delta\mathbf{u}})=\mathbf{D}_{\delta\mathbf{u}}\varphi(\mathbf{u})\equiv\left.\frac{\mathrm{d}}{\mathrm{d}\epsilon}\varphi(\mathbf{u}+\epsilon{\color{red}\delta\mathbf{u}})\right|_{\epsilon=0}
$$

也被称为 G$\mathrm{\hat{a}}$teaux 导数，$\delta$ 被称为变分算子

**注意，在上述定义中，存在一个关键问题，即 $\mathbf{u}$ 的构型表示**

- **$\mathbf{u} = \mathbf{u}(\mathbf{X})$，此时应有 $\delta\mathbf{u} = \delta\mathbf{u}(\mathbf{X})$，被称为 Lagrangian 变分**
- **$\mathbf{u} = \mathbf{u}(\mathbf{x})$，此时应有 $\delta\mathbf{u} = \delta\mathbf{u}(\mathbf{x})$，被称为 Eulerian 变分**

**在连续介质力学，特别是固体力学中，虚位移的变分通常采用物质描述，对应的变分方式被成为 Lagrangian 变分**

```{admonition} $\delta\mathbf{u}$
:class: tip, dropdown

$\mathbf{u}$ 在 $\boldsymbol{\eta}$ 方向的变分为

$$
\delta\mathbf{u} = \left.\frac{\mathrm{d}}{\mathrm{d}\epsilon}(\mathbf{u}+\epsilon\boldsymbol{\eta})\right|_{\epsilon=0}=\boldsymbol{\eta}
$$

故 $\boldsymbol{\eta} = \delta\mathbf{u}$ 

```

变分算子与微分算子在形式上类似,但二者的本质区别在于:

- 微分算子作用于函数,描述函数值随自变量变化的变化率(函数空间→数值)
- 变分算子作用于泛函,描述泛函值随函数(作为自变量)变化的变化率(泛函空间→数值)

```{admonition} 线性性
:class: tip, dropdown

变分算子是线性的

$$
\begin{aligned}
\delta\varphi(\mathbf{u},\alpha\delta\mathbf{u}_{1}+\beta\delta\mathbf{u}_{2})=\left.\frac{\mathrm{d}}{\mathrm{d}\epsilon}\varphi(\mathbf{u}+\epsilon(\alpha\delta\mathbf{u}_{1}+\beta\delta\mathbf{u}_{2}))\right|_{\epsilon=0}
\end{aligned}
$$

记 $g(\epsilon)=\varphi(\mathbf{u}+\epsilon(\alpha\delta\mathbf{u}_{1}+\beta\delta\mathbf{u}_{2}))$，故

$$
\begin{aligned}
\left.\frac{\mathrm{d}g}{\mathrm{d}\epsilon}\right|_{\epsilon=0} &= \frac{\partial\varphi}{\partial\mathbf{u}}\cdot(\alpha\delta\mathbf{u}_{1}+\beta\delta\mathbf{u}_{2})\\ 
&=\frac{\partial\varphi}{\partial\mathbf{u}}\cdot\alpha\delta\mathbf{u}_{1}+\frac{\partial\varphi}{\partial\mathbf{u}}\cdot\beta\delta\mathbf{u}_{2}\\
&=\left.\frac{\mathrm{d}}{\mathrm{d}\epsilon}\varphi(\mathbf{u}+\epsilon\alpha\delta\mathbf{u}_{1})\right|_{\epsilon=0} + \left.\frac{\mathrm{d}}{\mathrm{d}\epsilon}\varphi(\mathbf{u}+\epsilon\beta\delta\mathbf{u}_{2})\right|_{\epsilon=0}\\
&=\delta\varphi(\mathbf{u},\alpha\delta\mathbf{u}_{1})+\delta\varphi(\mathbf{u},\beta\delta\mathbf{u}_{2})
\end{aligned}
$$

```

类似地，变分算子在和，积，比，幂与微分算子一致；此外，变分算子与微分算子和积分算子具有可交换性

$$
\begin{aligned}
\delta(\nabla\mathbf{u})&=\left[\frac{\mathrm{d}}{\mathrm{d}\epsilon}\nabla(\mathbf{u}+\epsilon\delta\mathbf{u})\right]_{\epsilon=0}=\nabla(\delta\mathbf{u})\\
\delta\left(\int_{\Omega}\mathbf{u}\mathrm{d}v\right)&=\left[\frac{\mathrm{d}}{\mathrm{d}\epsilon}\int_{\Omega}(\mathbf{u}+\epsilon\delta\mathbf{u})\mathrm{d}v\right]_{\epsilon=0}=\int_{\Omega}\delta\mathbf{u}\mathrm{d}v
\end{aligned}
$$


```{admonition} 一些重要的变分运算
:class: tip, dropdown

$$
\nabla\delta\mathbf{u} = \mathbf{F}^{-T}  \nabla_0 \delta\mathbf{u}; \quad \nabla\delta\mathbf{v} = \mathbf{F}^{-T}  \nabla_0 \delta\mathbf{v}
$$

$$
\delta\mathbf{F} = \nabla_0 \delta\mathbf{u}; \quad \delta\dot{\mathbf{F}} = \nabla_0 \delta\mathbf{v}; \quad \delta\mathbf{F}^{-1} = -\nabla\delta\mathbf{u}
$$

$$
\delta\boldsymbol{\varepsilon} = \frac{1}{2}\left[(\nabla_0 \delta\mathbf{u})^{\mathrm{T}} + \nabla_0 \delta\mathbf{u}\right]
$$

$$
\delta\mathbf{E} = \frac{1}{2}\mathbf{F}^{\mathrm{T}} \cdot \left[(\nabla\delta\mathbf{u})^{\mathrm{T}} + \nabla\delta\mathbf{u}\right] \cdot \mathbf{F} \approx \mathbf{F}^{\mathrm{T}} \cdot \delta\boldsymbol{\varepsilon} \cdot \mathbf{F}
$$

$$
\delta\mathbf{d} = \frac{1}{2}\left[(\nabla\delta\mathbf{v})^{\mathrm{T}} + \nabla\delta\mathbf{v}\right] = \delta\dot{\mathbf{F}} \cdot \mathbf{F}^{-1}
$$

$$
\delta (F^{-1}) = \delta (\frac{\partial (\mathbf{x}-\mathbf{u})}{\partial \mathbf{x}})=-\delta (\frac{\partial \mathbf{u}}{\partial \mathbf{x}})
$$

```