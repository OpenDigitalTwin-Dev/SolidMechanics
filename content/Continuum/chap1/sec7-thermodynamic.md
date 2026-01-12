# 热力学原理

*热力学第一定律：系统总能量的变化率等于外力所做功的变化率与热量输入的变化率之和*

## 能量方程

### 空间描述

根据热力学第一定律，有

$$
\frac{\mathrm{d}}{\mathrm{d}t}\int_{\Omega}\rho\epsilon\mathrm{d}v=W_{\text{net}}+H_{\text{net}}
$$ (sec7-eq:thermo)

其中，$\epsilon$ 是存储在单位质量的总能量，$W_{\text{net}}$ 是输入到系统中的净功率，$H_{\text{net}}$ 是输入到系统中的净热传递速率

单位质量的总储存能量 $\epsilon$ 包含内能和动能

$$
\epsilon = e_{c} + \frac{1}{2}(\mathbf{v}\cdot\mathbf{v})
$$

$e_{c}$ 为单位质量的内能，是所有微观能量形式的总和，$\frac{1}{2}(\mathbf{v}\cdot\mathbf{v})$ 是动能

在连续体没有体偶的情况下，输入功率 $W_{\text{net}}$ 可以表示为

$$
\begin{aligned}
W_{\text{net}}&=\oint_{\Gamma}\mathbf{t}\cdot\mathbf{v}\mathrm{d}s+\int_{\Omega}\mathbf{f}\cdot\mathbf{v}\mathrm{d}v
\end{aligned}
$$

由于

$$
\nabla\cdot(\boldsymbol{\sigma}\mathbf{v})=\left(\nabla \cdot \boldsymbol{\sigma}\right) \cdot \mathbf{v}+\boldsymbol{\sigma}:\nabla\mathbf{v},
$$

故由 $\boldsymbol{\sigma}$ 的对称性，再结合散度定理，得到

$$
\begin{aligned}
\oint_{\Gamma}\mathbf{t}\cdot\mathbf{v}\mathrm{d}s &= \oint_{\Gamma}\boldsymbol{\sigma}\mathbf{n}\cdot\mathbf{v}\mathrm{d}s=\oint_{\Gamma}(\boldsymbol{\sigma}\mathbf{v})\cdot\mathbf{n}\mathrm{d}s\\
&=\int_{\Omega}\nabla\cdot(\boldsymbol{\sigma}\mathbf{v})\mathrm{d}s\\
&=\int_{\Omega}\left((\nabla \cdot \boldsymbol{\sigma}) \cdot \mathbf{v}+\boldsymbol{\sigma}:\nabla\mathbf{v}\right)\mathrm{d}s
\end{aligned}
$$

结合线动量守恒方程 {eq}`sec6-eq:linear-momentum-local`，有

$$
\begin{aligned}
W_{\text{net}}&=\int_{\Omega}[(\nabla \cdot \boldsymbol{\sigma}+\mathbf{f}) \cdot \mathbf{v}+\boldsymbol{\sigma}:\nabla\mathbf{v}]\mathrm{d}v\\
&=\int_{\Omega}[\rho\frac{\mathrm{d}\mathbf{v}}{\mathrm{d}t} \cdot \mathbf{v}+\boldsymbol{\sigma}:\nabla\mathbf{v}]\mathrm{d}v
\end{aligned}
$$

由于 $\boldsymbol{\sigma}$ 是对称的，故

$$
\boldsymbol{\sigma}:\nabla\mathbf{v}=\boldsymbol{\sigma}:\frac{1}{2}[\nabla\mathbf{v} + (\nabla\mathbf{v})^{T}] = \boldsymbol{\sigma}:\mathbf{d},
$$

再结合 Reynolds 输运定理 {eq}`sec6-eq:reynolds`

$$
\int_{\Omega}\rho\frac{\mathrm{d}\mathbf{v}}{\mathrm{d}t} \cdot \mathbf{v}\mathrm{d}v = \frac{1}{2}\int_{\Omega}\rho\frac{\mathrm{d}}{\mathrm{d}t} (\mathbf{v}\cdot \mathbf{v})\mathrm{d}v = \frac{1}{2}\frac{\mathrm{d}}{\mathrm{d}t}\int_{\Omega}\rho\mathbf{v}\cdot \mathbf{v}\mathrm{d}v
$$

最终，$W_{\text{net}}$ 可以写为

$$
W_{\text{net}}=\frac{1}{2}\frac{\mathrm{d}}{\mathrm{d}t}\int_{\Omega}\rho\mathbf{v}\cdot \mathbf{v}\mathrm{d}v+\int_{\Omega}\boldsymbol{\sigma}:\mathbf{d}\mathrm{d}v
$$

