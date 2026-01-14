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

类似地，变分算子在和，积，比，幂与微分算子一致

## 变分运算的可交换性

**在变分算子的定义中，存在一个关键的描述问题**

- **Lagrangian 变分: $\mathbf{u} = \mathbf{u}(\mathbf{X})$，此时 $\delta\mathbf{u} = \delta\mathbf{u}(\mathbf{X})$ 是针对所有材料点的全局扰动，进行变分运算时，$\mathbf{X}$ 保持不变**
- **Eulerian 变分: $\mathbf{u} = \mathbf{u}(\mathbf{x})$，此时 $\delta\mathbf{u} = \delta\mathbf{u}(\mathbf{x})$ 是针对所有空间点全局扰动，为表示区分，记为 $\delta_{x}$，进行变分运算时，$\mathbf{x}$ 保持不变**

**在连续介质力学，特别是固体力学中，虚位移的变分通常采用物质描述，也就是 Lagrangian 变分**

### 交换性

对于 Lagrangian 变分和初始构型，显然有

$$
\begin{aligned}
\delta(\nabla_{0}\mathbf{u})&=\left[\frac{\mathrm{d}}{\mathrm{d}\epsilon}\nabla_{0}(\mathbf{u}+\epsilon\delta\mathbf{u})\right]_{\epsilon=0}=\nabla_{0}(\delta\mathbf{u})\\
\delta\left(\int_{\Omega_{0}}\mathbf{u}\mathrm{d}V\right)&=\left[\frac{\mathrm{d}}{\mathrm{d}\epsilon}\int_{\Omega_{0}}(\mathbf{u}+\epsilon\delta\mathbf{u})\mathrm{d}V\right]_{\epsilon=0}=\int_{\Omega_{0}}\delta\mathbf{u}\mathrm{d}V
\end{aligned}
$$

```{admonition} 一个例子
:class: tip, dropdown

考虑 $a(x) = x^{2}$，给定一个材料扰动

$$
x_{\epsilon}=x+\epsilon\eta(x)
$$

于是

$$
\begin{aligned}
\delta\nabla a &= \delta (2x) = 2\eta\\
\nabla\delta a &= \nabla(2x\eta) = 2\eta+2x\nabla\eta
\end{aligned}
$$

前者是梯度场的变分，后者是变分后场的梯度，得到 $\delta\nabla a \neq \nabla\delta a$，其原因在于**变分与梯度所使用的描述不同**


如果都使用 **Lagrangian 描述**，记初始状态为 $x = X$，变形后为 $x = X + \epsilon\eta(X)$，此时

$$
A(X) = a(x(X)) = (X + \epsilon\eta(X))^{2}
$$

于是

$$
\begin{aligned}
\delta\nabla_{0} a &= \frac{\mathrm{d}}{\mathrm{d}\epsilon} \left[2(X + \epsilon\eta)(1+\epsilon\nabla\eta)\right]_{\epsilon=0}\\
&=2\frac{\mathrm{d}}{\mathrm{d}\epsilon}\left[X+\epsilon\eta + \epsilon X\nabla\eta + \epsilon^{2}\eta\nabla\eta\right]_{\epsilon=0}\\
&=2\eta+2X\nabla\eta
\end{aligned}
$$

另一方面

$$
\begin{aligned}
\nabla_{0} \delta a &= \nabla_{0}\frac{\mathrm{d}}{\mathrm{d}\epsilon} \left[(X + \epsilon\eta(X))^{2}\right]_{\epsilon=0}\\
&=\nabla_{0}(2X\eta)\\
&=2\eta+2X\nabla\eta
\end{aligned}
$$

此时有，$\delta\nabla_{0} a = \nabla_{0} \delta a$

如果都使用 **Eulerian 描述**，则

$$
\begin{aligned}
\delta_{x}\nabla a &= \delta_{x} (2x) =  2\frac{\mathrm{d}}{\mathrm{d}\epsilon} (x + \epsilon\eta) = 2\eta \\
\nabla \delta_{x}a &= \nabla (\frac{\mathrm{d}}{\mathrm{d}\epsilon}\left[(x+\epsilon\eta)^2\right]_{\epsilon=0})
\end{aligned}
$$

```

 
```{admonition} 一些重要的变分运算
:class: tip, dropdown

$$
\nabla\delta\mathbf{u} = \nabla_0 \delta\mathbf{u}\ \mathbf{F}^{-1}; \quad \nabla\delta\mathbf{v} = \nabla_0 \delta\mathbf{v}\ \mathbf{F}^{-1}
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