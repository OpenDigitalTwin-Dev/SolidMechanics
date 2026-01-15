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

设 $\mathcal{F}$ 对 $\psi$ **可微**，则其一阶变分定义为

$$
\delta\mathcal{F}(\psi;\eta)\equiv\left.\frac{\mathrm{d}}{\mathrm{d}\epsilon}\mathcal{F}(\psi+\epsilon\eta)\right|_{\epsilon=0}
$$ (sec8-eq:1st-variation)

其中，$\psi$ 和 $\eta$ 同属于一个向量空间，一阶变分也称为 G$\mathrm{\hat{a}}$teaux 导数，$\delta$ 被称为变分算子

通常，把 $\eta$ 记为 $\delta\psi$ 因此，式 {eq}`sec8-eq:1st-variation` 通常也写为

$$
\delta\mathcal{F}(\psi;\delta\psi)\equiv\left.\frac{\mathrm{d}}{\mathrm{d}\epsilon}\mathcal{F}(\psi+\epsilon\delta\psi)\right|_{\epsilon=0}
$$

当 $\mathcal{F} = \psi$ 时，代入上式，是自洽的

对构型的扰动，称为 Lagrangian 微分，此时 $\mathbf{X}$ 固定；对物理场的扰动，称为 Eulerian 微分，此时 $\mathbf{x}$ 固定


变分算子与微分算子在形式上类似,但二者的本质区别在于:

- 微分算子作用于函数,描述函数值随自变量变化的变化率(函数空间→数值)
- 变分算子作用于泛函,描述泛函值随函数(作为自变量)变化的变化率(泛函空间→数值)

变分算子在和，积，比，幂的运算与微分算子一致

**类似于偏导数计算，对于多变量泛函，变分运算也可以指定变分变量，并默认其它变量保持不变**

```{admonition} 线性性
:class: tip, dropdown


$$
\begin{aligned}
\delta\mathcal{F}(\psi;\alpha\delta\psi_{1}+\beta\delta\psi_{2})=\left.\frac{\mathrm{d}}{\mathrm{d}\epsilon}\mathcal{F}(\psi+\epsilon(\alpha\delta\psi_{1}+\beta\delta\psi_{2}))\right|_{\epsilon=0}
\end{aligned}
$$

记 $g(\epsilon)=\mathcal{F}(\psi+\epsilon(\alpha\delta\psi_{1}+\beta\delta\psi_{2}))$，故

$$
\begin{aligned}
\left.\frac{\mathrm{d}g}{\mathrm{d}\epsilon}\right|_{\epsilon=0} &= \frac{\partial\mathcal{F}}{\partial\psi}\cdot(\alpha\delta\psi_{1}+\beta\delta\psi_{2})\\ 
&=\frac{\partial\mathcal{F}}{\partial\psi}\cdot\alpha\delta\psi_{1}+\frac{\partial\mathcal{F}}{\partial\psi}\cdot\beta\delta\psi_{2}\\
&=\left.\frac{\mathrm{d}}{\mathrm{d}\epsilon}\mathcal{F}(\psi+\epsilon\alpha\delta\psi_{1})\right|_{\epsilon=0} + \left.\frac{\mathrm{d}}{\mathrm{d}\epsilon}\mathcal{F}(\psi+\epsilon\beta\delta\psi_{2})\right|_{\epsilon=0}\\
&=\delta\mathcal{F}(\psi;\alpha\delta\psi_{1})+\delta\mathcal{F}(\psi;\beta\delta\psi_{2})
\end{aligned}
$$

```

## 变分运算的可交换性


对于 Lagrangian 变分和初始构型的运算，显然有

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
```

### 交换公式

$$
\delta (\nabla \mathbf{u}) = \nabla (\delta \mathbf{u}) - (\nabla \mathbf{u})(\nabla \delta \mathbf{u})
$$

```{admonition} 证明
:class: tip, dropdown