净热传递速率 $H_{\text{net}}$ 可以表示为

$$
H_{\text{net}}=-\oint_{\Gamma}\mathbf{q}\cdot\mathbf{n}\mathrm{d}s+\int_{\Omega}g\mathrm{d}v=\int_{\Omega}(-\nabla\cdot\mathbf{q}+g)\mathrm{d}v
$$

其中，$\mathbf{q}$ 是热流量，$g$ 是单位体积内的内部热源项

最终，热力学第一定律 {eq}`sec7-eq:thermo` 可以写为

$$
\frac{\mathrm{d}}{\mathrm{d}t}\int_{\Omega}\rho(e_{c} + \frac{1}{2}(\mathbf{v}\cdot\mathbf{v}))\mathrm{d}v=\frac{1}{2}\frac{\mathrm{d}}{\mathrm{d}t}\int_{\Omega}\rho\mathbf{v}\cdot \mathbf{v}\mathrm{d}v+\int_{\Omega}(\boldsymbol{\sigma}:\mathbf{d}-\nabla\cdot\mathbf{q}+g)\mathrm{d}v
$$

结合 Reynolds 输运定理 {eq}`sec6-eq:reynolds`，化简得到

$$
0=\int_{\Omega}(\rho\frac{\mathrm{d}e_{c}}{\mathrm{d}t}-\boldsymbol{\sigma}:\mathbf{d}+\nabla\cdot\mathbf{q}-g)\mathrm{d}v
$$

由于 $\Omega$ 的任意性，得到其局部形式

$$
\rho\frac{\mathrm{d}e_{c}}{\mathrm{d}t}=\boldsymbol{\sigma}:\mathbf{d}-\nabla\cdot\mathbf{q}+g
$$ (sec7-eq:thermo1)

也被称为热力学形式，其中 $\boldsymbol{\sigma}:\mathbf{d}$ 被称为应力功，$\mathbf{q}$ 可以写为

$$
\mathbf{q}=-\mathbf{k}\cdot\nabla T
$$

其中，$\mathbf{k}$ 是二阶热传导张量，$T$ 是温度

### 物质描述

将每一项分别使用物质描述表示

$$
\begin{aligned}
\frac{\mathrm{d}}{\mathrm{d}t}\int_{\Omega}\rho\epsilon\mathrm{d}v&=\frac{\mathrm{d}}{\mathrm{d}t}\int_{\Omega_{0}}\rho_{0}(e_{c}+ \frac{1}{2}(\mathbf{V}\cdot\mathbf{V}))\mathrm{d}V \\
&= \int_{\Omega_{0}}\rho_{0}\frac{\partial e_{c}}{\partial t}+\frac{1}{2}\rho_{0}\frac{\partial}{\partial t}(\mathbf{V}\cdot \mathbf{V})\mathrm{d}V
\end{aligned}
$$

输入功率项

$$
\begin{aligned}
W_{\text{net}}&=\int_{\Omega}\left[\frac{1}{2}\rho\frac{\mathrm{d}}{\mathrm{d}t}(\mathbf{v}\cdot \mathbf{v})+\boldsymbol{\sigma}:\nabla\mathbf{v}\right]\mathrm{d}v\\
&=\int_{\Omega_{0}}\left[\frac{1}{2}\rho_{0}\frac{\partial}{\partial t}(\mathbf{V}\cdot \mathbf{V})+\mathbf{P}:\nabla_{0}\mathbf{V}\right]\mathrm{d}V
\end{aligned}
$$

```{admonition} 证明
:class: tip, dropdown

由于 $\boldsymbol{\sigma}$ 是对称的，故

$$
\begin{aligned}
\boldsymbol{\sigma}:\nabla\mathbf{v} = \boldsymbol{\sigma}:((\nabla_{0}\mathbf{v})\mathbf{F}^{-1})
&= \text{tr}(\boldsymbol{\sigma}(\nabla_{0}\mathbf{v})\mathbf{F}^{-1}))\\
&=\text{tr}(\mathbf{F}^{-1}\boldsymbol{\sigma}(\nabla_{0}\mathbf{v}))\\
&=\boldsymbol{\sigma}\mathbf{F}^{-T}:\nabla_{0}\mathbf{v}
\end{aligned}
$$

```

净热传递速率

$$
H_{\text{net}} = \int_{\Omega}(-\nabla\cdot\mathbf{q}+g)\mathrm{d}v = \int_{\Omega_{0}}(-\nabla_{0}\cdot\mathbf{q}_{0}+g_{0})\mathrm{d}V
$$

其中，$g_{0} = Jg$，根据 Piola 恒等式 {eq}`sec2-eq:piola-eqs`，有

$$
\begin{aligned}
\nabla\cdot\mathbf{q}=\frac{1}{J}\nabla_{0}\cdot(J\mathbf{F}^{-1}\mathbf{q})
\end{aligned}
$$

因此 $\mathbf{q}_{0}=J\mathbf{F}^{-1}\mathbf{q}$

因此，物质描述的能量方程为

$$
\begin{aligned}
\rho_{0}\frac{\partial e_{c}}{\partial t}&=\mathbf{P}:\nabla_{0}\mathbf{V}-\nabla_{0}\cdot\mathbf{q}_{0}+g_{0}\\
&=(\mathbf{F}\mathbf{S}):\nabla_{0}\mathbf{V}-\nabla_{0}\cdot\mathbf{q}_{0}+g_{0}
\end{aligned}
$$

## 熵增原理

熵通常被视为衡量原子趋向无序程度的一种指标。根据热力学第二定律，系统内部的熵产生始终为正，这一规律被称为熵增原理或 Clausius–Duhem 不等式

记单位质量的熵密度为 $\eta$，故系统的总熵为

$$
\mathcal{E}=\int_{\Omega}\rho\eta\ \mathrm{d}v,
$$

记 $\theta\geq0$ 为绝对温度，因此熵增定义为

$$
\begin{aligned}
\Gamma &= \frac{\mathrm{d}\mathcal{E}}{\mathrm{d}t}-\left[-\oint_{\Gamma}\frac{1}{\theta}\mathbf{q}\cdot\mathbf{n}\mathrm{d}s+\int_{\Omega}\frac{g}{\theta}\mathrm{d}v\right]\\
&=\int_{\Omega}\left[\rho\frac{\mathrm{d}\eta}{\mathrm{d}t}+\nabla\cdot\left(\frac{\mathbf{q}}{\theta}\right)-\frac{g}{\theta}\right]\mathrm{d}v
\end{aligned}
$$

根据热力学第二定律，有 $\Gamma\geq0$，故

$$
\int_{\Omega}\rho\frac{\mathrm{d}\eta}{\mathrm{d}t}\mathrm{d}v\geq\int_{\Omega}\left[\frac{g}{\theta}-\nabla\cdot\left(\frac{\mathbf{q}}{\theta}\right)\right]\mathrm{d}v
$$ (sec7-eq:entropy)

其局部形式为

$$
\rho\frac{\mathrm{d}\eta}{\mathrm{d}t}\geq\frac{g}{\theta}-\nabla\cdot\left(\frac{\mathbf{q}}{\theta}\right)
$$

或

$$
\theta\rho\frac{\mathrm{d}\eta}{\mathrm{d}t}\geq g-\nabla\cdot\mathbf{q}-\frac{1}{\theta}\mathbf{q}\cdot\nabla\theta
$$ (sec7-eq:entropy1)

$\mathbf{q}/\theta$ 被称为熵流量，内能 $e_{c}$ 和不可逆的热能之和被称为 Helmohtz 自由能

$$
\Psi = e_{c} - \theta\eta
$$

于是，代入到 {eq}`sec7-eq:thermo1`，得到

$$
\begin{aligned}
\rho\frac{\mathrm{d}\Psi}{\mathrm{d}t} &= \boldsymbol{\sigma}:\mathbf{d}-\nabla\cdot\mathbf{q}+g - \rho\frac{\mathrm{d}(\theta\eta)}{\mathrm{d}t}\\
&=\boldsymbol{\sigma}:\mathbf{d}-\nabla\cdot\mathbf{q}+g - \rho\theta\frac{\mathrm{d}\eta}{\mathrm{d}t} - \rho\eta\frac{\mathrm{d}\theta}{\mathrm{d}t}\\
&=\boldsymbol{\sigma}:\mathbf{d} - \rho\eta\frac{\mathrm{d}\theta}{\mathrm{d}t} - \mathcal{D}
\end{aligned}
$$

其中

$$
\mathcal{D} = \rho\theta\frac{\mathrm{d}\eta}{\mathrm{d}t}+\nabla\cdot\mathbf{q} - g
$$

被称为内部耗散，于是方程 {eq}`sec7-eq:entropy1` 被写为

$$
\mathcal{D}-\frac{1}{\theta}\mathbf{q}\cdot\nabla\theta\geq0
$$

当 $\mathcal{D} > 0$ 时，该过程不可逆；当 $\mathcal{D}=0$ 时，过程可逆