$$
\begin{aligned}
\delta (\nabla \mathbf{u}) = \delta (\nabla_{0} \mathbf{u}\ \mathbf{F}^{-1}) &= \delta(\nabla_{0} \mathbf{u})\mathbf{F}^{-1} + \nabla_{0} \mathbf{u}\delta\mathbf{F}^{-1}\\
&=\nabla_{0}\delta\mathbf{u}\ \mathbf{F}^{-1}-\nabla_{0} \mathbf{u}\mathbf{F}^{-1}\nabla\delta\mathbf{u}\\
&=\nabla\delta\mathbf{u}-\nabla\mathbf{u}\nabla\delta\mathbf{u}
\end{aligned}
$$

其中用到了两条重要的公式

$$
\begin{aligned}
\nabla \mathbf{w} &= \nabla_{0} \mathbf{w}\ \mathbf{F}^{-1}\\
\delta\mathbf{F}^{-1} &=-\mathbf{F}^{-1}\nabla\delta\mathbf{u}
\end{aligned}
$$

前者是显然的，对于后者，由于 $\mathbf{F}\mathbf{F}^{-1} = \mathbf{I}$，故

$$
\begin{aligned}
\mathbf{0} = \delta(\mathbf{F}\mathbf{F}^{-1}) = \delta\mathbf{F}\mathbf{F}^{-1}+\mathbf{F}\delta\mathbf{F}^{-1}
\end{aligned}
$$

于是

$$
\delta\mathbf{F}^{-1} = -\mathbf{F}^{-1}\delta\mathbf{F}\mathbf{F}^{-1}=-\mathbf{F}^{-1}\nabla_0\delta\mathbf{u}\mathbf{F}^{-1}=-\mathbf{F}^{-1}\nabla\delta\mathbf{u}
$$

```


### 一些重要的变分运算

**虽然都统一使用 $\delta$ 来表示变分，但也区分为对不同变量的微分，例如 $\mathbf{u}$ 的变分和对 $\mathbf{v}$ 的变分，可以通过右端的变分量进行区分**

**一般来说，时间无关量的变分量是 $\mathbf{u}$，如 $\mathbf{F}$ 和 $\mathbf{E}$，时间，时间相关量的变分量是 $\dot{\mathbf{F}}$ 和 $\dot{\mathbf{E}}$**

$$
\nabla\delta\mathbf{u} = \nabla_0 \delta\mathbf{u}\ \mathbf{F}^{-1}; \quad \nabla\delta\mathbf{v} = \nabla_0 \delta\mathbf{v}\ \mathbf{F}^{-1}
$$

```{admonition} 证明
:class: tip, dropdown

代入 $\mathbf{w} = \mathbf{\delta u}$ 和 $\mathbf{w} = \mathbf{\delta v}$ 到

$$
\nabla\mathbf{w} = \nabla_{0}\mathbf{w}\ \mathbf{F}^{-1}
$$

立证

```

$$
\delta\mathbf{F} = \delta(\nabla_0 \mathbf{u}) = \nabla_0\delta\mathbf{u}
$$

$$
\delta\dot{\mathbf{F}} = \delta(\nabla_0 \mathbf{v}) = \nabla_0\delta\mathbf{v}
$$

$$
\delta\mathbf{F}^{-1} = -\nabla\delta\mathbf{u}
$$

```{admonition} 证明
:class: tip, dropdown

一方面

$$
\delta\mathbf{F}^{-1} = \delta \nabla(\mathbf{x} - \mathbf{u}) = \delta(\mathbf{I} - \nabla\mathbf{u}) = -\delta\nabla\mathbf{u}
$$

另一方面

$$
\delta\mathbf{F}^{-1} = -\mathbf{F}^{-1}\nabla\delta\mathbf{u}
$$

通常 $\delta\nabla\mathbf{u}\neq\nabla\delta\mathbf{u}$，接下来证明 $\delta\nabla\mathbf{u} = \mathbf{F}^{-1}\nabla\delta\mathbf{u}$，根据交换公式

$$
\delta \nabla \mathbf{u} = \nabla (\delta \mathbf{u}) - (\nabla \mathbf{u}) \cdot (\nabla \delta \mathbf{u}) = (\mathbf{I} - \nabla \mathbf{u})\nabla \delta \mathbf{u} = \mathbf{F}^{-1}\nabla \delta \mathbf{u}
$$

```

$$
\delta\boldsymbol{\varepsilon} = \frac{1}{2}\left[(\nabla_0 \delta\mathbf{u})^{\mathrm{T}} + \nabla_0 \delta\mathbf{u}\right]
$$

由 $\nabla_{0}$ 和 $\delta$ 的交换性立证

$$
\begin{aligned}
\delta\mathbf{E} &= \frac{1}{2}\mathbf{F}^{\mathrm{T}}  \left[(\nabla\delta\mathbf{u})^{\mathrm{T}} + \nabla\delta\mathbf{u}\right]  \mathbf{F}\\
&\approx \mathbf{F}^{\mathrm{T}}  \delta\boldsymbol{\varepsilon}  \mathbf{F}
\end{aligned}
$$

对于小位移小应变的情形，第二行近似成立

```{admonition} 证明
:class: tip, dropdown

$$
\begin{aligned}
\delta\mathbf{E} = \frac{1}{2}\delta (\mathbf{F}^{T}\mathbf{F}-\mathbf{I})&=\frac{1}{2}(\delta\mathbf{F}^{T}\mathbf{F}+\mathbf{F}^{T}\delta\mathbf{F})\\
&=\frac{1}{2}\left((\nabla_{0}\delta\mathbf{u})^{T}\mathbf{F}+\mathbf{F}^{T}\nabla_0\delta\mathbf{u}\right)\\
&=\frac{1}{2}\mathbf{F}^{T}\left((\nabla_{0}\delta\mathbf{u}\ \mathbf{F}^{-1})^{T}+\nabla_{0}\delta\mathbf{u}\ \mathbf{F}^{-1}\right)\mathbf{F}\\
&=\frac{1}{2}\mathbf{F}^{T}\left((\nabla\delta\mathbf{u})^{T}+\nabla\delta\mathbf{u}\right)\mathbf{F}\\
\end{aligned}
$$

```

$$
\delta_{\mathbf{v}}\mathbf{d} = \frac{1}{2}\left[(\nabla\delta\mathbf{v})^{\mathrm{T}} + \nabla\delta\mathbf{v}\right] = \text{sym}(\delta\dot{\mathbf{F}}\mathbf{F}^{-1})
$$

对 $\mathbf{d}$ 来说，变分变量为 $\mathbf{v}$，而 $\mathbf{u}$ 保持不变

```{admonition} 证明
:class: tip, dropdown

$$
\nabla\delta\mathbf{v}=\nabla_{0}\delta\mathbf{v}\ \mathbf{F}^{-1}=\delta\dot{\mathbf{F}}\mathbf{F}^{-1}
$$

```

```{admonition} 共轭性
:class: tip, dropdown

应力功率是标量，在任何描述下都相等，故

$$
P = \int_{V_0} \mathbf{S} : \dot{\mathbf{E}} \, dV_0 = \int_{V} \boldsymbol{\sigma} : \mathbf{d} \, dV
$$

虚功率

$$
\delta P = \int_{V_0} \mathbf{S} : \delta \dot{\mathbf{E}} \, dV_0
$$

由于

$$
\begin{aligned}
\delta \dot{\mathbf{E}} &= \delta \left( \frac{1}{2} (\dot{\mathbf{F}}^T \mathbf{F} + \mathbf{F}^T \dot{\mathbf{F}}) \right)\\
&= \frac{1}{2} \delta\left( (\nabla_0 \mathbf{v})^T \mathbf{F} + \mathbf{F}^T (\nabla_0 \mathbf{v}) \right)\\
&=\frac{1}{2} \left( (\nabla_0 \delta\mathbf{v})^T \mathbf{F} + \mathbf{F}^T (\nabla_0 \delta\mathbf{v}) \right)\\
&=\mathbf{F}^T [\operatorname{sym}(\nabla \delta \mathbf{v})] \mathbf{F}
\end{aligned}
$$

于是

$$
\delta P = \int_{V_0} \mathbf{S} : (\mathbf{F}^T [\operatorname{sym}(\nabla \delta \mathbf{v})] \mathbf{F}) \, dV_0
$$

由于（迹运算交换）

$$
\mathbf{S} : (\mathbf{F}^T \mathbf{X} \mathbf{F}) = (\mathbf{F} \mathbf{S} \mathbf{F}^T) : \mathbf{X}
$$

```

